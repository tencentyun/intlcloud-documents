
## Overview  
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the risk of your key being compromised. Therefore, we recommend you create sub-users and let them manage different services to avoid such risk.

By default, sub-users have no permission to use DTS. Therefore, you need to create policies to allow them to use it.

You can skip this section if you don't need to manage the permissions of DTS resources for sub-users.

## Creating and Authorizing Sub-user to Use DTS

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. On the left sidebar, select **User** > **User List** to enter the user list management page. 
3. Click **Create User** to enter the user creation page.
4. On the user creation page, select the creation method. Taking quick creation as an example, the steps are as follows:
![](https://main.qcloudimg.com/raw/2d440534f58569616876781850a85fea.png)
6. On the **Quick User Creation** page, set the sub-user name, access method, user permission, etc.
![](https://main.qcloudimg.com/raw/c4f8ec4822377cf67d96bc7a4f44dd83.png)
   - Console Login: Select **Console access** or **Programming access**.
   - User permission: Select the permission as needed. If you select **QcloudDTSFullAccess**, the sub-user will be granted all read/write permissions of the DTS service. If you select **QcloudDTSReadOnlyAccess**, only the read-only permission will be granted.
7. Click **Create User**.
8. You will be redirected to the page prompting that the user is successfully created, and you can get the sub-user information in the following two methods:
  - Click **Copy** to directly get and copy the login information of the sub-user.
  - Click **Send**, enter the email address, and the system will send the complete sub-user information to the specified email address.

## Authorizing Existing Sub-user to Use DTS
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the root account, locate the target sub-user in the user list, and click **Authorize**.
![](https://main.qcloudimg.com/raw/aad4942744471bc4ff29c9f2f01b242d.png)
2. In the pop-up window, select the **QcloudDTSFullAccess** preset policy and click **OK** to complete the authorization.
![](https://main.qcloudimg.com/raw/03bc84152430e6df16ced69af52a7a48.png)
