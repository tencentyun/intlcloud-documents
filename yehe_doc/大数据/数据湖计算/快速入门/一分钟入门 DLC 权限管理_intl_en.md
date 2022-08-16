## User and work group
Data Lake Compute manages user permissions through user authorization and work group authorization.
- Work group: You can bind users to a work group to grant them the data and engine permissions of the work group. Users in the same work group have the same permissions.
- User: You can select users in CAM, including sub-accounts and collaborator accounts.
>? If users are granted different permissions from those in their work groups, all the granted permissions will take effect.

## Directions
1. Select **Permission management** on the left sidebar in the Data Lake Compute console.
2. Create a work group.
Click **Work group > Add work group**. You can bind users to the created work group or create an empty work group. For detailed directions, see [User and User Group](https://intl.cloud.tencent.com/document/product/1155/48667)
![]()
![]()
3. Authorize the work group.
After creating the work group, click **Authorize** in the **Operation** column to add permissions, including **Data permission** and **Engine permission**.
![]()
	1. Data permission
		- Data catalog permission: It includes the permissions to create databases in a data catalog and create data catalogs.
		- Database and table permission: It includes fine-grained permissions at database and table levels to view and edit databases, tables, views, and functions.
![]()
	2. Engine permission
Select a data engine and grant the permissions to use, modify, or delete it.
![]()

4. Create a user.
Add a user and bind the user to a work group: Click **User > Add user**. Set **User type** to **General user** and bind the user to a work group, so that the user can get all the permissions of the work group. If you set **User type** to **Admin**, you don't need to bind the user to a work group.
![]()
![]()
5. Authorize a user.
Authorize a user in the user list. **Data permission** and **Engine permission** can be granted, just like with a work group.
![]()
For detailed directions, see [Sub-Account Permission Management](https://intl.cloud.tencent.com/document/product/1155/48667).
