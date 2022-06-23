
## Overview
After a migration task is started, if it is interrupted due to an exception, you can retry it.

>?Currently, you can retry a data migration task only if the migration is between MySQL, TDSQL-C for MySQL, MariaDB, Percona, and TDSQL for MySQL.

To retry a task, DTS identifies the data point where the task was interrupted based on the binlog offset, starts to pull the binlog from the position of the first GTID not executed in the source database, and continues to consume the data.

The support for task retry in different data migration scenarios is as detailed below:
- Source database export: The task can be retried only if the task is interrupted due to a database lock failure caused by time-consuming SQL statements in the source instance before it is locked.
- Data import: Retry is not supported.
- Incremental sync: Retry is supported.

## Directions
Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, select the target migration task, and click **Retry** in the **Operation** column.

