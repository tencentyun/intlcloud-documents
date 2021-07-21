This document describes the use limits of bandwidth packages.
>?BWP is currently in beta. To try it out, please apply for beta eligibility.

## Account Types
To learn about your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
<table>
<tr>
<th>Account Type</th><th>Available Bandwidth Package</th>
</tr>
<tr>
<td rowspan="2">Bill-by-CVM account</td><td>Device bandwidth package</td>
</tr>
<tr>
<td>IP bandwidth package (only available to elastic IPv6 addresses, IPv6 CLB instances and static single-line EIPs)</td>
</tr>
<tr>
<td>Bill-by-IP account</td><td>IP bandwidth package</td>
</tr>
</table>

## Bandwidth Packages
<table>
<tr>
<th width="13%">Limit</th><th width="44%">Device Bandwidth Package</th><th>IP Bandwidth Package</th>
</tr>
<tr>
<td>Quota</td><td>Only one device bandwidth package can be activated in each region.</td><td>Up to 20 IP bandwidth packages can be activated in one region.</td>
</tr>
<tr>
<td>Billing</td><td><ul><li>The device bandwidth package in a region cannot be used together with any other billing mode. </li><li>After a device bandwidth package is activated in a region, all the CVM and CLB instances in the region will be automatically billed in the bandwidth package. The original fees billed by monthly subscription will be refunded after being converted based on the number of hours actually used.</li></ul></td><td>The IP bandwidth package can be used together with other billing modes such as monthly bandwidth subscription, hourly bandwidth, and bill-by-traffic in the same region.</td>
</tr>
<tr>
<td>Resource</td><td>Resources cannot be added.</td><td><ul><li>Currently, monthly-subscribed EIPs and public IPs cannot be added to IP bandwidth packages.</li><li>Up to 100 resources including EIPs, public IPs, elastic IPv6 addresses, and CLB instances in the same region can be added to a single IP bandwidth package.</li></ul></td>
</tr>
</table>

## Peak Bandwidth
<table>
<tr>
<th width="19%">Peak Bandwidth</th><th>Description</th>
</tr>
<tr>
<td>Single instance</td><td>The peak bandwidth of instances including public IP and EIP in a single bandwidth package is 2 Gbps. The peak bandwidth is only regarded as the maximum bandwidth for reference, and not as the committed bandwidth. When bandwidth resources are contested, the peak bandwidth may be limited.</td>
</tr>
<tr>
<td>Single region</td><td>The sum of peak bandwidths of all the running instances billed on bandwidth packages cannot exceed 50 Gbps in one region. If your application requires a guaranteed or higher bandwidth, contact your sales rep or <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>. In this case, you need to pay the guaranteed bandwidth fee on a pro rata basis.</td>
</tr>
</table>
