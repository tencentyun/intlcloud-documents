## Overview of CVM Security Group
The backend CVM instances of CLB can perform access control through [Security Group](https://intl.cloud.tencent.com/document/product/213/12452), which acts as a firewall.
You can associate one or more security groups with a backend CVM, and add one or more rules to each security group to control the traffic access permissions of different servers. You can modify the rules for a security group at any time, and the new rules are automatically applied to all instances associated with that security group. For more information, see the [Security Group](https://intl.cloud.tencent.com/document/product/213/12452). In a VPC as instructed in [Overview](https://intl.cloud.tencent.com/document/product/215/535), you can also use a network ACL as instructed in [Rule Overview](https://intl.cloud.tencent.com/document/product/215/31850) for access control.

## Configuration of CVM Security Group
You need to allow the client IP and open the service port in the CVM security group.
If you want to use a CLB instance to forward business traffic to your CVM instance, the CVM security group should be configured as follows to ensure effective health checks:
1. Public network CLB: You need to allow the CLB VIP in the security group of the backend CVM, so that the CLB instance can use the VIP to check the health status of the backend CVM.
2. Private network CLB:
   - For private network CLB (formerly called the application private network CLB), if your CLB instance is in a VPC, the CLB VIP needs to be allowed in the security group of the backend CVM for health checks; if your CLB instance is in a basic network, no additional configuration is needed as the health check IP is allowed by default.
   - For classic private network CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be allowed in the security group of the backend CVM for health checks; otherwise, no additional configuration is needed as the health check IP is allowed by default.

## Configuration Sample
This example shows a sample of configuring CVM security groups when accessing a CVM through the CLB. To configure the rules of CLB security groups, please see [Configuring CLB Security Group](https://intl.cloud.tencent.com/document/product/214/14733).
- **Application Scenario 1:**
For a public network CLB configured with a TCP:80 listener and a backend service port 8080, if you want to allow only the ClientA IP and ClientB IP to access the CLB, you need to configure the inbound rules of the backend CVM security group as follows:
```
ClientA IP + 8080 allow
ClientB IP + 8080 allow
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```
- **Application Scenario 2:**
For a public network CLB configured with a HTTP:80 listener and a backend service port 8080, if you want to allow all Client IPs to access the CLB, you need to configure the inbound rules of the backend CVM security group as follows:
```
0.0.0.0/0 + 8080 allow
```
- **Application Scenario 3:**
Allow the CLB VIP on the CVM security group to perform health check. For a private network CLB (formerly "application private network CLB") using a VPC and configured with TCP:80 listener and real server port 8080, if you want to only allow the Client IPs (ClientA IP and ClientB IP) to access the CLB VIP, and to restrict Client IP to only access backend CVMs bound with the CLB,
a. Configure the security group inbound rules for the real server as follows:
```
ClientA IP + 8080 allow
ClientB IP + 8080 allow
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```
b. Configure the security group outbound rules for the server used as Client as follows:
```
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```
- **Application Scenario 4:**
After December 5, 2016, for a newly purchased classic private network CLB using a VPC, you need to allow the Client IP only for the CVM security group. It is not necessary to allow the CLB VIP, and the health check IP is allowed by default. Configure this CLB with TCP:80 listener and real server port 8080. If you want to only allow the Client IPs (ClientA IP and ClientB IP) to access the CLB VIP, and to restrict Client IPs to only access backend CVMs bound with the CLB,
a. Configure the security group inbound rules for the real server as follows:
```
ClientA IP + 8080 allow
ClientB IP + 8080 allow
0.0.0.0/0  + 8080 drop
```
b. Configure the security group outbound rules for the server used as Client as follows:
```
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```
- **Application Scenario 5: Blocklist**
If you need to configure a blocklist for some client IPs to deny their access requests, you can configure the security group associated with the cloud services. The security group rules need to be configured as follows:
   - Add the Client IP and port to be rejected into the security group, and select the option in the policy column to reject access from this IP.
   - Add another security group rule after completing the above configuration to allow access requests to the port from all IPs by default.
When the configuration completes, the security group rules are as follows:
```
clientA IP + port drop
clientB IP + port drop
0.0.0.0/0  + port accept
```
>!
>- Follow the steps above **strictly in the given order**, otherwise the blocklist configuration may fail.
>- The security group is stateful. The above configurations are all configurations of **inbound rules**.
>

## Operation Guide of CVM Security Groups
### Managing Backend CVM Security Groups Using the Console
1. Log into the [CLB Console](https://console.cloud.tencent.com/loadbalance) and click the corresponding CLB instance ID to enter the CLB details page.
2. On the page of CVMs bound to the CLB, click the target backend CVM ID to enter the CVM details page.
3. Click the **Security Group** tab. On the tab, bind/unbind a security group.

### Managing backend CVM security groups using Tencent Cloud API
See [AssociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33265) and [DisassociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33253).


