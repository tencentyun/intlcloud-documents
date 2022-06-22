## Issue
The migration/sync task takes too long or gets stuck. 

## Possible Causes
- The migrated data volume is high.
- The source database has a slow SQL statement.
- The source database content is non-compliant.
- The bandwidth is restricted or there are network jitters.
- No data is written to the source database during incremental migration or sync.
> ?If you select **Full + Incremental migration** as the migration type, after the full migration task is completed, the incremental migration task will continue, and you need to manually stop it by clicking **Done** in the **Operation** column; otherwise, the task will keep running, which is not the case of a stuck task.

## Solutions
#### High migrated data volume
The data volume is high, slowing down the migration/sync task.

#### Slow SQL statement in source database
Check whether the source database has a slow SQL statement; if so, process the statement; if not, check other causes.

#### Non-compliant source database content
The content in the source database is non-compliant. For example, if the source database has tables without a primary key, large queries involving such tables will slow down the task. We recommend you add a primary key to such tables or not migrate them.

#### Network problem
- If you use CCN for access, check the bandwidth configured in CCN. CCN only provides bandwidth below 10 Kbps between all regions free of charge, which is insufficient for DTS to transfer data. In this case, you need to configure a higher bandwidth.
- If you use a self-built database, check whether the network bandwidth is restricted.

#### No data written to source database during incremental migration or sync
In incremental migration or sync, if no data is written to the source database for a long time or there is an empty binlog, you can write data to the source database to resume the task.
