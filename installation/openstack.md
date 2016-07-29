# Openstack

# Openstack Requirements
We recommend the following for a base installation. Your openstack administrator will be able to provide more guidance.

### Recommended Openstack hardware.
* Openstack (version 2014.1.2 - Icehouse or above (ie, /v2/ API access and above)).
* API: V2 Only (Does not support keystone v3.0)
* Project defined on Openstack with (minimum, for a proof of concept setup):
  * 11 VM instances
    * 96 GB RAM
    * 60 vCPU
    * Optional: > 600GB Cinder Storage
  * Single Availability Zone (currently supported version)
  * Fixed & Floating IP network pre-configured
    * One public & one private per node.
    * IPv4 only
* An availability zone, usually defaulting to 'nova'.  Check your Open Stack installation for verification.

### Network
* 10 GbE network; 1GbE not recommended
  * 10GbE preferred for intra-cluster communication
    *  1GbE is acceptable, Listener performance will not be optimal
  *  10GbE preferred for public network communication
    *  1GbE is acceptable, Listener performance will not be optimal
* IPV4 network, IPV6 not supported.
* Fixed & Floating IP network pre-configured - 15 IP addresses
* Default floating_ip_pool enabled.

## Openstack Prerequisites
The below command are available if you have the python-novaclient pkg installed on your system.  If not, you can find the below details within the Horizon / Dashboard of your Openstack cluster.  Please write down the associated values for your Openstack cluster as they will be necessary for a proper installation of Listener.  When in doubt, consult your Openstack cluster admin for more assistance.

##### Availability Zones
```bash
nova availability-zone-list
+-------+-----------+
| Name  | Status    |
+-------+-----------+
| nova  | available |
+-------+-----------+
```

##### Openstack Flavors
Machine disk is usually the one limiting factor, they should always be above 40GB.  During the installation process, we request which 'flavor', or instance size you'd like to leverage per component in the platform.  Below is an example of the command to see what flavors are configured within the Openstack Cluster.  Please check with your administrator for more assistance.

```bash
nova flavor-list
+----------+-----------+-----------+------+-----------+------+-------+-------------+-----------+
| ID       | Name      | Memory_MB | Disk | Ephemeral | Swap | VCPUs | RXTX_Factor | Is_Public |
+----------+-----------+-----------+------+-----------+------+-------+-------------+-----------+
| 1        | m1.tiny   | 512       | 1    | 0         |      | 1     | 1.0         | True      |
| 2        | m1.small  | 2048      | 20   | 0         |      | 1     | 1.0         | True      |
| 3        | m1.medium | 4096      | 40   | 0         |      | 2     | 1.0         | True      |
| 4        | m1.large  | 8192      | 80   | 0         |      | 4     | 1.0         | True      |
| 5        | m1.xlarge | 16384     | 160  | 0         |      | 8     | 1.0         | True      |
+----------+-----------+-----------+------+-----------+------+-------+-------------+-----------+
```

##### Openstack Security Group
The installer will automatically create a new security group called ‘Listener-$env’ with the following rule sets:
```bash
Direction  | Ether | Type   | Port Range  | Remote CIDR
---------- | ----- | ------ | ----------- | -------------
Egress     | IPv6  | Any    | -           | ::/0
Egress     | IPv4  | Any    | -           | 0.0.0.0/0
Ingress    | IPv4  | ICMP   | -           | 0.0.0.0/0
Ingress    | IPv4  | TCP    | 1-65535     | 0.0.0.0/0
Ingress    | IPv4  | UDP    | 1-65535     | 0.0.0.0/0
```

##### Network
The installer will need to know what nova network to assign private IPs out of.
```bash
nova network-list
+--------------------------------------+------------------+------+
| ID                                   | Label            | Cidr |
+--------------------------------------+------------------+------+
| 4a129aa2-144b-4f03-9770-a446685ba37d | net04_ext        | -    |
| 97e438ef-59ff-4e72-9df5-d1f389b1360f | net-def-listener | -    |
+--------------------------------------+------------------+------+
```

