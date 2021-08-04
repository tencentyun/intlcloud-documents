## Overview
If you are a sub-account with admin permissions (AdministratorAccess) or full access to CAM (QcloudCamFullAccess) and have purchased CVM, VPC, COS, and other Tencent Cloud resources, you can create one or more sub-accounts for your team members and allow them to access your resources.


This document describes how to use the admin account to create a sub-user in the CAM console and bind the sub-user to a permission policy.
>?Both sub-users and collaborators are sub-accounts. For related definitions and permission descriptions, please see [User Types](https://intl.cloud.tencent.com/document/product/598/32633).

| Creation Method | Applicable Scenario | Description |
|---------|---------|---------|
| Quick creation | Creating admin users | They have the `AdministratorAccess` permission by default, which can be modified |
| Custom creation | Creating general sub-users and message recipients | They can be bound to permission policies as needed |


## Prerequisites
[A sub-account with admin permissions](https://intl.cloud.tencent.com/document/product/598/40985) or a sub-account with `QcloudCamFullAccess` has been created.

## Directions
### Creating in console

>?You can click the following tabs to view the directions to create and authorize different types of sub-accounts.

<dx-tabs>
::: Quick\screation

1. Log in to the Tencent Cloud console, go to [User List](https://console.cloud.tencent.com/cam), and click **Create User** to enter the user creation page.
2. On the user creation page, click **Quick Creation** to enter the quick user creation page.
3. On the quick user creation page, enter the username in **User Information** and adjust other options as needed.
>?You can click **Create User** to create up to 10 users at a time.
4. For **Password resetting required**, select whether the sub-user needs to reset the password upon next login as needed.
5. Click **Create User**. You will be redirected to the page prompting that the user is successfully created.
6. On the page prompting that the user is successfully created, you can get the sub-user information in the following two methods:
	- Click **Send**, enter the email address, and the system will send the complete sub-user information to the specified email address.
	- Click **Copy** and paste the information to a local file for storage.


:::
::: Custom\screation

1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the user list page, click **Create User** to enter the user creation page.
3. On the user creation page, click **Custom Creation** to enter the user type selection page.
4. On the user type selection page, select **Access Resources and Receive Messages** or **Receive Messages Only** and click **Next** to enter the user information.
![](https://main.qcloudimg.com/raw/cb2540de8c2d090f08e279a087066685.png)
5. Enter and confirm the information as prompted and click **Done**.
 - If you select **Access Resources and Receive Messages**, you will be redirected to the page prompting that the user is successfully created.
 - If you select **Receive Messages Only**, you will be redirected to the **User List** page.
:::
</dx-tabs>


### Creating through API
You can create a sub-user and configure permissions for them by calling the `AddUser` API with an access key. For more information, please see [AddUser](https://intl.cloud.tencent.com/document/product/598/32265).

## Related Documents
For more information on how to manage and authorize sub-users through user group, please see [Managing User Group](https://intl.cloud.tencent.com/document/product/598/10599) and [Setting User Group Permissions](https://intl.cloud.tencent.com/document/product/598/32666).
For more information on how to associate/dissociate a sub-user to/from policies, please see [Setting Sub-user Permissions](https://intl.cloud.tencent.com/document/product/598/32650).
For more information on how to log in as a sub-user, please see [Logging in as Sub-user](https://intl.cloud.tencent.com/document/product/598/34006).
For more information on how to reset a sub-user password, please see [Resetting Login Password for Sub-user](https://intl.cloud.tencent.com/document/product/598/32656).
For more information on how to subscribe to messages for a sub-user, please see [Sub-user Message Subscription](https://intl.cloud.tencent.com/document/product/598/32651).
