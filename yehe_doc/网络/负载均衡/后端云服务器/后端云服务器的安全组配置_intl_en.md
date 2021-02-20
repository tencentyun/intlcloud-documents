## CVM Security Group Overview
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) can be used for access control for real servers of CLB instances, which acts as a firewall.
You can associate one or more security groups with a real server and then add one or more rules to each security group to control the traffic access permissions of different servers. You can modify the rules of a security group at any time, and new rules will be automatically applied to all instances associated with the security group. For more information, please see [Security Group Operation Guide](https://intl.cloud.tencent.com/document/product/213/12452). In the [VPC](https://intl.cloud.tencent.com/document/product/215/535) environment, you can also use [Network ACL](https://intl.cloud.tencent.com/document/product/215/31850) for access control.

## CVM Security Group Configuration Description
The client IP and service port need to be opened to the internet in the CVM security group.
If you want to use CLB to forward business traffic to CVM, the CVM security group should be configured as follows to ensure effective health checks:
1. Public network CLB: you need to open the CLB VIP to the internet on the backend CVM security group, so that CLB can use the VIP to detect the backend CVM health status.
2. Private network CLB:
 - For private network CLB (formerly "private network Application CLB"), if your CLB instance is in a VPC, the CLB VIP needs to be opened to the internet in the backend CVM security group for health checks; if your CLB instance is in the basic network, no additional configuration is needed as the health check IP is opened to the internet by default.
 - For private network classic CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be opened to the internet (for health checks) in the backend CVM security group; otherwise, no configuration is required.

## CVM Security Group Configuration Samples
The following samples show you how to configure CVM security groups when accessing CVM through CLB. If you have also configured a security group on CLB, please see [Configuring CLB Security Groups
](https://intl.cloud.tencent.com/document/product/214/14733) for more information on how to configure CLB security group rules.
- **Application scenario 1:**
If a public network CLB instance is configured with a TCP:80 listener, the real server port is 8080, and you want only certain Client IPs (ClientA IP and ClientB IP) to access the CLB instance, then configure the security group inbound rules of the real server as follows:
```
 ClientA IP + 8080 allow
 ClientB IP + 8080 allow
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
- **Application scenario 2:**
If a public network CLB instance is configured with a HTTP:80 listener, the real server port is 8080, and you want all Client IPs to access the CLB instance, then configure the security group inbound rules of the real server as follows:
```
 0.0.0.0/0 + 8080 allow
```
- **Application scenario 3:**
For a private network CLB (formerly "private network Application CLB") instance, if the network type is VPC, the CVM security group needs to open the CLB VIP IP to the internet for health check, this CLB instance is configured with a TCP:80 listener, the real server port is 8080, and you want certain Client IPs (ClientA IP and ClientB IP) to access the CLB VIP and want the Client IPs to access only real servers bound to the CLB instance, then:
a. Configure the inbound rules for the real server security group as follows:
```
 ClientA IP + 8080 allow
 ClientB IP + 8080 allow
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
b. Configure the outbound rules for the client server security group as follows:
```
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
- **Application scenario 4:**
For a private network Classic CLB instance (i.e., a VPC CLB instance purchased after December 5, 2016), if the CVM security group only needs to open the Client IP to the internet (there is no need to open the CLB VIP, and the health check IP is opened by default), this CLB instance is configured with a TCP:80 listener, the real server port is 8080, and you want certain Client IPs (ClientA IP and ClientB IP) to access the CLB VIP and want the Client IPs to access only real servers bound to the CLB instance, then:
a. Configure the inbound rules for the real server security group as follows:
```
 ClientA IP + 8080 allow
 ClientB IP + 8080 allow
 0.0.0.0/0  + 8080 drop
```
b. Configure the outbound rules for the client server security group as follows:
```
 CLB VIP    + 8080 allow
 0.0.0.0/0  + 8080 drop
```
- **Application scenario 5: blacklist**
If you need to configure a blacklist for some client IPs to deny their access requests, you can configure the security group associated with Tencent Cloud services. The security group rules need to be configured as follows:
 - Add the client IP and port to be rejected into the security group and select the option in the "Policy" column to reject access from this IP.
 - Add another security group rule after completing the above configuration to allow access requests to the port from all IPs by default.
After the configuration is completed, the security group rules are as follows:

```
 clientA IP + port drop
 clientB IP + port drop
 0.0.0.0/0  + port accept
```

>?
>- The above configuration steps should be performed **in a correct order**; otherwise, the blacklist configuration cannot take effect.
>- Security groups are stateful; therefore, the above configurations are used for **inbound rules**, while outbound rules do not require special configuration.

## CVM Security Group Operation Guide
### Managing real server security group in console
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. On the CVM page, click the corresponding real server ID to enter the CVM instance details page.
3. Click the **Security Group** tab to bind/unbind the security group.

### Managing real server security group through TencentCloud API
For more information, please see [AssociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33265) and [DisassociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33253).
