### Will traffic coming out from a NAT firewall pass through the firewall for twice?
Yes, one for intranet IP address and the other for public IP address.

### What is the difference between Create New mode and Use Existing mode of a NAT firewall?
- Create New mode: If no NAT gateway is available in the current region, you can specify an instance to pass the firewall for accessing Internet by using the built-in NAT feature of the NAT firewall in Create New mode.
- Use Existing mode: If a NAT gateway is available in the current region, or you want a public outbound IP address to remain unchanged, you can use the Use Existing mode to smoothly access the NAT edge firewall between the NAT gateway and CVM instance.

### Can I use a NAT edge firewall to replace the existing NAT gateway?	
Yes. You can use a NAT edge firewall to replace the existing NAT gateway.

### Can a NAT edge firewall be enabled for a specified subnet only?
Yes. You can choose to enable the firewall toggle for the current subnet, or for all subnets in the route table associated with the current subnet.

### Will the network be interrupted when a NAT edge firewall is bound with an EIP?
No. Binding will not cause a network interruption.

### Will the network be interrupted when the NAT firewall toggle is turned on/off?
- Enable: If you enable the NAT edge firewall feature for a specified subnet only, the system will automatically add a routing policy with the next hop being the NAT edge firewall in the current route table and disable the original routing policies. In this case, Internet traffic of the current subnet will go through the NAT edge firewall.

- Disable: If you disable the NAT edge firewall feature for a specified subnet only, the system will automatically disable the routing policy with the next hop being the NAT edge firewall. In this case, this subnet will be disconnected from the Internet.

### Can I configure continuous ports for DNAT?
No. It is not allowed to configure multiple ports under the same rule. Each DNAT port uses one rule.

### Can I configure SNAT for a NAT edge firewall? You can perform the following operations to configure SNAT.	
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/switch), and select **Firewall toggle** -> **NAT edge firewall** to enter the NAT edge firewall page.
2. Select **Instance configuration** -> **Bound egress** -> **Create rule** in the Action column on the left.
3. Select the external IP address of the specified subnet or private network, and then click **OK**.

### How can I query subnets enabled with the firewall feature?
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/switch), and select **Firewall toggle** -> **NAT edge firewall** to enter the NAT edge firewall page.
2. Enter the **Firewall toggle** page to view all subnets enabled or disabled with the firewall feature.

### Do I need to restart my server after enabling the DNS feature in instance configuration? Will the feature take effect without a restart?	
You do not need to restart your server. Restarting your server will only validate the configuration sooner. This is similar to configuring DNS effective time on the VPC console. You can run the following commands to update your network configuration:
- Linux: dhclient
- Windows: ipconfig/flushdns

### How frequently will assets be automatically synchronized?	
Every 10 minutes.

### Why can't I enable the NAT firewall feature for a subnet?	
This situation may be caused by asynchronization of a changed asset scale. You can log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/switch), go to **Firewall toggle** -> **Edge firewall** -> **Sync assets** to manually synchronize the subnet asset information, and then try to enable the firewall feature again.

### How can I change the VPC for a NAT firewall?	
Click the Settings button in the upper right corner, and then access another VPC.

### How many VPCs can be bound to a NAT firewall?
There are no limitations currently.

### What if I failed to create a NAT edge firewall?
If your VPC has private line or peer connections, at least one 24/subnet must be reserved for firewall access.

### Why can't I access an allocated EIP after the NAT firewall feature is enabled?
A newly allocated EIP can be accessed only after being bound.
