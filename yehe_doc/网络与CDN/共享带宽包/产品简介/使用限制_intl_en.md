This document describes the use limits of bandwidth packages.

## Account Types
To learn about your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
<table>
<tr>
<th width="20%">Account type</th>
<th width="50%">Supported bandwidth package</th>
<th width="20%">Billing mode</th>
</tr>
<tr>
<td rowspan="2">Bill-by-CVM account</td><td>Device Bandwidth Package</td><td rowspan="2">Pay-as-you-go (monthly)</td>
</tr>
<tr>
<td>IP-based bandwidth package (elastic IPv6 addresses, <a href="https://www.tencentcloud.com/document/product/214/8848">IPv6 load balancers</a> and Static single line <a href="https://intl.cloud.tencent.com/document/product/213/5733">EIP</a>)</td>
</tr>
<tr>
<td>Bill-by-IP account</td>
<td>IP-based bandwidth package</td>
<td>Postpaid monthly and daily payment</td>
</tr>
</table>

## Shared Bandwidth Packages
<table>
<tr>
<th width="13%">Limit</th><th width="40%">Device Bandwidth Package</th><th>IP Bandwidth Package</th>
</tr>
<tr>
<td>Quota</td><td>Only one device bandwidth package can be activated in each region.</td><td>Up to 20 IP bandwidth packages can be activated in one region.</td>
</tr>
<tr>
<td>Billing</td><td><ul><li>No other billing modes are allowed if a device bandwidth package activated in a region</li><li>After a device bandwidth package is activated, the billing mode of all CVM and CLB instances in the region are automatically changed to the bandwidth package. </li></ul></td><td>The IP bandwidth package can be used together with other billing modes such as monthly bandwidth subscription, hourly bandwidth, and bill-by-traffic in the same region.</td>
</tr>
<tr>
<td>Resources</td><td>Resources cannot be added manually. </td>
<td>
<ul>
<li>Monthly subscribed EIPs and IPs cannot be added to an IP bandwidth package.
<li>Postpaid bandwidth package:</li><ul><li>You can add up to 100 resources in the same region (EIPs, IPs, elastic public IPv6 addresses and CLB instances)</li></ul>
</ul>
</td>
</tr>
</table>



## Peak Bandwidth
<table>
<tr>
<th width="19%">Peak Bandwidth</th><th>Description</th>
</tr>
<tr>
<td>Per instance</td><td>For each instance (such as public IPs, CLBs) added to the bandwidth package, the peak bandwidth is 2 Gbps. Note that this is the max possible bandwidth, but not the committed bandwidth. In case of resource contention, the peak bandwidth may not reach this value.</td>
</tr>
<tr>
<td>Per region</td><td><ul><li>50 Gbps. Note that this is the max possible bandwidth, but not the committed bandwidth. For a guaranteed or higher bandwidth capability, contact your sales rep or <a href="https://console.cloud.tencent.com/workorder/category"> submit a ticket</a> to apply for reserved bandwidth and guaranteed bandwidth fee on a pro rata basis.</li></ul></td>
</tr>
</table>
