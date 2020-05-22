## Introduction to CLB Security Group
After a CLB instance is created, you can configure a CLB security group to isolate public network traffic. Business traffic through the CLB is double checked by the CLB security group and the CVM security group:
1. Traffic of a client IP can be opened to the internet, but that must be done in both the CLB security group and CVM security group. In the absence of the former, only the latter needs to be opened to the internet.
2. You can deny access in either the CLB security group or the CVM security group to deny traffic of a client IP.
>
> - One CLB instance can be bound to five security groups at most.
> - You can choose whether to configure a security group for a CLB instance or not.
> - Currently, a security group can be configured for public network CLB but not private network CLB.
> - A CLB security group is bound to a CLB instance, while a CVM security group is bound to a CVM instance. The two can have the same inbound/outbound rules, which, however, target at different objects.

## Security Group Configuration Description
### CLB Security Group Configuration
You can configure both a CLB security group and a CVM security group and use the former to restrict listener port traffic and the latter to restrict service port traffic.
1. For security group rule configurations, please see the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup).
2. If you want to only allow access from the specified client IP, you need to open the client IP and listener port to the internet in the CLB security group, and the client IP and service port in the CVM security group.
3. To support access from any public IP, you need to open all IPs (0.0.0.0/0) and the listener port to the internet in the CLB security group as well as all IPs (0.0.0.0/0) and the service port on the CVM security group.

### CVM Security Group Configuration
The client IP and service port need to be opened to the internet in the CVM security group.
If you want to use CLB to forward business traffic to CVM, the CVM security group should be configured as follows to ensure effective health checks:
1. Public network CLB: You need to open the CLB VIP to the internet on the backend CVM security group, so that CLB can use the VIP to detect the backend CVM health status.
2. Private network CLB:
 - For private network CLB (formerly "Application private network CLB"), if your CLB instance is in a VPC, the CLB VIP needs to be opened to the internet in the backend CVM instance security group for health checks; if your CLB instance is in a basic network, no additional configuration is needed as the health check IP is opened to the internet by default.
 - For private network classic CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be opened to the internet (for health checks) in the backend CVM instance security group; otherwise, no configuration is required.

## Security Group Configuration Examples
### Configuring security groups for both CLB and CVM instances
Below is an example of public network CLB security group configuration which aims to:
- Only allow business traffic to enter from CLB port 80 and make CVM port 8080 provide services;
- Support access from all IPs instead of specified client IPs.

**1. Create a CLB instance and listener, and bind a CVM instance.**
Please see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975). An HTTP:80 listener is created and bound to a real server whose service port is 8080.
![](https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png)
**2. Configure a CLB security group policy.**
Go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 80 of all IPs to the internet and reject traffic from other ports.
![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png)
>
>- Security group rules are screened to take effect from top to bottom. If the new rule is put into effect, other rules will be denied by default; therefore, pay attention to their order.
>- A security group has an inbound rule and outbound rule. The above configuration is intended to restrict inbound traffic and is therefore an **inbound rule**, while the outbound rule does not need to be specially configured.

**3. Bind the security group to the CLB instance.**
Click **Security Group** on the CLB details page to select the corresponding security group and bind it to the CLB instance.
![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png)
The CLB security group configuration is completed, which only allows access to CLB from port 80.
![](https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png)
**4. Configure a CVM security group policy**
A CVM security group can be configured to only allow access from service port for traffic accessing the backend CVM instance.
Go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 8080 of all IPs to the internet. To ensure smooth remote CVM login and ping services, open 22, 3389, and ICMP services in the security group.
![](https://main.qcloudimg.com/raw/1afae187cfffaa3961e35b732bff7c4c.png)
**5. Bind the security group to the CVM instance.**
Click the ID of the CVM instance bound to CLB to enter the CVM details page, and then click the **Security Group** tab to configure a CVM security group policy.
![](https://main.qcloudimg.com/raw/8fdb3d63bd3da5a444b171c9de952352.png)

The CVM security group configuration is completed. Business traffic is allowed to access CVM only from CLB port 80, and use services provided by CVM port 8080.
>
>- Traffic of a client IP can be opened to the internet, but that must be done in both the CLB security group and CVM security group. In the absence of the former, only the latter needs to be opened to the internet.
>- For the public network CLB instance used in this example, the CLB VIP needs to be opened to the internet on the backend CVM security group for health checks. The current IP 0.0.0.0/0 already contains the CLB VIP.

### Configuring a Security Group Only in the CVM Instance
You can configure a security group only in the CVM instance without binding one to CLB. In this case, CLB opens traffic to all client IPs and ports, and inbound/outbound rules are filtered only through the CVM security group. For more information, please see [Access Control of Real Server](https://intl.cloud.tencent.com/document/product/214/6157).
