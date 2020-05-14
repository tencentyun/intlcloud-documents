## Problem

A local server fails to ping through an instance. Possible causes include:
- Incorrect destination server configuration
- Unsuccessful domain name resolution
- Link failure

If the local network is working normally (for example, other websites can be pinged through from the local network), troubleshoot this problem as follows:
- [Check whether the instance is configured with a public IP address](#isConfigurePublicIP).
- [Check security group settings](#CheckSecurityGroupSetting).
- [Check OS settings](#CheckOSSetting).
- [Perform other operations](#OtherOperations).

## Directions

<span id="isConfigurePublicIP"></span>
### Checking whether the instance is configured with a public IP address

> An instance can interwork with other computers on the Internet only if it has a public IP address. Without a public IP address, the instance cannot be pinged through outside the private IP address.
>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the "Instance List" page, select the instance ID or instance name to ping to go to the instance details page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Check whether the instance is configured with a public IP address in the "Network Information" area.
 - If yes, [check security group settings](#CheckSecurityGroupSetting).
 - If no, [bind an elastic public IP address to the instance](https://intl.cloud.tencent.com/document/product/213/16586).

<span id="CheckSecurityGroupSetting"></span>
### Checking security group settings

A security group is a virtual firewall that controls the inbound and outbound traffic of the associated instance. You can specify protocols, ports, and policies for the rules of a security group. Check whether ICMP that is used in the ping test is allowed in the security group associated with the instance. You can perform the following operations to view information on the security group associated with the instance and its inbound and outbound rules:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the "Instance List" page, select the instance ID or instance name that needs to be configured with a security group to go to the instance details page, as shown in the following figure:
3. Click the **Security Groups** tab to go to the security group management page for this instance, as shown in the following figure:
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Verify whether the security group associated with the instance allows ICMP based on the security group used by the instance and the detailed inbound and outbound rules.
 - If yes, [check OS settings](#CheckOSSetting).
 - If no, set the ICMP protocol policy to allow.

<span id="CheckOSSetting"></span>
### Checking OS settings

Choose a check method based on the OS type of the instance.
- For the Linux OS, [check Linux kernel parameters and firewall settings](# CheckLinux).
-For the Windows OS, [check Windows firewall settings](#CheckLinux).

<span id="CheckLinux"></span>
#### Checking Linux kernel parameters and firewall settings

> In the Linux OS, whether a ping test is allowed depends on both kernel and firewall settings. If either of them forbids the ping test, "Request timeout" occurs.

##### Checking the icmp_echo_ignore_all kernel parameter

1. Log in to the instance.
2. Run the following command to view the icmp_echo_ignore_all setting in the OS:
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - If the return result is 0, the OS allows all ICMP Echo requests. In this case, [check firewall settings](#CheckLinuxFirewall).
 - If the return result is 1, the OS forbids all ICMP Echo requests. In this case, perform [step 3](#Linux_step03).
3. <span id = "Linux_step03"> Run the following command to change the setting of the icmp_echo_ignore_all kernel parameter: </ span>
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### Checking firewall settings

Run the following command to check whether the firewall rules and corresponding ICMP rules of the current server are banned:
```
iptables -L
```
- If the following result is returned, the ICMP rules are not banned. In this case, [check whether the domain name is filed](#CheckDomainRegistration).
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
- If the return result shows that the ICMP rules are banned, run the following commands to enable these rules:
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Checking Windows firewall settings

1. Log in to the instance.
2. Open **Control Panel** and select **Windows Firewall Settings**.
3. On the "Windows Firewall" page, select **Advanced Settings**.
4. In the "Advanced Security Windows Firewall" window that appears, check whether the inbound and outbound rules for ICMP are banned.
 - If the inbound and outbound rules for ICMP are banned, enable these rules.


<span id="OtherOperations"></span>
### Other operations

If the preceding operations cannot solve the problem, do the following:
- If the domain name cannot be pinged through, check your website configuration.
- If the public IP address cannot be pinged through, attach information on the instance and two-way MTR data (from the local server to the CVM and from the CVM to the local server) to a ticket and [submit the ticket](https://console.cloud.tencent.com/workorder/category) to contact our engineers for assistance.
For more information on how to use MTR, see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).
