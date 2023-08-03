## Overview
You can manage the permissions of existing database accounts in the TencentDB for MySQL console. Specifically, you can grant or remove database accounts global as well as object-level permissions.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID or **Manage** in the **Operation** column to access the instance management page.
2. Select the **Database Management** > **Account Management** tab, find the account for which to modify the permissions, and click **Modify Permissions**.
![](https://qcloudimg.tencent-cloud.cn/raw/c791cf541807d81ef00270f648c6021e.png)
3. In the pop-up dialog box, select or deselect permissions and click **OK** to complete the modification.
 - **Global Privileges**: Grant global permissions to all databases in the instance.
 - **Object-Level Privileges**: Grant permissions to certain databases in the instance.
![](https://main.qcloudimg.com/raw/19e5e35796516b6a3cd5a346ce4dcd74.png)

## Related APIs
| API Name                                                      | Description     |
| ------------------------------------------------------------ | ------------ |
| [ModifyAccountPrivileges](https://intl.cloud.tencent.com/document/product/236/17496) | Modifies the permissions of a TencentDB instance account |

