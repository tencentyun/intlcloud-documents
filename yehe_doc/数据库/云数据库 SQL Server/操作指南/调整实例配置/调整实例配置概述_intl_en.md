TencentDB for SQL Server supports flexible scaling that allows you to quickly adjust instance architecture, version, and specification in the console. You can do so at any time (at the start, during rapid development, or during peak/off-peak hours), so you can get the most out of your resources and reduce unnecessary costs in real time.

## Prerequisites
- You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in running status and are not executing any tasks.

## Adjustment item
| Adjustment Item | Description |
|---------|---------|
| Architecture | a. Single-node (formerly Basic Edition) instances cannot be upgraded to two-node (formerly High Availability/Cluster Edition) instances. If needed, you can purchase new two-node instances and [migrate the data with DTS](https://www.tencentcloud.com/document/product/238/39006). |
| Version | a. Both single-node (formerly Basic Edition) and two-node (formerly High Availability/Cluster Edition) instances support version upgrade. <br>b. To upgrade the version of a two-node (formerly High Availability/Cluster Edition) instance associated with a read-only instance, disassociate the read-only instance first before upgrading or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. |
| Instance specification | a. All instance types support specification upgrade and downgrade. <br>b. The upper limit of disk capacity under the corresponding specification is as displayed on the **Adjust Configuration** page in the console. |
| Disk capacity | a. Two-node (formerly High Availability/Cluster Edition) instances of local disk edition support disk capacity expansion and reduction. <br>b. Two-node (formerly High Availability/Cluster Edition) instances of cloud disk edition support disk capacity expansion but not reduction. <br>c. Single-node (formerly Basic Edition) instances support disk capacity expansion but not reduction. |

>?If you need to horizontally scale the read capability of your database, use read-only instances to mitigate the pressure on the primary instance as instructed in [Managing Read-Only Instance](https://www.tencentcloud.com/document/product/238/43143).

## Restrictions on upgrade/downgrade

<table>
<thead><tr><th>Instance Type</th><th>Disk Type</th><th>Version Upgrade</th><th>Architecture Upgrade</th><th>Specification Upgrade</th><th>Disk Capacity Expansion</th><th>Version Downgrade	</th><th>Architecture Downgrade</th><th>Specification Downgrade</th><th>Disk Capacity Reduction</th></tr></thead>
<tbody>
<tr>
<td>Single-node (formerly Basic Edition) instance</td><td>Cloud disk</td><td>&#10003;</td><td>X</td><td>&#10003;</td><td>&#10003;</td><td>X</td><td>X</td><td>&#10003;</td><td>X</td></tr>
<tr>
<td rowspan="2">Two-node (formerly High Availability/Cluster Edition) instance</td>
<td>Local disk</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>X</td><td>X</td><td>&#10003;</td><td>&#10003;</td></tr>
<td>Cloud disk</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>X</td><td>X</td><td>&#10003;</td><td>X</td></tr>	
<tr>
<td rowspan="2">Read-only instance</td>
<td>Local disk</td><td>X</td><td>X</td><td>&#10003;</td><td>&#10003;</td><td>X</td><td>X</td><td>&#10003;</td><td>&#10003;</td></tr>
<td>Cloud disk</td><td>X</td><td>X</td><td>&#10003;</td><td>&#10003;</td><td>X</td><td>X</td><td>&#10003;</td><td>X</td></tr>

</tbody></table>	

## Instance disk space description
- **Two-node (formerly High Availability/Cluster Edition) instance - local disk**
When the size of the data stored in an instance exceeds its storage space, features such as database import and rollback will become unavailable. You will need to expand its capacity or delete some database tables in the console to release the storage space. We recommend that you check the disk monitoring metrics of the instance in time as instructed in [Viewing Monitoring Charts](https://intl.cloud.tencent.com/document/product/238/46503) and [set the alarm policy](https://intl.cloud.tencent.com/document/product/238/46501) for the disk in CM, so as to prevent disk overruns from affecting your business operations.
- **Two-node (formerly High Availability/Cluster Edition) instance - cloud disk**
When the size of the data stored in an instance exceeds its storage space, the database will become read-only. We recommend that you check the disk monitoring metrics of the instance in time as instructed in [Viewing Monitoring Charts](https://intl.cloud.tencent.com/document/product/238/46503), [set the alarm policy](https://intl.cloud.tencent.com/document/product/238/46501) for the disk in CM, and expand the storage space or delete tables in the console promptly, so as to prevent the read-only status from affecting your business operations. The instance will become readable/writable after your expand or free up the storage space.
- **Single-node (formerly Basic Edition) instance - cloud disk**
When the size of the data stored in an instance exceeds its storage space, the database will become read-only. We recommend that you check the disk monitoring metrics of the instance in time as instructed in [Viewing Monitoring Charts](https://intl.cloud.tencent.com/document/product/238/46503), [set the alarm policy](https://intl.cloud.tencent.com/document/product/238/46501) for the disk in CM, and expand the storage space or delete tables in the console promptly, so as to prevent the read-only status from affecting your business operations. The instance will become readable/writable after your expand or free up the storage space.

## Configuration adjustment rules
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for SQL Server instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the TencentDB for SQL Server instance may be disconnected for seconds). We recommend that you use applications configured with automatic reconnection feature and conduct the switch during the instance maintenance time. For more information, see [Setting Instance Maintenance Information](https://intl.cloud.tencent.com/document/product/238/35785).

## Limits
As a single-node (formerly Basic Edition) instance has only one database node and no secondary node as a hot backup, when the node fails or performs tasks such as configuration adjustment and version upgrade, it will become unavailable for a long time. If your business has high requirements for the database availability, we recommend that you use two-node (formerly High Availability/Cluster Edition) instances instead.

## Billing
For more information, see [Instance Adjustment Fees Description](https://intl.cloud.tencent.com/document/product/238/35799).

## Directions
- [Adjusting Instance Architecture](https://intl.cloud.tencent.com/document/product/238/44353)
- [Adjusting Instance Version](https://intl.cloud.tencent.com/document/product/238/44354)
- [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783)
