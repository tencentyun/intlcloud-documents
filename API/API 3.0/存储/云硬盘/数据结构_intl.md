## AttachDetail

This describes the number of mounted and mountable data disks of an instance.

Referenced by: DescribeInstancesDiskNum.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| AttachedDiskCount | Integer | The number of mounted data disks of the instance. |
| MaxAttachCount | Integer | The maximum number of data disks that can be mounted to an instance. |

## AutoSnapshotPolicy

This describes the detailed information of the scheduled snapshot policy.

Referenced by: DescribeAutoSnapshotPolicies, DescribeDiskAssociatedAutoSnapshotPolicy.

| Name | Type | Description |
|------|------|-------|
| AutoSnapshotPolicyId | String | The ID of the scheduled snapshot policy. |
| AutoSnapshotPolicyName | String | The name of the  policy. |
| AutoSnapshotPolicyState | String | The state of the scheduled snapshot policy. Value range: <br><li>NORMAL: Normal <br><li>ISOLATED: Isolated. |
| IsActivated | Boolean | Whether the scheduled snapshot policy is activated. |
| IsPermanent | Boolean | Whether snapshots created by this scheduled snapshot policy are retained permanently. |
| RetentionDays | Integer | The number of days that snapshots created by this scheduled snapshot policy are retained. |
| CreateTime | Timestamp | The creation time of the scheduled snapshot policy. |
| NextTriggerTime | Timestamp | The time that scheduled snapshots will be triggered next time. |
| Policy | Array of [Policy](#Policy) | The execution policy for scheduled snapshots. |
| DiskIdSet | Array of String | A list of IDs of the created cloud disks that are bound to the current scheduled snapshot policy. |

## Disk

The details of a cloud disk

Referenced by: DescribeDisks.

| Name | Type | Description |
|------|------|-------|
| DiskId | String | Cloud disk ID. |
| DiskUsage | String | Cloud disk type. Value range:<br><li>SYSTEM_DISK: System disk <br><li>DATA_DISK: Data disk. |
| DiskChargeType | String | Billing method. Value range: <br><li>PREPAID: Prepaid, that is, monthly subscription<br><li>POSTPAID_BY_HOUR: Postpaid, that is, pay as you go. |
| Portable | Boolean | Whether it is an elastic cloud disk. false: Non-elastic cloud disk; true: Elastic cloud disk. |
| Placement | [Placement](# placement) | Location of the cloud disk. |
| SnapshotAbility | Boolean | Whether the cloud disk is available for creating snapshots. Value range: <br><li>false: not available. true: available |
| DiskName | String | Cloud disk name. |
| DiskSize | Integer | Cloud disk size (in GB). |
| DiskState | String | Status of the cloud disk. Value range: <br><li>Not mounted: Not mounted <br><li>ATTACHING: Mounting <br><li>ATTACHED: Mounted <br><li>DETACHING: Un-mounting <br><li>EXPANDING: Expanding <br><li>ROLLBACKING: Rolling back <br><li>TORECYCE: To be reclaimed <br><li>DUMPING: Being duplicated |
| DiskType | String | Type of cloud disk medium. Value range: <br><li>CLOUD_BASIC: Ordinary cloud disk <br><li>CLOUD_PREMIUM: Premium cloud storage <br><li>CLOUD_SSD: SSD cloud disk. |
| Attached | Boolean | Whether the cloud disk is mounted to a CVM. Value range: <br><li>false: Not mounted <br><li>true: Mounted. |
| InstanceId | String | The ID of the CVM onto which the Cloud Block Storage is mounted. |
| CreateTime | Timestamp | The creation time of the cloud disk. |
| DeadlineTime | Timestamp | The expiration time of the cloud disk. |
| Rollbacking | Boolean | Whether the cloud disk is in the status of snapshot rollback. Value range: <br><li>false: No <br><li>true: Yes. |
| RollbackPercent | Integer | Progress of rolling back a snapshot to the cloud disk. |
| Encrypt | Boolean | Whether the cloud disk is encrypted. Value range: <br><li>false: Not encrypted <br><li>true: Encrypted. |
| AutoRenewFlagError | Boolean | Indicates whether the cloud disk is mounted to a CVM, and the both the CVM and cloud disk are on a monthly subscription. <br><li>true: the CVM has enabled auto renewal, but not the cloud disk<br><li>false: both the CVM and cloud disk has enabled auto renewal. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| RenewFlag | String | Auto renewal flag. Value range: <br><li>NOTIFY_AND_AUTO_RENEW: Notify expiry and renew automatically <br><li>NOTIFY_AND_MANUAL_RENEW: Notify expiry but do not renew automatically <br><li>DISABLE_NOTIFY_AND_MANUAL_RENEW: Neither notify expiry nor renew automatically. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| DeadlineError | Boolean | This field is applicable when a cloud disk is already mounted to an instance, and both the instance and the cloud disk are on a monthly subscription. <br><li>true: The cloud disk expires before the instance. <br><li>false: The cloud disk expires after the instance. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| IsReturnable | Boolean | Determines whether a prepaid cloud disk supports active return. <br><li>true: Active return supported. <br><li>false: Active return not supported. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| ReturnFailCode | Integer | In circumstances where the prepaid cloud disk does not support active return, this parameter indicates the reason that return is not supported. Value range: <br><li>1: The cloud disk has already been returned. <br><li>2: The cloud disk has already expired. <br><li>3: The cloud disk does not support return. <br><li> 8: The limit on the number of returns is exceeded. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| AutoSnapshotPolicyIds | Array of String | IDs of the scheduled snapshot policy  associated to the cloud disk. This parameter is returned only if the value of parameter ReturnBindAutoSnapshotPolicy is TRUE when the API DescribeDisks is called. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| Tags | Array of [Tag](#Tag) | The tag that is bound to the cloud disk. If the cloud disk does not have tag bound, the value is null. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| DeleteWithInstance | Boolean | Whether the cloud disk is terminated with the instance it is mounted to. <br><li>true: When an instance is terminated, the cloud disk will be terminated at the same time. This is only supported for pay-as-you-go cloud disks. <br><li>false: The cloud disk is not terminated when the instance is terminated. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| DifferDaysOfDeadline | Integer | The number of days from the present time until the disk expires. This is only applicable for prepaid disks. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| Migrating | Boolean | Whether the cloud disk is undergoing a type change. Value range: <br><li>false: Indicates that the cloud disk is not undergoing a type change. <br><li>true: Indicates that the cloud disk has initiated a type change, and is undergoing migration. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| MigratePercent | Integer | The percentage of the migration process. Range: 0-100.<br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| Shareable | Boolean | Whether the cloud disk is a shared cloud disk |
| InstanceIdList | Array of String | For cloud disks that are not shared, this parameter is an empty array. For shared cloud disks, this indicates the InstanceId of the CVM instance to which the cloud disk is currently mounted. |

## DiskChargePrepaid

The billing method of an instance

Referenced by: CreateDisks, InquiryPriceCreateDisks, InquiryPriceRenewDisks, RenewDisk.

| Name | Type | Required | Description |
|------|------|----------|------|
| Period | Integer | Yes | The purchased usage period of a cloud disk (in months). Value range: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 24, 36. |
| RenewFlag | String | No | Auto Renewal flag. Value range: <br><li>NOTIFY_AND_AUTO_RENEW: Notify expiry and renew automatically <br><li>NOTIFY_AND_MANUAL_RENEW: Notify expiry but do not renew automatically <br><li>DISABLE_NOTIFY_AND_MANUAL_RENEW: Neither notify expiry nor renew automatically <br><br>Default value range: NOTIFY_AND_MANUAL_RENEW: Notify expiry but do not renew automatically. |
| CurInstanceDeadline | Timestamp | No | This parameter is used when you align the expiration time of the cloud disk with that of the mounted server. It is the current expiration time of the server. In this case, the Period passed represents the renewal period of the server, and the cloud disk will be automatically renewed in alignment with the expiration time of the renewed server. Example value: 2018-03-30 20:15:03. |

## DiskConfig

Cloud disk configuration.

Referenced by: DescribeDiskConfigQuota.

| Name | Type | Description |
|------|------|-------|
| Available | Boolean | Whether the configuration is available. |
| DiskType | String | Type of cloud disk medium. Value range: <br><li>CLOUD_BASIC: Ordinary cloud disk <br><li>CLOUD_PREMIUM: Premium cloud storage <br><li>CLOUD_SSD: SSD cloud disk. |
| DiskUsage | String | Cloud disk type. Value range: <br><li>SYSTEM_DISK: System disk <br><li>DATA_DISK: Data disk. |
| DiskChargeType | String | Billing method. Value range: <br><li>PREPAID: Prepaid <br><li>POSTPAID_BY_HOUR: Postpaid, that is, pay as you go. |
| MaxDiskSize | Integer | The maximum configurable cloud disk size (in GB). |
| MinDiskSize | Integer | The minimum configurable cloud disk size (in GB). |
| Zone | String | The [Availability Region](/document/product/213/15753#ZoneInfo) of the cloud drive. |
| DeviceClass | String | The instance type. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| InstanceFamily | String | Instance model series. For more information, see [Instance Models](https://cloud.tencent.com/document/product/213/11518). <br/>Note: This field may return ‘null’, indicating that no valid values are available. |

## DiskOperationLog

The operation log of the cloud disk.

Referenced by: DescribeDiskOperationLogs.

| Name | Type | Description |
|------|------|-------|
| Operator | String | The UIN of the operator. |
| Operation | String | The type of the operation. Value range: <br/>CBS_OPERATION_ATTACH: Mount a cloud disk. <br/>CBS_OPERATION_DETACH: Un-mount a cloud disk. <br/>CBS_OPERATION_RENEW: Renew. <br/>CBS_OPERATION_EXPAND: Expand. <br/>CBS_OPERATION_CREATE: Create. <br/>CBS_OPERATION_ISOLATE: Isolate. <br/>CBS_OPERATION_MODIFY: Modify the attributes of the cloud disk <br/>ASP_OPERATION_BIND: Bind an scheduled snapshot policy. <br/>ASP_OPERATION_UNBIND: Unbind an scheduled snapshot policy. |
| DiskId | String | System disk ID. |
| OperationState | String | The state of the operation. Value range: <br/>SUCCESS: Indicates that the operation has succeeded. <br/>FAILED: Indicates that the operation has failed. <br/>PROCESSING: Indicates that the operation is in progress. |
| StartTime | String | Start time |
| EndTime | String | End time |

## Filter

Key-value pair filters for conditional filtering queries.

Referenced by: DescribeAutoSnapshotPolicies, DescribeDiskOperationLogs, DescribeDisks, DescribeSnapshotOperationLogs, DescribeSnapshots.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | The name of the filter key. |
| Values | Array of String | Yes | One or more filter values. |

## Image

Image

Referenced by: DescribeSnapshots.

| Name | Type | Description |
|------|------|-------|
| ImageId | String | The ID of the image instance. |
| ImageName | String | The name of the image. |

## Placement

This describes the abstract location of the instance, including the availability zone in which it is located, the projects to which it belongs, and the ID and name of the dedicated clusters to which it belongs.

Referenced by: CreateDisks, DescribeDisks, DescribeSnapshots.

| Name | Type | Required | Description |
|------|------|----------|------|
| Zone | String | Yes | The ID of the [Availability Zone](/document/product/213/15753#ZoneInfo) to which the cloud disk belongs. This parameter can be obtained from the Zone field in the returned values of [DescribeZones](/document/product/213/15707). |
| ProjectId | Integer | No | ID of the project to which the instance belongs. This parameter can be obtained from the projectId field in the returned values of [DescribeProject](/document/api/378/4400). If this is left empty, default project is used. |
| CdcId | String | No | The ID of the dedicated cluster to which the instance belongs. As an input parameter, it indicates that the resources of the designated CdcId dedicated cluster are to be operated. It can be empty. As an output parameter, it indicates the ID of the dedicated cluster to which the resources belong. It can be empty. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| CageId | String | No | The cage ID. As an input parameter, it indicates that the resources of the specified CageId are to be operated. It can be empty. As an output parameter, it indicates the cage ID to which the resources belong. It can be empty. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| CdcName | String | No| The name of the dedicated cluster. Ignore as an input parameter. As an output parameter, it indicates the name of the dedicated cluster to which the cloud disk belongs. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |

## Policy

Describes the execution policy for scheduled snapshots.  that, on the days specified by DayOfWeek, the scheduled snapshot policy is executed at the hour specified by Hour.

Referenced by: CreateAutoSnapshotPolicy, DescribeAutoSnapshotPolicies, DescribeDiskAssociatedAutoSnapshotPolicy, ModifyAutoSnapshotPolicyAttribute.

| Name | Type | Required | Description |
|------|------|----------|------|
| DayOfWeek | Array of Integer | Yes | Specifies the days of the week, from Monday to Sunday, on which an scheduled snapshot will be triggered. Value range: [0, 6]. 0 indicates triggering on Sunday, 1-6 indicate triggering on Monday to Saturday. |
| Hour | Array of Integer | Yes | Specifies the time to trigger the scheduled snapshot policy. The value range is [0-23]. 00:00-23:00 is a total of 24 time points that can be selected. 1 indicates 01:00, and so on. |

## PrepayPrice

The cost of a prepaid order.

Referenced by: InquiryPriceRenewDisks, InquiryPriceResizeDisk.

| Name | Type | Description |
|------|------|-------|
| OriginalPrice | Float | Original price of the prepaid fees of a cloud disk or snapshot (in USD). |
| DiscountPrice | Float | Discounted price of the prepaid fees of a cloud disk or snapshot (in USD). |

## Price

Describes the prepaid or postpaid price for the cloud disk.

Referenced by: InquiryPriceCreateDisks.

| Name | Type | Description |
|------|------|-------|
| OriginalPrice | Float | The original price of the advance fees of a prepaid cloud disk (in USD). <br/>Note: This field may return null, indicating that no valid value was found.|
| DiscountPrice | Float | The discounted price of the advance fees of a prepaid cloud disk (in USD). <br/>Note: This field may return null, indicating that no valid value was found. |
| UnitPrice | Float | The original unit price of a postpaid cloud disk (in USD). <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| ChargeUnit | String | The charged unit price of a postpaid cloud disk (in USD). Value range: <br><li>HOUR: Indicates that the actual unit price for the postpaid cloud disk is calculated on an hourly basis. <br/>Note: This field may return null, indicating that no valid value was found. |
| UnitPriceDiscount | Float | The discounted unit price of a postpaid cloud disk. (in USD). <br/>Note: This field may return null, indicating that no valid value was found. |

## Snapshot

The details of a snapshot

Referenced by: DescribeSnapshots.

| Name | Type | Description |
|------|------|-------|
| SnapshotId | String | Snapshot ID. |
| Placement | [Placement](# placement) | The location of the snapshot. |
| DiskUsage | String | The type of the cloud disk used to create the snapshot. Value range: <br><li>SYSTEM_DISK: System disk <br><li>DATA_DISK: Data disk |
| DiskId | String | ID of the cloud disk used to create the snapshot. |
| DiskSize | Integer | Size of the cloud disk used to create the snapshot (in GB). |
| SnapshotState | String | Status of the snapshot. Value range: <br><li>NORMAL: Normal <br><li>CREATING: Creating <br><li>ROLLBACKING: Rolling backing <br><li>COPYING_FROM_REMOTE: Duplicating snapshot across regions |
| SnapshotName | String | Snapshot name, custom snapshot alias. Call [ModifySnapshotAttribute](/document/product/362/15650) to modify this field. |
| Percent | Integer | The percentage of progress for snapshot creation. This field is always 100 after the snapshot is created successfully. |
| CreateTime | Timestamp | Creation time of the snapshot. |
| DeadlineTime | Timestamp | Expiration time of the snapshot. If the snapshot is permanently retained, this field is empty. |
| Encrypt | Boolean | Whether the snapshot is created from a encrypted disk. Value range: <br><li>true: Yes <br><li>false: No |
| IsPermanent | Boolean | No | Whether it is a permanent snapshot. Value range: <br><li>true: Permanent snapshot <br><li>false: Non-permanent snapshot. |
| CopyingToRegions | Array of String | The target region for the cross-region replication of the snapshot. The default value is []. |
| CopyFromRemote | Boolean | Whether the snapshot is replicated from another region. Value range: <br><li>true: Yes, the snapshot is replicated from another region. <br><li>false: No, the snapshot belongs to the local region. |
| Images | Array of [Image](#Image) | The image list that the snapshot is associated with. |
| ImageCount | Integer | The number of images that the snapshot is associated with. |

## SnapshotOperationLog

The snapshot operation log.

Referenced by: DescribeSnapshotOperationLogs.

| Name | Type | Description |
|------|------|-------|
| Operator | String | The UIN of the operator. <br/>Note: This field may return ‘null’, indicating that no valid values are available. |
| Operation | String | The type of the operation. Value range: <br/>SNAP_OPERATION_DELETE: Deletes the snapshot. <br/>SNAP_OPERATION_ROLLBACK: Rolls back the snapshot. <br/>SNAP_OPERATION_MODIFY: Modifies the attributes of the snapshot. <br/>SNAP_OPERATION_CREATE: Creates a snapshot. <br/>SNAP_OPERATION_COPY: Replicates the snapshot across regions. <br/>ASP_OPERATION_CREATE_SNAP: Creates a snapshot by using the scheduled snapshot policy. <br/>ASP_OPERATION_DELETE_SNAP: Deletes a snapshot by using the scheduled snapshot policy. |
| SnapshotId | String | Snapshot ID. |
| OperationState | String | Operation status. Value range: <br/>SUCCESS: Indicates that the operation has succeeded. <br/>FAILED: Indicates that the operation has failed. <br/>PROCESSING: Indicates that the operation is in progress. |
| StartTime | String | Start time |
| EndTime | String | End time |

## Tag

Tag.

Referenced by: CreateDisks, DescribeDisks.

| Name | Type | Required | Description |
|------|------|----------|------|
| Key | String | Yes | Tag key. |
| Value | String | Yes | Tag value. |

