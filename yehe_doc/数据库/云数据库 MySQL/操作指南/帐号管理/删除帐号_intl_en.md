## Operation Scenarios
In order to disable an existing database account, it must be deleted in the TencentDB for MySQL console.
>!
>- A database account cannot be recovered once deleted.
>- In order to avoid accidental deletion from interrupting normal use by your business, you need to make sure that the database account to be deleted is no longer used by any applications.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the "Operation" column to enter the instance management page.
2. Select the **Database Management** > **Manage Account** tab, find the account to be deleted, and select **More** > **Delete Account**.
![](https://qcloudimg.tencent-cloud.cn/raw/602d9e1d3471e28d89a6b95c2e0be272.png)
3. In the pop-up dialog box, click **OK** to delete the account.
![](https://main.qcloudimg.com/raw/c1680eda4e1abd7fb7b16d061475ada7.png)

## Related APIs
| API Name                                                      | Description     |
| -------------------------------------------------------- | -------- |
| [DeleteAccounts](https://intl.cloud.tencent.com/document/product/236/17501) | Deletes a TencentDB account |

