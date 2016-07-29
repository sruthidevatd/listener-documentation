### When creating openstack VMs, floating ip pool not found.

Error: `Unable to create floating ip: FloatingIpPoolNotFound: Floating ip pool not found.`

Listener is configured to use auto-floating-ip.  Please contact your Openstack administrator and ask for auto-floating-ip to be enabled in conjunction with your private OS network.


### HAProxy Security

Only TLSv1.2 is enabled for all inbound HTTPS traffic via HAProxy.  The following ciphers are also being set to restrict known vulnerablities:
```
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA
```

### Some REST APIs are constantly sending back 503s.

Log into your haproxy node. Bamboo may have stopped receiving haproxy configuration from mesos. The haproxy will server traffic using the previous configuration however, if the environment drastically changes, some requests may result in a 503. Simply restarting bamboo on the haproxy node will resolve this.

Log into your load balancer nodes and find the bamboo container.

`docker ps  | grep bamboo`

```bash
bfe06c946b03        registry-cloud-platform.marahon.mesos/bamboo:01.00.00.00     "/bin/sh -c /run.sh"     4 weeks ago         Up 4 weeks        0.0.0.0:8000->8000/tcp, 0.0.0.0:8080->80/tcp   bamboo
```

Now you can get the logs out by running the command by looking up the container id.

`docker logs --follow bfe06c946b03`

```bash
panic:
2015-11-21 01:20:12,089 DEBG 'bamboo' stdout output:
zk: connection closed
```

Now restart Bamboo.

`docker restart bfe06c946b03`

### During install, Ansible sends back an error regarding floating IPs

```
ERROR: Inventory script (ansible/openstack.py) had an execution error: Traceback (most recent call last):
  File "ansible/openstack.py", line 149, in <module>
    main(sys.argv)
  File "ansible/openstack.py", line 71, in main
    floatingIp = getFloatingIpFromServerForNetwork(server, credentials['NETWORK_NAME'])
  File "ansible/openstack.py", line 127, in getFloatingIpFromServerForNetwork
    for addr in server.addresses.get(network):
TypeError: 'NoneType' object is not iterable
```

The private network that was selected was incorrect or does not exist. Double check the OS_* variables under your `env_vars/env.yml`, specifically `OS_NETWORK_NAME` and `OS_NETWORK_UID`.  Both of those variables should reference the same private network. Retry the installation.

Also note, some special characters used in `OS_NETWORK_NAME` could cause problems.  Try to keep the name fairly basic, hyphens and [a-zA-Z0-9].

### Cinder(EBS) storage
Attaching block storage via cinder to a kafka system will increase the amount of data that can be store which allows for a much higher retention time. Enabling cinder storage, any data stored to zookeeper, elastic-search, data-services and kafka will be moved to a seperate volume. This configuration can be changed only at install time.

Cinder storage can be toggled by application
1. Edit the listener profile file(`env_vars/env.yml`) and adjust ZK_EBS, DS_EBS, ES_EBS or KAFKA_EBS.  Setting `ebs_enabled: False` will disable all Cinder / EBS volumes.
3. Retry the installation.

### Kafka Options
#### Finding Zookeeper Endpoints.
Zookeeper runs on all of the Mesos Masters.

#### Finding Listener Source topics.
Kafka source topic IDs can be located in the listener Web UI. For example.
`https://listener-stg.example.com/sources/5c7662e7-d623-4875-9bd3-8b68e72d82cf`

`5c7662e7-d623-4875-9bd3-8b68e72d82cf` Would be the source topic id.

Alternatively, this can be found via the kafka commands too.
` /opt/kafka/bin/kafka-topics.sh --zookeeper mesos_master1:2181,mesos_master2:2181,mesos_master3:2181/kafka --list`

#### View existing Kafka topic options.
To view existing configuration for a topic.
` /opt/kafka/bin/kafka-topics.sh --zookeeper mesos_master1:2181,mesos_master2:2181,mesos_master3:2181/kafka ----describe kafka_source_id`

#### Changing Kafka topic partitions
In some situations some topics may require a higher degree of parallelization. Increasing `--partitions` will increase the available throughput for a particular topic. Changing the number of topics will not rebalance the existing data in kafka. Partitions can only be increased. This is set to 6 by default via the kafka server properties.

```bash
/opt/kafka/bin/kafka-topics.sh --zookeeper mesos_master1:2181,mesos_master2:2181,mesos_master3:2181/kafka --alter --topic source_topic_id --partitions 8
```

#### Change the replication factor of a topic.
Increasing the `--replication-factor` will cause commit times to increase due to all x brokers committing the data. This will also decrease the amount of cluster disk space as data will be replicated more often. The default replication factor is 2.

```bash
/opt/kafka/bin/kafka-topics.sh --zookeeper mesos_master1:2181,mesos_master2:2181,mesos_master3:2181/kafka --alter --topic source_topic_id --replication-factor 3
```
