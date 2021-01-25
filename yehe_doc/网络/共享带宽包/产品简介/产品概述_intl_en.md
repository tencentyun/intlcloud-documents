## What is Tencent Cloud Bandwidth Package?
Tencent Cloud Bandwidth Package (BWP) is a multi-IP aggregated billing method that significantly reduces Internet access costs. When public network instances have traffic peaks at different times, you can use BWP for the aggregated bandwidth billing to greatly save your public network fees.
BWP supports [monthly top 5 billing](https://intl.cloud.tencent.com/document/product/684/15255) and [monthly 95th percentile billing](https://intl.cloud.tencent.com/document/product/684/15255) for different use cases.

## Product Types
- **IP bandwidth package**: applies to accounts whose public network fess are billed on public IP or CLB, which mean that the public network capability (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) are specified upon creation of the IP or CLB instance.
- **Device bandwidth package**: applies to accounts whose public network fees are billed on CVMs, which mean that the public network capability (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) are specified upon creation of the CVM instance. The public IP address and CLB acts only as public network egress.

Tencent Cloud offers different bandwidth packages for different accounts:
<table>
<tr>
<th>Account Type</th><th>Available Bandwidth Package</th>
</tr>
<tr>
<td rowspan="2">Bill-by-CVM account</td><td>Device bandwidth package</td>
</tr>
<tr>
<td>IP bandwidth package (only available to elastic IPv6 public IP addresses, IPv6 CLB instances and static single-line EIPs)</td>
</tr>
<tr>
<td>Bill-by-IP account</td><td>IP bandwidth package</td>
</tr>
</table>

To learn about your account type and available bandwidth package type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
>?You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change your bill-by-CVM account to bill-by-IP account, and the change cannot be reverted.
>

## Supported Resources 

### Device bandwidth package
Device bandwidth packages support CVMs and CLBs.

### IP bandwidth packages
IP bandwidth packages support public IPs, EIPs (bound with CVM or NAT Gateway), elastic IPv6 public IP addresses, and CLBs.
