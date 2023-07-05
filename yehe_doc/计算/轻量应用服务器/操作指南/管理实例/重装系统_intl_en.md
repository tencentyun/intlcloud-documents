## Overview

OS reinstallation is to reinstall the OS (and pre-installed applications) of a Lighthouse instance to restore it to the initial status or install a new system. This is a common way to recover the instance in the event of a system failure.

<dx-alert infotype="explain" title="">
Currently, Lighthouse supports the sensitive operation protection feature to effectively protect the security of account resources. It can be enabled in [security settings](https://console.cloud.tencent.com/developer/security). OS reinstallation is a sensitive operation.
</dx-alert>




## Notes
 - **Cross-OS reinstallation:** 
  - Currently, only instances in the Chinese mainland support cross-OS reinstallation, for example, from Linux to Windows or vice versa. A Linux instance system disk must be at least 40 GB in size as required by the Windows Server image; otherwise, cross-platform reinstallation will fail.
  - Instances outside the Chinese mainland only support same-OS reinstallation.
 - **Data backup:** After OS reinstallation, the system disk will be cleared and reset to the initial status of a new image. Therefore, you need to back up important data in it before reinstallation.
 - **Instance IP:** After OS reinstallation, the instance public IP will remain unchanged.
 - **Forced shutdown:** During OS reinstallation, the instance will be automatically shut down (soft shutdown will be performed first by default, and forced (hard) shutdown will be performed if soft shutdown fails).


## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the instance list and select a reinstallation method as desired.
 - In the instance card, select **More** > **Reset application** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dc9015130e76d6e42a8ff42d93658c95.png)
 - Click the instance card to enter the instance details page. On the **Overview** tab, click ***Reset application** in **Image details** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ce759d182b030207c73ca36de9f6d102.png)
 - Click the instance card to enter the instance details page. On the **Pre-installed application** tab, click **Reset application** in **Application information** as shown below:
<dx-alert infotype="explain" title="">
If the Lighthouse instance doesn't use an application image, you cannot reinstall the OS in this way.
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/013f084fab8164bcd95f7a2d2815d47c.png"/>
4. On the **Reset application** page, select the target image (you can select a system, application, basic Docker, custom, or shared image), read the reinstallation notes, select **I have read and understand the above notes.**, and click **OK** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/a14d73a12bec47a63f96e1e5390d8d89.png)

