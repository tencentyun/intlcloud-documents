Data Lake Compute provides the user mode and work group mode for personnel permission management. For more information on permissions, see [Permission Overview](https://intl.cloud.tencent.com/document/product/1155/48665).

## Description
- User: You can select users in CAM, including sub-accounts and collaborator accounts.
- Work group: It is a group of users with the same permissions managed in the product.

>? If users are granted different permissions from those granted in their work groups, all the granted permissions will take effect.

A work group allows you to quickly grant permissions to a batch of users, so it is recommended for batch user authorization.

## User Management
User management requires Data Lake Compute operation permissions. For more information, see [CAM Service](https://intl.cloud.tencent.com/document/product/1155/48664).

### Adding a user
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Click **Add user** to add an account with a specified user ID to Data Lake Compute for management.
![]()
3. After entering the **User ID**, bind the user to a work group (which requires the admin permission). If binding is not needed, directly click **Complete**.
![]()

### Viewing user information
A Data Lake Compute admin can modify the basic information and permissions of a user.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Search for the target **User ID** and click the **Username** to view the user information and permissions.
![]()

### Editing user information
You can edit the description and work group of a user. For detailed directions, see [Sub-Account Data Authorization](https://intl.cloud.tencent.com/document/product/1155/48667).
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Search for the target user account ID and click **Edit** in the **Operation** column to enter the edit page.

### Removing a user
If you don't want a user to use Data Lake Compute any more, you can use an admin account to remove the user. Then, the Data Lake Compute permission granted to the user will be revoked.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Search for and select one or multiple target user account IDs and click **Batch remove** to remove them from Data Lake Compute.
![]()

## Work Group Management
Work group management requires Data Lake Compute operation permissions. For more information, see [CAM Service](https://intl.cloud.tencent.com/document/product/1155/48664).

### Adding a work group
You can manage permissions that need to be repeatedly granted to users through a work group. The following describes how to add a work group.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Click **Work group** to enter the work group management page.
3. Click **Add work group**, enter relevant information, and click **Confirm**.
![]()

### Viewing work group information
You can view the information of a work group in the following steps:
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Click **Work group** to enter the work group management page.
3. Search for the target work group and click **Work group ID** or **Work group name** to view the work group information.
![]()

### Editing work group information
You can modify the description and users of a work group in the following steps:
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Click **Work group** to enter the work group management page.
3. Find the target **Work group name** and click **Edit** in the **Operation** column.
![]()
	- To edit the description, click ![](https://qcloudimg.tencent-cloud.cn/raw/a4e51dabc44f1c10173478745f6648c1.png).
	- You can click **Bind user** to add Data Lake Compute users to the work group.
	- Select multiple target users and click **Batch remove**, or click **Remove** in the **Operation** column of a specific target user. Removed users will no longer have the permissions of the work group, which does not affect other permissions granted to them though.

### Deleting a work group
A Data Lake Compute admin can remove work groups.
>! After a work group is removed, all its permissions granted to users in it will be revoked. Note that a removed work group cannot be recovered. Proceed with caution.

1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc), select the service region, and go to the **Permission management** page.
2. Click **Work group** to enter the work group management page.
3. Select multiple target work groups and click **Batch remove**, or click **Remove** in the **Operation** column of a specific target work group.
![]()


