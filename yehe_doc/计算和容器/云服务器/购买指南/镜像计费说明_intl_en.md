This document describes the billing of CVM instance images.

## Billing Overview
Check below for the billing details of images.
<table class="tg">
<thead>
  <tr>
    <th width="10%"> Image Type</th>
    <th width="90%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Public image</td>
    <td class="tg-0pky">It includes open-source images and commercial images.<br><li>Open-source images are free of charge.</li><li>You will be charged for licenses to use commercial images. Tencent Cloud now provides two commercial images, Windows Server image and Red Hat Enterprise Linux image.</td></li>
  </tr>
  <tr>
    <td class="tg-0pky">Custom image</td>
    <td class="tg-0pky">There are two billable items: <br><li>Snapshot fee: The image use the CBS snapshot service. As a result, retaining custom images incurs a snapshot fee. For billing details of CBS service, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>.</li><li>Image fee: If the custom image is sourced from a paid image, using it incurs fees.</li></td>
  </tr>
  <tr>
    <td class="tg-0pky">Shared image</td>
    <td class="tg-0pky">A shared image is a custom image shared from another Tencent Cloud account. If the shared image is sourced from a paid image, using it incurs fees.</td>
  </tr>
</tbody>
</table>

<span id="redhat"></span>

## Windows Server Image
#### Billing sample

Instance specification: Singapore Zone 1, Standard S5.MEDIUM2, pay-as-you-go.
- The Windows instance fee is 0.05 USD/hour. No image fee incurred.
![](https://qcloudimg.tencent-cloud.cn/raw/af8b0002847ce5f1542a90a1990e27ce.png)


## Red Hat Enterprise Linux Image
Red Hat Enterprise Linux is a commercial OS. The image fee includes the license fee. The same price applies across all Tencent Cloud regions.
<dx-alert infotype="explain" title="">
- Discounts (including discounts for spot instances) and vouchers are not applicable for the purchase of a license for the Red Hat Enterprise Linux image in Tencent Cloud.
- You can select an instance model that has been certified for Red Hat Enterprise Linux to use the Red Hat Enterprise Linux image. For supported image tags and instance models, see [FAQs about Red Hat Enterprise Linux Image](https://www.tencentcloud.com/document/product/213/55135).
- Red Hat Enterprise Linux image is now only available to beta users. To join the beta, please [submit a ticket](https://console.tencentcloud.com/workorder/category).
</dx-alert>

### Price of Licensed Red Hat Enterprise Linux image

|Specification | Pay-as-you-go on an hourly basis (Minimum billable unit: 1 hour) |
|---------|---------|
| 4 vCPU and below | 0.06 USD/hour |
| Above 4 vCPU | 0.13 USD/hour |

<dx-alert infotype="explain" title="">
If you choose a licensed Red Hat Enterprise Linux image when creating a **spot instance**, the image is billed on a pay-as-you-go basis and it cannot enjoy the discounts available for the **spot instance**.
</dx-alert>

### Image billing for OS reinstallation
- You can switch the OS of an instance between Red Hat Enterprise Linux and others. In this case, the image fee is calculated based on the new image. Note that you cannot switch between Windows OS and Linux OS in regions outside the Chinese mainland. 
- For a pay-as-you-go instance, when the OS is reinstalled to licensed Red Hat Enterprise Linux, the image is billed on a pay-as-you-go basis. If the Red Hat Enterprise Linux image is used during a billing cycle, you need to pay for the image license fee for the cycle.
**Example**:
You purchased a CentOS instance at 8:00 am on January 1, 2023. No image license fee occurred during 8:00 - 9:00 am. At 9:30 am, you reinstalled the instance OS with Red Hat Enterprise Linux, and you need to pay for the image license for the billing cycle 9:00 - 10:00 am. At 10:30 am, you reinstalled the instance OS with CentOS, and you need to pay for the image license for the billing cycle 10:00 - 11:00 am. After 11:00 am, you do not need to pay for the image license.

### Billing under RI mode
- When you select RI for a Linux instance, you need to pay for the license for the Red Hat Enterprise Linux image separately.
- A pay-as-you-go instance with the Red Hat Enterprise Linux image licensed in Tencent Cloud can enjoy a discount when the instance configuration matches RI. However the discount is not available to the image license, which is billed separately.


### Configuration modification

You cannot change the configuration and the billing mode for an instance with Red Hat Enterprise Linux OS.



