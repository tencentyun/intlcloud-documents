## Overview

System reinstallation is an important method for restoring instances to their initial statuses in the event of a system failure.

CVM supports the following two reinstallation types:
 - **Single-system reinstallation**: CVMs in all regions can be reinstalled to the same operating system.
 For example, Linux is reinstalled as Linux and Windows is reinstalled as Windows. 
 - **Cross-system reinstallation**: only CVMs in the Chinese mainland (excluding Hong Kong, China) can be reinstalled to a different operating system.
 For example, Linux is reinstalled as Windows and Windows is reinstalled as Linux.
>? 
> - Currently, all new CBS instances and local disks support cross-system reinstallation. However, some existing 20 GB local disks do not support cross-system reinstallation via the Console. If you need to implement cross-system reinstallation for instances on these local disks, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) to apply for the cross-system installation feature.
> - Spot instances do not support system reinstallation.

## Notes
 - **Preparing for reinstallation:** back up important data to your system disk before reinstallation because the system disk’s data will be lost after reinstallation. To retain your system data, we recommend that you [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) and use this image to reinstall the system.
 - **Image selection:** we recommend that you use the image provided by Tencent Cloud or your custom image instead of those from unknown or other sources. Do not perform other operations while the system disk is being reinstalled.
 - **Instance physical features:** the public IP of the instance will not change.
 - **Billing:** when adjusting the size of the system disk (for CBS only), you will be charged according to the pricing standards of CBS. For more information, see [Pricing List](https://intl.cloud.tencent.com/document/product/213/2255).
 - **Subsequent operations:** after the system disk is reinstalled, the data in the data disks will not be affected and will be available for use only after the data disks are remounted.

## Directions

You can use either of the following methods to reinstall the operating system:
- [Reinstall the system via the Console](#consoleRestart)
- [Reinstall the system via APIs](#apiRestart)

<span id="consoleRestart"></span>
### Reinstalling the system via the Console

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. In the row of the instance for which you want to reinstall the system, click **More** > **Reinstall the system**, as shown in the following figure:
![Reinstall the system](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. In the pop-up window that appears, click **OK, reinstall now**.
4. Select the image used by the current instance or another image, set the disk size, set the login password for the instance, and click **Start reinstall**.
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### Reinstalling the system via APIs

For more information, please see the [ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242) API.

## Subsequent Operations
If your CVM has mounted a data disk before cross-system reinstallation, please see the following documents about how to read data from the data disks of the original operating system:
- [Reading/Writing EXT Data Disks after Reinstalling a Linux CVM to Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856)
- [Reading/Writing NTFS Data Disks after Reinstalling a Windows CVM to Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857)
