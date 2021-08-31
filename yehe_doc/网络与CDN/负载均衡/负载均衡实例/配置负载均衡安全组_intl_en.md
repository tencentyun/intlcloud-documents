After a CLB instance is created, you can configure a CLB security group to isolate public network traffic. This document describes how to configure CLB security groups in different modes.
## Use Limits
- One CLB instance can be bound to five security groups at most.
- There can be 0–65535 security group rules.
- Security groups cannot be bound to classic private network CLB instances and private network CLB instances in the classic network. If a private network CLB instance is bound to an [Anycast EIP](https://intl.cloud.tencent.com/document/product/214/32426), security groups bound to the instance will not take effect.
- This feature is not supported for classic private network CLB and CLB in the classic network.


## Background
A security group is a virtual firewall that can filter stateful data packets and control outbound and inbound traffic at the instance level. For more information, please see [Security Group Overview](https://intl.cloud.tencent.com/document/product/213/12452).

A CLB security group is bound to a CLB instance, while a CVM security group is bound to a CVM instance. They target at different objects. CLB security groups can be generally configured in the following two modes:
- [Enable "Allow Traffic by Default in Security Group"](#open-security-group)
- [Disable "Allow Traffic by Default in Security Group"](#close-security-group)


<span id ="open-security-group"></span>
### Enabling "Allow Traffic by Default in Security Group"
![](https://main.qcloudimg.com/raw/0d2b50ca557d805ce5790fcdd3974b40.jpg)
After "Allow Traffic by Default in Security Group" is enabled:
<ul ><li>If you want to allow access only from a specified client IP, you <strong>need to open</strong> the client IP and listening port to the internet in the CLB security group, but you <strong>don't need to open</strong> the client IP and service port in the backend CVM security group. Access traffic from CLB only needs to pass through the CLB security group, as the real server allows traffic from CLB by default and doesn't need to open the port.</li>
<li>Traffic from public IPs (including general public IPs and EIPs) still needs to pass through the CVM security group.</li>
<li>If a CLB instance has no security group configured, all traffic will be allowed, and only ports configured with listeners on the VIP of the CLB instance can be accessed; therefore, the listening port will allow traffic from all IPs.</li>
<li>To reject traffic from a specified client IP, you must do so in the CLB security group, as doing so in the CVM security group takes effect only for traffic from public IPs (including general public IPs and EIPs) but <strong>not</strong> for traffic from CLB.</li></ul>

<span id ="close-security-group"></span>
### Disabling "Allow Traffic by Default in Security Group"
![](https://main.qcloudimg.com/raw/9357f8d81a0027110bd6a977cda4aafc.jpg)
After "Allow Traffic by Default in Security Group" is disabled:</p>
<ul ><li>If you want to only allow access from the specified client IP, you <strong>need to open</strong> the client IP and listening port to the internet in the CLB security group and <strong>open</strong> the client IP and service port in the CVM security group; therefore, business traffic passing through CLB will be double checked by both the CLB security group and CVM security group.</li>
<li>Traffic from public IPs (including general public IPs and EIPs) still needs to pass through the CVM security group.</li>
<li>If a CLB instance has no security group configured, all traffic will be allowed, and only ports configured with listeners on the VIP of the CLB instance can be accessed; therefore, the listening port will allow traffic from all IPs.</li>
<li>You can reject access in either the CLB security group or the CVM security group to reject traffic from a specified client IP.</li></ul>
<p >After "Allow Traffic by Default in Security Group" is disabled, the CVM security group should be configured as follows to ensure effective health check:</p>
<ol ><li>Configure public network CLB <br>You need to open the CLB VIP to the internet on the backend CVM security group, so that CLB can use the VIP to detect the backend CVM health status.</li>
<li>Configure private network CLB<ul><li>For private network CLB (formerly "private network application CLB"), if your CLB instance is in a VPC, the CLB VIP needs to be opened to the internet in the backend CVM security group for health check; if your CLB instance is in the classic network, no additional configuration is needed as the health check IP is opened to the internet by default. </li><li>For private network classic CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be opened to the internet (for health check) in the backend CVM security group; otherwise, no additional configuration is needed as the health check IP is opened to the internet by default.</li></ul></li></ol>



## Directions
The following public network CLB security group configuration example only allows business traffic to enter from CLB port 80 and make CVM port 8080 provide services. It does not limit the client IP but supports access from any IP.
> !For the public network CLB instance used in this example, the CLB VIP needs to be opened to the internet in the backend CVM security group for health check. The current IP `0.0.0.0/0` already contains the CLB VIP.

### Step 1. Create a CLB instance and listener and bind a CVM instance

For more information, please see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975). An HTTP:80 listener is created and bound to a backend CVM instance whose service port is 8080 in this example.
<img alt="" src="https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png" >

### Step 2. Configure a CLB security group

1. Configure a CLB security group rule. <br>Log in to the <a rel="nofollow" href="https://console.cloud.tencent.com/cvm/securitygroup">Security Group Console</a> to configure a security group rule. In the inbound rule, open port 80 of all IPs (i.e., `0.0.0.0/0`) to the internet and reject traffic from other ports.
> ?
> - Security group rules are screened to take effect from top to bottom. If the new rule is put into effect, other rules will be denied by default; therefore, pay attention to their order.
> - A security group has inbound and outbound rules. The above configuration is intended to restrict inbound traffic and is therefore an <strong>inbound rule</strong>, while the outbound rule does not need to be specially configured.
>
 ![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png) 

2. Bind the security group to the CLB instance
 1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
 2. On the "Instance Management" page, click the ID of the target CLB instance.
 3. On the instance details page, click the **Security Group** tab and click **Bind** in the **Bound Security Groups** module.
 4. In the **Configure Security Group** window that pops up, select the security group bound to the CLB instance and click **OK**.
    ![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png) 
 The CLB security group configuration is completed, which only allows access to CLB from port 80.
 <img alt="" src="https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png" >

### Step 3. Configure "Allow Traffic by Default in Security Group"
You can choose to enable or disable "Allow Traffic by Default in Security Group" with different configurations as follows:
- Method 1. Enable "Allow Traffic by Default in Security Group", so that the real server does not need to open the port to the internet.
>?This feature is not supported for classic private network CLB and CLB in the classic network.
- Method 2. Disable "Allow Traffic by Default in Security Group", and you also need to open the client IP to the internet (0.0.0.0/0 in this example) in the CVM security group.

#### Method 1. Enable "Allow Traffic by Default in Security Group"
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the "Instance Management" page, click the ID of the target CLB instance.
3. On the instance details page, click the **Security Group** tab.
2. On the "Security Group" tab, click <img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png"> to enable "Allow Traffic by Default".
3. After the "Allow Traffic by Default" feature is enabled, only security group rules in the <strong>rule preview</strong> as shown below need to be verified.
   ![](https://main.qcloudimg.com/raw/6caa47138ecb97cc3c60cb38971792fd.png)

#### Method 2. Disable "Allow Traffic by Default in Security Group"
If "Allow Traffic by Default" is disabled, you need to open the client IP to the internet in the CVM security group. Business traffic is allowed to access CVM only from CLB port 80 and use services provided by CVM port 8080.
>?Traffic from a specified client IP can be allowed, but that must be done in both the CLB security group and CVM security group. In the absence of the former, only the latter needs to be opened to the internet.
>
1. Configure a CVM security group rule
   A CVM security group can be configured to only allow access from service ports for traffic accessing the backend CVM instance. <br>Go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 8080 of all IPs to the internet. To ensure smooth remote CVM login and ping services, open 22, 3389, and ICMP services in the security group.
   ![](https://console.cloud.tencent.com/cvm/instance/index?rid=1)
2. Bind the security group to the CVM instance
 1. In the [CVM Console](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcvm%2Finstance%2Findex%3Frid%3D1), click the ID of CVM instance bound to the CLB instance to enter the details page.
 2. Select the **Security Group** tab and click **Bind** in the **Bound Security Groups** module.
 3. In the **Configure Security Group** window that pops up, select the security group bound to the CVM instance and click **OK**. <br><img alt="" src="https://main.qcloudimg.com/raw/6e0e1c2f834bb7425ef3ca010114165a.png" title="Click to view original image">
