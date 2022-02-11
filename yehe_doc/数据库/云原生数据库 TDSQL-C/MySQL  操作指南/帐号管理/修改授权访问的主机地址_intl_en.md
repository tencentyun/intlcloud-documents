
You can modify the host addresses authorized by a database account in the console to control the access to the database, thus enhancing database access security.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster management page.
2. On the cluster management page, select the **Account Management** tab and select **More** > **Modify Host** in the **Operation** column.
>?You cannot modify the host address of the `root` account.
>
![](https://qcloudimg.tencent-cloud.cn/raw/b156c4d127ed6f523f1dac0a77da6866.png)
3. In the pop-up window, enter the new host address and click **OK**.
>?The host address can be an IP or `%` (indicating not to limit the IP range).
>- Example 1: enter `%` to indicate not to limit the IP range, that is, clients at all IP addresses are allowed to use this account to access the database.
>- Example 2: enter `10.5.10.%`, which means that clients whose IP range is within `10.5.10.%` are allowed to use this account to access the database.

