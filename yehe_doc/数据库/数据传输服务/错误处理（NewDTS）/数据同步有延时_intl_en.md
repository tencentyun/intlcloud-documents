
## Issue
The content synced between the source and target databases has a delay. 

## Possible Causes
- The target database has a high load.
- The target database has a low specification.
- No data is written to the source database for a long time.
- The bandwidth is restricted or there are network jitters.

## Solutions
#### High load in target database
View the RPS of the source and target databases in the [monitoring data](https://intl.cloud.tencent.com/document/product/571/42606). If the RPS is low, the target database may have a high load.
If the target database has a high load, check whether the task is normal after the business traffic drops or upgrade the target database specification.

#### Low specification of target database
Upgrade the target database specification.

#### No data written to source database during incremental migration or sync
In incremental migration or sync, if no data is written to the source database for a long time or there is an empty binlog, you can write data to the source database to resume the task.

#### Network problem
- If you use CCN for access, check the bandwidth configured in CCN. CCN only provides bandwidth below 10 Kbps between all regions free of charge, which is insufficient for DTS to transfer data. In this case, you need to configure a [higher bandwidth](https://intl.cloud.tencent.com/document/product/1003/38894).
- If you use a self-built database, check whether the network bandwidth is restricted.

