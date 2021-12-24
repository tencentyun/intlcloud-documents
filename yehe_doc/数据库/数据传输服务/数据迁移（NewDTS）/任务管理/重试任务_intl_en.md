
## Overview
After a migration task is started, if it is interrupted due to an exception, you can retry it.

>?Currently, you can retry a migration task only if the source database is MySQL or TDSQL-C.

To retry a task, DTS uses the binlog offset to find the data point where the task was stopped, then pulls the binlog from the position of the first GTID not executed in the source database, and continues to consume the data.

The support for task retry in different data migration scenarios is as detailed below:
- Source database export: if the task is interrupted due to a database lock failure caused by time-consuming SQL statements in the source database before it is locked, the task can be retried.
- Data import: retry is not supported.
- Incremental sync: retry is supported.

## Directions
Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, select the target migration task, and click **Retry** in the **Operation** column.
