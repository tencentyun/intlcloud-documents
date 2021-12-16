﻿This document describes how to purchase a TMP instance.


## Prerequisite
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Pay-as-You-Go
1. Log in to the TMP purchase page and configure the following instance information.
<table>
<tr>
<th>Item</th>
<th>Description</th>
</tr>
<tr>
<td>Billing Mode</td>
<td>Select “pay-as-you-go”.</td>
</tr>
<tr>
<td>Region</td>
<td>Select the region where your business needs to be deployed.<br>
<dx-alert infotype="explain" title="">
Tencent Cloud services in different regions cannot communicate with each other over the private network; for example, a service in the Guangzhou region cannot report data to a TMP instance in the Shanghai region over the private network. Once an instance is purchased, the region cannot be changed. Therefore, you need to select the region with caution.
</dx-alert>
</td>
</tr>
<tr>
<td>Availability Zone</td>
<td>Select an AZ supported by the region.</td>
</tr>
<td>Network</td>
<td >VPC is supported. We recommend you choose the same VPC in the same region as your monitoring target. For more information, see <a href = "https://intl.cloud.tencent.com/zh/document/product/213/5227">Network Environment</a>.</td>
</tr>
<tr>
<td>Data Retention Period</td>
<td>Select the data retention period. In the pay-as-you-go billing mode, fees are charged based on the daily reported metric data volume and the data retention period. For more information, see <a href = "">Product Pricing/a>.</td>
</tr>
<tr>
<td>Instance Name</td>
<td>Enter an instance name.</td>
</tr>
<tr>
<td>Grafana Password/Confirm Password</td>
<td>Enter the password of Grafana that comes with the instance. The account is `admin` by default.<br>
<dx-alert infotype="explain" title="">
The password must begin with a letter or digit and contain at least one special symbol (`@$!%*#?&`), and its length should be between 6 and 24.
</dx-alert>
</td>
</tr>
<tr>
<td>Tag</td>
<td>Enter a tag for the instance (optional). For more information on tag configuration, see <a href = "https://intl.cloud.tencent.com/document/product/1116/43166">Tag Management</a>.</td>
</tr>
<tr>
<td>Validity Period</td>
<td>Select the validity period of the instance.</td>
</tr>
</table>

2. Read and indicate your consent to related terms of agreement, and then click **Buy Now**.
3. On the payment page, select a payment method and pay.
4. You can enter the instance list page after the purchase. The instance will be in **Creating** status, and you can use it after around 3-5 minutes when its status changes to **Running**.

## Subsequent Operations
 [Quickly get started with TMP](https://intl.cloud.tencent.com/document/product/1116/43159).
