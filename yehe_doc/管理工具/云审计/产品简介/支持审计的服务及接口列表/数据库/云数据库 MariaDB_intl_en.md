TencentDB for MariaDB is a highly secure enterprise-grade cloud database dedicated to the online transaction processing (OLTP) scenario. It has been used in Tencent's billing business for over a decade. It is compatible with MySQL syntax and has various advanced features such as thread pool, audit, and remote disaster recovery while delivering easy scalability, simplicity, and high cost performance of TencentDB.

TencentDB for MariaDB operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-----------------|---------|--------------------------------|
| Desolating postpaid instance        | mariadb | ActivateHourDBInstance         |
| Recovering dedicated instance          | mariadb | ActiveDedicatedDBInstance      |
| Checking IP status          | mariadb | CheckIpStatus                  |
| Cloning account            | mariadb | CloneAccount                   |
| Disabling public network address          | mariadb | CloseDBExtranetAccess          |
| Creating account            | mariadb | CreateAccount                  |
| Creating parameter template          | mariadb | CreateConfigTemplate           |
| Creating instance            | mariadb | CreateDBInstance               |
| Creating postpaid instance          | mariadb | CreateHourDBInstance           |
| Rolling back instance            | mariadb | CreateTmpInstances             |
| Deleting account            | mariadb | DeleteAccount                  |
| Deleting parameter template          | mariadb | DeleteConfigTemplate           |
| Deleting temp instance          | mariadb | DeleteTmpInstance              |
| Getting permission list          | mariadb | DescribeAccountPrivileges      |
| Viewing account list          | mariadb | DescribeAccounts               |
| Querying audit log          | mariadb | DescribeAuditLogs              |
| Querying audit rule details        | mariadb | DescribeAuditRuleDetail        |
| Querying the list of audit rules        | mariadb | DescribeAuditRules             |
| Querying audit policy          | mariadb | DescribeAuditStrategies        |
| Getting custom backup time       | mariadb | DescribeBackupTime             |
| Querying price for batch MariaDB instance renewal | mariadb | DescribeBatchRenewalPrice      |
| Querying binlog time      | mariadb | DescribeBinlogTime             |
| Querying parameter configuration history        | mariadb | DescribeConfigHistories        |
| Querying parameter template          | mariadb | DescribeConfigTemplate         |
| Querying the list of parameter templates        | mariadb | DescribeConfigTemplates        |
| Querying instance object          | mariadb | DescribeDatabaseObjects        |
| Querying instance database name         | mariadb | DescribeDatabases              |
| Querying the column information of instance table       | mariadb | DescribeDatabaseTable          |
| Querying monitoring information details        | mariadb | DescribeDBDetailMetrics        |
| Querying the key information of instance        | mariadb | DescribeDBEncryptAttributes    |
| Querying instance details          | mariadb | DescribeDBInstanceDetail       |
| Querying the high-availability information of instance       | mariadb | DescribeDBInstanceHAInfo       |
| Viewing instance list          | mariadb | DescribeDBInstances            |
| Querying instance specification          | mariadb | DescribeDBInstanceSpecs        |
| Getting instance list          | mariadb | DescribeDBLogFiles             |
| Querying monitoring information          | mariadb | DescribeDBMetrics              |
| Viewing database parameter         | mariadb | DescribeDBParameters           |
| Viewing instance performance data        | mariadb | DescribeDBPerformance          |
| Viewing instance performance data details      | mariadb | DescribeDBPerformanceDetails   |
| Viewing instance resource usage      | mariadb | DescribeDBResourceUsage        |
| Viewing instance resource usage details      | mariadb | DescribeDBResourceUsageDetails |
| Querying the security group information of instance       | mariadb | DescribeDBSecurityGroups       |
| Getting slow query log details       | mariadb | DescribeDBSlowLogAnalysis      |
| Querying the list of slow query logs       | mariadb | DescribeDBSlowLogs             |
| Querying instance sync mode        | mariadb | DescribeDBSyncMode             |
| Querying temp instance          | mariadb | DescribeDBTmpInstances         |
| Querying dedicated cluster specification        | mariadb | DescribeFenceDBInstanceSpecs   |
| Querying process status          | mariadb | DescribeFlow                   |
| Querying the proxy configuration of instance     | mariadb | DescribeInstanceProxyConfig    |
| Querying the SSL status of instance       | mariadb | DescribeInstanceSSLAttributes  |
| Querying latest DBA check result     | mariadb | DescribeLatestCloudDBAReport   |
| Viewing backup log settings        | mariadb | DescribeLogFileRetentionPeriod |
| Querying order information          | mariadb | DescribeOrders                 |
| Querying price            | mariadb | DescribePrice                  |
| Querying project            | mariadb | DescribeProjects               |
| Querying the security group information of project       | mariadb | DescribeProjectSecurityGroups  |
| Querying instance renewal price        | mariadb | DescribeRenewalPrice           |
| Querying purchasable AZs         | mariadb | DescribeSaleInfo               |
| Querying the list of sync tasks        | mariadb | DescribeSyncTasks              |
| Querying instance upgrade price        | mariadb | DescribeUpgradePrice           |
| Querying the information of user task        | mariadb | DescribeUserTasks              |
| Setting permission            | mariadb | GrantAccountPrivileges         |
| Initializing instance           | mariadb | InitDBInstances                |
| Isolating dedicated instance          | mariadb | IsolateDedicatedDBInstance     |
| Isolating postpaid instance         | mariadb | IsolateHourDBInstance          |
| Modifying account remarks          | mariadb | ModifyAccountDescription       |
| Setting auto-renewal in batches        | mariadb | ModifyAutoRenewFlag            |
| Setting custom backup time       | mariadb | ModifyBackupTime               |
| Modifying parameter template        | mariadb | ModifyConfigTemplate           |
| Modifying instance encryption information        | mariadb | ModifyDBEncryptAttributes      |
| Modifying instance name          | mariadb | ModifyDBInstanceName           |
| Modifying the security group of TencentDB instance       | mariadb | ModifyDBInstanceSecurityGroups |
| Modifying instance project        | mariadb | ModifyDBInstancesProject       |
| Modifying database parameter         | mariadb | ModifyDBParameters             |
| Modifying instance sync mode        | mariadb | ModifyDBSyncMode               |
| Modifying instance network          | mariadb | ModifyInstanceNetwork          |
| Modifying SSL information         | mariadb | ModifyInstanceSSLAttributes    |
| Modifying instance VIP         | mariadb | ModifyInstanceVip              |
| Modifying instance Vport       | mariadb | ModifyInstanceVport            |
| Modifying backup log settings        | mariadb | ModifyLogFileRetentionPeriod   |
| Opening public network address          | mariadb | OpenDBExtranetAccess           |
| Renewing instance            | mariadb | RenewDBInstance                |
| Resetting account password          | mariadb | ResetAccountPassword           |
| Enabling smart DBA         | mariadb | StartSmartDBA                  |
| Switching instance high-availability          | mariadb | SwitchDBInstanceHA             |
| Replacing original instance with temp instance       | mariadb | SwitchRollbackInstance         |
| Terminating dedicated instance          | mariadb | TerminateDedicatedDBInstance   |
| Expanding instance capacity            | mariadb | UpgradeDBInstance              |
| Upgrading dedicated instance          | mariadb | UpgradeDedicatedDBInstance     |
| Upgrading postpaid instance         | mariadb | UpgradeHourDBInstance          |
