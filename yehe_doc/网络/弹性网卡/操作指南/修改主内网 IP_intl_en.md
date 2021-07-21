This document describes how to modify the primary private IP of a CVM instance on the ENI console.
>!
>+ You can modify the primary private IP of the primary ENI, but not that of secondary ENIs.
>+ Note that modifying the primary IP of the primary ENI will automatically restart the associated instance and cause business interruption for about 30 seconds.
>+ The private IP can also be modified on the CVM console as instructed in [Modifying Private IP Addresses](https://intl.cloud.tencent.com/document/product/213/16561).

## Prerequisites
The primary ENI ID of the CVM instance has been obtained on the CVM console. For more information, see [Query Instance Info](https://intl.cloud.tencent.com/document/product/213/16533).

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Locate the ENI you want to modify the primary IP, and click its **ID/Name** to enter the details page.
4. Click the **IPv4 address management** tab, and check the primary private IPs that have been bound.
![](https://main.qcloudimg.com/raw/9ac36c5a428ae63f03b4a9d52e267152.png)
5. Locate the primary private IP you want to change, and click **Modify Primary IP* under the **Operation** column.
![](https://main.qcloudimg.com/raw/519cc573d98fe4d30948a5ae89033782.png)
6. Enter a new primary private IP in the pop-up window, and click **OK**.
![](https://main.qcloudimg.com/raw/495555a2c35cf0442c670a5a7c4b1fb9.png)
