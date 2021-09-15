After a CLB instance is created, you can configure a CLB security group to isolate public network traffic. This document describes how to configure CLB security groups in different modes.
## Use Limits
- One CLB instance can be bound to five security groups at most.
- Up to 512 rules are allowed for a security group.
- Security groups cannot be bound to classic network-based private CLB instances and classic private CLB instances. If a private CLB instance is bound to an [Anycast EIP](https://intl.cloud.tencent.com/document/product/214/32426), security groups bound to the instance will not take effect.
- **Allow by Default** is not available for classic private CLBs and classic network-based CLBs, and neither for [BM Physical Server 2.0](https://intl.cloud.tencent.com/document/product/213/11518).

## Background
A security group is a virtual firewall that can filter stateful data packets and control outbound and inbound traffic at the instance level. For more information, please see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).

A CLB security group is bound to a CLB instance, while a CVM security group is bound to a CVM instance. They target at different objects. For a CLB security group, you can choose to:
- [Enable **Allow by Default**](#open-security-group)
- [Disable **Allow by Default**](#close-security-group)

>?
>- For IPv4 CLB security groups, **Allow by Default** is disabled by default, you can enable it in the console.
>- For IPv6 CLB security groups, **Allow by Default** is enabled by default and you cannot disable it.


### Enabling **Allow by Default**[](id:open-security-group)
![](https://main.qcloudimg.com/raw/0d2b50ca557d805ce5790fcdd3974b40.jpg)
When **Allow by Default** is enabled:
<ul ><li>If you want to allow access only from a specified client IP, you <strong>need to allow</strong> it and the listening port in the CLB security group, however you <strong>don't need to allow</strong> the client IP and service port in the backend CVM security group. Access traffic from the CLB only pass through the CLB security group, as the real server allows traffic from CLB by default.</li>
<li>Traffic from public IPs (including general public IPs and EIPs) still needs to pass through the CVM security group.</li>
<li>If a CLB instance has no security group configured, all traffic will be allowed, and only ports configured with listeners on the VIP of the CLB instance can be accessed; therefore, the listening port will allow traffic from all IPs.</li>
<li>To reject traffic from a specified client IP, you need to configure in the CLB security group. Rejecting a client IP in the CVM security group takes effect only for traffic from public IPs (including general public IPs and EIPs) but <strong>not</strong> for traffic from CLB.</li></ul>


### Disabling **Allow by Default**[](id:close-security-group)
![](https://main.qcloudimg.com/raw/9357f8d81a0027110bd6a977cda4aafc.jpg)
When **Allow by Default** is disabled:</p>
<ul ><li>If you want to only allow access from the specified client IP, you <strong>need to allow</strong> the client IP and listening port in the CLB security group and <strong>also allow</strong> the client IP and service port in the CVM security group; therefore, business traffic passing through CLB will be double checked by both the CLB security group and CVM security group.</li>
<li>Traffic from public IPs (including general public IPs and EIPs) still needs to pass through the CVM security group.</li>
<li>If a CLB instance has no security group configured, only traffic passing through the CVM security group will be allowed.</li>
<li>You can reject access either the CLB security group or the CVM security group to reject traffic from a specified client IP.</li></ul>
<p >When **Allow by Default** is disabled, the CVM security group should be configured as follows to ensure effective health check:</p>
<ol ><li>Configure public network CLB<br>You need to allow the CLB VIP on the backend CVM security group, so that CLB can use the VIP to detect the backend CVM health status.</li>
<li>Configure private network CLB<ul><li>For private network CLB (formerly "private network application CLB"), if your CLB instance is in a VPC, the CLB VIP needs to be allowed in the backend CVM security group for health check; if your CLB instance is in the classic network, no additional configuration is needed as the health check IP is allowed by default.</li><li>For private network classic CLB, if your CLB instance was created before December 5, 2016 and is in a VPC, the CLB VIP needs to be allowed (for health check) in the backend CVM security group; otherwise, no additional configuration is needed as the health check IP is allowed by default.</li></ul></li></ol>

## Directions
In the following example, the security group is configured to only allow inbound traffic to the CLB from port 80, and the service is provided via CVM port 8080. There is no limit upon the client IPs.
> ! For the public network CLB instance used in this example, the CLB VIP needs to be allowed in the backend CVM security group for health check. The current IP is set to `0.0.0.0/0`, which means all IPs are allowed.

### Step 1. Create a CLB instance and listener, and bind them to a CVM

For more information, please see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975). An HTTP:80 listener is created and bound to a backend CVM instance whose service port is 8080 in this example.
<img alt="" src="https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png" >

### Step 2. Configure a CLB security group
1. Configure a CLB security group rule<br>Log in to the <a rel="nofollow" href="https://console.cloud.tencent.com/cvm/securitygroup">Security Group Console</a> to configure a security group rule. In the inbound rule, allow requests from port 80 of all IPs (i.e., `0.0.0.0/0`) and reject traffic from other ports.
> ?
> - Security group rules are screened to take effect from top to bottom. If the new rule is put into effect, other rules will be denied by default; therefore, pay attention to their order. For more information, see<a rel="nofollow" href="https://intl.cloud.tencent.com/document/product/215/38750">Security Group Overview</a>.
> - A security group has inbound and outbound rules. The above configuration is intended to restrict inbound traffic and is therefore an <strong>inbound rule</strong>, while the outbound rule does not need to be specially configured.
>
  ![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png) 

2. Bind the security group to the CLB instance
 1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
 2. On the "Instance Management" page, click the ID of the target CLB instance.
 3. On the instance details page, click the **Security Group** tab and click **Bind** in the **Bound Security Groups** module.
 4. In the **Configure Security Group** window that pops up, select the security group bound to the CLB instance and click **OK**.
       ![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png) 
     The CLB security group configuration is complete, which only allows access to CLB from port 80.
     <img alt="" src="https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png" >

### Step 3. Configure **Allow by Default**
You can choose to enable or disable **Allow by Default** with different configurations as follows:
- Method 1. Enable **Allow by Default**, so that the real server does not need to allow the port.
>?This feature is not supported for classic private network CLB and CLB in the classic network.
- Method 2. Disable **Allow by Default**, and you also need to allow the client IP (0.0.0.0/0 in this example) in the CVM security group.

#### Method 1. Enable **Allow by Default**
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click the ID of the target CLB instance.
3. On the instance details page, click the **Security Group** tab.
2. On the **Security Group** tab, click <img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png"> to enable **Allow by Default**.
3. When **Allow by Default** is enabled, only security group rules in the <strong>rule preview</strong> as shown below need to be verified.
    ![](https://main.qcloudimg.com/raw/6caa47138ecb97cc3c60cb38971792fd.png)

#### Method 2. Disable **Allow by Default**
If **Allow by Default** is disabled, you need to allow the client IP in the CVM security group. Business traffic is allowed to access CVM only from CLB port 80 and use services provided by CVM port 8080.
>?To allow traffic from a specified client IP, you need o allow the IP in both the CLB security group and CVM security group. If the CLB does not have a security group, please allow the IP in the CVM security group.
>
1. Configure a CVM security group rule
   A CVM security group can be configured to only allow access from service ports for traffic accessing the backend CVM instance.<br>Go to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, all port 8080 of all IPs. To ensure smooth remote CVM login and ping services, open 22, 3389, and ICMP services in the security group.
   ![](https://console.cloud.tencent.com/cvm/instance/index?rid=1)
2. Bind the security group to the CVM instance
 1. In the [CVM Console](https://cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcvm%2Finstance%2Findex%3Frid%3D1), click the ID of CVM instance bound to the CLB instance to enter the details page.
 2. Select the **Security Group** tab and click **Bind** in the **Bound Security Groups** module.
 3. In the **Configure Security Group** window that pops up, select the security group bound to the CVM instance and click **OK**.      <img alt="" src="https://main.qcloudimg.com/raw/6e0e1c2f834bb7425ef3ca010114165a.png" title="Click to view the original image">

