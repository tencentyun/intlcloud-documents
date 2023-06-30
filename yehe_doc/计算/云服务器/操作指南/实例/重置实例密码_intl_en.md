## Overview
If you forget your CVM instance login password, you can reset it on the console. This document describes how to reset your instance login password on the console.

<dx-alert infotype="notice" title="">

- When the instance is shut down, you can directly reset the login password.
- If the instance is still running, resetting the login password will force shut down it. To avoid affecting your business, please plan ahead and reset passwords during off-peak hours.
</dx-alert>


## Directions
<dx-tabs>
::: Resetting the password of a single instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, proceed according to the actually used view mode:
   - **List view**: in the row of the target instance, select **More** > **Password/Key** > **Reset Password** on the right as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/9317997308e40e06dcacc64cac24dd41.png)
   - **Tab view**: on the page of the target instance, click **Reset Password** as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/032ecb8f3544bb17892decba6c955d8a.png)
3. Select **Username** and enter the username of the selected instance. Enter the **New password**, re-enter the new password in the **Confirm Password** field, and click **Next**.
<dx-alert infotype="notice" title="">
The **Username** defaults to **System default**, and the default system username is used, such as `Administrator` for Windows, `ubuntu` for Ubuntu, and `root` for other Linux distributions. You can select **Specified user name** and enter the username.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/420c83619601563c1c3c0c64c0bf533d.png"/>
4. Reset the password according to the instance status:
 - To reset the password of **Running** instances, select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - To reset the password of **Shutdown** instances, click **Reset Password**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)   

:::
::: Resetting the passwords of multiple instances

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the CVM instances to reset password, and click **Reset Password** at the top of the instance list, as shown in the following figure:
![](https://main.qcloudimg.com/raw/38b9be9d0b1b6890f9b07852e91c8bd3.png)
3. Select **Username** and enter the username of the selected instance. Enter the **New password**, re-enter the new password in the **Confirm Password** field, and click **Next**.
<dx-alert infotype="notice" title="">
The **Username** defaults to **System default**, and the default system username is used, such as `Administrator` for Windows, `ubuntu` for Ubuntu, and `root` for other Linux distributions. You can select **Specified user name** and enter the username.
</dx-alert>
![](https://main.qcloudimg.com/raw/1abf9af8eb892191acc3998bb5845dea.png)
4. Reset the password according to the instance status:
 - To reset the password of **Running** instances, select **Agree to a forced shutdown** and click **Reset Password**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/ff478b4ab58289137c47356e00ad4c9a.png)
 - To reset the password of **Shutdown** instances, click **Reset Password**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/950198759de0f3f937df8c6dc4b2a72d.png)    

:::
</dx-tabs>

## FAQs
If you fail to reset the password for Windows CVM instances, refer to [Failed to Reset the CVM Password or the CVM Password Is Invalid](https://intl.cloud.tencent.com/document/product/213/35720) for troubleshooting.
