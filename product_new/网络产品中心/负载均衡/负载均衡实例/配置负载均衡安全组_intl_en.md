## Introduction to CLB Security Group
After a CLB instance is created, you can configure a CLB security group to isolate public network traffic. Business traffic through the CLB is double checked by the CLB security group and the CVM security group:
1. Traffic of a client IP can be opened to the internet, but that must be done in both the CLB security group and CVM security group. In the absence of the former, only the latter needs to be opened to the internet.
2. You can deny access in either the CLB security group or the CVM security group to deny traffic of a client IP.
>!
> - You can choose whether to configure a security group for a CLB instance or not.
> - Currently, a security group can be configured for public network CLB but not private network CLB.
> - A CLB security group is bound to a CLB instance, while a CVM security group is bound to a CVM instance. The two can have the same inbound/outbound rules, which, however, target at different objects.

## Security Group Configuration Descriptions
### CLB Security Group Configuration
You can configure both a CLB security group and a CVM security group, and use the former to restrict listener port traffic and the latter to restrict service port traffic.
1. For security group rule configurations, see [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup).
2. If you want to only allow access from the specified client IP, you need to open the client IP and listener port to the internet in the CLB security group, and the client IP and service port in the CVM security group.
3. To support access from any public IP, you need to open all IPs (0.0.0.0/0) and the listener port to the internet in the CLB security group as well as all IPs (0.0.0.0/0) and the service port on the CVM security group.

### CVM Security Group Configuration
The client IP and service port need to be opened to the internet in the CVM security group.
If you want to use CLB to forward business traffic to CVM, the CVM security group should be configured as follows to ensure effective health checks:
1. Public network CLB: You need to open the CLB VIP to the internet on the backend CVM security group, so that CLB can use the VIP to detect the backend CVM health status.
2. Private network CLB:
 - For private network CLB, if your CLB instance is in a VPC, the CLB VIP needs to be opened to the internet in the backend CVM security group for health checks; if your CLB instance is in a basic network, no additional configuration is needed as the health check IP is opened to the internet by default.
 - For private network classic CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be opened to the internet (for health checks) in the backend CVM security group; otherwise, no configuration is required.

## Security Group Configuration Examples
### Configuring Security Groups for both CLB and CVM Instances
Below is an example of public network CLB security group configuration which aims to:
- Only allow business traffic to enter from CLB port 80 and make CVM port 8080 provide services;
- Support access from all IPs instead of specified client IPs.

**1. Create a CLB instance and listener, and bind a CVM instance.**
See [Getting Started with CLB](http://intl.cloud.tencent.com/document/product/214/8975). An HTTP:80 listener is created and bound to a real server whose service port is 8080.
![](https://main.qcloudimg.com/raw/93afe658baef2444e7d3998455fceab3.png)
**2. Configure a CLB security group policy.**
Go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 80 of all IPs to the internet and reject traffic from other ports.
![](https://main.qcloudimg.com/raw/1d943546ef8206d5f0b164d7a19b3186.png)
>!
>- Security group rules are screened to take effect from top to bottom. If the new rule is put into effect, other rules will be denied by default; therefore, pay attention to their order. For more information, see [Security Group FAQs].
>- A security group has an inbound rule and outbound rule. The above configuration is intended to restrict inbound traffic and is therefore an ***inbound rule***, while the outbound rule does not need to be specially configured.

**3. Bind the security group to the CLB instance.**
Click **Security Group** on the CLB details page to select the corresponding security group and bind it to the CLB instance.
![](https://main.qcloudimg.com/raw/9eb619464c4962fc7f5539edda5c2710.png)
The CLB security group configuration is completed, which only allows access to CLB from port 80.
![](https://main.qcloudimg.com/raw/8168c5c5647762b17e9c0322c6277a03.png)
**4. Configure a CVM security group policy**
A CVM security group can be configured to only allow access from service port for traffic accessing the backend CVM instance.
Go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 8080 of all IPs to the internet. To ensure smooth remote CVM login and ping services, open 22, 3389, and ICMP services in the security group.
![](https://main.qcloudimg.com/raw/7831ad7213ec35cc91fa3ac6d9c4ac0f.png)
**5. Bind the security group to the CVM instance.**
Click the ID of the CVM instance bound to CLB to enter the CVM details page, and then click the **Security Group** tab to configure a CVM security group policy.
![](https://main.qcloudimg.com/raw/0ba8aef96312ccf0961c399818ade24c.png)

The CVM security group configuration is completed. Business traffic is allowed to access CVM only from CLB port 80, and use services provided by CVM port 8080.
>!
>- Traffic of a client IP can be opened to the internet, but that must be done in both the CLB security group and CVM security group. In the absence of the former, only the latter needs to be opened to the internet.
>- For the public network CLB instance used in this example, the CLB VIP needs to be opened to the internet on the backend CVM security group for health checks. The current IP 0.0.0.0/0 already contains the CLB VIP.

### Configuring a Security Group Only in the CVM Instance
You can configure a security group only in the CVM instance without binding one to CLB. In this case, CLB opens traffic to all client IPs and ports, and inbound/outbound rules are filtered only through the CVM security group. For more information, see [Access Control of Back-end CVMs](http://intl.cloud.tencent.com/document/product/214/6157).
