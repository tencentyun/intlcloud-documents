After creating a CLB instance, you can configure a CLB security group to isolate public network traffic. This document describes how to configure different modes of CLB security groups.
## Use Limits
- Each CLB instance can be bound with up to 5 security groups.
- Each CLB instance can have up to 512 security group rules.
- Classic private network CLB instances and private network CLB instances of the classic network type do not support binding security groups. If a private network CLB instance is bound with an [Anycast EIP](https://intl.cloud.tencent.com/document/product/214/32426), the security group bound with the private network CLB instance will be ineffective.
- The Allow Traffic by Default feature of security group is in beta, if you want to try it out, please submit a ticket for application. The feature is not supported for classic private network CLB instances and classic network CLB instances.


## Background
A security group is a virtual firewall that features stateful data packet filtering and controls inbound and outbound traffic of instances. For more information, please see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).

CLB security groups are bound with CLB instances and CVM security groups are bound with CVM instances, restricting different objects. There are two configuration modes of CLB security groups:
- [Enabling Allow Traffic by Default](#open)
- [Disabling Allow Traffic by Default](#close)


<span id ="open"></span>
### Enabling Allow Traffic by Default
![](https://main.qcloudimg.com/raw/0d2b50ca557d805ce5790fcdd3974b40.jpg)
After the Allow Traffic by Default feature is enabled:
<ul ><li>If you want to specify access from a client IP, the client IP **needs to be allowed** and the listening port **needs to be opened** on the CLB security group, while the client IP **does not need to be allowed** and the service port **does not need to be opened** on the backend CVM security group. The access traffic from a CLB instance only needs to be allowed by the CLB security group. Real servers allow the traffic by default and does not need to open its port.</li>
<li>Traffic from public IPs (including general public IPs and EIPs) still needs to be allowed by the CVM security group.</li>
<li>If a CLB instance is not configured with a security group, all traffic will be allowed. On a CLB VIP, only the ports configured with listeners can be accessed, so the listening port will allow the traffic of all IPs.</li>
<li>To deny traffic from a client IP, you need to deny the client IP access in the CLB security group. Denying IP access in a CVM security group is effective for the traffic from public IPs (including general public IPs and EIPs) **but not** CLB instances.</li></ul>

<span id ="close"></span>
### Disabling Allow Traffic by Default
![](https://main.qcloudimg.com/raw/9357f8d81a0027110bd6a977cda4aafc.jpg)
After the Allow Traffic by Default feature is disabled:
<ul ><li>If you want to specify access from a client IP, the client IP **needs to be allowed** both on the CLB and CVM security groups, and the listening port and service port **need to be opened** on the CLB and backend CVM security groups respectively. In this way, business traffic passes through a CLB instance will be double-checked by CLB and CVM security groups.</li>
<li>Traffic from public IPs (including general public IPs and EIPs) still needs to be allowed by the CVM security group.</li>
<li>If a CLB instance is not configured with a security group, all traffic will be allowed. On a CLB VIP, only the ports configured with listeners can be accessed, so the listening port will allow the traffic of all IPs.</li>
<li>To deny traffic from a client IP, you can deny the client IP access on either a CLB or CVM security group.</li></ul>
<p >When the Allow Traffic by Default feature is disabled, the following configurations are required for a CVM security group to guarantee the health check feature:</p>
<ol ><li>Configure a public network CLB instance: <br>You need to allow the CLB VIP on the backend CVM security group, so that the CLB instance can use the VIP to check the health status of the backend CVM.</li>
<li>Configure a private network CLB instance: <ul><li>For a private network CLB (formerly "application CLB") instance, if your CLB instance is in VPC, you need to allow the CLB VIP on the backend CVM security group for health checks. If your CLB instance is in the classic network, you do not need to configure the backend CVM security group as the health check IP is allowed by default.</li><li> For a classic private network CLB instance created before December 5, 2016, and the network type is VPC, you need to allow the CLB VIP on the backend CVM security group for health check. Classic private network CLB instances of other types do not require backend CVM security group configuration as the health check IPs are allowed by default.</li></ul></li></ol>



## Directions
The directions describe how to configure the security group of a sample public network CLB instance. The configuration allows business traffic to enter via the CLB port 80, provides service from the CVM port 8080, and allows access from all IPs.
> !For the public network CLB instance used here, the CLB VIP needs to be allowed on the security group of the backend CVM for health checks. The current IP `0.0.0.0/0` indicates all IPs including the CLB VIP.

### Step 1: Creating a CLB instance and listener, and binding a CVM instance

For more information, please see [Getting Started with CLB](http://intl.cloud.tencent.com/document/product/214/8975). An `HTTP:80` listener is created and bound to a backend CVM whose service port is 8080.
<img alt="" src="https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png" >

### Step 2: Configuring a CLB security group

1. Configure CLB security group rules:<br>Go to the <a rel="nofollow" href="https://console.cloud.tencent.com/cvm/securitygroup">Security Group console</a>, open the port 80 of all IPs (i.e., `0.0.0.0/0`) in the inbound rules, and deny the traffic of other ports.
> ?
> - The rules in a security group are prioritized from top to bottom. After an allowing rule is passed, other rules set afterward will be denied by default. Please pay attention to the rule configuration order. For more information, please see <a rel="nofollow" href="https://intl.cloud.tencent.com/document/product/215/38750">Security Group Overview</a>.
> - A security group has an inbound rule and outbound rule. The above configuration restricts the inbound traffic and is therefore an **inbound rule**, while the outbound rule does not need to be specially configured.
>
 ![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png) 

2. Bind the security group to a CLB instance
 1. Log in to the [CLB console](https://console.cloud.tencent.com/loadbalance).
 2. On the **Instance Management** page, click the ID of the target CLB instance.
 3. Select the **Security Group** tab and then click **Bind** in the **Bound with security group** section.
 4. In the **Configure Security Group** pop-up window, select the security group and click **OK**.
    ![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png) 
 The CLB security group configuration is completed, which only allows traffic to access the CLB instance from port 80.
 <img alt="" src="https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png" >

### Step 3: Configuring the Allow Traffic by Default feature
You can enable or disable the feature as follows:
- Method 1: Enabling the Allow Traffic by Default feature, which allows the real server to keep its port closed.
>?The Allow Traffic by Default feature of security group is in beta, if you want to try it out, please submit a ticket for application. The feature is not supported for classic private network CLB instances and classic network CLB instances.
- Method 2: Disabling the Allow Traffic by Default feature, for which the client IP should be allowed on the CVM security group (`0.0.0.0/0` is used here).

#### Method 1: Enable the Allow Traffic by Default feature
1. Log in to the [CLB console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click the ID of the target CLB instance.
3. Select the **Security Group** tab.
4. Toggle the switch <img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png"> on.
5. After it is enabled, only the security group rule in the **Rule preview** section will be used.
   ![](https://main.qcloudimg.com/raw/6caa47138ecb97cc3c60cb38971792fd.png)

#### Method 2: Disable the Allow Traffic by Default feature
When the feature is disabled, the client IP needs to be allowed on the CVM security group. The business traffic can only access the CVM instance via the CLB port 80, and get service from the CVM port 8080.
>?To allow the traffic from a specified client IP, you need to allow it both on the CLB and CVM security groups. If the CLB instance is not configured with a security group, you will only need to allow it on the CVM security group.
>
1. Configure CVM security group rules
   For the traffic accessing a backend CVM instance, you can configure a CVM security group to only allow service port access. Please go to the [Security Group console](https://console.cloud.tencent.com/cvm/securitygroup) to configure a security group policy. In the inbound rule, open port 8080 for all IPs. To ensure smooth remote CVM login and ping services, please open port 22, port 3389, and ICMP service in the security group.
   ![](https://console.cloud.tencent.com/cvm/instance/index?rid=1)
2. Bind the security group to a CVM instance
 1. Log in to the [CVM console](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fcvm%2Finstance%2Findex%3Frid%3D1), click the ID of the target CVM instance to enter the details page.
 2. Select the **Security Groups** tab and then click **Bind** in the **Bound with security group** section.
 3. In the **Configure Security Group** pop-up window, select a security group and click **OK**.<br><img alt="" src="https://main.qcloudimg.com/raw/6e0e1c2f834bb7425ef3ca010114165a.png" title="Click to see clearly">
