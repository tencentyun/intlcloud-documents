Data Lake Compute permissions include data permissions and data engine permissions. If you have the admin permission, you can log in to the Data Lake Compute console or use an API to grant a sub-user data and data engine permissions. Sub-users cannot use, modify, or delete data or data engines before they are authorized.

## User and work group
Data Lake Compute provides the user mode and work group mode for personnel permission management.
User: You can select users in CAM, including sub-accounts and collaborator accounts.
Work group: It is a group of users with the same permissions managed in the product.
>? If users are granted different permissions from those granted in their work groups, all the granted permissions will take effect.

A work group allows you to quickly grant permissions to a batch of users, so it is recommended for batch user authorization. For detailed directions, see [User and User Group](https://intl.cloud.tencent.com/document/product/1155/48666).
## User type
In Data Lake Compute, **User type** can be **Admin** or **General user**.
- Admin: An admin have all the data, engine, and task permissions and can add, authorize, and remove users and work groups in Data Lake Compute.
- General user: A general user is added by an admin, has no Data Lake Compute permissions by default, and needs to be authorized. Only data and engine permissions that can be **regranted** can be granted to general users.

| Permission and Operation | Admin | General User |
|---------|---------|---------|
| Data permissions  | All  | None by default (to be authorized by an admin) |
| Data engine permissions    | All  | None by default (to be authorized by an admin) |
| User management  | Yes |  No |
| Work group management | Yes   | No |
| Authorization scope  | All | Permissions that **can be regranted** |

>? The above permissions only include those defined in Data Lake Compute. To perform purchase, configuration adjustment, and refund operations that involve billing, log in to the CAM console and get the financial collaborator permission `QCloudFinanceFullAccess` (for detailed directions, see [Creating and Authorizing Sub-account](https://intl.cloud.tencent.com/document/product/598/40985)).

## Data permissions
Data Lake Compute data permissions allow operations on data catalogs, databases, and data tables. To facilitate your management and configuration, permissions can be granted in the standard or advanced mode.
- In standard mode, you can grant roles while ignoring the specific permission configuration (for more information on roles and permissions, see [Sub-Account Permission Management](https://intl.cloud.tencent.com/document/product/1155/48667)). The authorization granularity can be data catalog, database, or data table. This mode is suitable for quick authorization with no complex permission management involved.
- In advanced mode, you can grant permissions at the database, data table, view, or function level. It is suitable for refined permission management.

SQL statements for permission operations are as follows:

| Action | CREATE | ALTER | DROP     |  SELECT   |  INSERT |        DELETE   |  Target |
|---------|---------|---------|---------|---------|---------|---------|---------|
| CREATE DATABASE|  ✓| -| - | - | - | -|    Cataglog|
| ALTER DATABASE| -|    ✓| -| -| -| -|                  Database|
| DROP DATABASE|    -|  -   | ✓| -|     -| -|           Database|
| CREATE TABLE|     ✓| -| - | - | - | -|    Database|
| CREATE TABLE AS SELECT| ✓| -| - | ✓ | ✓ | -|      Database/Table|
| DROP TABLE| -|    -   | ✓| -|     -| -|   Table|
| ALTER TABLE LOCATION  |  -|   ✓| -| -| -| -|              Table|
| ALTER PARTITION LOCATION|      -|     ✓| -| -| -| -|                  Table|
| ALTER TABLE ADD PARTITION|     -|     ✓| -| -| -| -|                  Table|
| ALTER TABLE DROP PARTITION    | -|    ✓| -| -| -| -|                          Table|
| ALTER TABLE|   -|     ✓| -| -| -| -|                      Table|
| CREATE VIEW| ✓| -| - | - | - | -|                 Database|
| ALTER VIEW PROPERTIES |  -|   ✓| -| -| -| -|  View|
| ALTER VIEW RENAME |  -|   ✓| -| -| -| -|          View|
| DROP VIEW PROPERTIES|      -| ✓| ✓| -| -| -|          View|
| DROP VIEW|            -|  -   | ✓| -|     -| -|           View|
| SELECT TABLE|             -|  -   | -| ✓|     -| -|   Table|
| INSERT    |               -|  -   | -| -|     ✓| -|   Table|
| INSERT OVERWRITE  |           -|  -   | -| -|     ✓| ✓|   Table|
| CREATE FUNCTION|      ✓| -| - | - | - | -|            Database|
| DROP FUNCTION|    -| -| ✓ | - | - | -|    Function|
| SELECT VIEW       |       -| -| - | ✓ | - | -|    View|
| SELECT FUNCTION       |   -| -| - | ✓ | - | -|            Function|

## Data engine permissions
Data Lake Compute data engine permissions allow using, modifying, manipulating, monitoring, and deleting data engines as detailed below:
- Use: The permission to use engines to perform tasks.
- Modify: The permission to modify the basic information and configuration information of engines (modifying the configuration information requires the CAM financial collaborator permission).
- Manipulate: The permission to suspend and restart engines.
- Monitor: The permission to view the running tasks and monitoring information of engines.
- Delete: The permission to return engines.

## Permission granting
A single user can be granted multiple permissions. For detailed directions, see [Sub-Account Permission Management](https://intl.cloud.tencent.com/document/product/1155/48667).

