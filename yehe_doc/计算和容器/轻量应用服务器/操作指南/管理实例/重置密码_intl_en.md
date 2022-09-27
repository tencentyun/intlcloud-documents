## Overview

You can reset the passwords Lighthouse instances in the following scenarios:
- Log in to an instance remotely on a local computer for the first time.
 - Reset the user (root) password before the first remote login or SSH key login of a Linux instance.
 - Reset the password of admin account (e.g., `Administrator`) with a custom password. It's recommended if you password.
- Reset the password if you have forgotten your instance login password.

## Notes
- You can only reset the login passwords when the instance is shut down.
- Running instances will be shut down when you reset their login passwords. To avoid service interruptions and data losses, plan ahead and reset passwords during off-peak hours.
- For instances created with Ubuntu images, password login is disabled for the `root` account by default. To enable it, see [How do I log in to an instance as the root user on Ubuntu?](https://intl.cloud.tencent.com/document/product/1103/41257).
- To improve the instance security, we recommend you use an SSH key pair to log in to Linux instances. For more information, see [Managing SSH Keys](https://intl.cloud.tencent.com/document/product/1103/41392).

## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and open the window to reset the instance password in the following way:
 - In the instance card, select **More** > **Reset password** in the top-right corner.
 ![](https://qcloudimg.tencent-cloud.cn/raw/8d0219d3e7a2369848339cce1c265bab.png)
 - Select the instance card to enter the instance details page, and click **Reset password** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/14aa88a4c25d71c0124d3bf578e0b39a.png)
2. Reset the password according to the instance status.
<dx-tabs>
::: Running instance
For instances in Running status, do the following:
 1. Confirm the username, enter the **New password**, re-enter the new password in the **Confirm password** field, and click **Next**.
 <dx-alert infotype="notice" title="">
 The **Username** defaults to **System default**, and the default system username is used, such as `Administrator` for Windows, `ubuntu` for Ubuntu, and `root` for other Linux distributions. You can also select **Specified user name** and enter the username.
 </dx-alert>
 ![](https://qcloudimg.tencent-cloud.cn/raw/fa5f8a3bd19e1e27dd39bf7376a5cd37.png)
 2. Select **Agree to a forced shutdown** and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/08247201a8b6a9d5ef3352ab389c2fc5.png)

:::
::: Shutdown instance
For instances in Shutdown status, do the following:
 1. Confirm the username, enter the **New password**, re-enter the new password in the **Confirm password** field, and click **Next**.
<dx-alert infotype="notice" title="">
The **Username** defaults to **System default**, and the default system username is used, such as `Administrator` for Windows, `ubuntu` for Ubuntu, and `root` for other Linux distributions. You can also select **Specified user name** and enter the username.
</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/440daaa933e5af20301b5ccff99b41f5.png)
 2. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/57f83817dfaa298c51d280c64ce04099.png)

:::
</dx-tabs>



