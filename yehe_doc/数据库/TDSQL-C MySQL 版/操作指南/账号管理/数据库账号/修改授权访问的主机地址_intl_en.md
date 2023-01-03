
You can modify the host address authorized by a database account in the console. By doing so, you can control the access to the database and enhance database connection security.

## Directions
>?You can’t modify the host address of the `root` account.
>
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb), find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
2. On the cluster management page, select the **Account Management** tab and select **More** > **Modify Host** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RDND198_5.png)
3. In the pop-up window, enter a new host address and click **OK**.
>?The host address can be an IP or `%` (indicating no limit on the IP range).
>- Example 1: Enter `%` to indicate no limit on the IP range, that is, clients at all IP addresses are allowed to use this account to access the database.
>- Example 2: Enter `10.5.10.%` to indicate that clients with an IP range within `10.5.10.%` are allowed to use this account to access the database.

