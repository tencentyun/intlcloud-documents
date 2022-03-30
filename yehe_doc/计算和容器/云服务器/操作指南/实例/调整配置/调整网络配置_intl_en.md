## Overview
Tencent Cloud allows you to change the public network billing mode or public network bandwidth as needed. The change takes effect immediately. To learn more about the restrictions and price, see [Adjusting Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10580).

## Directions
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index). At the top of the **Instances** page, select the region where the target CVM instance resides.
2. On the instance management page, proceed according to the actually used view mode:
<dx-tabs>
::: List view
Select **More** > **Resource Adjustment** > **Adjust Network** on the right of the target CVM instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/bcece3bef3230a16bbe4b00e71105cf8.png)

:::
::: Tab view
Select **More Actions** > **Resource Adjustment** > **Adjust Network** in the top-right corner of the page of the target instance as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4a57295676734b183310cfc8f06a8e25.png)

:::
</dx-tabs>
3. In the **Adjust Network** pop-up window, adjust the public network billing mode or public network bandwidth as needed:
 - Network billing mode[](id:adjustModule): Tencent Cloud provides two network billing modes: **bill-by-traffic** and **bill-by-bandwidth**. The bill-by-bandwidth mode is **hourly postpaid**.
 - Target bandwidth cap[](id:adjustBandwidth): Tencent Cloud provides two network configurations: **dedicated public network** and **shared public network** (billed by bandwidth package and currently in beta test). This document takes adjusting the configuration of the dedicated public network as an example, i.e., adjusting the bandwidth cap of a single CVM instance.
<dx-alert infotype="explain" title="">
For more information about the bandwidth cap, see [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523).
</dx-alert>
4. Select the target billing mode or set the target bandwidth value and click **OK**.



## Relevant Documentation

- [Adjusting Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10580)
- [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578) 
- [Billing Modes](https://intl.cloud.tencent.com/document/product/684/15254)
- [Public Network Bandwidth Cap](https://intl.cloud.tencent.com/document/product/213/12523)
