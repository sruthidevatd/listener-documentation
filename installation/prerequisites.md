# Listener Installation Prerequisites

## DNS
* DNS A - record
* Openstack VM's should automatically be available via their public, floating IP's (or manually managed by the customer).
* A single, round-robin A record will be needed, manually created to reference the floating IP of each LB node.
* Numerous service VIP CNAMES will need to be manually created to point at the above load balancer A record.
* A detailed report of IP addresses and DNS records is provided at the end of the installation process.
  * [ENV_NAME] will be the name chosen for the Listener environment
  * [IP1], [IP2] will be chosen from the pool of IP addresses

```
A-Record:  
  lb-[ENV_NAME].subdomain.domain.com -> [IP1], [IP2]

C-Name Records:
  listener-[ENV_NAME].subdomain.domain.com                     -> lb-[ENV_NAME].subdomain.domain.com
  listener-app-services-[ENV_NAME].subdomain.domain.com        -> lb-[ENV_NAME].subdomain.domain.com
  listener-data-services-[ENV_NAME].subdomain.domain.com       -> lb-[ENV_NAME].subdomain.domain.com
  listener-ingest-services-[ENV_NAME].subdomain.domain.com     -> lb-[ENV_NAME].subdomain.domain.com
  listener-log-services-[ENV_NAME].subdomain.domain.com        -> lb-[ENV_NAME].subdomain.domain.com
  listener-manager-[ENV_NAME].subdomain.domain.com             -> lb-[ENV_NAME].subdomain.domain.com
  listener-system-services-[ENV_NAME].subdomain.domain.com     -> lb-[ENV_NAME].subdomain.domain.com
  marathon-[ENV_NAME].subdomain.domain.com                     -> lb-[ENV_NAME].subdomain.domain.com
  mesos-[ENV_NAME].subdomain.domain.com                        -> lb-[ENV_NAME].subdomain.domain.com
  elasticsearch-[ENV_NAME].subdomain.domain.com                -> lb-[ENV_NAME].subdomain.domain.com
  kibana-[ENV_NAME].subdomain.domain.com                       -> lb-[ENV_NAME].subdomain.domain.com
  consul-[ENV_NAME].subdomain.domain.com                      -> lb-[ENV_NAME].subdomain.domain.com
```

## Installation Machine
The installation of Listener and the underlying platform infrastructure can be performed on any node running Docker with access to your Openstack cluster.  We recommend using a machine with plenty of local storage as you'll first need to download the QCOWs to upload to Openstack.  Running this from an Ubuntu VM on the OS cluster for optimal performance is ideal, but setting up Docker within Ubuntu is out of scope of this document.

* Docker Engine 1.10.1 or higher (https://www.docker.com/products/docker-engine)
  * Native Docker Engine on Mac / Windows is untested.  We recommend running Docker Enginer within a VM on your corp network / Openstack cluster.
  * 20 GB local storage for downloading Listener Openstack images (this is temporary; images are eventually uploaded to the Openstack cluster).
  * Routable access to Openstack Cluster of choice w/ proper DNS resolution working.
  * Routable access to the internet for downloading Listener assets.


## Security / HTTPS Certificate
* Have access to a signed, wildcard key/cert based on the sub-domain Listener will be installed under.  This is necessary as numerous aliases will be used for various components of the product.
* A Subject alternative name cert can be used. Please reference the DNS documentations for the correct CNs
* The certificate will need to be based on the sub-domain in which Listener will be using (i.e. subdomain.domain.com)
* The certificate should be in the .pem format
* SSH: All machines will have an ssh key created / installed during the installation process. Adding additional accounts / keys is out side the scope of this document.


## LDAP authentication
To configure ldap authentication during the post installation steps,  you'll need the following information:
* LDAP Authentication
  * LDAP server
  * Port
  * Encryption Details
  * Domain Search User
  * Domain Search Password
  * Domain Base
  * LDAP User Fields
    * Name Field (ex: name)
    * Email Field (ex: email)
    * Member of Field (ex: memberOf)
