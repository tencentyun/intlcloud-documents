## IPv4 Address
Tencent Cloud provides two IPv4 addresses for private network and public network access respectively. The IP addresses will not change unless you unbind or change them.

### Private IPv4 addresses
A private IPv4 address is used to implement Tencent Cloud private network services. It cannot be accessed from Internet. Each CVM instance has a default private IPv4 address at the time when it is created. The private IPv4 address can be automatically assigned by the system, which can also be customized in the VPC.

#### Attributes
- The IPv4 private network service is user-sensitive, and different users are isolated from each other. By default, Tencent Cloud services of another user cannot be accessed via the IPv4 private network.
- The IPv4 private network service is region-sensitive, and different regions are isolated from each other. By default, Tencent Cloud services and VPC under the same account in a different region cannot be accessed via the IPv4 private network.

#### Use cases
The private IPv4 address can be used for:
- IPv4 private network interconnection between Cloud Load Balancer and CVM instances in the same VPC or classic network.
- IPv4 private network interconnection between CVM instances in the same VPC or classic network.
- IPv4 private network interconnection between CVM instances and other Tencent Cloud services (such as TencentDB) in the same VPC or classic network.

#### Relevant operations
- For details on acquiring the private IPv4 address of an instance and setting the DNS, see [Getting Private IP Addresses and Setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).
- For details on modifying the private IPv4 addresses of CVM instances in a VPC, see [Modifying Private IP Addresses](https://intl.cloud.tencent.com/document/product/213/16561).

### Public IPv4 addresses
A public IPv4 address including public IP and EIP allows a CVM to access and be accessed through the IPv4 public network.
#### Main differences
The table below lists the main difference between a public IP and an EIP:
<table>
<thead>
<tr>
<th colspan="2" width="16%">Item</th>
<th>Public IPs</th>
<th>EIPs</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="2">Use cases</td>
<td>If you want to create a CVM with a public IP automatically assigned that will be released with the CVM, choose a public IP.</td>
<td>If you want to use a public IP address for a long time and bind it to a specified CVM based on business needs, choose an EIP. You can bind an EIP to and unbind it from a CVM repeatedly, which still exists after the CVM is released.</td>
</tr>
<tr>
<td colspan="2">Ability to access/be accessed by public networks</td>
<td colspan="2">Both are public IPs and have the same ability to access/be accessed by public networks.</td>
</tr>
<tr>
<td colspan="2">Acquisition method</td>
<td>It can only be obtained when you purchase a CVM.</td>
<td><li>You can apply for an EIP on the Console.</li><li>You can convert a public IP to an EIP.</li></td>
</tr>
<tr>
<td colspan="2">Features</td>
<td>It has the same lifecycle as the CVM, and will be released upon release of the bound CVM.</td>
<td><li>It’s independent from other resources. You can bind it to/unbind it from CVMs and NAT gateways any time.</li><li>You can release it when it's no longer needed.</li></td>
</tr>
<tr>
<td colspan="2" >IP idle fee</td>
<td>Free of charge.</td>
<td>EIP incurs an IP idle fee, which varies by the bill-by-IP and bill-by-CVM accounts.</td>
</tr>
<tr>
<td colspan="2" rowspan="2">Quota</td>
<td>It is subject to the quota of CVMs.</td>
<td>Each account can apply for 20 EIPs in each region.</td>
</tr>
<tr>
<td colspan="2">For the quota of the public IP addresses for a single CVM, see Quota Limits.
</td>
</tr>
<tr>
<td rowspan="4" >Operations</td>
<td>Converting an IP</td>
<td>Supported. <br>When a public IP is converted to an EIP, the IP address will not change, and only IP attributes change.</td>
<td>An EIP cannot be converted to a public IP.</td>
</tr>
<tr>
<td>Changing an IP</td>
<td>Public IPs can be directly changed.
For details, see <a href="https://intl.cloud.tencent.com/document/product/213/16642" target="_blank">Changing Public IP Addresses</a>.</td>
<td>EIPs cannot be directly changed. You need to unbind and release the EIP, apply for a new one and bind it again.</td>
</tr>
<tr>
<td>Releasing an IP</td>
<td>If you no longer need a public IP, you can return it on the <a href="https://console.cloud.tencent.com/cvm" target="_blank">CVM Console </a> by selecting **Operation** -> **More** -> **IP/ENI** -> **Return Public IP**.</td>
<td>You can release an ENI on the ENI Console.</td>
</tr>
<tr>
<td>Retrieving an IP</td>
<td colspan="2">You can recover public IPs/EIPs that you have used if they are not used by other users.</td>
</tr>
</tbody></table>

#### Billing
The traffic cost generated from IPv4 public network access through a public IPv4 address will be billed. For more information, see [Public Network Billing](https://buy.cloud.tencent.com/price/idc).

