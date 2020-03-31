## Operation Scenario
This document describes how to initialize an instance in the TencentDB for MariaDB Console.

## Directions
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql), select an instance in **Uninitialized** status in the instance list, and select **More** > **Initialize** in the "Operation" column.
![](https://main.qcloudimg.com/raw/f79e8eb644d318a5d0d84bdcd3551170.png)
3. In the pop-up dialog box, configure initialization parameters and click **OK** to start initialization.
 - Supported Character Set: select the character set supported by the MariaDB database.
 - Table Name Case Sensitivity: specify whether a table name is case-sensitive, which is "yes" by default.
 - Enable Strong Sync: enable strong sync to ensure data consistency in the slave in case the master fails.
![](https://main.qcloudimg.com/raw/14c32214404c1842fdf3b2d11b81c711.png)
4. Return to the instance list. After the status of the instance changes to **Running**, it is initialized successfully.
![](https://main.qcloudimg.com/raw/6abac4ea4ecdbdc47f652da8690d9e48.png)

