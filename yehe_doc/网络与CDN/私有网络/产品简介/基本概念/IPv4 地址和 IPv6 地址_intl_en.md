IP addresses support IPv4 and IPv6 addressing protocols. IPv4 is widely used, but the number of network addresses is limited, making IPv6 a good complement.

## IPv4 Addresses
Tencent Cloud provides IPv4 addresses for both the private and public network access. A public IPv4 address can be common or elastic. As shown in the following figure, **EIP** indicates an elastic IPv4 address, **Private** indicates a private IPv4 address, and **Public** indicates a public IPv4 address. These IPs will not change unless you unbind or change them.
>?Unless otherwise specified, private IP, public IP and EIP all refer to IPv4 addresses.
>
![](https://main.qcloudimg.com/raw/6bb952befc42a89392b4d2369f04820d.png)

### Private IPv4 addresses
A private IPv4 address is used for Tencent Cloud private network access, which cannot be used to access the internet. Once a CVM instance is created, it will be automatically assigned with a private IPv4 address. The private IPv4 address can also be customized in a VPC environment.

#### Attributes
- The IPv4 private network is user-specific, and different users are isolated from each other. By default, cloud services of another user cannot be accessed via the IPv4 private network.
- The IPv4 private network is region-specific, and different regions are isolated from each other. By default, cloud services under the same account in a different region cannot be accessed via the IPv4 private network.

#### Use cases
The private IPv4 address can be used for:
- Interconnection between VPC-based or classic network-based CLB and CVM instances over an IPv4 private network.
- Interconnection between VPC-based or classic network-based CVM instances over an IPv4 private network.
- Interconnection between VPC-based or classic network-based CVM instances and other Tencent Cloud services (such as TencentDB) over an IPv4 private network.

#### Relevant operations
- For more information about how to obtain the private IPv4 address of the instance and set DNS, refer to [Getting Private IP Addresses and Setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).
- For more information about how to change the private IPv4 addresses of CVM instances in a VPC, see [Modifying Private IP Addresses](https://intl.cloud.tencent.com/document/product/213/16561).

### Public IPv4 addresses
Tencent Cloud provides public IPs and EIPs for public network access. A CVM instance with a public IPv4 address can access and be accessed over an IPv4 public network.

#### Comparison
The following table compares public IPs with EIPs.
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
<td colspan="2">Use cases</td>
<td>If you want to create a CVM that supports public network access, you can choose to use a public IP address automatically assigned by the system at the creation of a CVM instance. This public IP address has the same lifecycle as the CVM, and will be released upon the release of the bound CVM.</td>
<td>If you want to use a public IP for a long time, you can choose an elastic IP (EIP) and bind it to the specified CVM as needed. EIP can be bound or unbound many times, and will still exist after the CVM is released.</td>
</tr>
<tr>
<td colspan="2">Public network access</td>
<td colspan="2">Both support public network access.</td>
</tr>
<tr>
<td colspan="2">Acquisition method</td>
<td>It can only be obtained when you purchase a CVM.</td>
<td><li>1. Apply for an EIP in the console.</li><li>2. Convert a public IP address to an EIP.</li></td>
</tr>
<tr>
<td colspan="2">Features</td>
<td>It has the same lifecycle as the CVM, and will be released upon the release of the bound CVM.</td>
<td><li>It is independent from other resources. You can bind it to or unbind it from CVMs and NAT Gateways at anytime.</li><li>You can release an EIP when you no longer need it.</li></td>
</tr>
<tr>
<td colspan="2" >Fees</td>
<td>Only the public network fee will be charged.</td>
<td>The IP resource fee is a part of the EIP fee, which varies by the account type. For more information, see <a href="https://intl.cloud.tencent.com/document/product/684/15246">Checking Account Type</a>.</td>
</tr>
<tr>
<td colspan="2" rowspan="2">Quota</td>
<td>It is subject to the number of CVMs you purchased.</td>
<td>Each account can apply for 20 EIPs in each region.</td>
</tr>
<tr>
<td colspan="2">For the quota of public IPs (including EIPs) bound to a CVM, see the limits on public IPs bound to a CVM.</td>
</tr>
<tr>
<td rowspan="4" >Operations</td>
<td>Converting an IP</td>
<td>A public IP can be converted to an EIP. The IP address will not change after the conversion.</td>
<td>An EIP cannot be converted back to a public IP.</td>
</tr>
<tr>
<td>Changing an IP</td>
<td>A public IP can be directly changed.
For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/16642" target="_blank">Changing Public IP Addresses</a></td>
<td>EIPs cannot be directly changed. You need to unbind and release the EIP, apply for a new one, and bind it again.</td>
</tr>
<tr>
<td>Releasing an IP</td>
<td>If you no longer need a public IP, you can log in to the <a href="https://console.cloud.tencent.com/cvm" target="_blank">CVM console</a>, locate the public IP, and in the <b>Operation</b> column, select <b>More > IP/ENI > Return Public IP</b> to return it.</td>
<td>You can release an EIP in the EIP console.</td>
</tr>
<tr>
<td>Retrieving an IP</td>
<td colspan="2">You can retrieve public IPs/EIPs that you have used if they have not been used by other users.</td>
</tr>
</tbody></table>

#### Billing
The public network traffic generated by public IPv4 addresses will be charged with public network fees. For more information, see [Public Network Pricing](https://intl.cloud.tencent.com/document/product/213/39743).


## Relevant Information
- For more information about how to quickly build an IPv4 Virtual Private Cloud (VPC), see [Building Up an IPv4 VPC](https://intl.cloud.tencent.com/document/product/215/31891).
- For more information about EIPs, see [Elastic IP](https://intl.cloud.tencent.com/document/product/215/34109).

