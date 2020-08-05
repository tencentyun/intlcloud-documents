This document describes how to initialize an instance in the TDSQL Console.

## Directions
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), select an uninitialized instance in the instance list, and click **Initialize** in the "Operation" column.
![](https://main.qcloudimg.com/raw/56ca04a4b112c334b4e755a6a5aabd72.png)
2. In the initialization dialog box that pops up, select the configuration as needed, and click **OK** to initialize the instance.
 - Supported character sets: select the character set supported by MySQL.
 - Case-sensitive table name: set whether the table name of database is case-sensitive.
 - Enable strong sync: enable strong sync to ensure data consistency in the secondary instance in case the primary fails. At least 2 nodes are required for this option to work.
![](https://main.qcloudimg.com/raw/7ec7d0fd038f2bb14760d11199afe1f0.png)
3. Return to the instance list and view the initialized instance. When the status becomes "Running", the instance can be connected.

