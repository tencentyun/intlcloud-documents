
### Why does my CPU utilization exceed 100%?
MariaDB is designed by default to overuse idle resources, so your business can preempt some idle CPU resources. Therefore, when your instance uses more CPU cores than the default value, it's normal for CPU utilization to appear higher than 100% in the monitoring view.

However, if your CPU load always exceeds 60%, we recommend that you expand your database as soon as possible.

### I have purchased 16 GB of memory. The monitoring page shows that the memory has been almost used up, but why is my business not affected?
The memory allocation mechanism of the database makes the most of idle memory to improve the cache hit rate rather than reading data from the disk. Therefore, it is normal that your memory is used up. Generally, you only need to check whether your business is affected.

### What is the maximum data volume of each table in TencentDB for MariaDB (without affecting the normal read/write efficiency)?
We recommend that you keep the data volume below 20 million entries; otherwise, TencentDB for MariaDB performance will be affected.

### Does the connection method of a TencentDB for MariaDB data source need to be changed?
TencentDB for MariaDB is compatible with MySQL protocols and connection programs under such protocols; therefore, no change is needed.

### What syntax does TencentDB for MariaDB audit support?
>!As the database audit feature is being refactored and upgraded, it is not available for newly purchased instances during this period.
>
Database audit currently supports most SQL statements. If you find any deficiency, [contact us](https://cloud.tencent.com/about/connect) for feedback.
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
2. Transaction and procedures will be divided into multiple statements.

### Why does strong sync in TencentDB for MariaDB have primary/replica delay?
The strong sync mechanism is to return a response immediately after data is written to (stored in) a replica log. In this case, data still needs to be written to the table through the log; therefore, delay will occur. For more information, see [System Architecture](https://intl.cloud.tencent.com/document/product/237/1057).
