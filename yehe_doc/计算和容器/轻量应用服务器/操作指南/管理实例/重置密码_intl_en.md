## Overview

Lighthouse allows you to reset the instance login password for the following scenarios:
- You log in to an instance remotely on a local computer for the first time.
 - You use remote login software (or SSH) to log in to a Linux instance for the first time and need to perform this operation to reset the user (root) password.
 - Before logging in to a Windows instance for the first time, if you select **Random Password** for **Login Methods** during instance creation, we recommend you perform this operation to customize the admin account (e.g., `Administrator`) password.
- If you forgot your instance login password, you can reset it in the console.

## Notes
- You can only reset the login passwords of shutdown instances.
- Running instances will be shut down when you reset their login passwords. To avoid service interruptions and data losses, plan ahead and reset passwords during off-peak hours.
- Instances created with Ubuntu images under the `root` username disable to log in to the instance via password by default. To enable it, please refer to [How to log in to an instance with the root user on Ubuntu systems?](https://intl.cloud.tencent.com/document/product/1103/41257).
- To improve the instance security, we recommend you use an SSH key pair to log in to Linux instances. For more information, see [Managing Keys](https://intl.cloud.tencent.com/document/product/1103/41392).

## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. On the **Instances** page, click the card of the target instance.
3. Enter the instance details page and click **Reset password** in the top-right corner.
4. In the pop-up window, the password resetting steps vary by instance status as follows:
<dx-tabs>
::: Running instance
If the instance whose password needs to be reset is Running, perform the following operations:
 1. Confirm the username for which to reset the password, enter the **New password**, re-enter the new password in the **Confirm password** field, and click **Next**.
 <dx-alert infotype="notice" title="">
    The **Username** defaults to **System default**, and the default system username is used, such as `Administrator` for Windows, `ubuntu` for Ubuntu, and `root` for other Linux distributions. You can select **Specified user name** and enter the username.
    </dx-alert>
    ![](https://qcloudimg.tencent-cloud.cn/raw/d2e31e20f88cd7dc9167c2cdb77af60d.png)
 2. Select **Agree to a forced shutdown** and click **Reset password** as shown below:
     ![](https://qcloudimg.tencent-cloud.cn/raw/c7da2fb6683367bae3e1b8cf4aec38c8.png)
     :::
     ::: Shutdown instance
     If you need to reset the password of an instance in Shutdown status, perform the following operations:
 1. Confirm the username for which to reset the password, enter the **New password**, re-enter the new password in the **Confirm password** field, and click **Next**.
	<dx-alert infotype="notice" title="">
	The **Username** defaults to **System default**, and the default system username is used, such as `Administrator` for Windows, `ubuntu` for Ubuntu, and `root` for other Linux distributions. You can select **Specified user name** and enter the username.
	</dx-alert>
	  ![](https://qcloudimg.tencent-cloud.cn/raw/9604f84907bd4154d96e2eeb0c9fe1e8.png)
 2. Click **Reset password** as shown below:
	  ![](https://qcloudimg.tencent-cloud.cn/raw/fe680e817ae643c1ce3b12a6b454f09d.png)
	  :::
	  </dx-tabs>



