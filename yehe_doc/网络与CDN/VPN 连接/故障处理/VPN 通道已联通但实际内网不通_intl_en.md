## Symptom
A VPN connection is used to connect a VPC to an IDC and the status of the VPN tunnel is **Linked**, but the private network cannot be connected.
![](https://main.qcloudimg.com/raw/5a4bf0112e8a761e80a69ab05031303c.png)

## Possible Causes
If the tunnel is in a normal status yet the private network cannot be connected, the possible causes are as follows:
+ No routes directing to the private IP range in the IDC are added in the route table of the VPC subnet.
+ The security policy on the VPC/IDC side does not make the corresponding source and destination IPs open to Internet
+ No tunnels directing to the private IP range in the IDC are added to the VPN gateway (route-based gateway).
+ The firewall of the operating system of private network server on the VPC/IDC side does not allow the customer IP range to pass
+ The SPD policy on the VPC/IDC side does not contain the source and destination IPs
+ No routing policies are configured in the VPN gateway.


## Troubleshooting
1. Check whether the route table of the VPC subnet contains any route whose destination IP address is the private IP range on the IDC side and whose next hop address is the corresponding VPN gateway. Meanwhile, check whether there is any route on the IDC side whose destination IP address is the VPC IP range and whose next hop address is the corresponding VPN tunnel.
    Go to the [VPC subnet route table](https://console.cloud.tencent.com/vpc/route?fromNav). Click the route table ID to enter the details page and check these aspects:
	![]()
    Execute the command on the IDC side to check the routing (take Huawei’s device as an example):
	
   ```plaintext
   display ip routing-table     //Check whether there is any route whose destination IP address is the cloud VPC IP range and whose next hop is the corresponding VPN tunnel
   ```
   + If so, please go to [Step 3](#step3).
   + If not, please complete the routing information according to business requirements before going to [Step 2](#step2).
2. [](id:step2)Check whether the communication is back to normal. In other words, log in to a server in the VPC/IDC and use the ping command to test the connectivity of the private IP of the peer server.
>?To log in to the CVM in the VPC, please see [Logging in to Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436) or [Logging in to a Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435).
>
    + If it is, the problem is solved.
    - If not, please go to [Step 3](#step3)
3. [](id:step3)Check whether the security group associated with the server in the VPC and the network ACL associated with the subnet allow the traffic from the local IDC to pass through. Meanwhile, check whether the IDC allows the traffic from the cloud VPC to pass through.
   Go to the [server security group in VPC](https://console.cloud.tencent.com/vpc/securitygroup) page. Click the security group ID to enter the “Security Group Rule” page to check:
   ![]()
   Go to [VPC subnet ACL rule](https://console.cloud.tencent.com/vpc/acl), click the network ACL ID to enter the “Basic Info” page, and click “Inbound Rule” tab to check:
    ![]()
    Security policy check on the IDC side (take Huawei Firewall as an example here):
   
   ```plaintext
   display   current-configuration   configuration security-policy
   ```
  + If they do, please go to [Step 5](#step5).
  + If not, please make the private IP ranges of the security devices on the security group/network ACL/IDC side open to Internet, and then go to [Step 4](#step4).
4. [](id:step4)Check whether the communication is back to normal. In other words, log in to a server in the VPC/IDC and use the ping command to test the connectivity of the private IP of the peer server.
    + If it is, the problem is solved.
    + If not, please go to [Step 5](#step5).
5. [](id:step5)Check whether the CVM instance in the VPC and the firewall of the operating system of the server on the private network in the IDC have the policy to open the peer IP range to internet.
   Checking the firewall on a Linux server: `iptables  --list`
   Checking the firewall on a Windows server: **Control Panel** > **System and Security** > **Windows Defender Firewall** > **Allow an app through Windows Firewall**
   + If they do, please go to [Step 7](#step7).
   + If not, please enable the Internet connectivity of the business which needs to be connected in the private network firewall, and then go to [Step 6](#step6).
6. [](id:step6)Check whether the communication is back to normal. In other words, log in to a server in the VPC/IDC and use the ping command to test the connectivity of the private IP of the peer server.
   + If it is, the problem is solved.
   - If not, please go to [Step 7](#step7).
7. [](id:step7)Check whether the proxy identity (SPD policy) of VPN tunnels on the VPC and IDC sides contains private IP ranges that need to be interconnected.
   Go to the [SPD policy page in the VPC console](https://console.cloud.tencent.com/vpc/vpnConn?rid=1). Click the **VPN tunnel ID** to enter the **Basic information** page, and you can check the SPD policy:
	 ![]()
    SPD policy check on the IDC side (take Huawei Firewall as an example here):
	
   ```plaintext
   display current-configuration configuration acl
   ```
   + If it is, please go to [Step 8](#step8).
   + If not, please add the missing SPD policies and go to [Step 8](#step8)
8. [](id:step8)Check whether the route table of the VPN gateway contains the required routing policy. On the **VPN gateway** page, click the ID of the target VPN gateway to enter the **Route table** page, and you can check the routing policies.
   ![]()
   
    + If so, please go to [Step 9](#step9).
    + If not, specify the next hop on the **Route** tab and perform [step 9](#step9).
    ![]()
9. [](id:step9)Check whether the communication is back to normal. In other words, log in to a server in the VPC/IDC and use the ping command to test the connectivity of the private IP of the peer server.
   + If it is, the problem is solved.
   + If not, please go to [Step 10](#step10).
10. [](id:step10)Collect the troubleshooting information above and [submit a ticket](https://console.cloud.tencent.com/workorder/category) or ask the device manufacturer for help.
