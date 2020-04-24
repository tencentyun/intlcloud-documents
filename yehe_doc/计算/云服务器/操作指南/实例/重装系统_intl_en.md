## Scenario

Reinstalling the operating system can restore an instance to its state upon startup. This is an important method to restore instances upon system failures. This document describes how to reinstall the operating system.
CVMs support the following reinstallation types:
 - **Reinstalling the original operating system**: CVMs in all regions support reinstalling the original operating system.
 For example, a Linux or Windows operating system can be reinstalled. 
 - **Changing the operating system**: only CVMs in Mainland China support changing the operating system.
 For example, you can reinstall the operating system to change from a Linux operating system to a Windows operating system or from a Windows operating system to a Linux operating system.
> 
> - Currently, all new instances with cloud and local disks support changing the operating system. Some existing instances with 20-GB local disks do not support changing the operating system in the console. To change the operating system for these instances, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM).
> - Spot instances do not support reinstalling the operating system.

## Notes
 - **Reinstallation preparations**: data in the system disk will be lost after reinstallation. Before reinstallation, you need to back up important information in the system disk. To back up system runtime data, we recommend that you [create a custom image](https://intl.cloud.tencent.com/document/product/213/4942) and use the custom image to reinstall the operating system.
 - **Image selection**: we recommend that you use the image provided by Tencent Cloud or a custom image to reinstall the operating system. Do not use images from other unauthorized sources. When reinstalling the system disk, do not perform any other operations.
 - **Physical instance feature**: the public IP address of the instance will remain unchanged.
 - **Billing**: when adjusting the size of the system disk (only the cloud disk is supported), you will be charged based on the pricing standard for cloud disks. For details, see the [Pricing List](https://intl.cloud.tencent.com/document/product/213/2255).
 - **Subsequent operation**: after the system disk is reinstalled, data in the data disk is not affected. However, you must first re-mount the data disk so that you can use it.

## Directions

You can use either of the following methods to reinstall the operating system:
- [Using the console to reinstall the operating system](#consoleRestart)
- [Using APIs to reinstall the operating system](#apiRestart)

<span id="consoleRestart"></span>
### Using the console to reinstall the operating system

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/).
2. In the instance whose operating system needs to be reinstalled, choose **More** > **Reinstall the system**, as shown in the following figure.
![Reinstall the system](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. In the **Reinstall the system** window that appears, select an image, adjust the disk size, enter the password, and click **Start reinstall**.
> Enter the password that was set or automatically generated when you configured the CVM instance. If you have forgotten the CVM login password, reset it by referring to [Resetting the Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
>
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### Using APIs to reinstall the operating system

For details, see [ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242).

## Subsequent Operations
If your CVM has mounted a data disk before operating system reinstallation and the operating system to be reinstalled is different from the original operating system, refer to the following documents for how to read data from data disks of the original operating system.
- [Reading or Writing EXT Data Disks After Changing a Linux CVM to a Windows CVM](https://intl.cloud.tencent.com/document/product/213/3856)
- [Reading or Writing NTFS Data Disks After Chaning a Windows CVM to a Linux CVM](https://intl.cloud.tencent.com/document/product/213/3857)
