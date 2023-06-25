>? **Anti DDoS EIP** is available only to bill-by-IP accounts.

## Step 1: Purchase an Anti-DDoS Pro (Enterprise)
Log in to the Anti-DDoS console and go to the [Anti-DDoS Pro Purchase Page](https://buy.cloud.tencent.com/antiddos#/native). For more information, see [Purchase Directions](https://intl.cloud.tencent.com/document/product/1029/36115).


## Step 2: Create a BGP Bandwidth Package
Create a BGP bandwidth package. For details, see [Creating an IP Bandwidth Package](https://intl.cloud.tencent.com/document/product/684/34597).
>? If you have created a general BGP bandwidth package in the target region, please skip to [Step 3](#S3).

## Step 3: Create an Anti DDoS EIP[](id:S3)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/ip?rid=1) and click ** Public IP** in the left sidebar.
2. Select a region on the page that appears and click **Apply**.
![](https://qcloudimg.tencent-cloud.cn/raw/003d439050c7b453d9a8e8b15d3230d9.png)
3. In the **Apply for EIP** window, configure relevant parameters and click **OK**.<br><img src="https://qcloudimg.tencent-cloud.cn/raw/a06f987db8c4817200ea5e17a9143bc8.png" width=500px>
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>IP type</td>
<td>Select <strong>Anti DDoS EIP</strong></td>
</tr>
<tr>
<td>Billing mode</td>
<td>Only bandwidth package is supported</td>
</tr>
<tr>
<td>Bandwidth package</td>
<td>Select the desired <strong>general BGP bandwidth package</strong></td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set the bandwidth cap as needed and allocate bandwidth resources reasonably</td>
</tr>
<tr>
<td>Anti-DDoS Pro (Enterprise)</td>
<td>Select the target <strong>Anti-DDoS Pro (Enterprise) instance</strong></td>
</tr>
<tr>
<td>Quantity</td>
<td>Select the quantity of EIPs to be applied and ensure that it does not exceed the total quota</td>
</tr>
<tr>
<td>Name</td>
<td>EIP instance name (optional)</td>
</tr>
<tr>
<td>Tag</td>
<td>You can add a tag and use it for permission management</td>
</tr>
</tbody></table>

## Related Operations
To bind cloud resources with the EIP, please [contact us](https://www.tencentcloud.com/contact-us).