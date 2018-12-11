## AutoScalingGroup

Scaling group

It is referenced by the API DescribeAutoScalingGroups.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Scaling group ID |
| AutoScalingGroupName | String | Scaling group name |
| AutoScalingGroupStatus | String | Scaling group status |
| CreatedTime | Timestamp | Creation time, expressed in UTC. |
| DefaultCooldown | Integer | Default cooldown period (in sec) |
| DesiredCapacity | Integer | Desired number of instances |
| EnabledStatus | String | Status. Possible values: `ENABLED` and `DISABLED` |
| ForwardLoadBalancerSet | Array of [ForwardLoadBalancer](#ForwardLoadBalancer) | List of application-based load balancers |
| InstanceCount | Integer | Number of instances |
| InServiceInstanceCount | Integer | Number of instances in the `IN_SERVICE` status |
| LaunchConfigurationId | String | Launch configuration ID |
| LaunchConfigurationName | String | Launch configuration name |
| LoadBalancerIdSet | Array of String | List of traditional load balancer IDs |
| MaxSize | Array of Integer | The maximum number of instances |
| MinSize | Array of Integer | The minimum number of instances |
| ProjectId | Array of Integer | Project ID |
| SubnetIdSet | Array of String | Subnet ID List |
| TerminationPolicySet | Array of String | Termination policies |
| VpcId | String | VPC ID |
| ZoneSet | Array of String | List of availability zones |

## AutoScalingGroupAbstract

Brief information of a scaling group.

It is referenced by the API DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| AutoScalingGroupId | String | Scaling group ID |
| AutoScalingGroupName | String | Scaling group name |

## DataDisk

Configuration information of data disk in launch configuration. If this parameter is not specified, no data disk will be purchased by default. You can specify only one data disk when purchasing it.

It is referenced by the APIs CreateLaunchConfiguration and DescribeLaunchConfigurations.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | Type of data disk. For more information on the limits of data disk type, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Value range:<br><li>LOCAL_BASIC: Local disk<br><li>LOCAL_SSD: Local SSD storage<br><li>CLOUD_BASIC: HDD storage<br><li>CLOUD_PREMIUM: Premium cloud storage<br><li>CLOUD_SSD: cloud SSD storage<br><br>Default: LOCAL_BASIC. |
| DiskSize | Integer | No | Data disk size (in GB). The minimum adjustment increment is 10 GB. Different types of data disks have different value ranges. For information on limits, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Default is 0, indicating that no data disk is purchased. |

## EnhancedService

The enabling conditions and settings of an instance's enhanced services, such as Cloud Security, Cloud Monitor and other instance agents.

Relevant APIs: `CreateLaunchConfiguration` and `DescribeLaunchConfigurations`.

| Name | Type | Required | Description |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | No | Enable the Cloud Security service. If this parameter is not specified, the Cloud Security service is enabled by default. |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | No | Enable the Cloud Monitor service. If this parameter is not specified, the Cloud Monitor service is enabled by default. |

## Filter

>Key-value pair filters for conditional filtering queries, such as filtering ID, name, status, etc.
> * If more than one `Filter` exists, the relation between these `Filters` is a logical `AND`.
> * If there are multiple `Values` for only one `Filter`, the relation between these `Values` under the same `Filter` is a logical `OR`.
>
> Take the `Filter` in the API [DescribeInstances](https://cloud.tencent.com/document/api/213/9388) as an example. We can use the following filters to query the instance that resides in the availability zone (`zone`) of Guangzhou Zone 1 ***and*** is billed (`instance-charge-type`) on a prepaid basis ***or*** on a postpaid basis:
```
Filters.1.Name=zone
&Filters.1.Values.1=ap-guangzhou-1
&Filters.2.Name=instance-charge-type
&Filters.2.Values.1=PREPAID
&Filters.3.Values.2=POSTPAID_BY_HOUR
```

Relevant APIs: `DescribeAutoScalingGroups`, `DescribeAutoScalingInstances`, `DescribeLaunchConfigurations` and `DescribeScheduledActions`.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | The field to be filtered |
| Values | Array of String | Yes | Filter values of the field |

## ForwardLoadBalancer

Application load balancer

Relevant APIs: CreateAutoScalingGroup and DescribeAutoScalingGroups.

| Name | Type | Required | Description |
|------|------|----------|------|
| LoadBalancerId | String | Yes | Load balancer ID |
| ListenerId | String | Yes | ID of the application-based load balancer listener |
| TargetAttributes | Array of [TargetAttribute](#TargetAttribute) | Yes | List of target rule attributes |
| LocationId | String | No | Forwarding rule ID |

## Instance

Instance information

Relevant APIs: DescribeAutoScalingInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| AutoScalingGroupId | String | Scaling group ID |
| LaunchConfigurationId | String | Launch configuration ID |
| LaunchConfigurationName | String | Launch configuration name |
| LifeCycleState | String | Lifecycle status. Possible values: IN_SERVICE, CREATING, TERMINATING, ATTACHING, DETACHING, ATTACHING_LB and DETACHING_LB. |
| HealthStatus | String | Health status. Possible values: HEALTHY and UNHEALTHY |
| ProtectedFromScaleIn | Boolean | Indicates whether to protect the instance from scaling down |
| Zone | String | Availability zone |
| CreationType | Array of String | Creation type. Possible values: AUTO_CREATION and MANUAL_ATTACHING. |
| AddTime | Timestamp | The time when the instance is added |

## InternetAccessible

The accessibility, billing method and maximum bandwidth for an instance created by a launch configuration on the public network

Relevant APIs: `CreateLaunchConfiguration` and `DescribeLaunchConfigurations`.

| Name | Type | Required | Description |
|------|------|----------|------|
| InternetChargeType | String | No | Network billing type. Value range:<br><li>BANDWIDTH_PREPAID: Prepaid by bandwidth<br><li>TRAFFIC_POSTPAID_BY_HOUR: Postpaid by traffic on an hourly basis<br><li>BANDWIDTH_POSTPAID_BY_HOUR: Postpaid by bandwidth on an hourly basis<br><li>BANDWIDTH_PACKAGE: Bandwidth package<br>Default: TRAFFIC_POSTPAID_BY_HOUR. |
| InternetMaxBandwidthOut | Integer | No | The maximum outbound bandwidth to the internet (in Mbps). Default is 0 Mbps. The upper limit of bandwidth varies with different models. For more information, see [Purchase Network Bandwidth](https://cloud.tencent.com/document/product/213/509). |
| PublicIpAssigned | Boolean | No | Whether to assign public IP. Value range:<br><li>TRUE: Assign public IP<br><li>FALSE: Not assign public IP<br><br>If the public network bandwidth is greater than 0 Mbps, you are free to choose whether to enable the public IP (which is enabled by default). If the internet bandwidth is 0 Mbps, the public IP is not assigned. |

## LaunchConfiguration

Information of launch configurations matching the condition.

Relevant APIs: DescribeLaunchConfigurations.

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
| AutoScalingGroupAbstractSet | Array of [AutoScalingGroupAbstract](#AutoScalingGroupAbstract) | Scaling group to which the launch configuration is attached |
| UserData | String | Custom data |
| CreatedTime | Timestamp | Creation time of the launch configuration |
| EnhancedService | [EnhancedService](#EnhancedService) | Indicates whether the enhanced service is enabled for the instance and the service settings |
| ImageId | String | Image ID |
| LaunchConfigurationStatus | String | Launch configuration status. Possible values: <br><li>NORMAL: normal<br><li>IMAGE_ABNORMAL: image abnormal<br><li>CBS_SNAP_ABNORMAL: data disk snapshot abnormal<br><li>SECURITY_GROUP_ABNORMAL: security group abnormal<br> |

## LimitedLoginSettings

The configuration and information related to instance login. For security reasons, sensitive information will not be listed.

Relevant APIs: DescribeLaunchConfigurations.

| Name | Type | Description |
|------|------|-------|
| KeyIds | Array of String | Key ID list |

## LoginSettings

The configuration and information related to instance login.

Relevant APIs: CreateLaunchConfiguration.

| Name | Type | Required | Description |
|------|------|----------|------|
|Password|String|No|Login password of the instance. The rule of password complexity varies with different operating systems: <br><li>For Linux instances, the password must be a combination of 8-16 characters comprised of at least two of the following types: [a-z, A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ].<br><li>For Windows instances, the password must be a combination of 12-16 characters comprised of at least three of the following types: [a-z], [A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /].<br><br>If this parameter is not specified, a password is randomly generated and sent to you via the internal message. |
| KeyIds | Array of String | No | List of key IDs. An instance associated with the key can be accessed using the corresponding private key. KeyId can be obtained via the API DescribeKeyPairs. A key and a password cannot be specified at the same time, and specifying the key is not supported in Windows. You can specify only one key when purchasing an instance. |
| KeepImageLogin | Boolean | No | Indicates whether to keep the original settings for an image. You cannot specify this parameter if Password or KeyIds.N is specified. You can specify this parameter to TRUE only when you create an instance using a custom image, shared image, or image imported from external resources. Value range:<br><li>TRUE: Keep the login settings for the image<br><li>FALSE: Do not keep the login settings for the image<br><br>Default: FALSE. |

## RunMonitorServiceEnabled

Information on the Cloud Monitor service.

Relevant APIs: `CreateLaunchConfiguration` and `DescribeLaunchConfigurations`.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Indicates whether to enable [Cloud Monitor](https://cloud.tencent.com/document/product/248). Value range:<br><li>TRUE: Enable Cloud Monitor<br><li>FALSE: Disable Cloud Monitor<br><br>Default: TRUE. |

## RunSecurityServiceEnabled

Information on the Cloud Security service

Relevant APIs: `CreateLaunchConfiguration` and `DescribeLaunchConfigurations`.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Indicates whether to enable [Cloud Security](https://cloud.tencent.com/document/product/296). Value range: <br><li>TRUE: Enable Cloud Security<br><li>FALSE: Disable Cloud Security<br><br>Default: TRUE. |

## ScheduledAction

Information on the scheduled task

Relevant APIs: DescribeScheduledActions.

| Name | Type | Description |
|------|------|-------|
| ScheduledActionId | String | Scheduled task ID |
| ScheduledActionName | String | Scheduled task name |
| AutoScalingGroupId | String | ID of the scaling group to which the scheduled task belongs |
| StartTime | Timestamp | Start time of the scheduled task, which is based on `Beijing Time` (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`. |
| Recurrence | String | Repetition mode of the scheduled task |
| EndTime | Timestamp | End time of the scheduled task, which is based on `Beijing Time` (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`. |
| MaxSize | Integer | The maximum number of instances set for the scheduled task |
| DesiredCapacity | Integer | Desired number of instances set for the scheduled task |
| MinSize | Integer | The minimum number of instances set for the scheduled task |
| CreatedTime | Timestamp | Creation time of the scheduled task, which is based on `UTC` and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ssZ`. |

## SystemDisk

System disk configuration of the launch configuration. If this parameter is not specified, the default value is assigned to it.

Relevant APIs: `CreateLaunchConfiguration` and `DescribeLaunchConfigurations`.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | Type of system disk. For more information on the limits of system disk type, see [CVM Instance Configuration](https://cloud.tencent.com/document/product/213/2177). Value range:<br><li>LOCAL_BASIC: Local disk<br><li>LOCAL_SSD: Local SSD disk<br><li>CLOUD_BASIC: HDD cloud disk<br><li>CLOUD_PREMIUM: Premium cloud storage<br><li>CLOUD_SSD: SSD cloud disk<br><br>Default: LOCAL_BASIC. |
| DiskSize | Integer | No | System disk size (in GB). Default is 50. |

## TargetAttribute

Target attributes of a load balancer

Relevant APIs: `CreateAutoScalingGroup` and `DescribeAutoScalingGroups`.

| Name | Type | Required | Description |
|------|------|----------|------|
| Port | Integer | Yes | Port |
| Weight | Integer | Yes | Weight |


