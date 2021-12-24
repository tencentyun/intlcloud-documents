
## Overview
During the full + incremental data migration, once the full migration is completed, the task will automatically start the incremental migration, which will not stop on its own and must be ended manually. 

## Prerequisites
The data migration type is full + incremental migration. 

## Directions
Log in to the [DTS console](https://console.cloud.tencent.com/dts/migration), select **Data Migration** on the left sidebar, select the target migration task, and click **Complete** to stop it. You can complete a task only when it meets the following conditions:
 - The displayed migration step is **Incremental Sync**.
 - The source-target database data gap is 0 MB, and the source-target database time lag is 0s.

![](https://qcloudimg.tencent-cloud.cn/raw/19f54868ca6574ac523daa12889d7042.png)

