## Overview
You can log in to the Tencent Cloud SSM console to view and edit information list, name, status, region and other details of the credential.

## Prerequisites
- You have created your account and password in the [SSM console](https://console.cloud.tencent.com/ssm).
- You have created a database credential. If haven’t, see [Creating a Database Credential](https://intl.cloud.tencent.com/document/product/1078/41801).

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Database Credential** on the left sidebar.
 ![](https://main.qcloudimg.com/raw/42ef59cd190a31b35e67c0d1cd2f8ef9.png)
2. Click the drop-down button in the top left corner of the credential list to modify the region.
   ![](https://main.qcloudimg.com/raw/38bab9413fb1ce9c98f836ee185d1aac.png)
3. Search for a credential by entering keywords relevant to tags and credential names in the search box.
![](https://main.qcloudimg.com/raw/63eecf8040190c58885ff9d92dab6bb2.png)
4. Click **Secret Name** to check the details of the credential.
>? You can enable or disable rotation by clicking **Rotation Status**. For details, see [Modifying rotation information](#modify_rotate).

 ![](https://main.qcloudimg.com/raw/2cb436b878c81466c24a5ef48bd8f63a.png)
5. On the credential details page, you can modify the credential description and version information, enable/disable the credential, and set rotation.

### Modifying basic information
- **Secret Status** can be changed by enabling the status toggle. If the toggle displays grayed out, the credential is disabled.
- **Description** describes what the credential is used for. Maximum length: 2048 bytes. This is an optional field.

[](id:modify_rotate)
### Modifying rotation information
The "Rotation Information" section displays the rotation status, rotation cycle, end time of last rotation and start time of next rotation (this information is available only when rotation is enabled).
- **Configure Rotation**: Click this button to enter the rotation information including rotation cycle (from 30 to 365 days) and start time of next rotation (from current time plus 24 hours to current time plus 365 days) in the pop-up window.
   ![](https://main.qcloudimg.com/raw/0633d5eeda529188bcf4377332bfafe4.png)

- **Rotate Now**: Click this button to read through a pop-up notice and then click **OK** to start rotation.
>? To start rotation, the rotation status must be enabled.

   ![](https://main.qcloudimg.com/raw/b53d1e8c3ce94723b7983f9de35a034a.png)

### Version Information
The version number of a credential will be shown in the "Version Information" section. To check the credential’s account name and password, you can click **View**.
>! The plaintext of the password is automatically obtained and updated by the SSM API. For security considerations, it is not recommended that you check the values of the managed credentials on the console.

![](https://main.qcloudimg.com/raw/a61b4f400fd2d21571751edc3df7df5e.png)

