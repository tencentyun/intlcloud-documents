## Overview

System reinstallation is an important method to restore instances to their initial status in the event of a system failure.

CVM supports the following two reinstallation types:
 - **Single-system reinstallation*: is applicable to CVMs in any region.
 For example, reinstall from Linux to Linux or from Windows to Windows. 
 - **Cross-system reinstallation**: is available to Mainland China only, excluding Hong Kong (China).
 For example, reinstall from Linux to Windows or from Linux to Windows.
>? 
> - Currently, all new CBS instances and local disks support cross-system reinstallation. However, some existing 20-GB local disks do not support cross-system reinstallation via the Console. If you are using these local disks, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) to apply for the cross-system installation feature, when needed.
> - Spot instances do not support system reinstallation.

## Notes
 - **Preparations**: back up important data in your system disk before reinstallation, because data in the system disk will be lost after reinstallation. To keep your system data, we recommend that you [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) and use this image to reinstall the system
 - **Recommended images:** we recommend that you use the image provided by Tencent Cloud or your custom image instead of those from unknown or other sources. Do not perform any other operations when the system disk is being reinstalled.
 - **Instance physical features:** the public IP of the instance does not change.
 - **Billing**: when adjusting the size of the system disk (for CBS only), you will be charged according to the pricing standards of CBS. For more information, see [Pricing List](https://intl.cloud.tencent.com/document/product/213/2255).
 - **Subsequent operations:** after the system disk is reinstalled, data in data disks is not affected, but will be available for use only after the data disks are remounted.

## Directions

You can reinstall the operating system in two ways:
- [Reinstalling the system via the Console](#consoleRestart)
- [Reinstalling the system via APIs](#apiRestart)

<span id="consoleRestart"></span>
### Reinstalling the system via the Console

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. In the row of the instance for which you want to reinstall the system, choose **More** > **Reinstall the system**, as shown in the following figure:
![Reinstall the system](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. In the system reinstallation window that appears, click **OK, reinstall now**.
4. Select the image used by the current instance or another image, set the disk size, enter the password, and click **Start install**.
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### Reinstalling the system via APIs

For more information, see the [ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242) API.

## See Also
If your CVM has mounted a data disk before the cross-system reinstallation, see the following documents about how to read data from data disks of the original operating system.
- [Reading/Writing EXT Data Disks after Reinstalling a Linux CVM to Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856)
- [Reading/Writing NTFS Data Disks after Reinstalling a Windows CVM to Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857)
