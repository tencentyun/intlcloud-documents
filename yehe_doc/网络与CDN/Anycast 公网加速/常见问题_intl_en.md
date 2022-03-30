### What is Anycast Internet Acceleration (AIA)?
Anycast Internet Acceleration (AIA) is a cross-region dynamic acceleration network that significantly enhances your businesses' access to public network. Different from other acceleration services at the application layer, AIA can achieve IP transfer optimization and multi-entry nearby access, while reducing issues such as network jitter and packet loss, which can ultimately improve the service quality of your in-cloud applications, expand their service scope, and streamline backend deployment.

### What's the difference between an Anycast EIP and Public IP?
An Anycast EIP is published in multiple regions simultaneously, so that the access traffic can reach the nearest region for transfer over Tencent Cloud private network. It works based on Anycast, so the bandwidth price is higher.
A public IP or EIP is only published in the region to which it belongs, and generally, the access traffic reaches it over the public network.
<table>
<tr>
<th width="20%">Item</th>
<th width="40%">Anycast EIP</th>
<th width="40%">Public IP</th>
</tr>
<tr>
<td>Publishing method</td>
<td>Anycast</td>
<td>Unicast</td>
</tr>
<tr>
<td>IP publishing region</td>
<td>Multiple</td>
<td>Single</td>
</tr>
<tr>
<td>Network price</td>
<td>Higher unit price, bill by bandwidth</td>
<td>Lower unit price, bill according to <a href="https://intl.cloud.tencent.com/document/product/213/39743">Public Network Fee</a>.
</tr>
<tr>
<td>Unbinding</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>AIA</td>
<td>Available</td>
<td>Unavailable. The public network is used by default, and when it fails, temporary free traffic scheduling will be provided.</td>
</tr>
</table>

### Why are regions isolated?
Different regions of Tencent Cloud are completely isolated to ensure maximal stability and fault tolerance among those regions.

### What is an acceleration region?
An acceleration region is where an Anycast EIP is published.
More acceleration regions will be supported as Tencent Cloud's infrastructure expands. Currently, transfers among Europe, United States, and Asia Pacific are accelerated.
>?AIA only provides acceleration services for regions other than the Chinese mainland and does not accelerate cross-border transmission between the Chinese mainland and overseas regions.
>


### What is a service region?
A service region is the region to which an Anycast EIP belongs after it is created. The EIP can only be bound to resources in its region. Backend logic computing (such as CVM) is performed there.

### What is the difference between a private IP and a public IP of a CVM instance?
A private IP is a connection address that provides services for a client whose source IP is from the private network.
Public IP: A connection address that provides public network communication for a client whose source IP is a public network.
They can be directly mapped to each other through network address translation.
Servers in the same region can communicate via private network. Servers across different regions can only communicate via public network.

### Why is AIA more expensive than public network?
If you purchase an Anycast EIP for constant acceleration, you need to pay the service at a unit price higher than that of the public network.
If you purchase a public IP, when the public network fails, Tencent Cloud will provide temporary acceleration service to help you bypass the failure and avoid service interruption. This value-added service is free of charge and imperceptible to your business. You pay the same price as that of the public network.

### How is AIA billed?
AIA is billed by 95th percentile of the monthly bandwidth under an account. For details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/644/12617).

### Is AIA billed by outbound or inbound bandwidth?
Acceleration traffic is billed by either the outbound or inbound bandwidth. The higher one prevail.

### Can AIA be billed by traffic?
No. AIA only supports bill-by-bandwidth.

### How does AIA limit the speed?
The bandwidth limit of an Anycast EIP refers to the total bandwidth of this IP. 
For example, if you set the bandwidth limit for an Anycast EIP to 100 Mbps, the total outbound bandwidth limit for all acceleration regions is 100 Mbps.


