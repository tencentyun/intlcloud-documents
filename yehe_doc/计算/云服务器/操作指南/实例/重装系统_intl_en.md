## Operation Scenario

Reinstalling the operation system is an important method to restore instances to their initial status in the event of a system failure. This document describes how to reinstall the operating system.
Cloud Virtual Machine (CVM) supports two reinstallation types:
 - **Single-system reinstallation**: is applicable to CVMs in any region.
 For example, reinstall from Linux to Linux or from Windows to Windows. 
 - **Cross-system reinstallation**: is available to Mainland China only, excluding Hong Kong, SAR.
 For example, reinstall from Linux to Windows or from Linux to Windows.
> 
> - Currently, all new CBS instances and local disks support cross-system reinstallation. However, some existing 20-GB local disks currently do not support cross-system reinstallation through the console. If you are using these local disks, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) to apply for the cross-system installation feature, when needed.
> - Spot instances do not support system reinstallation.

## Notes
 - **Preparations:** back up important data in your system disk before reinstallation, because data in the system disk will be lost after reinstallation. To keep your system data, we recommend that you [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) and use this image to reinstall the system.
 - **Recommended images:** we recommend that you use the image provided by Tencent Cloud or your custom image instead of those from unknown or other sources. Do not perform any other operations when the system disk is being reinstalled.
 - **Physical features of the instance:** the public IP address of the instance does not change.
 - **Billing:** when adjusting the size of the system disk (for CBS only), you will be charged according to the pricing standards of CBS. For more information, see [CBS Pricing](https://intl.cloud.tencent.com/document/product/213/2255).
 - **Subsequent operations:** after the system disk is reinstalled, data in data disks is not affected, but will be available for use only after the data disks are remounted.

## Directions

You can reinstall the operating system in two ways:
- [Reinstalling the system in the console](#consoleRestart)
- [Reinstalling the system through the API](#apiRestart)

<span id="consoleRestart"></span>
### Reinstalling the system in the console

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the row of the instance for which you want to reinstall the system, choose **More** > **Reinstall System**, as shown in the following figure:
![Reinstall the system](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. In the system reinstallation window that appears, select the image used by the current instance or another image, set the disk size, enter the password, and click **Reinstall Now**.
> Here, the password is the one that you set when configuring the CVM instance or that was generated automatically by the system. If you forget the login password of your CVM instance and want to reset it, see [Resetting the Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
>
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### Reinstalling the system through the API

- For more information, see the [ResetInstance API](https://intl.cloud.tencent.com/document/product/599/30458).
