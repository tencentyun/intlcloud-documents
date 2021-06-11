## Error description
A VPN connection is used to connect VPC to IDC and the status of VPN tunnel is **Connected**, but the server of the VPC failed to ping the private IP of the IDC.

## Possible causes
If the tunnel is in a normal status yet the private network cannot be connected, the possible causes are as follows:
+ No routes directing to the private IP range in the IDC are added in the route table of the VPC subnet.
+ The security policy on the VPC/IDC side does not make the corresponding source and destination IPs open to Internet
+ The firewall of the operating system of private network server on the VPC/IDC side does not allow the customer IP range to pass
+ The SPD policy on the VPC/IDC side does not contain the source and destination IPs

## Solutions
1. Check whether the route table of the VPC subnet contains any route whose destination IP address is the private IP range on the IDC side and whose next hop address is the corresponding VPN gateway. Meanwhile, check whether there is any route on the IDC side whose destination IP address is the VPC IP range and whose next hop address is the corresponding VPN tunnel.
    Go to the [VPC subnet route table](https://console.cloud.tencent.com/vpc/route?fromNav). Click the route table ID to enter the details page and check these aspects.

    Execute the command on the IDC side to check the routing (take Huawei’s device as an example):
	```plaintext
display ip routing-table     //Check whether there is any route whose destination IP address is the cloud VPC IP range and whose next hop is the corresponding VPN tunnel
   ```
   + If so, please go to [Step 3](#step3).
   + If not, please complete the routing information according to business requirements before going to [Step 2](#step2).
2. <span id="step2"></span>Check whether the communication is back to normal. In other words, log in to a CVM in the VPC/IDC and use the ping command to test the connectivity of the private IP of the customer server.
>?To log in to the CVM in the VPC, please see [Logging in to Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436) or [Logging in to a Windows Instance](https://intl.cloud.tencent.com/document/product/213/5435).
>
    + If it is, the problem is solved.
    - If not, please go to [Step 3](#step3).
3. <span id="step3"></span>Check whether the security group associated with the VPC server and the network ACL associated with the subnet allow the traffic in the local IDC to pass through. Meanwhile, check whether the IDC allows the traffic in the cloud VPC to pass through.
Go to the [server security group in VPC](https://console.cloud.tencent.com/vpc/securitygroup) page. Click the security group ID to enter the “Security Group Rule” page to check.
Go to [VPC subnet ACL rule](https://console.cloud.tencent.com/vpc/acl), click the network ACL ID to enter the “Basic Info” page, and click “Inbound Rule” tab to check.

 Security policy check on the IDC side (take Huawei Firewall as an example here):
   ```plaintext
display   current-configuration   configuration security-policy
   ```
  + If they do, please go to [Step 5](#step5).
  + If not, please make the private IP ranges of the security devices on the security group/network ACL/IDC side open to Internet, and then go to [Step 4](#step4).
4. <span id="step4"></span>Check whether the communication is back to normal. In other words, In other words, log in to a CVM in the VPC/IDC and use the ping command to test the connectivity of the private IP of the customer server.
    + If it is, the problem is solved.
    + If not, please go to [Step 5](#step5).
5. <span id="step5"></span>Check whether the CVM in VPC and the firewall of the operating system of the private network server on the IDC side have the policy to open the customer IP range to Internet.
   Checking the firewall in a Linux server: `iptables  --list`
   Checking the firewall in a Windows server: Control Panel\System and Security\Windows Firewall\Apps Allowed
   + If they do, please go to [Step 7](#step7).
   + If not, please enable the Internet connectivity of the business which needs to be connected in the private network firewall, and then go to [Step 6](#step6).
6. <span id="step6"></span>Check whether the communication is back to normal. In other words, In other words, log in to a CVM in the VPC/IDC and use the ping command to test the connectivity of the private IP of the customer server.
   + If it is, the problem is solved.
   - If not, please go to [Step 7](#step7).
7. <span id="step7"></span>Check whether the proxy identity (SPD policy) of VPN tunnels on the VPC and IDC sides contain private IP ranges that need to be interconnected.
   Go to [SPD policy on VPC side](https://console.cloud.tencent.com/vpc/vpnConn?rid=1). Click the VPN tunnel ID to go to the “Basic Info” page, and you can check the SPD policy.

    Security policy check on the IDC side (take Huawei Firewall as an example here):
	```plaintext
display current-configuration configuration acl
   ```
   + If it is, please go to [Step 9](#step9).
   + If not, please add the missing SPD policies and go to [Step 8](#step8).
8. <span id="step8"></span>Check whether the communication is back to normal. In other words, In other words, log in to a CVM in the VPC/IDC and use the ping command to test the connectivity of the private IP of the customer server.
   + If it is, the problem is solved.
   + If not, please go to [Step 9](#step9).
9. <span id="step9"></span>Collect the troubleshooting information above and [submit a ticket](https://console.cloud.tencent.com/workorder/category) or ask the device manufacturer for help.
