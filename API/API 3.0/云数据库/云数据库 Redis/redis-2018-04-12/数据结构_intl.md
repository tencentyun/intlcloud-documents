## InstanceClusterNode

Instance node type

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| Name | String | Node name |
| RunId | String | ID of the runtime node of the instance |
| Role | Integer | Cluster role. 0: master; 1: slave |
| Status | Integer | Node statues. 0: read-write; 1: read; 2: backup |
| Connected | Integer | Service status. 0: down; 1: on |
| CreateTime | String | Node creation time |
| DownTime | String | Node offline time |
| Slots | String | Distribution of the node slots |
| Keys | Integer | Distribution of the node keys |
| Qps | Integer | Node QPS |
| QpsSlope | Float | QPS skew of the node |
| Storage | Integer | Node storage |
| StorageSlope | Float | Storage skew of the node |

## InstanceClusterShard

Information list of instance shards

Referenced by: DescribeInstanceShards.

| Name | Type | Description |
|------|------|-------|
| ShardName | String | Shard node name |
| ShardId | String | Shard node ID |
| Role | Integer | Role |
| Keys | Integer | Number of keys |
| Slots | String | Slot information |
| Storage | Integer | Storage capacity |
| StorageSlope | Float | Capacity skew |
| Runid | String | ID of the runtime node of the instance |
| Connected | Integer | Service status. 0: down; 1: on |

## InstanceEnumParam

Descriptions of enumeration parameters of the instance

Referenced by: DescribeInstanceParams.

| Name | Type | Description |
|------|------|-------|
| ParamName | String | Parameter name |
| ValueType | String | Parameter type: enum |
| NeedRestart | String | Whether restart is required after a modification is made; value range: true, false |
| DefaultValue | String | Default value of the parameter |
| CurrentValue | String | Current value of the parameter |
| Tips | String | Parameter description |
| EnumValue | Array of String | Value range of the parameter |

## InstanceIntegerParam

Descriptions of integer parameters of the instance

Referenced by: DescribeInstanceParams.

| Name | Type | Description |
|------|------|-------|
| ParamName | String | Parameter name |
| ValueType | String | Parameter type: integer |
| NeedRestart | String | Whether restart is required after a modification is made; value range: true, false |
| DefaultValue | String | Default value of the parameter |
| CurrentValue | String | Current value of the parameter |
| Tips | String | Parameter description |
| Min | String | Minimum value of the parameter |
| Max | String | Maximum value of the parameter |

## InstanceNode

