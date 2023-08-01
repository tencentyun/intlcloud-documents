This document describes the billing policies of CVM images.

## Billing overview
The table below shows the billing details of different types of images.
<table class="tg">
<thead>
  <tr>
    <th width="10%">Image type</th>
    <th width=90%>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">Public image</td>
    <td class="tg-0pky">Include open-source images and commercial images:<br><li>Open-source images do not incur license fees.  </li><li>Using commercial images incurs license fees. Please check the license fee in your bill. Tencent Cloud now provides two series of commercial images, Windows Server images and Red Hat Enterprise Linux images. </td></li>
  </tr>
  <tr>
    <td class="tg-0pky">Custom image</td>
    <td class="tg-0pky">Billable items:<br><li>Snapshot fee: The image use the CBS snapshot service. As a result, retaining custom images incurs a snapshot fee. For regions in China, CBS Snapshot offers a <a href="https://intl.cloud.tencent.com/document/product/362/32415">free tier</a> of 80 GB and usage beyond the free tier will be billed over pay-as-you-go. For more details, see <a href="https://intl.cloud.tencent.com/document/product/362/32415">Billing Overview</a>. </li><li>Image fee: If the custom image is sourced from a paid image, using it incurs fees. </li></td>
  </tr>
  <tr>
    <td class="tg-0pky">Shared image</td>
    <td class="tg-0pky">A shared image is a custom image shared from another Tencent Cloud account. If the shared image is sourced from a paid image, using it incurs fees. </td>
  </tr>
</tbody>
</table>

<span id="redhat"></span>

## Windows server images

For usage of Windows images in Chinese mainland regions, the license fee is waived. For regions outside the Chinese mainland, licenses are charged as part of the instance fee. See the example below for better understanding.

>!The prices in the exmaple are for reference only. Refer to the purchase page for the actual prices.

#### Billing example

A user wants to purchase Standard S5.MEDIUM2 instances in Singapore Zone 1 over pay-as-you-go. The instance configurations are the same except the image.
- CentOS instance: 0.04 USD/hour.
- Windows instance : 0.05 USD/hour. The license fee is included in the instance fee. The image does not incur additional fees.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QCPB267_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16902727662468.png)


## Red Hat Enterprise Linux images
Red Hat Enterprise Linux is a commercial OS. Tencent ‍Cloud ‍is licensed to provide related images. The image fee of Red Hat Enterprise Linux images includes the license fee, and is the same for all Tencent Cloud regions.
<dx-alert infotype="explain" title="">
- All Tencent Cloud discounts (including RI discounts) and vouchers cannot apply to the license fee of Red Hat Enterprise Linux images.
- To use Red Hat Enterprise Linux images, select an instance type that is verified by Red Hat Enterprise Linux when you purchase the CVM. For more details, see [FAQs about Red Hat Enterprise Linux Image](https://www.tencentcloud.com/document/product/213/55135).
- Red Hat Enterprise Linux image ‍is now in beta. To join the beta, [submit a ticket](https://console.tencentcloud.com/workorder/category).
</dx-alert>

### Licensed Red Hat Enterprise Linux image pricing

| Specification | Pay-As-You-Go on an Hourly Basis (Minimum Billable Unit: 1 Hour)|
|---------|---------|
| 4 vCPU and below | 0.06 USD/hour |
| Above 4 vCPU | 0.13 USD/hour |

<dx-alert infotype="explain" title="">
If you choose a licensed Red Hat Enterprise Linux image when creating a **spot instance**, the image is billed on a pay-as-you-go basis and it cannot enjoy the discounts available for the **spot instance**.
</dx-alert>

### OS reinstallation and image billing
- A switch between Red Hat Enterprise Linux and any other OS is supported, but switching between Windows and Linux is unavailable in regions outside the Chinese mainland. When the OS is switched, the new image is billed instead.
- When licensed Red Hat Enterprise Linux is reinstalled on a pay-as-you-go instance, images are billed on a pay-as-you-go basis. During an instance billing cycle, any usage of the images incurs a license fee.
**Example**:
You purchased a CentOS instance on January 1, 2023 at 8:00 AM, reinstalled it using a Red Hat Enterprise Linux at 9:30 AM, and then switched it back to CentOS at 10:30 AM. In this case, there was no license fee during 8:00-9:00 AM, the license fee was incurred for 9:00 - 10:00 AM and 10:00 - 11:00 AM. There was no license fee after 11:00 AM. 

### Images for [RI](https://www.tencentcloud.com/document/product/213/30571) 
- For Linux RIs, the instance fee does not include the license fee for the Red Hat Enterprise Linux image. The license fee is billed separately.
- For PAYG instances using licensed Red Hat Enterprise Linux images, RI discounts can apply to the instance fee, but not the image license fee. The license fee is billed separately.


### Adjusting configuration

You cannot adjust the configuration and billing mode for instances with Red Hat Enterprise Linux OS.



