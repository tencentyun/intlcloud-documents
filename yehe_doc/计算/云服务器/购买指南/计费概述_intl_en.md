You can use the [CVM Price Calculator](https://buy.tencentcloud.com/price/cvm/calculator) to estimate the total price of instances you want to purchase, and place the order together. 

<dx-alert infotype="notice" title="">
To ensure that you obtain accurate prices, please log in first.
</dx-alert>

## Billing Modes

Tencent Cloud offers three billing modes for CVM instances: RI, pay-as-you-go and spot. For more information, see [Billing Mode](https://www.tencentcloud.com/document/product/213/2180).

## Instance

The instance model determines the hardware configuration of its host. Every model has different computing and storage capacities. You can choose the computing capacity, storage space, and network access method for the instances that best suits your service scale.
Tencent Cloud provides various CVM models with different hardware specifications. For details, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).

For more information about instance prices, see [Billing Mode](https://intl.cloud.tencent.com/document/product/213/2180).

## Storage

Tencent Cloud provides a wide range of data storage devices for CVM instances. Different storage types have different price and performance. They are categorized as follows:
- Use case: System disk and data disk
- Architecture: Cloud disk, local disk and COS bucket

Tencent Cloud now provides multiple [types of cloud disks](https://www.tencentcloud.com/document/product/362/31636), including Premium Cloud Storage, Balanced SSD, SSD, Enhanced SSD and ulTra SSD. The billing modes include prepaid subscriptions, pay-as-you-go and spot.
For more information about disk prices, see [Pricing List](https://intl.cloud.tencent.com/document/product/213/2255).

## Network Bandwidth

Tencent Cloud provides high-quality multi-line BGP networks to ensure optimal network experience. Two billing options are available: Bill-by-traffic and bill-by-bandwidth.
- Bill-by-bandwidth: Billed based on the public network transmission rate (in Mbps). It’s applicable to scenarios with the bandwidth utilization over 10%.
- Bill-by-traffic: Billed based on the total size of data transmission (in GB). It’s applicable to scenarios with the bandwidth utilization lower than 10%.

For more information about the network billing mode, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).


## Image[](id:mirrorBilling)
Check below for the billing details of images. For more information, see [Billing Description](https://www.tencentcloud.com/document/product/213/55134).
<table>
<tr>
<th width="16%">Image Type</th><th>Description</th>
</tr>
<tr>
<td>Public image</td>
<td>It includes open-source images and commercial images.
<ul style="margin:0px">
<li>You do not need to pay for licenses when you use open-source images.</li>
<li>You will be charged for licenses to use commercial images.
</li>
</ul>
</td>
</tr>
<tr>
<td>Custom image</td>
<td>
The billing consists of the following two parts:
<ul style="margin:0px">
<li>Snapshot fee: The image use the CBS snapshot service. As a result, retaining custom images incurs a snapshot fee. A 80 GB <a href="https://intl.cloud.tencent.com/document/product/362/32415">free tier</a> is provided for Chinese regions For billing details of CBS service, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</li>
<li>Image fee: If the custom image is sourced from a paid image, using it incurs fees.</li>
</ul>
</td>
</tr>
<tr>
<td>Shared image</td>
<td>A shared image is a custom image shared from another Tencent Cloud account. If the shared image is sourced from a paid image, using it incurs fees.</td>
</tr>
</table>


