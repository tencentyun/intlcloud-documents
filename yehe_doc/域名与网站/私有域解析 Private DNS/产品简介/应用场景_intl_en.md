This document describes the common use cases of Private DNS.

### Private Network Access Hijacking
You can use Private DNS to create a private domain name, associate it with a VPC, add a DNS record for it, and set resource mapping to implement the private network hijacking feature. Then, when you access the private domain in the VPC, the mapped resource that you set in advance will be returned.


### Tencent Cloud Service Resource Management
You can use private DNS records to manage Tencent Cloud resources such as CVM, CLB, CDN, and COS in VPCs. For example, you can plan the hosts of CVM instances according to the region, business scenario, server information, etc. and use the host information to add private domain names and DNS records for such instances. These private domain names are inaccessible outside the VPCs, which makes it easier for you to manage CVM resources.

### Mutual Access Between Tencent Cloud Service Resources
You can connect VPCs with traditional IDCs through Direct Connect or VPN so that they can access each other's resources at private domain names, facilitating the intuitive use of Tencent Cloud service resources.

### Tencent Cloud Service Resource Switching
Generally, in order to ensure the stable operation of a high-concurrency business, the business is distributed on multiple CVM instances for them to share the pressure, and the same VPC can be established for such instances to enable mutual access between them at private IPs. However, when an instance is switched, its private IP will also change accordingly. Therefore, it is necessary to modify the business code and release the change, which is extremely inconvenient.
In this case, you can create a private domain name for each instance in your VPC through Private DNS and add DNS records pointing to the corresponding private IPs. The instances can access each other at the private domain names, and when an instance is switched, you do not need to modify the code. Instead, you can simply modify the DNS record of its domain name.