This guide will walk you through the installation steps. It is assumed that you have an environment ready to install Listener that meets the [prerequisites](prerequisites.md) outlined previously.  The following steps are outlined for a linux centric installation machine.  Mac / Windows will differ slightly.  Please be aware how your local Docker Engine volume mounts work.

## Installation
All user environment settings are required to be in a file named: `env.yml`.  This should reside in a local folder on the installation machine and then mounted into the installation container during the docker run.  Let's create those now:

* `mkdir env_vars`
* `touch env_vars/env.yml`

### Environments file
The environments file describes the listener environment and describes the VMs that are used to operate Listener. 

This is an example file used to deploy listener on Openstack. More configuration options can be found for [Openstack](openstack.md) & [Aws](aws.md). This file is required for installation and should be saved into CVS.
A full listing of all configuration options and their explanations can be found at [env_vars](env_vars.md)

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
```

### TLS Certificate
All inbound communication is configured with TLS certificates.  Follow the below steps to add in your custom certificate bundle during installation time.  Note, not adding in a custom certificate will result in the default self signed setup which may cause issues with some browsers and clients (as it is not trusted).
* The pem file should reside under the `env_vars` directory created above, in a file called `cert_bundle.pem`
* Request and retain a wildcard certificate for your specific domain: *.example.com 
* Bundle the certificate, private key and ca bundle into a single Pem file.  Details on how to do this can be found on the internet, but essentially you simply cat the various files together like so:
* `cat yourdomain.key yourdomain.com.crt ca_certificate_bundle.crt > env_vars/cert_bundle.pem`
* Please make sure to protect this file, along with your private key and certificate files.


## Run the Installer
######When installing on Opensack for the first time Listener Images must be uploaded to Glance.
Please view the [Openstack](openstack.md) Readme
 
We'll now mount in the `env_vars` directory we created above to `/env_vars` within the container. If there are missing variables the installer will exit.

`docker run -it -v env_vars:/env_vars $container`



