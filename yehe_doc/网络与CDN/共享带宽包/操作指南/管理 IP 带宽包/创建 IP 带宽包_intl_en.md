This document describes how to create an IP bandwidth package under your bill-by-IP account.


## Restrictions
- BWP is currently in beta. To try it out, please submit an application to be added to the beta list.
- A bill-by-IP account only supports creating an IP bandwidth package. If you have a bill-by-CVM account and want to use IP bandwidth packages, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change to bill-by-IP account. To determine your account type, see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246).
- Tencent Cloud provides the following bandwidth packages according to the bandwidth type.
<table>
<tr><th width="30%">Bandwidth Type</th><th>Restrictions</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/684/15254">BGP Bandwidth Package</a></td><td rowspan="2">This type can be manually created on the console.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/684/15254">Dedicated BGP Bandwidth Package</a></td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/684/15254">AIA BGP Bandwidth Package</a></td><td>When an Anycast EIP is created, this type will be automatically created, which cannot be manually created.</td></tr>
</table>

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Bandwidth Package** on the left sidebar.
2. Select a region, and click **+New** in the upper-left corner.
3. In the pop-up dialog box, enter the bandwidth package name, select a billing mode, and then click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/dc1d8af7fe8cf262d2067e8cc6df9dcf.png)
<table>
	<tr><th width="15%">Parameter</th><th>Description</th></tr>
	<tr><td><strong>Name</strong></td><td><ul><li>Supported characters: <code>a-z</code>, <code>0-9</code>, <code>.</code>, and <code>-</code></li><li>Length: 1-60 characters</li></ul></td></tr>
	<tr><td><strong>Line Type</strong></td><td><ul><li>General BGP: a bandwidth package using BGP IP lines</li>
	<tr><td><strong>Billing Mode/Billing Description</strong></td><td><ul><li>Pay as you go - Top 5 Billing: bill by the fifth highest bandwidth value collected per day</li><li>Pay as you go - Monthly 95th Percentile: bill by 95th percentile of the monthly peak bandwidth</li>For more information, see <a href="https://intl.cloud.tencent.com/document/product/684/15255">Billing Modes</a>.</ul></td></tr>
	<tr><td><strong>Advanced Options</strong></td><td>Tags (key-value pairs) used to categorize and manage bandwidth package resources</tr>
	<tr><td><strong>Unit Price</strong></td><td>As detailed in <a href="https://intl.cloud.tencent.com/document/product/684/15254">Product Pricing</a></td></tr>
</table>



## Subsequent Operations
[Adding Resources](https://intl.cloud.tencent.com/document/product/684/34599)
		
		
