## Problem

A failed ping test from a local server to an instance may be caused by the following:
- Incorrect server configuration
- Unsuccessful domain name resolution
- Linkage failure

If the local network is normal (i.e. other websites can be pinged), you can troubleshoot this problem by the following steps:
- [Check whether the instance is configured with a public IP](#isConfigurePublicIP)
- [Check the security group configuration](#CheckSecurityGroupSetting)
- [Check the OS configuration](#CheckOSSetting)
- [Check the domain name registration](#CheckDomainRegistration)
- [Other operations](#OtherOperations)

## Directions

<span id="isConfigurePublicIP"></span>
### Check whether the instance is configured with a public IP

> Only instance with public IP can access and be accessed by other computers on the Internet. An instance without public IP cannot be pinged outside the private IP.
>
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the “Instances” page, select the ID/name of the instance to be pinged to enter the instance details page, as shown below:
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Check whether the instance is configured with a public IP in “Network Information”.
 - If yes, please [check security group configuration](#CheckSecurityGroupSetting).
 - If no, please [bind an elastic public IP with the CVM](https://intl.cloud.tencent.com/document/product/213/16586).

<span id="CheckSecurityGroupSetting"></span>
### Check the security group configuration

Security group is a virtual firewall that allows you to control the inbound and outbound traffic of the associated instance. You can specify the protocol, port and policy of a security group rule. Check whether the ICMP protocol used in ping test is allowed in the security group associated with the instance. You can view the security group associated with the instance and its inbound/outbound rules by the following steps:
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the “Instances” page, select the ID/name of the instance to be configured with the security group to enter the instance details page, as shown below:
3. Select the **Security Groups** tab to enter the security group management page of the instance, as shown below:
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Verify whether the security group associated with the instance allows ICMP based on the security group used by the instance and the detailed inbound and outbound rules.
 - If yes, please [check OS configuration](#CheckOSSetting).
 - If no, please configure the ICMP protocol policy as allow.

<span id="CheckOSSetting"></span>
### Check the system configuration

Choose different methods to check the system configuration based on its operating system.
- For Linux OS, please [check Linux kernel parameters and firewall configuration](# CheckLinux).
-For Windows OS, please [check Windows firewall configuration](#CheckLinux).

<span id="CheckLinux"></span>
#### Checking kernel parameters and firewall configuratio on Linux

> On Linux system, whether a ping test is allowed depends on both kernel and firewall configuration. If either of them blocks the ping test, "Request timeout" occurs.

##### Checking kernel parameters icmp_echo_ignore_all

1. Log in to the instance.
2. Execute the following command to view the icmp_echo_ignore_all configuration of the system.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - If 0 is returned, the system allows all ICMP Echo requests. Please [check the firewall configuration](#CheckLinuxFirewall).
 - If 1 is returned, the system blocks all ICMP Echo requests. Please execute [Step 3](#Linux_step03).
3. <span id = "Linux_step03"> Execute the following command to modify the configuration of the kernel parameter icmp_echo_ignore_all. </ span>
```
echo "1" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### Checking firewell configuration

Execute the following command to check whether firewall rules of the current server and corresponding rules for ICMP are disabled.
```
iptables -L
```
- If the following result is returned, corresponding rules for ICMP are not disabled. Please [check the domain name registration](#CheckDomainRegistration).
```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination  
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
```
- If the result is returned that corresponding rules for ICMP are disabled. Please execute the following command to enable them.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Checking firewall configuration on Windows

1. Log in to the instance.
2. Open **Control Panel** to select **Windows Firewall**
3. On the "Windows Firewall" page, select **Advanced settings**
4. In the pop-up “Windows Firewall with Advanced Security** window, check whether inbound and outbound rules for ICMP are disabled.
 - If inbound and outbound rules for ICMP are disabled, please enable them.

 - If inbound and outbound rules for ICMP have been enabled, please [check the domain name registration](#CheckDomainRegistration).

<span id="CheckDomainRegistration"></span>
### Check whether the domain name has been registered

> If you can ping the public IP but not the domain name, it may be because the domain name has not been registered or domain name resolution has an exception.
>
The Ministry of Industry and Information Technology stipulates that websites that have not obtained a permit or have not fulfilled ICP filing must not engage in Internet information services, otherwise the act is illegal. To ensure the normal running of the website, if you need to start a website, we recommend you perform website ICP filing first, obtain the ICP number issued by the Communications Authority, and then enable access.
- If your domain name has not been registered, please perform [domain name ICP filing](https://console.cloud.tencent.com/beian) first.
- If you use Tencent Cloud domain name service, you can log in to [Domain Name Service Console] (https://console.cloud.tencent.com/domain) to view the corresponding domain name situation.
- If your domain name has been registered, please check DNS.

<span id="OtherOperations"></span>
### Other Operations

If the above operations cannot solve the problem, please refer to:
- If the domain name cannot be pinged, check your website configuration.
- If the public IP cannot be pinged, contact our technical personnel to locate the problem by [submitting a ticket](https://console.cloud.tencent.com/workorder/category) along with relevant instance information and MTR data (from local server to CVM and from CVM to local server).
For more information on how to use MTR, please see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).
