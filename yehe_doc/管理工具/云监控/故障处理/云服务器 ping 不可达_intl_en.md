## Overview
This document describes how to troubleshoot and solve the problem of a CVM instance being unreachable when pinged.

## Problem Analysis

The CVM instance on the local server may be unreachable when pinged for the following reasons:

- The target CVM configuration is incorrect
- The domain name resolution fails
- The link is abnormal

  

## Troubleshooting Approaches

If the local network is normal (that is, other websites can be pinged through), troubleshoot the problem as follows:

- [Check whether the instance is configured with a public IP address](#isConfigurePublicIP)
- [Check the security group settings](#CheckSecurityGroupSetting)
- [Check the OS settings](#CheckOSSetting)
- [Check whether the domain name is registered](#CheckDomainRegistration)
- [Check the DNS](#CheckDNS)
- [Perform other operations](#OtherOperations)

## Directions

<span id="isConfigurePublicIP"></span>

### Checking whether the instance is configured with a public IP address

>? Only CVM instances configured with public IP addresses can communicate with other computers on the Internet. For CVM instances that are not configured with public IP addresses, the attempt to ping through the private IP address of an instance through the Internet will fail.
>
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the ID or the name of the target instance to access its details page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Check whether the instance is configured with a public IP address under "Network Information".
 - If yes, [check the security group settings](#CheckSecurityGroupSetting).
 - If no, [bind an EIP](https://intl.cloud.tencent.com/document/product/213/16586#.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip-.E7.BB.91.E5.AE.9A.E4.BA.91.E4.BA.A7.E5.93.81).

<span id="CheckSecurityGroupSetting"></span>
### Checking the security group settings

A security group is a virtual firewall that allows you to control the inbound and outbound traffic of an associated instance. You can specify the protocol, port, and policy in a security group rule. The ICMP protocol is used in the ping test. Therefore, you need to check whether ICMP is allowed in the security group associated with the instance. To view the security group associated with the instance and its inbound and outbound rules, perform the following steps:
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the ID or the name of the target instance to access the instance details page.
3. Click the **Security Groups** tab to access the security group management page of the instance, as shown in the following figure:
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Check the security group associated with the instance and the detailed inbound and outbound rules to determine whether this security group allows ICMP.
 - If yes, [check the OS settings](#CheckOSSetting).
 - If no, enable the ICMP protocol policy in the security group.

<span id="CheckOSSetting"></span>
### Checking the OS settings

Based on the operating system (OS) of the instance, select one of the following methods to check the OS settings:
- For the Linux OS, [check the Linux kernel parameters and the firewall settings](#CheckLinux).
- For the Windows OS, [check the Windows firewall settings](#CheckLinux).

<span id="CheckLinux"></span>
#### Checking the Linux kernel parameters and the firewall settings

>? In the Linux system, the kernel and the firewall settings determine whether a ping test is allowed. If the ping test is prohibited in either settings, "Request timeout" will be returned in a ping test.

##### Checking the kernel parameter `icmp_echo_ignore_all`

1. Log in to the instance.
2. Run the following command to view the settings of icmp_echo_ignore_all.
```plaintext
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - If 0 is returned, the OS allows all ICMP Echo requests. In this case, [check the firewall settings](#CheckLinuxFirewall).
 - If 1 is returned, the OS denies all ICMP Echo requests. In this case, perform [step 3](#Linux_step03).
3. <span id="Linux_step03">Run the following command to change the settings of the kernel parameter icmp_echo_ignore_all.</span>
```plaintext
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### Checking the firewall settings

Run the following command to check whether the firewall rules of the CVM instance and the corresponding ICMP rules are deactivated.
```plaintext
iptables -L
```
- If the following result is returned, the ICMP rules are active. In this case, [check whether the domain name is registered](#CheckDomainRegistration).
```plaintext
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination  
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
```
- If the return result indicates that the corresponding ICMP rules are inactive, run the following commands to activate them.
```plaintext
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Checking the Windows firewall settings

Check the Windows firewall settings.
1. Log in to the instance.
2. Open **Control Panel** and select **Windows Firewall**.
3. On the **Windows Firewall** page, select **Advanced settings**.
4. In the **Windows Firewall with Advanced Security** window that appears, check whether the inbound or outbound rules for ICMP are deactivated.
5. If the inbound or outbound rules for ICMP are deactivated, please activate them.
### Performing other operations

If you cannot solve the problem by performing the operations above, perform the following operations:
- If the domain name cannot be pinged through, check your website configurations.
- If the public IP address cannot be pinged through, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and attach relevant information about the instance and the two-way (from the local server to the CVM and from the CVM to the local server) MTR data to receive assistance.
For more information on how to use MTR, see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).