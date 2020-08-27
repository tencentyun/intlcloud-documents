TencentDB for Redis is a database service provided by Tencent Cloud based on the Redis protocol, which leverages Tencent Cloud's many years of experience in distributed caching and features high availability, reliability, and flexibility. Compatible with Redis 2.8, 4.0, and 5.0 protocols and available in both Standard and Cluster architecture editions, it supports up to 4 TB of storage capacity and tens of millions of concurrent requests, meeting the needs in different scenarios such as caching, storage, and computing.

TencentDB for Redis operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------------|-------|-------------------------------|
| Deactivating instance in recycle bin                 | redis | CleanUpInstance               |
| CreateInstanceAccount   | redis | CreateInstanceAccount         |
| DeleteInstanceAccount   | redis | DeleteInstanceAccount         |
| Querying the download URL of instance backup             | redis | DescribeBackupUrl             |
| DescribeInstanceAccount | redis | DescribeInstanceAccount       |
| Querying instance order information                | redis | DescribeInstanceDealDetail    |
| Querying instance parameter modification records              | redis | DescribeInstanceParamRecords  |
| Querying instance parameter                  | redis | DescribeInstanceParams        |
| DescribeInstances       | redis | DescribeInstances             |
| Querying the security group information of instance               | redis | DescribeInstanceSecurityGroup |
| Querying instance shard information                | redis | DescribeInstanceShards        |
| Querying the security group information of project               | redis | DescribeProjectSecurityGroup  |
| Querying task information                  | redis | DescribeTaskInfo              |
| Querying task list information                | redis | DescribeTaskList              |
| Terminating postpaid instance                 | redis | DestroyPostpaidInstance       |
| Terminating prepaid instance               | redis | DestroyPrepaidInstance        |
| Disabling read-only access to instance replica                | redis | DisableReplicaReadonly        |
| Enabling read-only access to instance replica                | redis | EnableReplicaReadonly         |
| Modifying Redis password               | redis | ModfiyInstancePassword        |
| Setting auto backup time                | redis | ModifyAutoBackupConfig        |
| ModifyInstanceAccount   | redis | ModifyInstanceAccount         |
| Modifying instance parameter                  | redis | ModifyInstanceParams          |
| Modifying instance network                  | redis | ModifyNetworkConfig           |
| Restoring instance from recycle bin                 | redis | StartupInstance               |
