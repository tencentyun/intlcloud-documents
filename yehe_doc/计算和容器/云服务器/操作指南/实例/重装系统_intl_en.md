## Overview

OS reinstallation can restore instances to their initial statuses, which is a common way to recover the instance in the event of a system failure.

CVM supports the following two reinstallation types:
 - **Reinstall on the same platform**: CVMs in all regions can be reinstalled to the OS of the same platform.
 For example, you can always reinstall a Linux instance on a Linux OS, and Windows instance on a Windows OS. 
 - **Reinstall on different platform**: only CVMs in the Chinese mainland can be reinstalled to an OS of different platform.
 For example, a Linux instance can be reinstalled on a Windows OS, and a Windows instance on a Linux OS.
>? 
> - Currently, all new instances with cloud disks or local disks can be reinstalled on different OS platform. Some existing 20 GB local disk instances do not support cross-system reinstallation on the console. Users who use them need to [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) to apply for this feature.
> - Spot instances do not support system reinstallation.

## Notes
 - **Preparation:** After the re-installation, all data in the system disk are cleared. Please back up important data in advance. To retain your system runtime data, we recommend that you [create a custom image](/doc/product/213/4942) and use this image to reinstall the system.
 - **Image selection:** we recommend that you use the image provided by Tencent Cloud or your custom image instead of those from unknown or other sources. Do not perform other operations while the system disk is being reinstalled.
 - **Instance physical features:** the public IP of the instance will not change.
 - **Specification limits**: if you want to use an image with Windows 2016,  or 2019 versions, the instance memory should be greater than 2 GB.
 - **Billing:** if you adjust the size of the system disk (for cloud disks only), you will be charged according to the pricing standards of CBS. For more information, see [Pricing List](/doc/product/213/%E7%A1%AC%E7%9B%98%E4%BB%B7%E6%A0%BC).
 - **Subsequent operations:** after the system disk is reinstalled, the data in the data disks will not be affected and will be available for use only after the data disks are reattached.

## Directions
You can use either of the following methods to reinstall the operating system:
<dx-tabs>
::: Reinstalling the system in the console[](id:useConsole)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. Locate the instance, and click **More** > **Reinstall the System** under the **Operation** column, as shown in the following figure:
![](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. In the pop-up window that appears, read notes and click **Next**.
4. Select an image, set the instance login method, and click **OK**, as shown in the following figure:
>? You can select **Follow Image** as the login method only when the image type is **Custom Image** or **Shared Image**.
>
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)
:::
::: Reinstalling the system via an API[](id:useAPI)
For more information, please see the [ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242) API.
:::
</dx-tabs>

## Subsequent Operations
If the CVM has attached a data disk and you need to reinstall it on a different platform, please see the following documents about how to read data from the data disks of the original operating system:
- [Reading/Writing EXT Data Disks after Reinstalling a Linux CVM to Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856)
- [Reading/Writing NTFS Data Disks after Reinstalling a Windows CVM to Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857)
