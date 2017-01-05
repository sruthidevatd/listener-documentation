## AWS prerequisites

To deploy a Teradata Listener env on aws, you will need some key pieces of information

* Public AMI's are available in the following regions:
  * us-east-1, us-west-1, us-west-2, eu-west-1, eu-central-1, ap-northeast-1, ap-southeast-1, ap-southeast-2, sa-east-1
  * Requires a user specified VPC ID and VPC subnet ID.
  * Requires a user pre-defined Security Group to control ingress/egress, port 22. The installer will create another Security Group to define inner-communication between services within the Listener nodes
  * Our installer will handle route53 creation of all associated A Records and CNames.  We do require the associated zone id and subdomain you wish to use.
  * Instance types can be anything available in your selected region.  By default we normally start customers with the following:
    * masterFlavor:   t2.large
    * slaveFlavor:    m4.2xlarge
    * haproxyFlavor:  t2.medium
    * kafkaFlavor:    m4.xlarge
  * An ssh keypair must be created ahead of time.  The Public key should be uploaded to the region in question.  Make sure to write down the associated keyname as that will be required, along with the Private key, during the installation process.


## Settings
Create a SSH keyPair and upload the public key to the AWS EC2 region of your choice.  They keyname you set should be leveraged below as the `keyname` value.

The installer uses the associated private key to perform configurations across all the bootstrapped nodes. Please copy this private key to `env_vars/aws.pem`.  This file name should match the `ssh_key_priv` value below (be sure to keep the /env_var prefix).

The rest of the values should easily pertain to values within your specific VPC, along with the `AWS_REGION`, `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`

All environment file variables are defined in [env_vars](env_vars.md)

### Example AWS env_vars/env.yml

```
cloud_type:   aws
listener_env: dev
AWS_REGION:   us-west-2
AWS_ACCESS_KEY_ID:     < fill in >
AWS_SECRET_ACCESS_KEY: < fill in>
ebs_enabled: True
zk_ebs:       30
es_ebs:       30
ds_ebs:       30
kafka_ebs:    500
num_master:   1
num_slave:    3
num_haproxy:  1
num_kafka:    1
ssh_key_priv:   /env_vars/aws.pem
keyname:        devops-shared
masterFlavor:   t2.large
slaveFlavor:    m4.2xlarge
haproxyFlavor:  t2.medium
kafkaFlavor:    m4.xlarge
nameserver:     172.31.0.2
smtp_server:    smtp.gmail.com:25
vpc_id:                 vpc-12312310
vpc_subnet_id:          subnet-432432432
defaultSecurityGroupId: sg-123234
zone:                   example.com
subdomain:              example.com
analytics_id: UA-69207726-6
```

#### Optional:
`analytics_id` is used to help the Listener development team understand how the software is used. No confidentail information is sent to google analytics. If this behavior is not wanted, this can be left out of the env.yml file.

## Manage AWS Script
We've included an AWS management process that can be used to easily stop, start or destroy all instances in a Listener environment.  This can also be used via a cronjob to schedule the stopping / starting during off-hours to help save on costs.
The below demonstrates running docker in interactive mode, like a user would do at a terminal.  To run docker via a script / cronjob, please substitute the `-it` options with `-d`.

Before running the following commands, set your credentials, container and REGION accordingly within your shell:
```
AWS_ACCESS_KEY_ID=<fill in with your aws access key id>
AWS_SECRET_ACCESS_KEY=<fill in with your aws access key>
AWS_REGION=us-west-2 # or your associated region of use
container=<you should receive this container along with your Listener License purchase>
```

### List all Listener Environments
```
docker run -it -e AWS_REGION=$AWS_REGION -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY --entrypoint=/opt/listener/bin/manage_aws_env.py $container -l
```

This should provide an output containing all the unique Envs and a total count of instances online:
```
dev
test
stg
-=-=-=-
total listener_env instances: 54
```
 
### Stop Environment
With the env names listed above, we can now easily stop one of these.  Fill in the appropriate env name as applicable. 
```
docker run -it -e AWS_REGION=$AWS_REGION -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY --entrypoint=/opt/listener/bin/manage_aws_env.py $container -e greg1 -a stop
```

```
Stopping greg1 aws environment
mesos-slave4-greg1 	52.40.112.62 	172.31.45.106 	i-1826e2c3 	running
mesos-slave3-greg1 	52.40.19.7 	172.31.40.128 	i-5f26e284 	running
mesos-master1-greg1 	52.40.41.235 	172.31.42.61 	i-1427e3cf 	running
haproxy1-greg1 	52.34.169.121 	172.31.46.177 	i-1527e3ce 	running
mesos-slave1-greg1 	52.36.88.38 	172.31.40.83 	i-5e26e285 	running
kafka1-greg1 	52.10.16.230 	172.31.45.110 	i-5c26e287 	running
mesos-slave2-greg1 	52.25.155.60 	172.31.38.62 	i-1b26e2c0 	running
```


### Start Environment
```
docker run -it -e AWS_REGION=$AWS_REGION -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY --entrypoint=/opt/listener/bin/manage_aws_env.py $container -e greg1 -a start
```

Starting is pretty similar to stopping, however we do attempt to start services in a specific order.  Note, depending on your quorum size, it may take a few minutes(~15 Minutes) for the various clusters to elect a leader and before all Microservices are available.

```
starting up greg1 aws environment
mesos-slave4-greg1 	None 	172.31.45.106 	i-1826e2c3 	stopped
mesos-slave3-greg1 	None 	172.31.40.128 	i-5f26e284 	stopped
mesos-master1-greg1 	None 	172.31.42.61 	i-1427e3cf 	stopped
haproxy1-greg1 	52.34.169.121 	172.31.46.177 	i-1527e3ce 	stopped
mesos-slave1-greg1 	None 	172.31.40.83 	i-5e26e285 	stopped
kafka1-greg1 	None 	172.31.45.110 	i-5c26e287 	stopped
mesos-slave2-greg1 	None 	172.31.38.62 	i-1b26e2c0 	stopped

starting instance class mesos-master
starting instance class haproxy
starting instance class kafka
starting instance class mesos-slave
```
 
 
 
### Destroy Environment
```
docker run -it -e AWS_REGION=$AWS_REGION -e AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID -e AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY --entrypoint=/opt/listener/bin/manage_aws_env.py $container -e greg1 -a destroy
```

Careful, this will immediately destroy any associated instances!!!  It will also remove any attached EBS volumes, which means, your data is gone forever!!!  Elastic IP's will also be listed and culled!!! At this time, Route53 & Security groups are not removed.

```
Destroying greg1 aws environment
mesos-slave4-greg1 	52.10.115.20 	172.31.45.106 	i-1826e2c3 	running
mesos-slave3-greg1 	52.27.176.239 	172.31.40.128 	i-5f26e284 	running
mesos-master1-greg1 	52.40.195.99 	172.31.42.61 	i-1427e3cf 	running
haproxy1-greg1 	52.34.169.121 	172.31.46.177 	i-1527e3ce 	running
mesos-slave1-greg1 	52.26.98.59 	172.31.40.83 	i-5e26e285 	running
kafka1-greg1 	52.37.134.190 	172.31.45.110 	i-5c26e287 	running
mesos-slave2-greg1 	52.26.11.163 	172.31.38.62 	i-1b26e2c0 	running

Sleep 1 minute for volumes to detach
Deleting the following volumes
Removing the following ip allocations
Address:52.34.169.121
```