### Network Topology
Listener will require access to the public internet to fetch patches and perform roll backs. The python library `python-neutronclient` will need to be installed.
An example network will look like this.
```bash
neutron subnet-list
+--------------------------------------+----------------------+-----------------+----------------------------------------------------+
| id                                   | name                 | cidr            | allocation_pools                                   |
+--------------------------------------+----------------------+-----------------+----------------------------------------------------+
| 15c8efb1-119e-4eaf-918e-15c1d8040c39 | net-def-listener-sub | 192.168.10.0/23 | {"start": "192.168.10.2", "end": "192.168.11.254"} |
+--------------------------------------+----------------------+-----------------+----------------------------------------------------+

neutron router-list
+--------------------------------------+-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| id                                   | name              | external_gateway_info                                                                                                                                                                     |
+--------------------------------------+-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| 6e422a40-9104-4747-ba82-76403a889394 | rtr-def-listenenr | {"network_id": "4a129aa2-144b-4f03-9770-a446685ba37d", "enable_snat": true, "external_fixed_ips": [{"subnet_id": "93eab520-8d78-4bbd-8d86-e55dbd5821db", "ip_address": "10.25.168.200"}]} |
+--------------------------------------+-------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

## Settings
All environment file variables are defined in [env_vars](env_vars.md)

Using your favorite editor, populate the following keys with your specific environment details gathered from the [prerequisites](prerequisites.md)
### Example Openstack env_vars/env.yml
```
cloud_type:  os
listener_env: dev
subdomain:    example.com
ebs_enabled: True
zk_ebs:      30
es_ebs:      30
ds_ebs:      30
kafka_ebs:   500
availability_zone: nova
num_master:  1
num_slave:   3
num_haproxy: 1
num_kafka:   1
ssh_key_pub:   /env_vars/ansible.pub
ssh_key_priv:  /env_vars/ansible
masterFlavor:  1
slaveFlavor:   2
haproxyFlavor: 2
kafkaFlavor:   3
nameserver:    8.8.8.8
smtp_server:   smtp.gmail.com:25
OS_AUTH_URL:     https://horizon.example.com:5000/v2.0
OS_TENANT_ID:    4ee7cacaa4cfcb4bd39e1b888888885e
OS_TENANT_NAME:  listener
OS_USERNAME:     <fill in>
OS_PASSWORD:     <fill in>
OS_NETWORK_UID:  97e111ef-1111-2222-9df5-d1f111b1360f
OS_NETWORK_NAME: network123
analytics_id: UA-69207726-4
```

#### Optional:
`analytics_id` is used to help the Listener development team understand how the software is used. No confidentail information is sent to google analytics. If this behavior is not wanted, this can be left out of the env.yml file.

## Openstack Pre-Install

The following steps are only necessary for Openstack deployments.  Specifically built QCOW images need to be downloaded and uploaded to your Openstack cluster.  We have scripts within the Installer container to help facilitate these two steps.  Note, the names and versions of the images are specific to each Listener release.

### Download Listener Openstack Images

First make a directory that has adequate space to for 4 large QCOW images, roughly ~20GB should be expected.

`mkdir images/`

Next, run the Installer container with the specific entrypoint option to run the download process.  Be sure to the mount points in the container are always /images and /env_vars.

`docker run -it -v images:/images -v env_vars:/env_vars --entrypoint="/opt/listener/bin/pre-install-download.sh" $container`

This process will take time and requires access to the internet to download the respective images. It will then perform a checksum against each image for validation.  Below depicts an example output after the download process.

```
Downloading mesos-master image...
    checksum matches!

Downloading mesos-slave image...
    checksum matches!

Downloading kafka image...
    checksum matches!

Downloading haproxy image...
    checksum matches!


**************************************
Image assets for Teradata Listener 79 have finished downloading!
```

If any of the above images checksum do NOT match, stop the process (Ctrl - C), remove all files under `images/` and attempt to run again.


### Upload Listener Openstack Images

The following steps are only necessary for Openstack deployments.  Now that we have downloaded and checksumed the associated QCOW images for your particular installation, we can proceed with step 2, uploading the images to your Openstack cluster.  In the below command, be sure to point at the same `images/` mount as in the previous step.  Make sure to keep all the image names intact, they should not be changed.

`docker run -it -v images:/images -v env_vars:/env_vars --entrypoint="/opt/listener/bin/pre-install-upload.sh" $container`

Again this will use the OS_* values in your `env_vars/env.yml` file.  If you receive an error, please check all our credentials and settings within this file.



## Install Openstack

Once ready to proceed, run the installer.  It will leverage the values within `env_vars/env.yml` and the associated images already uploaded to your Openstack cluster.

`docker run -it -v env_vars:/env_vars $container`
