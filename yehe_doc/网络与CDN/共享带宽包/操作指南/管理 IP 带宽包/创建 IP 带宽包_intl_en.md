This document describes how to create an IP bandwidth package under your bill-by-IP account.


## Restrictions
- The Bandwidth Package (BWP) is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- A bill-by-IP account only supports creating an IP bandwidth package. If you have a bill-by-CVM account and want to use IP bandwidth packages, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change to bill-by-IP account. To learn about your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
- Tencent Cloud provides the following bandwidth packages according to the bandwidth type.
<table>
<tr><th width="30%">Bandwidth Type</th><th>Restrictions</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/684/15254">BGP Bandwidth Package</a></td><td rowspan="2">It can be manually created in the console.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/684/15254">Dedicated BGP Bandwidth Package</a></td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/684/15254">AIA BGP Bandwidth Package</a></td><td>It is auto-created when an Anycast EIP or static single-line EIP is created, and cannot be manually created.</td></tr>
</table>

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** on the left sidebar.
2. Select a region, and click **+New** in the upper-left corner.
3. In the pop-up dialog box, enter the bandwidth package name, select a billing mode, and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/dc1d8af7fe8cf262d2067e8cc6df9dcf.png)
<table>
	<tr><th width="15%">Parameter</th><th>Description</th></tr>
	<tr><td><strong>Name</strong></td><td><ul><li>Supported characters: <code>a-z</code>, <code>0-9</code>, <code>.</code>, and <code>-</code></li><li>Length: 1-60 characters</li></ul></td></tr>
	<tr><td><strong>Line Type</strong></td><td><ul><li>General BGP: A bandwidth package using BGP IP lines.</li><li>Dedicated BGP: A bandwidth package using dedicated BGP IP lines.<br/>Currently, only bill-by-IP accounts support dedicated BGP bandwidth packages. If you have a bill-by-CVM account and want to use IP bandwidth packages, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to change to bill-by-IP account. To learn about your account type, see <a href="https://intl.cloud.tencent.com/document/product/684/15246">Checking Account Type</a>.</li></ul></td></tr>
	<tr><td><strong>Billing Mode/Billing Description</strong></td><td><ul><li>Pay as you go - Top 5 Billing: Bill by the fifth highest bandwidth value collected per day</li><li>Pay as you go - Monthly 95th Percentile: Bill by 95th percentile of the monthly peak bandwidth</li>For more information, see <a href="https://intl.cloud.tencent.com/document/product/684/15255">Billing Modes</a>.</ul></td></tr>
	<tr><td><strong>Advanced Options</strong></td><td>Tags (key-value pairs) used to categorize and manage bandwidth package resources</tr>
	<tr><td><strong>Unit Price</strong></td><td>As detailed in <a href="https://intl.cloud.tencent.com/document/product/684/15254">Product Pricing</a></td></tr>
</table>


## See Also
[Adding Resources](https://intl.cloud.tencent.com/document/product/684/34599)
		
		
