You can use the [CVM Price Calculator](https://buy.intl.cloud.tencent.com/price/cvm/calculator) to check out the combined price of all the products you need. Also, you can add products to the shopping list to purchase all items together.

<dx-alert infotype="notice" title="">
To ensure that you obtain accurate prices, please log in first.
</dx-alert>



## Billing Modes

CVM supports reserved instance, pay-as-you-go and spot billing. For more information, see [Billing Plans](https://intl.cloud.tencent.com/document/product/213/2180).

## Instances

The instance type determines the hardware configuration of its host. Every instance type has different computing and storage capacities. You can choose the computing capacity, storage space, and network access method for the instances that best suits your service scale.
Tencent Cloud provides various models with different hardware specifications. For details, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

For more information about instance prices, see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).

## Storage

Tencent Cloud provides a wide range of flexible, cost-effective and user-friendly data storage devices for CVM instances. Each storage device has a unique price and performance characteristics, making them suitable for different use cases. They can be categorized as follows:
- Use case: system disk and data disk
- Architecture: cloud disk, local disk and Cloud Object Storage

Tencent Cloud now provides two types of cloud disks, including Premium Cloud Storage and SSD. The billing mode is pay as you go.
For more information about disk prices, see [Pricing List](https://intl.cloud.tencent.com/document/product/213/2255).

## Network Bandwidth

Tencent Cloud provides high-quality multi-line BGP networks to ensure optimal network experience. There are two billing options: bill-by-traffic and bill-by-bandwidth.
- Bill-by-bandwidth: billed based on the public network transmission rate (in Mbps). When your bandwidth utilization is higher than 10%, we recommend bill-by-bandwidth.
- Bill-by-traffic: it is billed based on the total amount of data transmission (in GB). When your bandwidth utilization is less than 10%, we recommend bill-by-traffic.

For more information about the network billing mode, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).


## Image Billing[](id:mirrorBilling)
Check below for the billing details of images.
<table>
<tr>
<th width="16%">Image Type</th><th>Description</th>
</tr>
<tr>
<td>Public image</td>
<td>This type contains open-source images and commercial images.
<ul style="margin:0px">
<li>Open-source images are free of charge.</li>
<li>You will be charged for licenses to use commercial images. The fees are varied by the instance specifications and regions. For the actual prices, please go to the <a href="https://buy.intl.cloud.tencent.com/price/cvm/calculator">Pricing Center</a>. If the Windows images are used in regions within Chinese mainland, the license fees are waived. If they are used outside Chinese mainland, the license fees are contained in instance fees. For more information, see <a href="#ep">Billing sample</a>.</li>
</ul>
</td>
</tr>
<tr>
<td>Custom image</td>
<td>
The billing consists of the following two parts:
<ul style="margin:0px">
<li>Snapshot fee: The image use the CBS snapshot service. As a result, retaining custom images incurs a snapshot fee. For billing details of CBS service, see the <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</li>
<li>Image fee: If the custom image is sourced from paid images, using it incurs fees.</li>
</ul>
</td>
</tr>
<tr>
<td>Shared image</td>
<td>An shared image is a custom image shared to other Tencent Cloud accounts. If the shared image is sourced from paid images, using it incurs fees.</td>
</tr>
</table>


#### Billing sample[](id:ep)

Background: Singapore Zone 1, Standard S5.MEDIUM2 instance, pay-as-you-go billing mode.
- The Windows instance fee is 0.05 USD/hour. The “Image” is free of charge. See the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/af8b0002847ce5f1542a90a1990e27ce.png)
