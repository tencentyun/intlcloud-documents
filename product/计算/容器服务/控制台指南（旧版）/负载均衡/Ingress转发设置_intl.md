
### Prerequisites of using Ingress
Ingress service supports three scenarios as follows:

- Access from public network
- Access within cluster only
- Access via private network in VPC

Ingress supports application-based LB. An appropriate port needs to be enabled for the backend container node of an application-based LB. By default, CVM port is enabled for access from public network and access via private network in VPC, while CVM port is disabled for access within cluster only. However, if Ingress is set, CVM port is automatically enabled for the backend service. Services with access method disabled do not support setting of Ingress.

You can flexibly set an access method with Ingress for your service. The method for accessing a service does not conflict with Ingress. 

### Wildcard in a domain name
A domain name must comply with the public network application-type load balancer domain name rules and Ingress domain name rules of Kubernetes:
1. It supports regular expression with a length limited to 1-80 characters.
2. Character sets supported by a non-regular domain name: a-z, 0-9, . and -.

A domain name with wildcard only supports the format of `\*.example.com`, and only one "*" can be used in a domain name.

### Example of Ingress setting

Create a backend service that needs to use Ingress:

- hello service: Port 80 is listened with the entry file in /path_hello/index.html
- bye service: Port 80 is listened with the entry file in /path_bye/index.html

Create an Ingress on the Ingress page (skip this step if an Ingress already exists).
![Alt text](https://main.qcloudimg.com/raw/eddbd40851224cca0385dd999e2809ad.png)

Resolve your domain name to the VIP of the load balancer. For more information, please see Domain Name Resolution Help Documentation.
<!--Temp Remove Link：https://cloud.tencent.com/document/product/302/3446-->

In the example below, www .qcloudccs.com is resolved to sample load balancer.

Set Ingress forwarding rules:

![Alt text](https://main.qcloudimg.com/raw/36f66fa38e6aef83eaf3abee5b8388a9.png)

Access test:

![Alt text](https://main.qcloudimg.com/raw/e2067d908b46da463b4e45ce4ce7354c.png)
![Alt text](https://main.qcloudimg.com/raw/88de2b4a80425cf183e6a6859e9d215f.png)

