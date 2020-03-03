Tencent Cloud offers different types of IPs for internet access and private network access. These IPs will not change unless you unbind or change them.

## IPs for Internet Access
A public IP address is an IP address in the Internet that is not reserved. A CVM with a public IP address can access other computers in the Internet and can also be accessed by other computers.
Tencent Cloud offers public IPs and elastic IPs for internet access.
<table >
<thead>
<tr>
<th colspan="2" width="16%">Item</th>
<th>Public IP Address</th>
<th>Elastic IP Address</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2">Mutual access to Internet</td>
<td colspan="2">Both supports mutual access internet.</td>
</tr>
<tr>
<td colspan="2">How to Obtain</td>
<td>It can only be obtained when you purchase a CVM.</td>
<td><li>You can <a href="https://cloud.tencent.com/document/product/213/16586#.E7.94.B3.E8.AF.B7.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip" target="_blank">apply for an EIP </a>in the console. </li><li><a href="https://cloud.tencent.com/document/product/213/16586#.E5.85.AC.E7.BD.91-ip-.E8.BD.AC.E5.BC.B9.E6.80.A7-ip" target="_blank">Converting a public IP address to an EIP</a>.</li></td>
</tr>
<tr>
<td colspan="2">Features</td>
<td>It’s lifecycle is bound with the CVM, and will be released upon the release of the bound CVM.</td>
<td><li>It is independent from other resources. You can bind it to and unbind it from CVMs and NAT gateways at any time.</li><li>You can release it when it's no longer needed.</li></td>
</tr>
<tr>
<td colspan="2" >Fees</td>
<td>Free of charge</td>
<td><li>Bound: the EIP is free of charge when it’s bound with other Tencent Cloud resources (such as a CVM or a NAT gateway). </li>
<li>Not bound: a <a href="https://cloud.tencent.com/document/product/213/17156" target="_blank">resource occupation fees</a> will be incurred if the EIP is not bound with any resource.</li>
<li>Released: no fees will be incurred.</li>
</td>
</tr>
<tr>
<td colspan="2" rowspan="2">Quota</td>
<td>It is subject to the quota of CVMs.</td>
<td>Each account can apply for 20 EIPs in each region.</td>
</tr>
<tr>
<td colspan="2">For the quota of the public IP addresses for a single CVM, see <a href="https://cloud.tencent.com/document/product/213/5733#.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.BB.91.E5.AE.9A.E5.85.AC.E7.BD.91-ip-.E9.99.90.E5.88.B6" target="_blank">Quota Details</a>.
</td>
</tr>
<tr>
<td rowspan="4" >Operations</td>
<td>Converting an IP</td>
<td>A public IP can be converted to an EIP. For details, refer to <a href="https://cloud.tencent.com/document/product/213/16586#.E5.85.AC.E7.BD.91-ip-.E8.BD.AC.E5.BC.B9.E6.80.A7-ip" target="_blank">Converting a public IP to an EIP</a>. <br>When a public IP is converted to a elastic public IP, the IP address will not change.</td>
<td>An EIP cannot be converted into a public IP.</td>
</tr>
<tr>
<td>Replacing an IP</td>
<td>Public IPs can be directly replaced.
For details, refer to <a href="https://cloud.tencent.com/document/product/213/16642" target="_blank">Replacing public IP addresses</a>.</td>
<td>EIPs cannot be directly replaced. You need to unbind and release the EIP, apply for a new one and bind it again.</td>
</tr>
<tr>
<td>Releasing an IP</td>
<td>If you no longer need a certain public IP, you can return it in the <a href="https://console.cloud.tencent.com/cvm" target="_blank">CVM console </a> by selecting **Operation** > **More** > **IP/ENI** > **Return public IP**.</td>
<td>Release it in the EIP console. For details, refer to <a href="https://cloud.tencent.com/document/product/213/16586#.E9.87.8A.E6.94.BE.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip" target="_blank">Releasing EIPs</a>.</td>
</tr>
<tr>
<td>Recovering an IP</td>
<td colspan="2">You can recover public IPs/EIPs that you have used if they are not used by other users. For details, refer to <a href="https://cloud.tencent.com/document/product/213/34376" target="_blank"> Recovering Public IPs</a>.</td>
</tr>
</tbody></table>

## IPs for Private Network Access
A private IP address is used to implement Tencent Cloud private network services. It cannot be accessed from internet. Each CVM instance has a default network interface assigned with a private IP (i.e. eth0). The private IP address can be automatically assigned by the system. In a VPC environment, the private IP address can also be customized by the user.

### Attributes
- Private network services are user-sensitive. Different users are isolated from each other, which means that the cloud services of the other user cannot be accessed via the private network by default.
- Private network services are region-sensitive. Different regions are isolated from each other, which means that the cloud services under the same account in a different region cannot be accessed via the private network by default.

### Applicable scenarios
The private IP can be used for the communication between CLBs and CVM instances, and between CVM instances and other Tencent Cloud services (such as TencentDB).

### Relevant Operations
- For details on acquiring the private IP address of an instance and setting the DNS, refer to [Acquiring private IP address and setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).
- For details on modifying the private IPs of CVM instances in a VPC, refer to [Modifying private IP addresses](https://intl.cloud.tencent.com/document/product/213/16561).
