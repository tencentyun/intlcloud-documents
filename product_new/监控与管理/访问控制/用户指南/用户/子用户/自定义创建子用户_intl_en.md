## Introduction
This document describes how to create a custom sub-user and configure permissions for it. The sub-user can manage the resources under the root account within the scope of the configured permissions.

## Directions
### Creating in console
You can log in to the Tencent Cloud Console to create a custom sub-user and configure permissions for it.
1. 	Log in to the CAM Console and select **User** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. 	On the user list page, click **Create User**.
3. 	Click **Create Custom User**.
4. On the user type selection page, select **Access Resources and Receive Messages** and click **Next**.
5. Enter a username (required), notes, a mobile number, and email address.
 > 
 > - Click **Add User** to add more users. You can create up to 10 users at a time. 
 > - As the sub-user will log in with the username, the username cannot be changed once the user is created.
6. Configure the **Access Mode** for the sub-user.
 - Programming access: enable `SecretId` and `SecretKey`, and the sub-user will be able to use TencentCloud APIs, SDKs, and other developer tools to manage the resources under the root account within the scope of configured permissions.
 - Tencent Cloud Console access: enable password and the sub-user will be able to log in to the Tencent Cloud Console to manage the resources under the root account within the scope of the configured permissions.
 > To ensure the security of your account, we recommend enabling login and operation protection.
7. Click **Next**.
8. On the permissions configuration page, configure permissions for the new sub-user in one of the following ways according to your needs. After being associated with a policy, the sub-user will have the permissions described by the policy.
 - Select policies from policy list: click **Select policies from policy list** and select the policies you want to associate with the sub-user.
 - Use existing user policies: click **Use existing user policies** and select the user whose permissions you want to use; the new sub-user will be associated with the policies of the existing user.
 - Use group permissions: you can add the sub-user to an existing user group or a new user group, and the sub-user will be associated with the policies of the user group. This is the best way to manage user permissions by roles and functions.
9. Click **Next** to enter the review page.
10. On the review page, double check the information, click **Complete**, and you will see a prompt saying that you have successfully created a sub-user.
11. You can get the sub-user information in the following ways.
 - Click **Enter User Email** > **OK** and the information of the new sub-user will be sent to the specified email address.
 - Click **Download Security Credentials** and some of the information will be saved to a local Excel file.

### Creating through API
You can create a sub-user and configure permissions for it by calling the `AddUser` API through an access key.
## Relevant Documents
For more information on how to manage sub-users through user groups and group permissions, please see [User Group Management](https://intl.cloud.tencent.com/document/product/598/10599?from_cn_redirect=1) and [Setting User Group Permissions](https://intl.cloud.tencent.com/document/product/598/32666).

For more information on how to associate/dissociate a sub-user to/from policies, please see [Setting Sub-User Permissions](https://intl.cloud.tencent.com/document/product/598/32650).

For more information on how to log in as a sub-user, please see [Logging in as a Sub-User](https://intl.cloud.tencent.com/document/product/598/34006).

For more information on how to reset a sub-user password, please see [Resetting Login Passwords for Sub-Users](https://intl.cloud.tencent.com/document/product/598/32656).

For more information on set message subscription for sub-users, please see [Sub-Users Message Subscriptions](https://intl.cloud.tencent.com/document/product/598/32651).

