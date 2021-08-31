
This document describes how to initialize an instance in the TencentDB for MariaDB Console.

## Directions
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/mariadb), select an instance in **Uninitialized** status in the instance list, and select **More** > **Initialize** in the "Operation" column.

2. In the pop-up dialog box, configure initialization parameters and click **OK** to start initialization.
 - Supported Character Set: select the character set supported by the MariaDB database.
 - Table Name Case Sensitivity: specify whether a table name is case-sensitive, which is "yes" by default.
 - Enable Strong Sync: enable strong sync to ensure data consistency in the slave in case the master fails.
![](https://main.qcloudimg.com/raw/7a23281da406e8d26510ed6a2a98133b.png)
3. Return to the instance list. After the status of the instance changes to **Running**, it is initialized successfully.
![](https://main.qcloudimg.com/raw/b090390ac6bd3eb879d548606947311c.png)


