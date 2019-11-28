## Introduction
This document describes how to modify the passwords of sub-users. After modification, the sub-user can use the new password to log in and manage resources under the root account.
## Directions
1. Go to the **User List** page and locate the sub-user whose password you want to modify. Click on the username to go to the user details page.
2. Go to **Security** > **Access Security** > **Console Login Management** and click **Manage**. See the following image for reference:
 ![](https://main.qcloudimg.com/raw/38da51b500940ab5d45b0e03f5f566f8.png)
3. A **Console Access** window will pops up. You can set reset the current user’s password here. See the following image for reference:
![](https://main.qcloudimg.com/raw/40431bf5f8ff652253172e6981d3890e.png)
 - If your current sub-user needs to access Tencent Cloud by logging in to the console, select **Enable** for **Console Access**.
 - If you need to set a new password for the sub-user, you can do so in two ways:
    - If you select **Auto-generate Password** in **Access Password**, the system will automatically generate a console login password. You can copy and save it. If needed, you can click **Download.csv** to save the password.
    - If you select **Customize Password** in **Access Password**, enter the password you want to set for this sub-user’s console login password.
 -  If you want the current user to reset their own password, you can select **Enforce Password Reset**. The sub-user will be required to reset their console login password the next time they log in.
