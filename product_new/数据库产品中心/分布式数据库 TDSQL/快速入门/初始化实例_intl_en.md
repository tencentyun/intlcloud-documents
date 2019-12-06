## Operation Scenario
This document describes how to initialize an instance in the TDSQL Console.

## Directions
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), select an uninitialized instance in the instance list, and click **Initialize** in the "Operation" column.
<!-- ![](https://main.qcloudimg.com/raw/9243906ccf164fec9bc21048f3c69e19.png) -->
2. In the initialization dialog box that pops up, select the configuration as needed, and click **OK** to initialize the instance.
 - Supported Character Set: Select the character set supported by the MySQL database.
 - Table Name Case Sensitivity: Set whether the table name of database is case-sensitive.
 - Enable Strong Sync: Enable strong sync to ensure data consistency in the slave in case the master fails. At least 2 nodes are required for this option to work.
<!-- ![](https://main.qcloudimg.com/raw/0b3f4f13fc2f390a443977b66b559670.png) -->
3. When the instance status changes to **Running**, the initialization is completed, and you can connect to the database for operations.

