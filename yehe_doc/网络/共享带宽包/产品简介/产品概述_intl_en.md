## What is Tencent Cloud Bandwidth Package?
Tencent Cloud Bandwidth Package (BWP) is a multi-IP aggregated billing method that significantly reduces Internet access costs. When public network witnesses several peaks at different periods, you can use BWP for the aggregated bandwidth billing, greatly saving your public network fees.
BWP offers [monthly top 5](https://intl.cloud.tencent.com/document/product/684/15255#.E6.9C.88-top5-.E8.AE.A1.E8.B4.B9) and [monthly 95th percentile](https://intl.cloud.tencent.com/document/product/684/15255#.E6.9C.8895.E8.AE.A1.E8.B4.B9) billing options for different use cases.

## Product Types
- **IP bandwidth package**: applies to accounts whose public network fess are billed on public IP or CLB, which mean that the public network capability (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) are specified upon creation of the IP or CLB instance.
- **Device bandwidth package**: applies to accounts whose public network fees are billed on CVMs, which mean that the public network capability (bandwidth cap) and billing method (bill-by-traffic or bill-by-bandwidth) are specified upon creation of the CVM instance. The public IP address and CLB acts only as public network egress. 

These bandwidth packages are available to different Tencent Cloud accounts as follows.
<table>
<tr>
<th>Account Type</th><th>Available Bandwidth Package</th>
</tr>
<tr>
<td rowspan="2">Bill-by-CVM account</td><td>Device bandwidth package</td>
</tr>
<tr>
<td>IP bandwidth package</td>
</tr>
<tr>
<td>Bill-by-IP account</td><td>IP bandwidth package</td>
</tr>
</table>

To learn about your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
>?You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change your bill-by-CVM account to bill-by-IP account, and the change cannot be reverted.

## Supported Resources 
### Device bandwidth package
Device bandwidth packages support CVMs and CLBs.

### IP bandwidth packages
IP bandwidth packages support public IPs, EIPs (bound with CVM, NAT gateway) and CLBs.
