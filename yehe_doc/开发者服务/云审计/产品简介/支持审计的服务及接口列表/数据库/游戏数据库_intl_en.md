Based on the design principles and technologies of NoSQL databases, Tencent Cloud TcaplusDB is specially developed for gaming data storage by taking into account gaming characteristics and the balance between performance and costs. Currently, it provides stable data storage services for popular games with tens of millions of DAUs, such as Honor of Kings, CrossFire, and Naruto Mobile. Backed by Tencent Cloud's infrastructure nodes deployed in Asia, Europe, North America, South America, and Oceania, it can be used globally once integrated.

TcaplusDB operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------------|-----------|-------------------------|
| Clearing table data                   | tcaplusdb | ClearTables             |
| Creating backup                    | tcaplusdb | CreateBackup            |
| Creating cluster                    | tcaplusdb | CreateCluster           |
| Creating table group                   | tcaplusdb | CreateTableGroup        |
| Creating tables in batches                   | tcaplusdb | CreateTables            |
| Deleting cluster                    | tcaplusdb | DeleteCluster           |
| Deleting IDL description file               | tcaplusdb | DeleteIdlFiles          |
| Deleting table group                   | tcaplusdb | DeleteTableGroup        |
| Deleting the global distributed indexes of TcaplusDB table    | tcaplusdb | DeleteTableIndex        |
| Deleting table                     | tcaplusdb | DeleteTables            |
| Querying cluster information list                | tcaplusdb | DescribeClusters        |
| Getting the list of tags associated with cluster             | tcaplusdb | DescribeClusterTags     |
| Querying table description file details               | tcaplusdb | DescribeIdlFileInfos    |
| Querying region list                  | tcaplusdb | DescribeRegions         |
| Querying table group list                 | tcaplusdb | DescribeTableGroups     |
| Getting the list of tags associated with table group            | tcaplusdb | DescribeTableGroupTags  |
| Querying table details                   | tcaplusdb | DescribeTables          |
| Querying the details of table in recycle bin              | tcaplusdb | DescribeTablesInRecycle |
| Querying table tag list                | tcaplusdb | DescribeTableTags       |
| Querying task list                  | tcaplusdb | DescribeTasks           |
| Querying whether the current user is in the allowlist            | tcaplusdb | DescribeUinInWhitelist  |
| Modifying cluster name                  | tcaplusdb | ModifyClusterName       |
| Modifying cluster password                  | tcaplusdb | ModifyClusterPassword   |
| Modifying cluster tags                  | tcaplusdb | ModifyClusterTags       |
| Modifying table group name                 | tcaplusdb | ModifyTableGroupName    |
| Modifying table group tags                 | tcaplusdb | ModifyTableGroupTags    |
| Modifying table remarks                 | tcaplusdb | ModifyTableMemos        |
| Modifying table structures in batches                 | tcaplusdb | ModifyTables            |
| Modifying table tags                  | tcaplusdb | ModifyTableTags         |
| Recovering table from recycle bin                | tcaplusdb | RecoverRecycleTables    |
| Creating and modifying the global distributed indexes of TcaplusDB table | tcaplusdb | SetTableIndex           |
