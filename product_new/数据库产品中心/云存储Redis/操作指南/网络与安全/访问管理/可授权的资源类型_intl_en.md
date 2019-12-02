Resource-level permission can be used to specify which resources a user can manipulate. Redis supports certain resource-level permission. This means that for Redis operations that support resource-level permission, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| ---------------------------- | ------------------------------------------------------------ |
| [Redis instance](#xiangguan) | `qcs::redis:$region::instance/*`<br>`qcs::redis:$region:$account:instanceId/$instanceId` |

The table below lists the Redis API operations which currently support resource-level permission control as well as the resources supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

>Any TencentDB API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

<span id="xiangguan"></span>
#### Redis Instance

| API Operation | Resource Path |
| ---------------------------------------- | ------------------------------------------------------------ |
| AssignProject                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| AssociateSecurityGroups                  | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| AutoRenew                                | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| BackupInstance                           | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CleanInstance                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CleanUpInstance                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ClearInstance                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ClearRedis                               | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CreateInstance                           | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CreateInstanceAccount                    | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CreateInstanceHour                       | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CreateInstances                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| CreateRedis                              | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DeleteInstance                           | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DeleteInstanceAccount                    | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeAutoBackupConfig                 | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeBackupUrl                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeDBSecurityGroupsDetail           | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceAccount                  | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceBackups                  | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceDealDetail               | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceParamRecords             | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceParams                   | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceSecurityGroup            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceSecurityGroupsAssociated | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceShards                   | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstanceSlowlog                  | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeInstances                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeProjectSecurityGroup             | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeRedis                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeRedisDealDetail                  | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeRedisProduct                     | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeRedisProductList                 | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeRedisRegions                     | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeRedisZones                       | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeSlowLog                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeTaskInfo                         | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeTaskList                         | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeTasks                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DescribeVPCRedis                         | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DestroyPostpaidInstance                  | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DestroyPrepaidInstance                   | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| DisableReplicaReadonly                   | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| EnableReplicaReadonly                    | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ExportRedisBackup                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| GetBackupDownloadUrl                     | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| GetRedisBackupList                       | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| GetRedisPerformance                      | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| GetRedisSlowLogList                      | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| GetRedisTaskList                         | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| InitRedisPassword                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| InquiryRedisPrice                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ManualBackupInstance                     | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModfiyInstancePassword                   | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModfiyRedisPassword                      | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyAutoBackupConfig                   | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyDBInstanceSecurityGroups           | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyInstance                           | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyInstanceAccount                    | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyInstanceParams                     | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyInstanceSecurityGroup              | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyNetworkConfig                      | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyRedisName                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyRedisParams                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ModifyRedisProject                       | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| RenewInstance                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| RenewRedis                               | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ResetPassword                            | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| ResetRedisPassword                       | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| RestoreInstance                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| SetRedisAutoRenew                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| StartupInstance                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| SwitchInstanceVip                        | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| UnAssociateSecurityGroups                | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| UpgradeInstance                          | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| UpgradeRedis                             | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
| UpgradeRedisInquiryPrice                 | `qcs::redis:$region:$account:instanceId/*`    `qcs::redis:$region:$account:instanceId/$instanceId` |
