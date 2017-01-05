# Listener Installation Prerequisites

## DNS
* DNS A - record
* Openstack VMs should be available automatically via their public, floating IPs (or manually managed by the customer).
* A single, round-robin A record needs to be manually created to reference the floating IP of each LB node.
* Numerous service VIP CNAMES needs to be manually created to point to the load balancer A record.
* A detailed report of IP addresses and DNS records is provided at the end of the installation process.
  * [ENV_NAME] is the name chosen for the Listener environment
  * [IP1], [IP2] is chosen from the pool of IP addresses
* Ensure the domain name conforms to the host name requirements described in [RFC 952 DOD INTERNET HOST TABLE SPECIFICATION](https://tools.ietf.org/html/rfc952), which states "A "name" (Net, Host, Gateway, or Domain name) is a text string up to 24 characters drawn from the alphabet (A-Z), digits (0-9), minus sign (-), and period (.). Note that periods are only allowed when they serve to delimit components of "domain style names”." The underscore(_) character is not mentioned as valid usage and must be avoided. See "2.1  Host Names and Numbers" in [RFC 1123 Requirements for Internet Hosts -- Application and Support](https://tools.ietf.org/html/rfc1123#page-13).


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
  listener-streamer-services-[ENV_NAME].subdomain.domain.com   -> lb-[ENV_NAME].subdomain.domain.com
  marathon-[ENV_NAME].subdomain.domain.com                     -> lb-[ENV_NAME].subdomain.domain.com
  mesos-[ENV_NAME].subdomain.domain.com                        -> lb-[ENV_NAME].subdomain.domain.com
  elasticsearch-[ENV_NAME].subdomain.domain.com                -> lb-[ENV_NAME].subdomain.domain.com
  kibana-[ENV_NAME].subdomain.domain.com                       -> lb-[ENV_NAME].subdomain.domain.com
  consul-[ENV_NAME].subdomain.domain.com                      -> lb-[ENV_NAME].subdomain.domain.com
```

## Installation Machine
Installation of Listener and the underlying platform infrastructure can be performed on any node running Docker with access to your Openstack cluster.  We recommend using a machine with plenty of local storage because you must first download the QCOWs to upload to Openstack.  Running this from an Ubuntu VM on the OS cluster for optimal performance is ideal; however, setting up Docker within Ubuntu is outside the scope of this document.

* Docker Engine 1.10.1 or higher (https://www.docker.com/products/docker-engine)
  * Native Docker Engine on Mac or Windows is untested.  We recommend running Docker Enginer within a VM on your corp network/Openstack cluster.
  * 20 GB local storage for downloading Listener Openstack images (this is temporary; images are eventually uploaded to the Openstack cluster).
  * Routable access to Openstack Cluster of choice w/ proper DNS resolution working.
  * Routable access to the internet for downloading Listener assets.


## Security / HTTPS Certificate
* You must have access to a signed, wildcard key/cert based on the sub-domain under which Listener will be installed.  This is necessary because numerous aliases will be used for various components of the product.
* A Subject alternative name cert can be used. Refer to the DNS documentations for the correct CNs.
* The certificate will be based on the sub-domain Listener uses (subdomain.domain.com).
* The certificate must be in the .pem format
* SSH: All machines will have an ssh key created during the installation process. Adding additional accounts or keys is outside the scope of this document.


## LDAP authentication
To configure ldap authentication during the post installation steps,  you need the following information:
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
