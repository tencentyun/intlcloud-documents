Tencent Cloud has two types of IP addresses, public IP addresses and private IP addresses.

## Public IP Addresses
A public IP address is an IP address in the Internet that is not reserved. A CVM with a public IP address can access other computers in the Internet and can also be accessed by other computers.
Tencent Cloud public IP addresses come in two types, public IPs and EIPs. Both of these can provide CVMs with the ability to access and be accessed by public networks.
<table>
<thead>
<tr>
<th colspan="2" width="16%">Item</th>
<th>Ordinary Public IPs</th>
<th>EIPs</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2">Ability to access/be accessed by public networks</td>
<td colspan="2">Both are public IPs, with no difference between them in terms of the ability to access/be accessed by public networks.</td>
</tr>
<tr>
<td colspan="2">How to acquire</td>
<td>It can only be allocated when purchasing the CVM. It cannot be acquired if not assigned at time of purchase.</td>
<td><li>You can <a href="https://intl.cloud.tencent.com/document/product/213/16586#.E7.94.B3.E8.AF.B7.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip" target="_blank">apply for an EIP </a>in the console.</li><li><a href="https://intl.cloud.tencent.com/document/product/213/16586#.E5.85.AC.E7.BD.91-ip-.E8.BD.AC.E5.BC.B9.E6.80.A7-ip" target="_blank">Converting an ordinary public IP to an EIP</a>.</li></td>
</tr>
<tr>
<td colspan="2">Features</td>
<td>It has the same lifecycle as the CVM, and will be released upon release of the bound CVM.</td>
<td><li>It’s independent from other resources. You can bind it to/unbind it from CVMs and NAT gateways any time.</li><li>You can release it when it's no longer needed.</li></td>
</tr>
<tr>
<td colspan="2" >Fees</td>
<td>Free of charge</td>
<td><li>Bound: When the EIP is bound with other Tencent Cloud resources (such as CVM and NAT gateway), it’s free of charge. See <a href="https://intl.cloud.tencent.com/document/product/213/17156" target="_blank">EIP Billing </a> for details.</li>
<li>Idle: When the EIP is not bound with any resource, it’s in idle status and will incur resource occupation fee.</li>
<li>Released: No fees will be incurred.</li>
</td>
</tr>
<tr>
<td colspan="2" rowspan="2">Quota</td>
<td>It is subject to the quota of CVMs.</td>
<td>Each account can apply for 20 EIPs in each region.</td>
</tr>
<tr>
<td colspan="2">For the quota of EIPs bound to a single CVM, refer to <a href="https://intl.cloud.tencent.com/document/product/213/16586" target="_blank">Quota details</a>.
</td>
</tr>
<tr>
<td rowspan="4" >Operations</td>
<td>Converting an IP</td>
<td>A public IP can be converted to an EIP. For details, refer to <a href="https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip" target="_blank"> Converting an ordinary public IP to an EIP</a>.</td>
<td>An EIP cannot be converted into an ordinary public IP.</td>
</tr>
<tr>
<td>Replacing IP</td>
<td>Public IPs can be directly replaced.
For details, refer to <a href="https://intl.cloud.tencent.com/document/product/213/16586#releasing-eips" target="_blank">Replacing public IP addresses</a>.</td>
<td>EIPs cannot be directly replaced. You need to unbind and release the EIP, apply for a new one and bind it again.</td>
</tr>
<tr>
<td>Releasing IP</td>
<td>If you no longer need a certain public IP, you can return it in the <a href="https://console.cloud.tencent.com/cvm" target="_blank">CVM console </a> by selecting **Operation** > **More** > **IP/ENI** > **Return public IP**.</td>
<td>It can also be released on the EIP console. For details, refer to <a href="https://intl.cloud.tencent.com/document/product/213/16586#releasing-eips" target="_blank">Releasing EIPs</a>.</td>
</tr>
<tr>
<td>Retrieving IP</td>
<td colspan="2">You can retrieve public IPs/EIPs that you have used if they are not used by other users. For details, refer to <a href="https://intl.cloud.tencent.com/document/product/213" target="_blank"> Applying for a specific IP address</a>.</td>
</tr>
</tbody></table>

## Private IP Addresses
A private IP address is used to implement Tencent Cloud private network services. It cannot be accessed from internet. Each CVM instance has a default network interface assigned with a private IP (i.e. eth0). The private IP address can be automatically assigned by the system. In a VPC environment, the private IP address can also be customized by the user.

### Attributes
- Private network services are user-sensitive. Different users are isolated from each other, which means that the cloud services of the other user cannot be accessed via the private network by default.
- Private network services are region-sensitive. Different regions are isolated from each other, which means that the cloud services under the same account in a different region cannot be accessed via the private network by default.

### Applicable scenarios
The private IP can be used for the communication between CLBs and CVM instances, and between CVM instances and other Tencent Cloud services (such as TencentDB).

### Relevant Operations
- For details on acquiring the private IP address of an instance and setting the DNS, refer to [Acquiring private IP address and setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).
- For details on modifying the private IPs of CVM instances in a VPC, refer to [Modifying private IP addresses](https://intl.cloud.tencent.com/document/product/213/16561).
