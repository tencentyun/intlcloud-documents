TencentDB for SQL Server supports quick adjustment of instance architecture, version, and specification and allows flexible scaling operations in the console. You can elastically adjust the instance configuration according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

## Prerequisites
You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in normal status (Running) and are not executing any tasks.

## Adjustment Item
| Adjustment Item | Description |
|---------|---------|
| Architecture | a. High-Availability Edition can be upgraded to Cluster Edition. <br>b. Basic Edition cannot be upgraded to High-Availability Edition/Cluster Edition. If needed, you can purchase new High-Availability Edition/Cluster Edition instances and [migrate the data with DTS](https://intl.cloud.tencent.com/document/product/238/39006). |
| Version | a. High-Availability Edition supports version upgrade. <br>b. To upgrade the version of a High-Availability Edition/Cluster Edition instance associated with a read-only instance, [submit a ticket](https://console.cloud.tencent.com/workorder/category). |
| Instance specification | a. All instance types support specification upgrade and downgrade. <br>b. The upper limit of disk capacity under the corresponding specification is as displayed on the **Adjust Configuration** page in the console. |
| Disk capacity | a. High-Availability Edition/Cluster Edition instances support disk capacity expansion/reduction.<br/>b. Basic Edition instances support disk capacity expansion but not reduction. |

>?If you need to horizontally scale the read capability of your database, use read-only instances to mitigate the pressure on the primary instance as instructed in [Managing Read-Only Instance](https://intl.cloud.tencent.com/document/product/238/43143).

## Restrictions on Upgrade/Downgrade
| Instance Type | Version Upgrade | Architecture Upgrade | Specification Upgrade | Disk Capacity Expansion | Version Downgrade | Architecture Downgrade | Specification Downgrade | Disk Capacity Reduction |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
| Basic Edition instance | X | X |   &#10003; |  &#10003; | X  | X  |  &#10003;  | X  |
| High-Availability Edition instance |  &#10003; |  &#10003; |  &#10003; |  &#10003; | X  | X  |  &#10003;  |  &#10003;  |
| Cluster Edition instance | X | X |   &#10003; |   &#10003; | X  | X  |  &#10003;  | &#10003;  |
| Read-Only instance | X| X |   &#10003; |  &#10003; | X  | X  |  &#10003;  |  &#10003;  |
| High-Availability/Cluster Edition instance associated with read-only instance | Submit a ticket | Submit a ticket |  Submit a ticket |  Submit a ticket | X  | X  | Submit a ticket  |  Submit a ticket |

## Instance Disk Space Description
- To ensure business continuity, upgrade your instance specifications or purchase additional disk capacity in time before disk capacity is used up.
- When the size of the data stored in a High-Availability Edition/Cluster Edition instance exceeds its disk capacity, features such as database import and rollback will become unavailable. You will need to expand its capacity or delete some database tables in the console to release the storage space.
- When the size of the data stored in a Basic Edition instance exceeds its disk capacity, the database will become read-only. You will need to expand its capacity or delete some database tables in the console to release the storage space and make it writable.

## Configuration Adjustment Rules
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of the instance remain unchanged after configuration adjustment.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for SQL Server instance can be accessed normally and the business will not be affected.
- Instance switch may be involved after the configuration adjustment is completed (i.e., the SQL Server instance may be disconnected for seconds). We recommend you configure an automatic reconnection feature for your application. Instance switch will be performed during the instance maintenance time. For more information, see [Setting Instance Maintenance Information](https://intl.cloud.tencent.com/document/product/238/35785).

## Notes
As a Basic Edition instance has only one database node and no secondary node as a hot backup, when the node fails or performs tasks such as configuration adjustment and version upgrade, it will become unavailable for a long time. If your business has high requirements for the database availability, we recommend you use High-Availability Edition or Cluster Edition instead of Basic Edition.

## Billing Rule
For more information, see [Instance Adjustment Fees Description](https://intl.cloud.tencent.com/document/product/238/35799).

## Directions
- [Adjusting Instance Architecture](https://intl.cloud.tencent.com/document/product/238/44353)
- [Adjusting Instance Version](https://intl.cloud.tencent.com/document/product/238/44354)
- [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783)
