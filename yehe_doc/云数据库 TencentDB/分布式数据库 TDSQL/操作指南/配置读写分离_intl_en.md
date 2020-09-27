
## Read/Write Separation Based on Read-only Account
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select the **Manage Account** tab and click **Create**.
3. In the pop-up dialog box, set the account information, set **Create as read-only account** to **Yes**, and click **Confirm and Go Next**.
4. In the pop-up dialog box, you can set **Read-only request allocation policy** to define the read policy when a slave failure (or long delay) occurs.
 - Select **Master Server** to read from the master when the delay of slave exceeds the limit.
 - Select **Report Errors** to report an error when the delay of the slave exceeds the limit.
 - Select **Read Only from Slave Server** to ignore the delay parameter and always read from the slave (this is generally used to pull binlogs for sync).
 - Set the **Read-only slave server delay parameter** to define the data sync delay time, which is to be used together with **Master Server** and **Report Errors** under the **Read-only request allocation policy**.
![](https://main.qcloudimg.com/raw/d6329e5b6626e419c2fbd07f5b50c3c9.png)

## Read/Write Separation Based on Comment
Add the **```/*slave*/```** field before each SQL statement to be "read" by the slave, and add the `-c` parameter after "mysql" to parse the comment, such as ```mysql -c -e "/*slave*/sql"```, to automatically assign "read" requests to the slave. Below are examples:
```
//Read from master//
select * from emp order by sal，deptno desc；
//Read from slave//
/*slave*/ select * from emp order by sal，deptno desc；
```
>!
>- This feature only supports read from slave (SELECT) rather than other operations. Non-SELECT statements will fail.
>- The `-c` parameter needs to be added after `mysql` to parse the comment.
>- ```/*slave*/``` must be in lowercase, and no spaces are needed before and after the statement.
>- If the MAR (strong sync) mechanism is affected by a slave exception, read from slave will be automatically switched to read from master.
