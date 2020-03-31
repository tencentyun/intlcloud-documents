### Why does my CPU utilization exceed 100%?
By default, TencentDB for MariaDB adopts the policy of overuse of idle resources that allows your business to preempt some idle CPU resources. Therefore, when the number of CPU cores of your instance exceeds the default value assigned, the CPU utilization may appear to exceed 100% in the monitoring view, which is actually normal.

However, if your CPU utilization always exceeds 60%, you are recommended to upgrade the database as soon as possible.

### I have purchased 16 GB of memory. The monitoring page shows that the memory has been almost used up, but why is my business not affected?
The memory allocation mechanism of the database makes the most of idle memory to improve the cache hit rate rather than reading data from the disk. Therefore, it is normal that your memory is used up. Generally, you only need to pay attention to whether your business is affected.

### What is the maximum data volume of each table in TencentDB for MariaDB (without affecting the normal read/write efficiency)?
You are recommended to keep the data volume below 20 million entries; otherwise, TencentDB for MariaDB performance will be affected.

### Does TencentDB for MariaDB allow me to use a set of self-built databases as slaves?
TencentDB for MariaDB provides two schemes for read/write separation: [read/write separation](https://intl.cloud.tencent.com/document/product/237/35409) and [self-built read-only instance](https://intl.cloud.tencent.com/document/product/237/8636).

### Does the connection method of a TencentDB for MariaDB data source need to be changed?
TencentDB for MariaDB is compatible with MySQL protocols and connection programs under such protocols; therefore, no change is needed.

### What syntax does TencentDB for MariaDB audit support?
Database audit currently supports most SQL statements. If you find any deficiency, please [contact us](https://console.cloud.tencent.com/workorder/category) for feedback.
1. Parsing of DCL, DDL, and DML statements is supported.
``` 
Insert,Replace,Select,Union,Update,Delete,CreateDatabase:,CreateEvent,CreateFunction,CreateIndex,CreateLog,
CreateTable,CreateServer,CreateProcedure,CreateTablespace,CreateTrigger,CreateView,CreateUDF,CreateUser,
ShowCharset,ShowCollation,ShowColumns,ShowCreate,ShowCreateDatabase,ShowDatabases,ShowEngines,ShowErrors,
ShowEvents,ShowFunction,ShowGrants,ShowLogEvents,ShowLogs,ShowProcedure,ShowOpenTables,ShowPlugins,
ShowProcessList,ShowMasterStatus,ShowPrivileges,ShowProfiles,ShowSlaveHosts,ShowSlaveStatus,ShowTableStatus,
ShowWarnings,ShowVariables,ShowStatus,ShowTriggers,Call,DropProcedure,DropDatabase,DropEvent,DropFunction,
DropIndex,DropLogfile,DropServer,DropTables,DropTablespace,DropTrigger,DropUser,DropView,AlterDatabase,
AlterEvent,AlterFunction,AlterLogfile,AlterProcedure,AlterServer,AlterTable,AlterTablespace,AlterUser,
AlterView,Rollback,Commit,Begin,Set,SetTrans,SetPassword,Release,Grant,RenameTable,RenameUser,Revoke,
Install,StopSlave,StartSlave,StartTrans,Use,DescribeTable,DescribeStmt,Flush,Load,LoadIndex,FlushTables,
Reset,CacheIndex,TruncateTable,Lock,Unlock,SavePoint,Help,Do,SubQuery,ShowTables,Execute,Deallocate,Binlog,
Kill,Partition,PrepareRepairXACheckCheckSumAnalyzeChangeOptimizePurgeHandlerSignalResignal
``` 
2. Transaction and stored procedures will be divided into multiple statements.


### Why does strong sync in TencentDB for MariaDB have master/slave delay?
The strong sync mechanism is to return a response immediately after data is written to (stored in) a slave log. In this case, data still needs to be written to the table through the log; therefore, delay will occur. For more information, please see [How Strong Sync Works](https://intl.cloud.tencent.com/document/product/237/1057).