Instance node

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | ID |
| InstanceClusterNode | Array of [InstanceClusterNode](#InstanceClusterNode) | Node details |

## InstanceParam

Instance parameter

Referenced by: ModifyInstanceParams.

| Name | Type | Required | Description |
|------|------|----------|------|
| Key | String | Yes | Set the parameter name |
| Value | String | Yes | Set the parameter value |

## InstanceParamHistory

History of instance parameter modifications

Referenced by: DescribeInstanceParamRecords.

| Name | Type | Description |
|------|------|-------|
| ParamName | String | Parameter name |
| PreValue | String | Value before modification |
| PreValue | String | Value after modification |
| Status | Integer | Status. 1: parameter configuration is being modified; 2: parameter configuration modified successfully; 3: failed to modify parameter configuration |
| ModifyTime | String | Modified time |

## InstanceSecurityGroupDetail

Security group information of an instance

Referenced by: DescribeInstanceSecurityGroup.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| SecurityGroupDetails | Array of [SecurityGroupDetail](#SecurityGroupDetail) | Security group information |

## InstanceSet

List of instance details

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceName | String | Instance name |
| InstanceId | String | Instance ID |
| Appid | Integer | User's Appid |
| ProjectId | Integer | Project ID |
| RegionId | Integer | Region ID. 1: Guangzhou; 4: Shanghai; 5: Hong Kong; 6: Toronto; 7: Shanghai Financial; 8: Beijing; 9: Singapore; 11: Shenzhen Financial; 15: Western America (Silicon Valley); 16: Chengdu; 17: Germany; 18: Korea; 19: Chongqing; 21: India; 22: Eastern America (Virginia); 23: Thailand; 24: Russia; 25: Japan |
| ZoneId | Integer | Zone ID |
| VpcId | Integer | VPC ID, such as 75101 |
| SubnetId | Integer | VPC subnet ID, such as 46315 |
| Status | Integer | Current status of the instance. 0: to be initialized; 1: instance in process; 2: instance running; -2: instance isolated; -3: instance to be deleted |
| WanIp | String | VIP of the instance |
| Port | Integer | Port number of the instance |
| Createtime | String | Instance creation time |
| Size | Float | Instance capacity in MB |
| SizeUsed | Float | This field has been obsoleted |
| Type | Integer | Instance type. 1: Redis 2.8 cluster edition; 2: Redis 2.8 master-slave edition; 3: CKV master-slave edition (Redis 3.2); 4: CKV cluster edition (Redis3.2); 5: Redis 2.8 standalone edition; 7: Redis 4.0 cluster edition |
| AutoRenewFlag | Integer | Whether to set the auto-renewal flag for the instance. 1: auto-renewal set; 0: auto-renewal not set |
| DeadlineTime | String | Instance expiry time |
| Engine | String | Engine: Redis community edition, Tencent Cloud CKV |
| ProductType | String | Product type: Redis 2.8 cluster edition, Redis 2.8 master-slave edition, Redis 3.2 master-slave edition (CKV master-slave edition), Redis 3.2 cluster edition (CKV cluster edition), Redis 2.8 standalone edition, Redis 4.0 cluster edition |
| UniqVpcId | String | VPC ID, such as vpc-fk33jsf43kgv |
| UniqSubnetId | String | VPC subnet ID, such as subnet-fd3j6l35mm0 |
| BillingMode | Integer | Billing method. 0: pay-as-you-go; 1: prepaid |
| InstanceTitle | String | Description of the instance status, such as "instance running" |
| OfflineTime | String | Scheduled offline time |
| SubStatus | Integer | Substatus returned for the instance in process |
| Tags | Array of String | Anti-affinity tag |
| InstanceNode | Array of [InstanceNode](#InstanceNode) | Node information of the instance |
| RedisShardSize | Integer | Shard size |
| RedisShardNum | Integer | Number of shards |
| RedisReplicasNum | Integer | Number of replicas |
| PriceId | Integer | Billing ID |
| CloseTime | String | Isolation time |
| SlaveReadWeight | Integer | Weight read from the replica |
| InstanceTags | Array of [InstanceTagInfo](#InstanceTagInfo) | Tags associated with the instance <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| ProjectName | String | Project name <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## InstanceTagInfo

Instance tag information

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| TagKey | String | Tag key |
| TagValue | String | Tag value |

## InstanceTextParam

Descriptions of text parameters of the instance

Referenced by: DescribeInstanceParams.

| Name | Type | Description |
|------|------|-------|
| ParamName | String | Parameter name |
| ValueType | String | Parameter type: text |
| NeedRestart | String | Whether restart is required after a modification is made; value range: true, false |
| DefaultValue | String | Default value of the parameter |
| CurrentValue | String | Current value of the parameter |
| Tips | String | Parameter description |
| TextValue | Array of String | Value range of the parameter |

## ProductConf

Product information

Referenced by: DescribeProductInfo.

| Name | Type | Description |
|------|------|-------|
| Type | Integer | Product type. 2: Redis master-slave edition; 3: CKV master-slave edition; 4: CKV cluster edition; 5: Redis standalone edition; 7: Redis cluster edition |
| TypeName | String | Product name: Redis master-slave edition, CKV master-slave edition, CKV cluster edition, Redis standalone edition, Redis cluster edition |
| MinBuyNum | Integer | Minimum purchasable quantity |
| MaxBuyNum | Integer | Maximum purchasable quantity |
| Saleout | Boolean | Whether the product is sold out |
| Engine | String | Product engine: Tencent Cloud CKV or Redis community edition |
| Version | String | Compatible version: Redis 2.8, Redis 3.2, Redis 4.0 |
| TotalSize | Array of String | Total capacity in G |
| ShardSize | Array of String | Shard size in G |
| ReplicaNum | Array of String | Number of replicas |
| ShardNum | Array of String | Number of shards |
| PayMode | String | Supported billing method. 1: prepaid; 0: pay-as-you-go |
| EnableRepicaReadOnly | Boolean | Whether to support read-only replicas |

## RedisBackupSet

Array of instance backups

Referenced by: DescribeInstanceBackups.

| Name | Type | Description |
|------|------|-------|
| StartTime | String | Backup start time |
| BackupId | String | Backup ID |
| BackupType | String | Backup type. manualBackupInstance: manual backup initiated by the user; systemBackupInstance: midnight backup initiated by the system |
| Status | Integer | Backup status.  1: backup is locked by another process; 2: backup is normal and not locked by any process; -1: backup has expired; 3: backup is being exported; 4: backup successfully exported |
| Remark | String | Remarks of the backup |
| Locked | Integer | Whether the backup is locked. 0: no; 1: yes |

## RegionConf

Region information

Referenced by: DescribeProductInfo.

| Name | Type | Description |
|------|------|-------|
| RegionId | String | Region ID |
| RegionName | String | Region name |
| RegionShortName | String | Short name of the region |
| Area | String | Name of the area where the region is located |
| ZoneSet | Array of [ZoneCapacityConf](#ZoneCapacityConf) | Availability zone information |

## SecurityGroupDetail

Security group details

Referenced by: DescribeInstanceSecurityGroup, DescribeProjectSecurityGroup.

| Name | Type | Description |
|------|------|-------|
| ProjectId | Integer | Project ID |
| CreateTime | String | Creation time |
| SecurityGroupId | String | Security group ID |
| SecurityGroupName | String | Security group name |
| SecurityGroupRemark | String | Security group remarks |
| InboundRule | Array of [SecurityGroupsInboundAndOutbound](#SecurityGroupsInboundAndOutbound) | Inbound rule of the security group |
| OutboundRule | Array of [SecurityGroupsInboundAndOutbound](#SecurityGroupsInboundAndOutbound) | Outbound rule of the security group |

## SecurityGroupsInboundAndOutbound

Inbound and outbound rules of the security group

Referenced by: DescribeInstanceSecurityGroup, DescribeProjectSecurityGroup.

| Name | Type | Description |
|------|------|-------|
| Action | String | Action to be executed |
| Ip | String | IP address |
| Port | String | Port number |
| Proto | String | Protocol type |

## TradeDealDetail

Order deal information

Referenced by: DescribeInstanceDealDetail.

| Name | Type | Description |
|------|------|-------|
| DealId | String | Order ID, which is used when TencentCloud API is called |
| DealName | String | Long order ID, which is used when an order issue is submitted for assistance |
| ZoneId | Integer | Availability zone ID |
| GoodsNum | Integer | Number of instances associated with the order |
| Creater | String | uin of the creator |
| CreatTime | String | Order creation time |
| OverdueTime | String | Order overdue time |
| EndTime | String | Order completion time |
| Status | Integer | Order status. 1: unpaid; 2: paid but not shipped; 3: shipping; 4: successfully shipped; 5: shipment failed; 6: refunded; 7: order closed; 8: order expired; 9: order invalidated; 10: product invalidated; 11: requested payment rejected; 12: paying |
| Description | String | Order status description |
| Price | Integer | Actual amount of the order |
| InstanceIds | Array of String | Instance ID |

## ZoneCapacityConf

Product information in the availability zone

Referenced by: DescribeProductInfo.

| Name | Type | Description |
|------|------|-------|
| ZoneId | String | Availability zone ID, such as ap-guangzhou-3 |
| ZoneName | String | Availability zone name |
| IsSaleout | Boolean | Whether the product is sold out in the availability zone |
| IsDefault | Boolean | Whether it is the default availability zone |
| NetWorkType | Array of String | Network type. basenet: basic network; vpcnet: VPC |
| ProductSet | Array of [ProductConf](#ProductConf) | Information such as product specifications in the availability zone |
| OldZoneId | Integer | Availability zone ID, such as 100003 |
