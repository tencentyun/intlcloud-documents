## Problem

A local server fails to ping an instance. Possible causes include:
- Incorrect destination server configuration
- Unsuccessful domain name resolution
- Linkage failure

If the local network is normal (other websites can be pinged from the local network), troubleshoot as follows:
- [Check whether the instance is configured with a public IP address](#isConfigurePublicIP).
- [Check the security group configuration](#CheckSecurityGroupSetting).
- [Check the operating system configuration](#CheckOSSetting).
- [Perform other operations](#OtherOperations).

## Directions

<span id="isConfigurePublicIP"></span>
### Checking whether the instance is configured with a public IP address

>? An instance can access other computers on the Internet only if it has a public IP address. Otherwise, the instance cannot be pinged through outside the private IP address.
>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the "Instances" page, select the ID/name of the instance to ping to enter the instance details page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Check whether the instance is configured with a public IP address in "Network Information".
 - If yes, [check the security group configuration](#CheckSecurityGroupSetting).
 - If no, [bind an elastic public IP address to the instance](https://intl.cloud.tencent.com/document/product/213/16586).

<span id="CheckSecurityGroupSetting"></span>
### Checking the security group configuration

A security group is a virtual firewall that controls the inbound and outbound traffic of the associated instance. You can specify the protocol, port, and policy in a security group rule. Because ICMP is used in the ping test, you need to check whether the protocol is allowed in the security group associated with the instance. To view the security group associated with the instance and its inbound and outbound rules, perform the following steps:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the "Instances" page, select the ID/name of the instance to be configured with a security group to enter the instance details page, as shown in the following figure:
3. Click the **Security Groups** tab to enter the security group management page of this instance, as shown in the following figure:
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Check the security group associated with the instance and the detailed inbound and outbound rules to determine whether this security group allows ICMP.
 - If yes, [check the operating system configuration](#CheckOSSetting).
 - If no, configure the ICMP protocol policy to allow.

<span id="CheckOSSetting"></span>
### Checking the operating system configuration

Based on the operating system of the instance, select a method to check the configuration:
- For Linux operating system, [check Linux kernel parameters and firewall configurations](# CheckLinux).
-For Windows operating system, [check the Windows firewall configuration](#CheckLinux).

<span id="CheckLinux"></span>
#### Checking Linux kernel parameters and firewall configurations

>? Whether a ping test is allowed in Linux operating system depends on both kernel and firewall configurations. If either of them denies the ping test, "Request timeout" occurs.

##### Checking the icmp_echo_ignore_all kernel parameter

1. Log in to the instance.
2. Run the following command to view the icmp_echo_ignore_all system configuration.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - If 0 is returned, all ICMP Echo requests are allowed by the system. In this case, [check the firewall configuration](#CheckLinuxFirewall).
 - If 1 is returned, all ICMP Echo requests are denied by the system. In this case, perform [step 3](#Linux_step03).
3. <span id = "Linux_step03"> Run the following command to modify the configuration of the icmp_echo_ignore_all kernel parameter.</ span>
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### Checking the firewall configuration

Run the following command to check whether the firewall rule and the corresponding ICMP rule of the current server are disabled:
```
iptables -L
```
- If the following result is returned, the ICMP rule is not disabled. In this case, [check whether the domain name has ICP filing](#CheckDomainRegistration) (for domain names served in Mainland China).
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
- If the return result shows that the ICMP rule is disabled, run the following commands to enable it.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Checking the Windows firewall configuration

1. Log in to the instance.
2. Open **Control Panel** and select **Windows Firewall**.
3. On the "Windows Firewall" page, select **Advanced settings**.
4. In the pop-up "Windows Firewall with Advanced Security" window, check whether ICMP inbound and outbound rules are disabled.
 - If ICMP inbound and outbound rules are disabled, please enable them.


<span id="OtherOperations"></span>
### Other operations

If the previous operations cannot troubleshoot the problem, refer to the following:
- If the domain name cannot be pinged, check your website configuration.
- If the public IP address cannot be pinged, attach information on the instance and two-way MTR data (from the local server to the CVM and from the CVM to the local server), and [submit the ticket](https://console.cloud.tencent.com/workorder/category) to contact our engineers for assistance.
For more information on how to use MTR, see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).
