## Problems

The CVM instance on the local server may be unreachable when pinged for the following reasons:
- Incorrect destination server configuration
- The domain name resolution fails
- The link is abnormal

If the local network is normal (that is, other websites can be pinged through), troubleshoot the problem as follows:
- [Check whether the instance is configured with a public IP address](#isConfigurePublicIP)
- [Check the security group settings](#CheckSecurityGroupSetting)
- [Check the OS settings](#CheckOSSetting)
- [Perform other operations](#OtherOperations)

## Troubleshooting


### Check whether the instance is configured with a public IP address[](id:isConfigurePublicIP)

<dx-alert infotype="explain" title="">
Only CVM instances configured with public IP addresses can communicate with other computers on the Internet. For CVM instances that are not configured with public IP addresses, the attempt to ping through the private IP address of an instance through the Internet will fail.
</dx-alert>


1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the ID or the name of the target instance to access its details page.
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. Check whether the instance is configured with a public IP address under **Network Information**.
   - If yes, [check the security group settings](#CheckSecurityGroupSetting).
   - If no, [bind an EIP to the instance](https://intl.cloud.tencent.com/document/product/213/16586).


### Check the security group settings[](id:CheckSecurityGroupSetting)

A security group is a virtual firewall that allows you to control the inbound and outbound traffic of an associated instance. You can specify the protocol, port, and policy in a security group rule. The ICMP protocol is used in the ping test. Therefore, you need to check whether ICMP is allowed in the security group associated with the instance. To view the security group associated with the instance and its inbound and outbound rules, perform the following steps:
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the ID or the name of the target instance to access the instance details page.
3. Click the **Security groups** tab to access the security group management page of the instance.
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. Check the security group associated with the instance and the detailed inbound and outbound rules to determine whether this security group allows ICMP.
   - If yes, [check the OS settings](#CheckOSSetting).
   - If no, enable the ICMP protocol policy in the security group.


### Check the OS settings[](id:CheckOSSetting)

Based on the operating system (OS) of the instance, select one of the following methods to check the OS settings:
- For the Linux OS, [check the Linux kernel parameters and the firewall settings](#CheckLinux).
- For the Windows OS, [check the Windows firewall settings](#CheckWindows). If the firewall settings are correct, try to [reset the Windows network settings](#reset).


#### Checking Linux kernel parameters and firewall configurations[](id:CheckLinux)

<dx-alert infotype="explain" title="">
In the Linux system, the kernel and the firewall settings determine whether a ping test is allowed. If the ping test is prohibited in either settings, "Request timeout" will be returned in a ping test.
</dx-alert>

##### Checking the kernel parameter `icmp_echo_ignore_all`

1. Log in to the instance via VNC. For details, see:
   - [Logging into Linux Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
   - [Logging into Windows Instances via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Run the following command to view the `icmp_echo_ignore_all` settings of the system:
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
   - If 0 is returned, the OS allows all ICMP Echo requests. In this case, [check the firewall settings](#CheckLinuxFirewall).
   - If 1 is returned, the OS denies all ICMP Echo requests. In this case, perform [step 3](#Linux_step03).

3. [](id:Linux_step03)Run the following command to change the settings of the kernel parameter icmp_echo_ignore_all.
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```


##### Checking the firewall settings[](id:CheckLinuxFirewall)

Run the following command to check whether the firewall rule and the corresponding ICMP rule of the current server are disabled:
```
iptables -L
```
- If the following result is returned, the corresponding ICMP rules are active.
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
- If the return result indicates that the corresponding ICMP rules are inactive, run the following commands to activate them.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```


#### Checking the Windows firewall settings[](id:CheckWindows)

1. Log in to the instance.
2. Open the **Control panel**, and select **Windows firewall settings**.
3. On the **Windows firewall** page, select **Advanced settings**.
4. In the pop-up "Windows firewall with advanced security" window, check whether ICMP inbound and outbound rules are disabled.
   - If ICMP inbound and outbound rules are disabled, please enable them.

### Reset the Windows network settings

1. Check whether your VPC network supports DHCP (DHCP is supported by a VPC network created after June 2018). If it does not support DHCP, check whether the static IP in the network settings is correct.
2. If it supports DHCP, check whether the private IP of DHCP is correct. If it is incorrect, log in via VNC on the official website, and run `PowerShell` as the admin. Implement `ipconfig /release` and `ipconfig/renew` (without the need to restart the instance) to re-obtain the IP.
3. If the IP of DHCP is correct, but the network still cannot be connected, click **Start** > **Run**, enter ` ncpa.cpl ` and click **OK**. Open the local connection, try to disable and enable the ENI.
4. If the problem persists, please run the following command in CMD as the admin, and restart the instance.
```plantext
reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles"  /f
```

### Other operations[](id:OtherOperations)

If you cannot solve the problem by performing the operations above, perform the following operations:
- If the domain name cannot be pinged through, check your website configurations.
- If the public IP address cannot be pinged through, [submit a ticket](https://console.cloud.tencent.com/workorder/category) and attach relevant information about the instance and the two-way (from the local server to the CVM and from the CVM to the local server) MTR data to receive assistance.
For more information on how to use MTR, see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).


