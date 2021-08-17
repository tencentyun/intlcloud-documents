Resource-level permission can be used to specify which resources a user can manipulate. Redis supports certain resource-level permission. This means that for Redis operations that support resource-level permission, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| ---------------------------- | ------------------------------------------------------------ |
| [Redis instance](#xiangguan) | `qcs::redis:$region::instance/*`<br>`qcs::redis:$region:$account:instance/$instance` |

The table below lists the Redis API operations which currently support resource-level permission control as well as the resources supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

>?Any TencentDB API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

<span id="xiangguan"></span>
### Instance

| API Operation | Resource Path |
| ---------------------------------------- | ------------------------------------------------------------ |
| AssignProject                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| AssociateSecurityGroups                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| AutoRenew                                | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| BackupInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CleanInstance                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CleanUpInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ClearInstance                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ClearRedis                               | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstanceAccount                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstanceHour                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstances                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateRedis                              | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DeleteInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DeleteInstanceAccount                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeAutoBackupConfig                 | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeBackupUrl                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeDBSecurityGroupsDetail           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceAccount                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceBackups                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceDealDetail               | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceParamRecords             | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceParams                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceSecurityGroup            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceSecurityGroupsAssociated | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceShards                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceSlowlog                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstances                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeProjectSecurityGroup             | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedis                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisDealDetail                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisProduct                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisProductList                 | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisRegions                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisZones                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeSlowLog                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeTaskInfo                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeTaskList                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeTasks                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeVPCRedis                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DestroyPostpaidInstance                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DestroyPrepaidInstance                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DisableReplicaReadonly                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| EnableReplicaReadonly                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ExportRedisBackup                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetBackupDownloadUrl                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisBackupList                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisPerformance                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisSlowLogList                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisTaskList                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| InitRedisPassword                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| InquiryRedisPrice                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ManualBackupInstance                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModfiyInstancePassword                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModfiyRedisPassword                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyAutoBackupConfig                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyDBInstanceSecurityGroups           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstanceAccount                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstanceParams                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstanceSecurityGroup              | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyNetworkConfig                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyRedisName                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyRedisParams                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyRedisProject                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| RenewInstance                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| RenewRedis                               | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ResetPassword                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ResetRedisPassword                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| RestoreInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| SetRedisAutoRenew                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| StartupInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| SwitchInstanceVip                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UnAssociateSecurityGroups                | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UpgradeInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UpgradeRedis                             | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UpgradeRedisInquiryPrice                 | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
