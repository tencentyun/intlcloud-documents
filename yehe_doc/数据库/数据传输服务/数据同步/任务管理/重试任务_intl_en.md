
## Overview
After a sync task is started, if it is interrupted due to an exception, you can retry it.

>?Currently, you can retry a sync task only if the source database is MySQL or TDSQL-C.

To retry a task, DTS identifies the data point where the task was interrupted based on the binlog offset, starts to pull the binlog from the position of the first GTID not executed in the source database, and continues to consume the data.

The support for task retry in different data sync scenarios is as detailed below:
- Source database export: retry is not supported.
- Data import: retry is not supported.
- Incremental sync: retry is supported.

## Directions
Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Sync** on the left sidebar, select the target sync task, and click **More** > **Retry** in the **Operation** column.


