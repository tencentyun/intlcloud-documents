## User permission
User permissions include data permissions and engine permissions (for more information on permissions, see [Permission Overview](https://intl.cloud.tencent.com/document/product/1155/48665)). The former is required to access data in Data Lake Compute, while the latter is used for resource management. Data Lake Compute enables permission management at the database, table, and column levels, so that you can authorize a user or work group for refined data permission management in different use cases.

## User and work group
You can authorize a user or create and authorize a work group of users. For detailed directions, see [User and Work Group](https://intl.cloud.tencent.com/document/product/1155/48666).
- User: You can select users in CAM, including sub-accounts and collaborator accounts.
- Work group: It is a group of users with the same permissions managed in the product.
>? If users are granted different permissions from those granted in their work groups, all the granted permissions will take effect.

A work group allows you to quickly grant permissions to a batch of users, so it is recommended for batch user authorization.

## Granting a user a permission
Grant permissions to the specified user.
1. Set a user to **Admin** or **General user**. Admins have the permissions of all the data and engines by default with no need to be bound to a work group. They can also manage admin users other than the root account. **Set an admin with caution.**
![]()

2. Bind a work group: General users need to be granted permissions or bound to a work group before they can access resources.
![]()

3. Add a data permission: In the **User list**, click **Authorize** in the **Operation** column and select **Data permission** to grant permissions at the data catalog or database/table level.
![]()
	- Add a data catalog permission. You can grant permissions to create databases under DataLakeCatalog and create other data catalogs.
![]()
	- Add a database/table permission: You can grant permissions in **Standard** or **Advanced** mode. In standard mode, you can grant database/table permissions in the specified catalog and set **Query & analytics**, **Data edit**, and **Owner** permissions.
![]()
Specific permissions are as follows:
<table>
<thead>
<tr>
<th >Permission Type</th>
<th >Database</th>
<th >Data Table</th>
<th >View and Function</th>
</tr>
</thead>
<tbody>
<tr>
<td>Query & analytics</td>
<td>&bull; Query all the tables, views, and functions in databases.
<br>&bull; Create data tables.</td>
<td>Query</td>
<td>Query</td>
</tr>
<tr>
<td>Data edit</td>
<td>&bull;  Modify and delete databases and create tables.
<br>&bull;  Permissions of all the tables, views, and functions.</td>
<td>&bull;  Query, insert, update, and delete data.
<br>&bull;  Modify and delete tables.</td>
<td>Query, create, modify, and delete.</td>
</tr>
<tr>
<td>Owner (grants the permission to re-authorize permissions in addition to data edit permissions)</td>
<td>&bull;  Modify and delete databases and create tables.
<br>&bull;  Permissions of all the tables, views, and functions.</td>
<td>&bull;  Query, insert, update, and delete data.
<br>&bull;  Modify and delete tables.</li></td>
<td>Query, create, modify, and delete.</td>
</tr>
</tbody>
</table>
	- Advanced permission settings: When selecting a single database, you can further set the permissions to query, insert, update, and delete tables, views, and functions; when selecting multiple databases, you can only set permissions at the database level.
In advanced mode, you can set permissions at the column level. When selecting a single data table, you can add the permission to query columns. You can select one or more columns or all of them for authorization.
![]()
Click **Confirm** and perform queries in the **Data Explore** module. Enter the following SQL statement to preview the information of **col1** and run the statement to view the preview result of the column.
![]()
The permission is not granted for data column **b** in the data table. If you enter the SQL statement to view the information of **b**, the query cannot be performed due to lack of permission.
![]()

4. Add an engine permission: In the **User list**, click **Authorize** in the **Operation** column and select **Engine permission** to grant permissions to use, modify, manipulate, monitor, and delete specified resources.
![]()

## Modifying a user permission
1. In the **User list**, click **Authorize** and select **Data permission** or **Engine permission**.
![]()
The following takes data permission as an example. On the **Data permission authorization** page, click **Add permission** or **Remove** to modify a permission. The steps for engine permission modification are similar.
![]()
2. Modify **Work group** or **User type**. Click **Operation** > **Edit** to enter the **Edit user** page, where you can modify the **Username**, **User type**, and **Description**. You can also add/remove general users to/from a work group.
![]()
Click **Edit** to modify **User type**.
![]()

## Viewing a user's permissions
1. Click a user ID in the user list to enter the user details page.
![]()
2. View the user's work group, data permission, and engine permission information
![]()

## Revoking a user's permissions
Remove permissions to be revoked from the permission list of a user. This operation requires the admin permission.
![]()

## Adding and removing a work group permission
Only admins can add or remove work group permissions in a similar way to manipulate data permissions. Users in a work group have all the permissions of the group, so you can bind users to a work group to grant them the data and engine permissions of the work group. Admins don't need to be bound to a work group.
![]()
