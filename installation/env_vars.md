### Environment file configuration details

### `cloud_type`
Target Cloud provider. 
Available options: 'aws' or 'os'
Example:
`cloud_type:  aws`

### `listener_env`
The listener environment name. Endpoints can be reached by going to `listener-aws-test.example.com` This value is used as hostnames and dns records. It must include valid characters.
https://en.wikipedia.org/wiki/Hostname
Example:
`listener_env: dev`
   
### `subdomain`
DNS Subdomain. 
Example:
`subdomain: example.com`

### `zone`
Dns Zone
Example:
`zone: example.com`

## EBS

### `ebs_enabled`
Using an EBS to store configuration, logs and kafka data is recommended. Setting to false disables EBS entirely. 
Example:
`ebs_enabled: True`


### `zk_ebs`
EBS for zookeeper data. 30gb is recommended. Mesos and Kafka Metadata is stored here.
Example:
`zk_ebs: 30`

### `es_ebs`
EBS for elastic search logstash data.
Example:
`es_ebs: 30`

### `ds_ebs`
EBS for listener database.
Example:
`ds_ebs: 30`

### `kafka_ebs`
EBS for kafka data. All data sent to listener is available for the `retention_hours`
Example:
`kafka_ebs: 500`

### `availability_zone`
The availability zone to deploy to. Multi AZ deployments are not supported yet.
Example:
availability_zone: us-west-2b

## Node Flavors
### `num_master`
Mesos-masters, should be either 1 or 3. 3 masters is recommended for production use.
Example:
`num_master: 3`

### `num_slave`
Mesos-Slaves, Should be at least 4
Example:
`num_slave: 4`

### `num_haproxy`
Load balancer nodes. Load balancers proxy inbound http/https traffic and stream data to clients. Two nodes is recommended for production use.
Example:
`num_haproxy: 2`

### `num_kafka`
All data sent to listener is stored in kafka for the length of the `retention_hours`. Three nodes is recommended for production use.
Example:
`num_kafka: 3`

## System flavors/Instance classes
### `masterFlavor`
Example:
`masterFlavor: t2.large`
### `slaveFlavor`
Example:
`slaveFlavor: m4.2xlarge`
### `haproxyFlavor`
Example:
`haproxyFlavor: m4.xlarge`
### `kafkaFlavor`
Example:
`kafkaFlavor: m4.xlarge`

## SSH
### `ssh_key_pub`
The path to the SSH public key
Example:
`ssh_key_pub:   /env_vars/ansible.pub``

### `ssh_key_priv`
The path to the SSH private key taht was used to create the systems.
Example:
`ssh_key_priv:  /env_vars/ansible`

### `keyname`
The Name of the ssh Public key to be used on AWS instances.
`keyname: devops-shared`

## Listener Configuration
#### `smtp_server`
The SMTP relay server for your environment. Listener may send emails to source owners in the event of some failures.
Example:
`smtp_server: "smtp.gmail.com:25"`

### `retention_hours`
Data is available for 72 hours before it's automatically purged and no longer accessible.
Example:
`retention_hours: 72`

### `nameserver`
The upstream name server to be used. Defaults to 8.8.8.8 if not set. When using AWS, use the VPC DHCP resolver endpoint for your VPC.
http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html#AmazonDNS
Example:
`nameserver: "172.31.0.2"`

## AWS Configuration

### `AWS_ACCESS_KEY_ID`
The AWS Access key ID
Example:
`AWS_ACCESS_KEY_ID:     < fill in >`

### `AWS_SECRET_ACCESS_KEY`
The AWS Secret access key ID
Example:
`AWS_SECRET_ACCESS_KEY: < fill in>`

### `AWS_REGION`
The AWS region to deploy listener to.
Example:
`AWS_REGION: us-west-2`

### `defaultSecurityGroupId`
The AWS default security group. 
Example:
`defaultSecurityGroupId: "sg-1e84c97a"`
   
### `vpc_id`
The VPIC ID
Example:
`vpc_id: "vpc-7591f910"`

### `vpc_subnet_id`
The VPC Subnet ID that everything goes into
Example:
`vpc_subnet_id: "subnet-67811a10"`

## Openstack Configuration
### `OS_AUTH_URL`
Openstack Authentication URL.
Example:
`OS_AUTH_URL:     https://horizon.example.com:5000/v2.0`

### `OS_TENANT_ID`
Entity that owns the resources.
Example:
`OS_TENANT_ID    4ee7cacaa4cfcb4bd39e1b888888885e`

### `OS_TENANT_NAME`
Entity that owns the resources.
Example:
`OS_TENANT_NAME:  listener`

### `OS_USERNAME`
The opesnstack user
Example:
`OS_USERNAME:     <fill in>`
    
### `OS_PASSWORD`
The Openstack user's password.
Example:
`OS_PASSWORD:     <fill in>`
    
### `OS_NETWORK_UID`
The neutron network ID that the nodes are created with.
Example:
`OS_NETWORK_UID:  97e111ef-1111-2222-9df5-d1f111b1360f`

### `OS_NETWORK_NAME`
The neutron network Name that the nodes are created with.
Example:
`OS_NETWORK_NAME: network123`

## Optional.
### `analytics_id`
If you would like to help the listener team make more data driven decision, please consider enabling the following. No confidential information is sent to Google Analytics
Example:
Openstack: `analytics_id: UA-69207726-4`
AWS: `analytics_id: UA-69207726-6`
