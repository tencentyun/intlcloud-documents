## Scenarios

System reinstallation allows you to restore an instance to its initial status at launch, which is an important recovery method if the instance has a system failure. This document describes how to reinstall the operating system.


CVM supports the following two reinstallation types:
 - **Reinstall on the same platform**: CVMs in all regions can be reinstalled to the OS of the same platform.
 For example, you can always reinstall a Linux instance on a Linux OS, and Windows instance on a Windows OS. 
 - **Reinstall on different platform**: only CVMs in the Chinese mainland can be reinstalled to an OS of different platform.
 For example, a Linux instance can be reinstalled on a Windows OS, and a Windows instance on a Linux OS.
<dx-alert infotype="explain" title="">
- All newly added cloud disk and local disk instances support reinstallation on different platforms. Some existing 20 GB local disk instances do not support cross-platform reinstallation in the console. If you use such instances, you need to [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
- Spot instances do not support system reinstallation.
</dx-alert>



## Notes
 - **Preparation:** A reinstallation clears all data in the system disk. Therefore, you must back up important data in the system disk in advance. If you want to retain your system operating data, we recommend you [create a custom image](/doc/product/213/4942) and use this image to reinstall the operating system.
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
2. On the instance management page, proceed according to the actually used view mode:
  - **List view**: in the row of the target instance, select **More** > **Reinstall System** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/292e93008168285d01416391632ff43c.png)
  - **Tab view**: on the page of the target instance, select **More Actions** > **Reinstall the System** in the top-right corner as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/27a65b9ae3e68ab8a6a59e2186ce115d.png)
3. In the pop-up window that appears, read notes and click **Next**.
4. Select the image that is used by the current instance or another image, set the instance login method, and click **OK**, as shown below:
<dx-alert infotype="explain" title="">
Only when the image type is **custom image** or **shared image** can you select **Follow image** as the login method.
</dx-alert>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Akym383_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230407162815.png"/>

:::
::: Reinstalling the system via an API[](id:useAPI)
For details, see [ResetInstance](https://www.tencentcloud.com/document/product/213/33242).

:::
</dx-tabs>

## Related Operations
If the CVM has attached a data disk and you need to reinstall it on a different platform, please see the following documents about how to read data from the data disks of the original operating system:
- [Read/Write EXT Data Disks after Reinstalling a Linux CVM to Windows CVM](https://www.tencentcloud.com/document/product/213/3856)
- [Read/Write NTFS Data Disks after Reinstalling a Windows CVM to Linux CVM](https://www.tencentcloud.com/document/product/213/3857)

