## Operation Scenario
You can manage the permission of existing database accounts in the TencentDB for MySQL Console. Specifically, you can grant database accounts global or object-level permission and cancel such permission.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance for which to modify the permission and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select **Database Management** > **Account Management**, find the account for which to modify the permission, and click **More** > **Modify Permissions**.
![](https://main.qcloudimg.com/raw/144f93c6415892d0fe828f3cf267c94e.png)
4. In the pop-up dialog box, select or deselect the permission and click **OK** to complete the modification.
 - **Global permission**: Grants full permission to all databases in the instance.
 - **Object-level permission**: Grants permission to certain databases in the instance.
![](https://main.qcloudimg.com/raw/19e5e35796516b6a3cd5a346ce4dcd74.png)


## Related APIs

| API Name                                                      | Description     |
| ------------------------------------------------------------ | ------------ |
| [ModifyAccountPrivileges](http://intl.cloud.tencent.com/document/product/236/17496) | Modifies the permission of a TencentDB instance account |

