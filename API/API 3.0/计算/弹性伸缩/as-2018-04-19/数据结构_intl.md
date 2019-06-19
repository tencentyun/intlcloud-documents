## Activity

Information about eligible scaling activities.

Referenced by: DescribeAutoScalingActivities.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Scaling group ID. |
| ActivityId | String | Scaling activity ID. |
| ActivityType | String | Scaling activity type. Value range: <br><br/><li>SCALE_OUT: scale-out <li>SCALE_IN: scale-in <li>ATTACH_INSTANCES: adding an instance <li>REMOVE_INSTANCES: terminating an instance <li>DETACH_INSTANCES: removing an instance <li>TERMINATE_INSTANCES_UNEXPECTEDLY: terminating an instance in the CVM console <li>REPLACE_UNHEALTHY_INSTANCE: replacing an unhealthy instance |
| StatusCode | String | Scaling activity status. Value range: <br><br/><li>INIT: initializing <br/><li>RUNNING: running <br/><li>SUCCESSFUL: succeeded <br/><li>PARTIALLY_SUCCESSFUL: partially succeeded <br/><li>FAILED: failed <br/><li>CANCELLED: canceled |
| StatusMessage | String | Description of the scaling activity status. |
| Cause | String | Cause of the scaling activity. |
| Description | String | Description of the scaling activity. |
| StartTime | Timestamp | Start time of the scaling activity. |
| EndTime | Timestamp | End time of the scaling activity. |
| CreatedTime | Timestamp | Creation time of the scaling activity. |
| ActivityRelatedInstanceSet | Array of [ActivtyRelatedInstance](#ActivtyRelatedInstance) | Information set of the instances related to the scaling activity. |
| StatusMessageSimplified | String | Brief description of the scaling activity status. |

## ActivtyRelatedInstance

Information of the instances related to the current scaling activity.

Referenced by: DescribeAutoScalingActivities.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID. |
| InstanceStatus | String | Status of the instance in the scaling activity. Value range: <br/><li>SUCCESSFUL: succeeded <br/><li>FAILED: failed |

## AutoScalingGroup

Scaling group

Referenced by: DescribeAutoScalingGroups.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Scaling group ID |
| AutoScalingGroupName | String | Scaling group name |
| AutoScalingGroupStatus | String | Scaling group status |
| CreatedTime | Timestamp | Creation time in UTC format |
| DefaultCooldown | Integer | Default cooldown period in seconds |
| DesiredCapacity | Integer | Desired number of instances |
| EnabledStatus | String | Enabled status; value range: `ENABLED`, `DISABLED` |
| ForwardLoadBalancerSet | Array of [ForwardLoadBalancer](#ForwardLoadBalancer) | List of application load balancers |
| InstanceCount | Integer | Number of instances |
| InServiceInstanceCount | Integer | Number of instances in `IN_SERVICE` status |
| LaunchConfigurationId | String | Launch configuration ID |
| LaunchConfigurationName | String | Launch configuration name |
| LoadBalancerIdSet | Array of String | List of Classic load balancer IDs |
| MaxSize | Integer | Maximum number of instances |
| MinSize | Integer | Minimum number of instances |
| ProjectId | Integer | Project ID |
| SubnetIdSet | Array of String | Subnet ID list |
| TerminationPolicySet | Array of String | Termination policy |
| VpcId | String | VPC ID |
| ZoneSet | Array of String | Availability zone list |
| RetryPolicy | String | Retry policy |

## AutoScalingGroupAbstract

Brief information of a scaling group.

Referenced by: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Scaling group ID. |
| AutoScalingGroupName | String | Scaling group name. |

## DataDisk

Data disk configuration information of a launch configuration. If this parameter is not specified, no data disk is purchased by default. Currently, it is only supported to specify a data disk during purchase.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | Data disk type. For more information about restrictions on data disk types, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Value range: <br><li>LOCAL_BASIC: local disk <br><li>LOCAL_SSD: Local SSD <br><li>CLOUD_BASIC: HDD cloud disk <br><li>CLOUD_PREMIUM: Premium cloud disk <br><li>CLOUD_SSD: SSD cloud disk <br><br>Default value: LOCAL_BASIC. |
| DiskSize | Integer | No | Data disk size in GB. The minimum adjustment step width is 10 GB, and the value range varies for different data disk types. For details, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). The default value is 0, which means that data disk is not purchased. For more information about restrictions, see the product documentation. |
| SnapshotId | String | No | Data disk snapshot ID, such as `snap-l8psqwnt`. |

## EnhancedService

This describes the conditions of enhancement services for the instance and their settings, such as the Agent of Cloud Security or Cloud Monitor.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | No | This is to enable the Cloud Security service. If this parameter is not specified, the Cloud Security service is enabled by default. |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | No | This is to enable the Cloud Monitor service. If this parameter is not specified, the Cloud Monitor service is enabled by default. |

## Filter

> Used to describe key-value pair filters for conditional filtering queries, such as filtering ID, name and state.
> * If there are multiple `Filter`, the relationship among them is logical `AND`.
> * If there are multiple `Values` in the same `Filter`, the relationship among the `Values` in the same `Filter` is logical `OR`.
>
> Take the `Filter` of the [DescribeInstances](https://cloud.tencent.com/document/api/213/9388) API as an example. If you want to query the instances in availability zone (`zone`) "Guangzhou Zone 1" ***and*** with billing method (`instance-charge-type`) "prepaid" ***or*** "postpaid", the query can be implemented as follows:
```
Filters.1.Name=zone
&Filters.1.Values.1=ap-guangzhou-1
&Filters.2.Name=instance-charge-type
&Filters.2.Values.1=PREPAID
&Filters.3.Values.2=POSTPAID_BY_HOUR
```

Referenced by: DescribeAutoScalingActivities, DescribeAutoScalingGroups, DescribeAutoScalingInstances, DescribeLaunchConfigurations, DescribeScheduledActions.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Field to be filtered. |
| Values ​​| Array of String | Yes | Filter value of the field. |

## ForwardLoadBalancer

Application load balancer

Referenced by: CreateAutoScalingGroup, DescribeAutoScalingGroups, ModifyLoadBalancers.

| Name | Type | Required | Description |
|------|------|----------|------|
| LoadBalancerId | String | Yes | Load balancer ID |
| ListenerId | String | Yes | Application load balancing listener ID |
| TargetAttributes | Array of [TargetAttribute](#TargetAttribute) | Yes | Target rule attribute list |
| LocationId | String | No | Forwarding rule ID |

## Instance

Instance information

Referenced by: DescribeAutoScalingInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| AutoScalingGroupId | String | Scaling group ID |
| LaunchConfigurationId | String | Launch configuration ID |
| LaunchConfigurationName | String | Launch configuration name |
| LifeCycleState | String | Lifecycle status; value range: IN_SERVICE, CREATING, TERMINATING, ATTACHING, DETACHING, ATTACHING_LB, DETACHING_LB |
| HealthStatus | String | Health status; value range: HEALTHY, UNHEALTHY |
| ProtectedFromScaleIn | Boolean | Whether to add scale-in protection|
| Zone | String | Availability zone |
| CreationType | String | Creation type; value range: AUTO_CREATION, MANUAL_ATTACHING. |
| AddTime | Timestamp | Instance addition time |
| InstanceType | String | Instance type |

## InstanceMarketOptionsRequest

Options related to a CVM bidding request

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| SpotOptions | [SpotMarketOptions](#SpotMarketOptions) | Yes | Bidding-related options |
| MarketType | String | No | Market option type; currently, this only supports the value "spot" |

## InternetAccessible

This describes the internet accessibility of the instance created by a launch configuration and declares the internet usage billing method of the instance and the maximum bandwidth

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| InternetChargeType | String | No | Internet billing method. Value range: <br><li>BANDWIDTH_PREPAID: Prepaid by bandwidth <br><li>TRAFFIC_POSTPAID_BY_HOUR: Postpaid by traffic on a per hour basis <br><li>BANDWIDTH_POSTPAID_BY_HOUR: Postpaid by bandwidth on a per hour basis <br><li>BANDWIDTH_PACKAGE: BWP user <br>Default value: TRAFFIC_POSTPAID_BY_HOUR. |
| InternetMaxBandwidthOut | Integer | No | The upper limit of outbound Internet bandwidth in Mbps. Default value: 0 Mbps. The upper limit of bandwidth varies for different models. For details, see [Buying Network Bandwidth](https://cloud.tencent.com/document/product/213/509). |
| PublicIpAssigned | Boolean | No | Whether to assign a public IP. Value range: <br><li>TRUE: A public IP is assigned <br><li>FALSE: No public IP is assigned <br><br>If the Internet bandwidth is greater than 0 Mbps, either value can be used. The default value is TRUE. If the Internet bandwidth is 0, it is not allowed to assign a public IP. |

## LaunchConfiguration

Information set of eligible launch configurations.

Referenced by: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| ProjectId | Integer | ID of the project to which the instance belongs. |
| LaunchConfigurationId | String | Launch configuration ID. |
| LaunchConfigurationName | String | Launch configuration name. |
| InstanceType | String | Instance model. |
| SystemDisk | [SystemDisk](#SystemDisk) | Information of the instance's system disk configuration. |
| DataDisks | Array of [DataDisk](#DataDisk) | Information of the instance's data disk configuration. |
| LoginSettings | [LimitedLoginSettings](#LimitedLoginSettings) | Instance login settings. |
| InternetAccessible | [InternetAccessible](#InternetAccessible) | Information of the Internet bandwidth configuration. |
| SecurityGroupIds | Array of String | Security group of the instance. |
| AutoScalingGroupAbstractSet | Array of [AutoScalingGroupAbstract](#AutoScalingGroupAbstract) | Scaling group associated with the launch configuration. |
| UserData | String | Custom data. |
| CreatedTime | Timestamp | Creation time of the launch configuration. |
| EnhancedService | [EnhancedService](#EnhancedService) | Conditions of enhancement services for the instance and their settings. |
| ImageId | String | Image ID. |
| LaunchConfigurationStatus | String | Current status of the launch configuration. Value range: <br><li>NORMAL: normal <br><li>IMAGE_ABNORMAL: Exception with the image of the launch configuration <br><li>CBS_SNAP_ABNORMAL: Exception with the data disk snapshot of the launch configuration <br><li>SECURITY_GROUP_ABNORMAL: Exception with the security group of the launch configuration <br> |
| InstanceChargeType | String | Instance billing type. CVM instances are POSTPAID_BY_HOUR by default. <br/><br><li>POSTPAID_BY_HOUR: Pay-as-you-go on an hourly basis <br/><br><li>SPOTPAID: Bidding |
| InstanceMarketOptions | [InstanceMarketOptionsRequest](#InstanceMarketOptionsRequest) | Market-related options of the instance, such as the parameters related to stop instances. If the billing method of instance is specified as bidding, this parameter must be passed in. |
| InstanceTypes | Array of String | List of instance models. |

## LimitedLoginSettings

This describes the configuration and information related to instance login. For security reasons, sensitive information is not described.

Referenced by: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| KeyIds | Array of String | List of key IDs. |

## LoginSettings

This describes the configuration and information related to instance login.

Referenced by: CreateLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| Password | String | No | Instance login password. Different operating systems have different password complexity restrictions as follows: <br><li>For Linux instances, the password must be 8 to 16 characters long, including at least two of the following three types of characters: [a-z，A-Z]、[0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ]. <br><li>For Windows instances, the passwords must be 12 to 16 characters long, including at least three of the following four types of characters: [a-z], [A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /]. <br><br>If this parameter is not specified, the system will generate a random password and notify the user of it through internal messages. |
| KeyIds | Array of String | No | List of key IDs. After the key is associated, the instance can be accessed through the corresponding private key. KeyId can be obtained through the DescribeKeyPairs API. Key and password cannot be specified simultaneously. For Windows, it is not supported to specify the key. Currently, it is only supported to specify a key at the time of purchase. |
| KeepImageLogin | Boolean | No | This is to keep the original settings of the image. This parameter cannot be specified together with Password or KeyIds.N. This parameter can be specified as TRUE only if the instance is created using a custom, shared or imported image. Value range: <br><li>TRUE: This indicates the login settings for the image are kept <br><li>FALSE: This indicates the login settings if the image are not kept <br><br>Default value: FALSE. |

## RunMonitorServiceEnabled

This describes the information related to the Cloud Monitor service.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable the [Cloud Monitor](https://cloud.tencent.com/document/product/248) service. Value range: <br><li>TRUE: Cloud Monitor is enabled <br><li>FALSE: Cloud Monitor is disabled <br><br>Default value: TRUE. |

## RunSecurityServiceEnabled

This describes the information about the Cloud Security service

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable the [Cloud Security](https://cloud.tencent.com/document/product/296) service. Value range: <br><li>TRUE: Cloud Security is enabled <br><li>FALSE: Cloud Security is disabled <br><br>Default value: TRUE. |

## ScheduledAction

This describes the information of a scheduled action.

Referenced by: DescribeScheduledActions.

| Name | Type | Description |
|------|------|-------|
| ScheduledActionId | String | Scheduled action ID. |
| ScheduledActionName | String | Scheduled action name. |
| AutoScalingGroupId | String | ID of the scaling group where the scheduled action is located. |
| StartTime | Timestamp | Start time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. |
| Recurrence | String | The repeating mode of the scheduled action. |
| EndTime | Timestamp | End time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. |
| MaxSize | Integer | Maximum number of instances set by the scheduled action. |
| DesiredCapacity | Integer | Desired number of instances set by the scheduled action. |
| MinSize | Integer | Minimum number of instances set by the scheduled action. |
| CreatedTime | Timestamp | Creation time of the scheduled action. The value is in `UTC time` in the format of `YYYY-MM-DDThh:mm:ssZ` according to the `ISO8601` standard. |

## SpotMarketOptions

Bidding-related options

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| MaxPrice | String | Yes | Bidding price such as "1.05" |
| SpotInstanceType | String | No | Spot request type; currently, only "one-time" type is supported; one-time by default |

## SystemDisk

System disk configuration information of a launch configuration. If this parameter is not specified, one is assigned according to the system default value.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | System disk type. For more information about restrictions on system disk types, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Value range: <br><li>LOCAL_BASIC: local disk <br><li>LOCAL_SSD: Local SSD <br><li>CLOUD_BASIC: HDD cloud disk <br><li>CLOUD_PREMIUM: Premium cloud disk <br><li>CLOUD_SSD: SSD cloud disk <br><br>Default value: LOCAL_BASIC. |
| DiskSize | Integer | No | System disk size in GB. Default value: 50 |

## TargetAttribute

Load balancer target attribute

Referenced by: CreateAutoScalingGroup, DescribeAutoScalingGroups, ModifyLoadBalancers.

| Name | Type | Required | Description |
|------|------|----------|------|
| Port | Integer | Yes | Port |
| Weight | Integer | Yes | Weight |
