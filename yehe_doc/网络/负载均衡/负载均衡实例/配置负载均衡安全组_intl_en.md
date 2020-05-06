## Introduction to CLB Security Group
After a CLB instance is created, you can configure a CLB security group to isolate public network traffic. Business traffic through the CLB instance is double checked by the CLB security group and the CVM security group:
1. To allow the traffic from a specified client IP, you need to open 2 ports for the traffic, i.e., one port in your CLB security group and another one in your CVM security group. If your CLB instance is not configured with any security group, you will only need to open one port in the CVM security group.
2. To reject the traffic from a specified client IP, you can deny its access in either the CLB security group or the CVM security group.
>
> - Each CLB instance can be bound to 5 security groups.
> - You can choose whether to configure a security group for a CLB instance or not.
> - Currently, security group configuration is supported for public network CLB instances but not for private network CLB instances.
> - A CLB security group is bound to a CLB instance, while a CVM security group is bound to a CVM instance. The two can have the same inbound/outbound rules, which, however, target at different objects.

## Security Group Configuration Instructions
### CLB security group configuration
You can configure both a CLB security group and a CVM security group, and use the former to restrict listener port traffic and the latter to restrict service port traffic.
1. For security group rule configurations, please see [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup).
2. To allow the access of a specified client IP, you need to allow the client IP and open the listening port in the CLB security group, as well as allow the client IP and open the service port in the CVM security group.
3. To allow access of all public IPs, you need to allow all IPs (0.0.0.0/0) and open the listening port in CLB security group, as well as allow all IPs (0.0.0.0/0) and open the service port in CVM security group.

### CVM security group configuration
You need to allow the client IP and open the service port in the CVM security group.
If you want to use a CLB instance to forward business traffic to your CVM instance, the CVM security group should be configured as follows to ensure effective health checks:
1. Public network CLB: you need to allow the CLB VIP in the security group of the backend CVM, so that the CLB instance can use the VIP to check the health status of backend CVM.
2. Private network CLB:
 - For private network CLB (formerly called the application private network CLB), if your CLB instance is in a VPC, the CLB VIP needs to be allowed in the security group of the backend CVM for health checks; if your CLB instance is in a basic network, no additional configuration is needed as the health check IP is allowed by default.
 - For classic private network CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be allowed in the security group of the backend CVM for health checks; otherwise, no additional configuration is needed as the health check IP is allowed by default.

## Security Group Configuration Examples
### Configuring security groups for both CLB and CVM instances
Below is an example of public network CLB security group configuration which aims to:
- Only allow business traffic to enter from CLB port 80 and make CVM port 8080 provide services;
- Allow access from all IPs instead of specified client IPs.

**1. Create a CLB instance and listener, and bind a CVM instance.**
Please see [Getting Started with CLB](http://intl.cloud.tencent.com/document/product/214/8975). An `HTTP:80` listener is created and bound to a real server whose service port is 8080.
![](https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png)
**2. Configure a CLB security group policy.**
Please go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 80 for all IPs and reject traffic to enter from other ports.
![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png)
>
>- Security group rules are executed from top to bottom. If the new rule is put into effect, other rules will be invalid by default; therefore, pay attention to the configuring order.
>- A security group has an inbound rule and outbound rule. The above configuration restricts the inbound traffic and is therefore an ***inbound rule***, while the outbound rule does not need to be specially configured.

**3. Bind the security group to the CLB instance.**
Click **Security Group** tab on the CLB details page to select the corresponding security group and bind it to the CLB instance.
![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png)
The CLB security group configuration is completed, which only allows traffic to access the CLB instance from port 80.
![](https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png)
**4. Configure a CVM security group policy**
A CVM security group can be configured for the backend CVM to only allow traffic to access a specified service port.
Please go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 8080 for all IPs. To ensure smooth remote CVM login and ping services, please open port 22, port 3389, and ICMP service in the security group.
![](https://main.qcloudimg.com/raw/1afae187cfffaa3961e35b732bff7c4c.png)
**5. Bind the security group to the CVM instance.**
Click the ID of the CVM instance bound to CLB to enter the CVM details page, and then click the **Security Group** tab to configure a CVM security group policy.
![](https://main.qcloudimg.com/raw/8fdb3d63bd3da5a444b171c9de952352.png)

The CVM security group configuration is completed. Business traffic is allowed to access CVM only from CLB port 80, and the CVM port 8080 is used to provide services.
>
>- To allow the traffic from a specified client IP, you need to open 2 ports for the traffic, i.e., one port in your CLB security group and another one in your CVM security group. If your CLB instance is not configured with any security group, you will only need to open one port in the CVM security group.
>- For the public network CLB instance used in this example, the CLB VIP needs to be allowed in the security group of the backend CVM for health checks. The current IP `0.0.0.0/0` indicates all IPs including the CLB VIP.

### Only configuring a security group on the CVM instance
You can configure a security group only on the CVM instance. In this case, traffic of all client IPs are allowed and all ports are opened on your CLB instance by default. The inbound and outbound rules are filtered only by the CVM security group. For more information, please see [Security Group Configuration Instruction for Real Servers](http://intl.cloud.tencent.com/document/product/214/6157).
