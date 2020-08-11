This document describes how to initialize an instance in the TDSQL Console.

## Directions
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), locate the uninitialized instance in the instance list, and click **Initialize** in the "Operation" column.

2. In the instance initialization dialog box that pops up, select the configuration as needed, and click **OK** to initialize the instance.
 - Supported character sets: select the character set supported by MySQL.
 - Case-sensitive table name: set whether the table name of database is case-sensitive.
 - Enable strong sync: enable strong sync to ensure data consistency in the secondary instance in case the primary fails. At least 2 nodes are required for this option to work.

3. Return to the instance list to locate the instance. When the status changes **Running**, the instance can be connected.

