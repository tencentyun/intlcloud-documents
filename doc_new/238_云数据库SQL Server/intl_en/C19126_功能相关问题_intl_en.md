### What is SQL Server?
SQL Server is a relational database from Microsoft. It has high scalability and performance as well as the ability to query, search, synchronize, report, and analyze data. There are multiple editions of SQL Server, and each edition has its unique features.
Database supports SQL Server 2008 R2 SP3, 2012 SP3, and 2016 SP1, which enables custom applications developed by Microsoft .NET and Visual Studio. With many new features and key improvements in the use of data in service-oriented architecture (SOA) and business processes based on Microsoft BizTalk Server, 2016 SP1 has become the most powerful and inclusive SQL Server version. You can easily set up, operate, and scale up SQL Server deployment on the cloud to cope with fast business changes.

### What is the architecture of TencentDB for SQL Server like?
TencentDB for SQL Server consists of a master database and a mirror database that are deployed in different racks. Each database corresponds to a group of monitoring agents which monitor the database in real time based on the heartbeat. The cluster management scheduling center consists of two sets of independently deployed decision-making clusters and configuration clusters and is mainly used to manage the normal operations of the database node group, access gateway cluster and HDFS. The Hadoop distributed file system (HDFS) makes available data disaster recovery service with cold backup. The gateway cluster is accessed to provide a unique IP, and if the data node is switched, the IP won't change.

### How do I create a TencentDB for SQL Server instance and connect to a database?
You can manage the database in the TencentDB for SQL Server Console.
For detailed directions, see [Creating an Instance and Connecting to a Database](https://cloud.tencent.com/document/product/238/7516).

### How do I manage the account of a TencentDB for SQL Server instance?
TencentDB for SQL Server do not allow the creation/deletion of databases and creating/deleting/modifying accounts via Microsoft SQL Server Management. You can go to **[TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) > Instance Details page > Account Management** to create, delete, an account or modify account permission.
Currently, the console only allows you to use the "read-write" and "read-only" permissions. If you need permissions at a higher level, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application (no sa account is provided).

### How do I monitor a TencentDB for SQL Server instance?
TencentDB for SQL Server supports 25 common parameters of SQL Server. You can collect statistics of other parameters by configuring the counters of SSMS. For more information, see [Monitoring and Alarming](https://cloud.tencent.com/document/product/238/7524).
Currently, alarming is supported for the following metrics through Cloud Monitor. You can configure alarms in **[Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview)** > **Alarm Configuration** > **Alarm Policy**.
- CPU utilization
- Connection count
- TrafficIn
- TrafficOut
- IOPS
- Storage capacity

### How do I roll back a TencentDB for SQL Server instance?
The full and log backups in TencentDB for SQL Server are retained for seven days; therefore, you can roll back to any time point within the past seven days.
For detailed directions, see [Database Instance Rollback](https://cloud.tencent.com/document/product/238/7522).

### How do I back up a TencentDB for SQL Server instance?
In the TencentDB for SQL Server Console, you can restore the database to another instance (such as a self-built instance) using a downloaded backup file.
For detailed directions, see [Database Instance Backup](https://cloud.tencent.com/document/product/238/7523).


### How do I migrate data to TencentDB for SQL Server?
TencentDB for SQL Server supports migrating data from [an SQL Server instance created by CVM](https://cloud.tencent.com/document/product/238/32585) or [COS](https://cloud.tencent.com/document/product/238/19103).

### How do I upgrade a TencentDB for SQL Server instance?
Upgrade means upgrading an existing TencentDB for SQL Server instance to a higher specification.
1. Select an instance in the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver) and click **Upgrade** in the **Operation** column.
2. On the upgrade page that pops up, select the desired specification based on your needs and make the payment. Once payment is completed, the system will automatically upgrade the instance specification.
Upgrade fee = (price of target specification - price of original specification) x remaining validity period

>?
>- You can only upgrade an instance to a higher specification. Downgrade is not supported.
>- You cannot cancel the upgrade process once it has started.


### How do I use the Windows Client Upload Tool in SQL Server?
1. After downloading the Windows Client Upload Tool to the local file system, decompress it to any folder (note: no Chinese characters are allowed in the path) to get the "bin" and "etc" directories.
2. In order to protect the security of your data, before the backup is uploaded, you need to edit the configuration file etc\conf.json and enter your own API key (secretId and secretKey). Please be sure to keep your API key private and avoid disclosure. To ensure the stability of the transfer process, this tool now supports transfer resuming.
**Please save the conf.json file in "UTF-8 without BOM" (it is recommended to convert the code with Notepad++ on Windows).**
![](https://main.qcloudimg.com/raw/b79bd31b582f82c00ce36d81856bc2b5.png)
3. In Windows Command Prompt, go to the decompressed "Windows Client Upload Tool" directory and call upload-tool.exe in the bin directory to complete the upload operation. upload-tool.exe has two parameters: -r and -p. -p indicates the absolute local path of the backup file; -r indicates the region where the transit storage is located (please select the region where your TencentDB instance is located).
![](https://main.qcloudimg.com/raw/012b37a5b851138c1dbd464344c05db2.png)

**Region mappings (the identifier is case-sensitive)**

| Region | -r Parameter | 
|:---------:|:---------:|
| Guangzhou | gz | 
| Shanghai | sh | 
| Hong Kong | hk | 
| Shanghai Finance | shjr | 
| Beijing | bj | 
| Shenzhen Finance | szjr | 



