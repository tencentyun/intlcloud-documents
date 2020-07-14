## Overview
This document describes how to change the password for a sub-user. After the modification, the sub-user can use the new password to log in and manage resources under the root account.
## Directions
>?These directions only apply to created custom sub-users.
>
1. In [User List](https://console.cloud.tencent.com/cam), locate the sub-user whose password needs to be changed and click the **username** to enter the user details page.
2. Go to **Security** > **Access Security** > **Console Login Management** and click **Manage** as shown below:
![](https://main.qcloudimg.com/raw/38da51b500940ab5d45b0e03f5f566f8.png)
3. In the **Console Access** window that pops up, set the password for the current user as shown below:
![](https://main.qcloudimg.com/raw/40431bf5f8ff652253172e6981d3890e.png)
 - If the current sub-user needs to access Tencent Cloud by logging in to the console, select **Enable** for **Console Access**.
 - If you need to set a new password for the sub-user, you can do so in the following two ways:
    - If you select **Auto-generate password** in **Access Password**, the system will automatically generate a console login password. You can copy and save it. If needed, you can also click **Download .csv** to save the password.
    - If you select **Customize Password** in **Access Password**, enter the password you want to set as the sub-user's console login password.
 -  If you want the current user to reset their own password, you can select **Enforce Password Reset**. The sub-user will be required to reset their console login password the next time they log in.
 
## Related documents
For more information on how to create custom sub-users, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
For more information on how to change the login password for collaborators, please see [Modifying Account Password](https://intl.cloud.tencent.com/document/product/378/36001).

