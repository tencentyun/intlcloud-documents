### How can I use the NAT gateway and EIP?
- The NAT gateway provides the capability to translate between private IPs and public IPs in a VPC. It is an ingress/egress for public network traffic in a VPC. For instructions on using the Tencent Cloud NAT gateway, see [NAT Gateway](https://cloud.tencent.com/document/product/215/4975).
- The NAT gateway and EIP are two ways for the CVM to access the Internet. You can use either one of them or both of them to design your public network access architecture. For more information, see [Solution](https://cloud.tencent.com/document/product/215/4975#nat-.E7.BD.91.E5.85.B3.E5.92.8C.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip-.E7.9A.84.E4.BD.BF.E7.94.A8).



### How can I create an NAT gateway?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to create an NAT gateway. For more information, see [Creating NAT Gateways](https://cloud.tencent.com/document/product/552/18186#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.88.9B.E5.BB.BA-nat-.E7.BD.91.E5.85.B3).


### How can I modify the NAT gateway configuration?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to modify the attributes of a created NAT gateway. For more information, see [Modifying NAT Gateway Configuration](https://cloud.tencent.com/document/product/552/18179).


### How can I manage the EIPs bound to the NAT gateway?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to manage the EIPs bound to the NAT gateway. For more information, see [Managing EIPs Bound to NAT Gateway](https://cloud.tencent.com/document/product/552/18180).


### How can I view NAT gateway monitoring information?
After logging in to [Tencent Cloud Console](https://console.cloud.tencent.com/), you can view monitoring information and export data via the console to view NAT gateway monitoring information. For more information, see [Viewing NAT Gateway Monitoring Information](https://cloud.tencent.com/document/product/552/18181).

### How can I set alarms?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to set alarms for NAT gateways to monitor their status. For more information, see [Setting Alarm](https://cloud.tencent.com/document/product/552/18182).

### How can I delete an NAT gateway?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and delete an NAT gateway if you do not need it. For more information, see [Deleting NAT Gateway](https://cloud.tencent.com/document/product/552/18183).

### How can I enable gateway traffic control details?
After logging in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and enabling "Gateway Traffic Control Details", you can view the metrics of IP traffic passing through an NAT gateway over the last 7 days, and also set the outbound bandwidth from an IP to a specific NAT gateway. For more information, see [Enabling Gateway Traffic Control Details](https://cloud.tencent.com/document/product/552/18184).

### How can I set gateway traffic control details?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to set the outbound bandwidth from an IP to a specific NAT gateway. For more information, see [Setting Gateway Traffic Control Details](https://cloud.tencent.com/document/product/552/18242).


### How can I view gateway traffic control details?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to view the traffic control details for the restricted IP. For more information, see [Viewing Gateway Traffic Control Details](https://cloud.tencent.com/document/product/552/18239).

### How can I bind a high defense package?
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) to bind a high defense package to the NAT gateway to defend against DDoS attacks. For more information, see [Binding Steps](https://cloud.tencent.com/document/product/552/18185).

### How can I configure port mapping on an NAT gateway in the VPC?

Currently, a dynamic NAT random corresponding port is used within the network and writing a static NAT is not supported.


### Where can I find more information on security?
Tencent Cloud provides various network and security services such as security groups, encrypted login, and EIPs to ensure that your instance provides internal and external services securely, efficiently, and freely. For more information on CVM security, see [Network and Security Overview](/document/product/213/5220).

### How can I prevent others from viewing my system?
You can completely control the visibility of your system, and the CVM allows you to place running instances into any security group you select. On the [Console - Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, you can specify inter-group communication and IP subnets on the network that can communicate with the CVM.

### How can I troubleshoot security issues?
For suspected security risks or adverse events, see [Security Help Guide](/document/product/301/9610) for troubleshooting, and see [CVM Security](/document/product/296) to resolve security issues. 

