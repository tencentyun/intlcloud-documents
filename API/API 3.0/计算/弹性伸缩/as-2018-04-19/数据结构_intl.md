## Activity

Information on eligible scaling activities.

Referenced by: DescribeAutoScalingActivities.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Auto scaling group ID |
| ActivityId | String | Scaling activity ID |
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
| InstanceId | String | Instance ID |
| InstanceStatus | String | Status of the instance in the scaling activity. Value range: <br/><li>INIT: initializing <br/><li>RUNNING: running <br/><li>SUCCESSFUL: succeeded <br/><li>FAILED: failed |

## AutoScalingGroup

Auto scaling group

Referenced by: DescribeAutoScalingGroups.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Auto scaling group ID |
| AutoScalingGroupName | String | Auto scaling group name |
| AutoScalingGroupStatus | String | Current status of the auto scaling group. Value range: <br><li>NORMAL: normal <br><li>CVM_ABNORMAL: Exception with the launch configuration <br><li>LB_ABNORMAL: exception with the load balancer <br><li>VPC_ABNORMAL: exception with the VPC <br><li>INSUFFICIENT_BALANCE: insufficient balance <br> |
| CreatedTime | Timestamp | Creation time in UTC format |
| DefaultCooldown | Integer | Default cooldown period in seconds |
| DesiredCapacity | Integer | Desired number of instances |
| EnabledStatus | String | Enabled status; valid values: `ENABLED`, `DISABLED` |
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
| InActivityStatus | String | Whether the auto scaling group is performing a scaling activity. `IN_ACTIVITY` indicates yes, and `NOT_IN_ACTIVITY` indicates no. |
| Tags | Array of [Tag](#Tag) | List of auto scaling group tags |
| ServiceSettings | [ServiceSettings](#ServiceSettings) | Service settings |

## AutoScalingGroupAbstract

Brief information of an auto scaling group.

Referenced by: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Auto scaling group ID |
| AutoScalingGroupName | String | Auto scaling group name |

## AutoScalingNotification

AS event notification

Referenced by: DescribeNotificationConfigurations.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Auto scaling group ID |
| NotificationUserGroupIds | Array of String | List of user group IDs. |
| NotificationTypes | Array of String | List of notification events. |
| AutoScalingNotificationId | String | Event notification ID. |

## DataDisk

Configuration information of data disk in launch configuration. If this parameter is not specified, no data disk will be purchased by default. You can specify only one data disk when purchasing it.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | Data disk type. For more information on limits of data disk types, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Value range: <br><li>LOCAL_BASIC: Local disk <br><li>LOCAL_SSD: Local SSD disk <br><li>CLOUD_BASIC: HDD cloud disk <br><li>CLOUD_PREMIUM: Premium cloud disk <br><li>CLOUD_SSD: SSD cloud disk <br><br>Default value: CLOUD_BASIC. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| DiskSize | Integer | No | Data disk size (in GB). The minimum adjustment increment is 10 GB. Different types of data disks have different value ranges. For more information on limits, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). The default value is 0, indicating that no data disk is purchased. For more information, see the product documentation. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| SnapshotId | String | No | ID of the data disk snapshot in the format of `snap-l8psqwnt`. <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## EnhancedService

This describes the conditions of enhancement services for the instance and their settings, such as the Agent of Cloud Security or Cloud Monitor.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | No | Enable the Cloud Security service. If this parameter is not specified, the Cloud Security service is enabled by default. |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | No | Enable the Cloud Monitor service. If this parameter is not specified, the Cloud Monitor service is enabled by default. |

## Filter

>Key-value pair filters for conditional filtering queries, such as filtering ID, name, status, etc.
> * If there are multiple `Filter`, the relationship among them is logical `AND`.
> * If there are multiple `Values` in the same `Filter`, the relationship among the `Values` in the same `Filter` is logical `OR`.
>
> Take the `Filter` in the API [DescribeInstances](https://cloud.tencent.com/document/api/213/9388) as an example. We can use the following filters to query the instance that resides in the availability zone (`zone`) of Guangzhou Zone 1 ***and*** is billed (`instance-charge-type`) on a prepaid basis ***or*** on a postpaid basis:
```
Filters.0.Name=zone
&Filters.0.Values.1=ap-guangzhou-1
&Filters.1.Name=instance-charge-type
&Filters.1.Values.1=PREPAID
&Filters.1.Values.2=POSTPAID_BY_HOUR
```

Referenced by: DescribeAutoScalingActivities, DescribeAutoScalingGroups, DescribeAutoScalingInstances, DescribeLaunchConfigurations, DescribeLifecycleHooks, DescribeNotificationConfigurations, DescribePaiInstances, DescribeScalingPolicies, DescribeScheduledActions.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | The field to be filtered |
| Values | Array of String | Yes | Filter values of the field |

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
| AutoScalingGroupId | String | Auto scaling group ID |
| LaunchConfigurationId | String | Launch configuration ID |
| LaunchConfigurationName | String | Launch configuration name |
| LifeCycleState | String | Lifecycle status; valid values: IN_SERVICE, CREATING, TERMINATING, ATTACHING, DETACHING, ATTACHING_LB, DETACHING_LB |
| HealthStatus | String | Health status; valid values: HEALTHY, UNHEALTHY |
| ProtectedFromScaleIn | Boolean | Whether to add scale-in protection|
| Zone | String | Availability zone |
| CreationType | String | Creation type. Value range: AUTO_CREATION, MANUAL_ATTACHING. |
| AddTime | Timestamp | Instance addition time |
| InstanceType | String | Instance type |
| VersionNumber | Integer | Version number |

## InstanceChargePrepaid

This describes the billing mode of an instance

Referenced by: CreatePaiInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| Period | Integer | Yes | Purchased usage period of an instance (in month). Value range: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 24, 36. |
| RenewFlag | String | No | Auto-renewal flag. Value range: <br><li>NOTIFY_AND_AUTO_RENEW: Notify expiry and renew automatically <br><li>NOTIFY_AND_MANUAL_RENEW: Notify expiry but not renew automatically <br><li>DISABLE_NOTIFY_AND_MANUAL_RENEW: Neither notify expiry nor renew automatically <br><br>Default value: NOTIFY_AND_MANUAL_RENEW. If this parameter is specified as NOTIFY_AND_AUTO_RENEW, the instance will be automatically renewed on a monthly basis if the account balance is sufficient. |

## InstanceMarketOptionsRequest

Options related to a CVM bidding request

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| SpotOptions | [SpotMarketOptions](#SpotMarketOptions) | Yes | Bidding-related options |
| MarketType | String | No | Market option type. Current, only "spot" is supported <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## InstanceTag

Instance tag. This parameter is used to bind tags to newly added instances.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| Key | String | Yes | Tag key |
| Value | String | Yes | Tag value |

## InternetAccessible

This describes the internet accessibility of the instance created by a launch configuration and declares the internet usage billing mode of the instance and the maximum bandwidth

Referenced by: CreateLaunchConfiguration, CreatePaiInstance, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| InternetChargeType | String | No | Network billing mode. Value range: <br><li>BANDWIDTH_PREPAID: Prepaid by bandwidth <br><li>TRAFFIC_POSTPAID_BY_HOUR: Postpaid by traffic on a per hour basis <br><li>BANDWIDTH_POSTPAID_BY_HOUR: Postpaid by bandwidth on a per hour basis <br><li>BANDWIDTH_PACKAGE: BWP user <br>Default value: TRAFFIC_POSTPAID_BY_HOUR. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| InternetMaxBandwidthOut | Integer | No | The maximum outbound bandwidth of the public network (in Mbps). The default value is 0 Mbps. The upper limit of bandwidth varies with different models. For more information, see [Purchasing Network Bandwidth](https://cloud.tencent.com/document/product/213/509). <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| PublicIpAssigned | Boolean | No | Whether to assign a public IP. Value range: <br><li>TRUE: Assign a public IP <br><li>FALSE: Do not assign a public IP <br><br>If the public network bandwidth is greater than 0 Mbps, you are free to choose whether to enable the public IP (which is enabled by default). If the public network bandwidth is 0 Mbps, no public IP is allowed to be assigned. <br/>Note: This field may return null, indicating that no valid values can be obtained |

## LaunchConfiguration

Information set of eligible launch configurations.

Referenced by: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| ProjectId | Integer | Project ID to which an instance belongs |
| LaunchConfigurationId | String | Launch configuration ID |
| LaunchConfigurationName | String | Launch configuration name |
| InstanceType | String | Instance type |
| SystemDisk | [SystemDisk](#SystemDisk) | Configuration information of the instance's system disk |
| DataDisks | Array of [DataDisk](#DataDisk) | Configuration information of the instance's data disk |
| LoginSettings | [LimitedLoginSettings](#LimitedLoginSettings) | Instance login settings |
| InternetAccessible | [InternetAccessible](#InternetAccessible) | Settings for public network bandwidth information |
| SecurityGroupIds | Array of String | The security group to which the instance belongs |
| AutoScalingGroupAbstractSet | Array of [AutoScalingGroupAbstract](#AutoScalingGroupAbstract) | Auto scaling group to which the launch configuration is attached |
| UserData | String | Custom data. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CreatedTime | Timestamp | Creation time of the launch configuration |
| EnhancedService | [EnhancedService](#EnhancedService) | Indicates whether the enhanced service is enabled for the instance and the service settings |
| ImageId | String | Image ID |
| LaunchConfigurationStatus | String | Current status of the launch configuration. Value range: <br><li>NORMAL: normal <br><li>IMAGE_ABNORMAL: Exception with the image of the launch configuration <br><li>CBS_SNAP_ABNORMAL: Exception with the data disk snapshot of the launch configuration <br><li>SECURITY_GROUP_ABNORMAL: Exception with the security group of the launch configuration <br> |
| InstanceChargeType | String | Instance billing type. CVM instances are POSTPAID_BY_HOUR by default. <br/><br><li>POSTPAID_BY_HOUR: Pay-as-you-go on an hourly basis <br/><br><li>SPOTPAID: Bidding |
| InstanceMarketOptions | [InstanceMarketOptionsRequest](#InstanceMarketOptionsRequest) | Market-related options of the instance, such as the parameters related to spot instances. If the billing mode of instance is specified as bidding, this parameter must be passed in. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| InstanceTypes | Array of String | List of instance models. |
| InstanceTags | Array of [InstanceTag](#InstanceTag) | List of tags. |
| VersionNumber | Integer | Version number. |
| UpdatedTime | Timestamp | Updated time |
| CamRoleName | String | CAM role name, which can be obtained from the `roleName` field in the return value of the DescribeRoleList API. |

## LifecycleHook

Lifecycle hook

Referenced by: DescribeLifecycleHooks.

| Name | Type | Description |
|------|------|-------|
| LifecycleHookId | String | Lifecycle hook ID |
| LifecycleHookName | String | Lifecycle hook name |
| AutoScalingGroupId | String | Auto scaling group ID |
| DefaultResult | String | Default result of the lifecycle hook |
| HeartbeatTimeout | Integer | Wait timeout period of the lifecycle hook |
| LifecycleTransition | String | Applicable scenario of the lifecycle hook |
| NotificationMetadata | String | Additional information for the notification target |
| CreatedTime | Timestamp | Creation time |
| NotificationTarget | [NotificationTarget](#NotificationTarget) | Notification target |

## LimitedLoginSettings

This describes the configuration and information related to instance login. For security reasons, sensitive information is not described.

Referenced by: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| KeyIds | Array of String | Key ID list |

## LoginSettings

This describes the configuration and information related to instance login.

Referenced by: CreateLaunchConfiguration, CreatePaiInstance, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| Password | String | No | Login password of the instance. The rule of password complexity varies with different operating systems: <br><li>For Linux instances, the password must be a combination of 8-16 characters comprised of at least two of the following types: [a-z, A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ]. <br><li>For Windows instances, the password must be a combination of 12-16 characters comprised of at least three of the following types: [a-z], [A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /]. <br><br>If this parameter is not specified, a password is randomly generated and sent to you via the internal message. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| KeyIds | Array of String | No | List of key IDs. An instance associated with the key can be accessed using the corresponding private key. KeyId can be obtained via the API DescribeKeyPairs. A key and a password cannot be specified at the same time, and specifying the key is not supported in Windows. You can specify only one key when purchasing an instance. |
| KeepImageLogin | Boolean | No | Whether to keep the original settings for an image. You cannot specify this parameter if Password or KeyIds.N is specified. You can specify this parameter to TRUE only when you create an instance using a custom image, shared image, or image imported from external resources. Value range: <br><li>TRUE: Keep the login settings for the image <br><li>FALSE: Do not keep the login settings for the image <br><br>Default value: FALSE. <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## MetricAlarm

Alarming metric of AS

Referenced by: CreateScalingPolicy, DescribeScalingPolicies, ModifyScalingPolicy.

| Name | Type | Required | Description |
|------|------|----------|------|
| ComparisonOperator | String | Yes | Comparison operator. Value range: <br><li>GREATER_THAN: greater than </li><li>GREATER_THAN_OR_EQUAL_TO: greater than or equal to </li><li>LESS_THAN: less than </li><li> LESS_THAN_OR_EQUAL_TO: less than or equal to </li><li> EQUAL_TO: equal to </li> <li>NOT_EQUAL_TO: not equal to </li> |
| MetricName | String | Yes | Metric name. Value range: <br><li>CPU_UTILIZATION: CPU utilization </li><li>MEM_UTILIZATION: memory utilization </li><li>LAN_TRAFFIC_OUT: private network outbound bandwidth </li><li>LAN_TRAFFIC_IN: private network inbound bandwidth </li><li>WAN_TRAFFIC_OUT: public network outbound bandwidth </li><li>WAN_TRAFFIC_IN: public network inbound bandwidth </li> |
| Threshold | Integer | Yes | Alarming threshold: <br><li>CPU_UTILIZATION: [1, 100] in % </li><li>MEM_UTILIZATION: [1, 100] in % </li><li>LAN_TRAFFIC_OUT: >0 in Mbps </li><li>LAN_TRAFFIC_IN: >0 in Mbps </li><li>WAN_TRAFFIC_OUT: >0 in Mbps </li><li>WAN_TRAFFIC_IN: >0 in Mbps </li> |
| Period | Integer | Yes | Time period in seconds. Enumerated values: 60, 300. |
| ContinuousTime | Integer | Yes | Number of repetitions. Value range: [1, 10] |
| Statistic | String | No | Statistics type. Value range: <br><li>AVERAGE: average </li><li>MAXIMUM: maximum <li>MINIMUM: minimum </li><br> Default value: AVERAGE |

## NotificationTarget

Inform target.

Referenced by: CreateLifecycleHook, DescribeLifecycleHooks, UpgradeLifecycleHook.

| Name | Type | Required | Description |
|------|------|----------|------|
| TargetType | String | Yes | Target type. Value range: `CMQ_QUEUE`, `CMQ_TOPIC`. <br/><li> CMQ_QUEUE: CMQ queue model. </li><li> CMQ_TOPIC: CMQ topic model. </li> |
| QueueName | String | No | Queue name. If `TargetType` is `CMQ_QUEUE`, this parameter is required. |
| TopicName | String | No | Topic name. If `TargetType` is `CMQ_TOPIC`, this parameter is required. |

## PaiInstance

PAI instance

Referenced by: DescribePaiInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| DomainName | String | Instance domain name |

## RunMonitorServiceEnabled

This describes the information related to the Cloud Monitor service.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable [Cloud Monitor](https://cloud.tencent.com/document/product/248). Value range: <br><li>TRUE: Cloud Monitor is enabled <br><li>FALSE: Cloud Monitor is disabled <br><br>Default value: TRUE. <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## RunSecurityServiceEnabled

This describes the information on the Cloud Security service

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable [Cloud Security](https://cloud.tencent.com/document/product/296). Value range: <br><li>TRUE: Cloud Security is enabled <br><li>FALSE: Cloud Security is disabled <br><br>Default value: TRUE. <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## ScalingPolicy

Alarm trigger policy.

Referenced by: DescribeScalingPolicies.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Auto scaling group ID |
| AutoScalingPolicyId | String | Alarm trigger policy ID. |
| ScalingPolicyName | String | Name of the alarm trigger policy. |
| AdjustmentType | String | The method to adjust the desired number of instances after the alarm is triggered. Value range: <br><li>CHANGE_IN_CAPACITY: Increase or decrease the desired number of instances </li><li>EXACT_CAPACITY: Adjust to the specified desired number of instances </li> <li>PERCENT_CHANGE_IN_CAPACITY: Adjust the desired number of instances by percentage </li> |
| AdjustmentValue | Integer | The adjusted value of desired number of instances after the alarm is triggered. |
| Cooldown | Integer | Cooldown period. |
| MetricAlarm | [MetricAlarm](#MetricAlarm) | Alarm monitoring metric. |
| NotificationUserGroupIds | Array of String | Notification group ID, which is the set of user group IDs. |

## ScheduledAction

This describes the information of a scheduled action.

Referenced by: DescribeScheduledActions.

| Name | Type | Description |
|------|------|-------|
| ScheduledActionId | String | Scheduled action ID. |
| ScheduledActionName | String | Scheduled action name. |
| AutoScalingGroupId | String | ID of the auto scaling group to which the scheduled action belongs. |
| StartTime | Timestamp | Start time of the scheduled action, which is based on `Beijing Time` (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`. |
| Recurrence | String | Repetition mode of the scheduled action. |
| EndTime | Timestamp | End time of the scheduled action, which is based on `Beijing Time` (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`. |
| MaxSize | Integer | The maximum number of instances set for the scheduled action. |
| DesiredCapacity | Integer | Desired number of instances set for the scheduled action. |
| MinSize | Integer | The minimum number of instances set for the scheduled action. |
| CreatedTime | Timestamp | Creation time of the scheduled action, which is based on `UTC` and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ssZ`. |

## ServiceSettings

Service settings

Referenced by: CreateAutoScalingGroup, DescribeAutoScalingGroups, ModifyAutoScalingGroup.

| Name | Type | Required | Description |
|------|------|----------|------|
| ReplaceMonitorUnhealthy | Boolean | No | Enable unhealthy instance replacement. If this feature is enabled, AS will replace instances that are flagged as unhealthy by Cloud Monitor. If this parameter is not specified, the value is False by default. |

## SpotMarketOptions

Bidding-related options

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| MaxPrice | String | Yes | Bidding price such as "1.05" |
| SpotInstanceType | String | No | Spot request type; currently, only "one-time" type is supported; one-time by default <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## SystemDisk

System disk configuration of the launch configuration. If this parameter is not specified, the default value is assigned to it.

Referenced by: CreateLaunchConfiguration, DescribeLaunchConfigurations, UpgradeLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | System disk type. For more information on limits of system disk types, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Value range: <br><li>LOCAL_BASIC: Local disk <br><li>LOCAL_SSD: Local SSD disk <br><li>CLOUD_BASIC: HDD cloud disk <br><li>CLOUD_PREMIUM: Premium cloud disk <br><li>CLOUD_SSD: SSD cloud disk <br><br>Default value: CLOUD_BASIC. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| DiskSize | Integer | No | System disk size in GB. Default value: 50 <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## Tag

Resource type and tag key-value pair

Referenced by: CreateAutoScalingGroup, DescribeAutoScalingGroups.

| Name | Type | Required | Description |
|------|------|----------|------|
| Key | String | Yes | Tag key |
| Value | String | Yes | Tag value |
| ResourceType | String | No | Type of the resource bound to the tag. Currently supported type: "auto-scaling-group" <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## TargetAttribute

Load balancer target attribute

Referenced by: CreateAutoScalingGroup, DescribeAutoScalingGroups, ModifyLoadBalancers.

| Name | Type | Required | Description |
|------|------|----------|------|
| Port | Integer | Yes | Port |
| Weight | Integer | Yes | Weight |

