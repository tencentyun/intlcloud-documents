### Which configuration items can I adjust in TencentDB for SQL Server?
TencentDB for SQL Server supports quick adjustment of the instance architecture, version, and specification and allows flexible scaling operations in the console. You can elastically adjust the configurations of SQL Server instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/238/44352).

### Can I expand/reduce the disk space of a TencentDB for SQL Server instance?
- TencentDB for SQL Server two-node (formerly high-availability/cluster edition) local disk instance: The disk space can be expanded and reduced.
- TencentDB for SQL Server two-node (formerly high-availability/cluster edition) cloud disk instance: The disk space can only be expanded.
- TencentDB for SQL Server single-node (formerly basic edition) instance: The disk space can only be expanded.

### Can I upgrade/downgrade the CPU/memory specifications of a TencentDB for SQL Server instance?
Yes. For more information, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783).

### Is the service still available when the specification of a TencentDB for SQL Server single-node (formerly basic edition) instance is changed?
When the configuration of a single-node (formerly basic edition) instance is adjusted (CPU/memory specification upgrade/downgrade as well as disk space expansion), the instance will be restarted and remain unavailable for about three minutes. Therefore, perform this operation during off-peak hours.

### Will the service be interrupted when the specification of a TencentDB for SQL Server two-node (formerly high-availability/cluster edition) is changed?
- During **specification upgrade or disk space expansion** of a two-node (formerly high-availability edition) instance, if in-place update conditions are met, the service will not experience any momentary disconnections, and the configuration will take effect immediately after the request is submitted without causing any impact on the business. If migration update conditions are met, the configuration will be upgraded by migrating data. The more the data, the longer the migration. During the migration, the instance can still be accessed. After the migration is completed, a switch will occur, causing a momentary database disconnection. Therefore, your business should have a reconnection mechanism. During the disconnection, most database, account, and network operations cannot be performed. Switch during off-peak hours.
- During **disk space reduction** in a two-node (formerly high-availability/cluster edition) instance, the service will not experience any momentary disconnections. The adjustment will take effect immediately after you submit the request. There is no impact on your business.
- During **specification downgrade** in a two-node (formerly high-availability/cluster edition) instance, the instance will be restarted and remain unavailable for about one minute. Therefore, perform this operation during off-peak hours.

For more information on configuration adjustment scenarios and impacts, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/238/35783).

[](id:KRGGSJLC)
### How do I perform disk space expansion/reduction and specification upgrade/downgrade in TencentDB for SQL Server?
**Disk space expansion/reduction and specification upgrade/downgrade** refer to changing the current TencentDB for SQL Server instance from specification A to specification B. In the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the target instance and click **Adjust Configuration** in the **Operation** column. In the **Adjust Configuration** pop-up window, select the target specification and time to take effect as needed and make the payment. Then, the system will automatically change the instance specification. For more information, see [Adjusting Instance Specification](https://www.tencentcloud.com/document/product/238/35783).

### How are TencentDB for SQL Server disk space expansion/reduction and specification upgrade/downgrade fees calculated?
For a pay-as-you-go instance:
- Upgrade fees: After upgrade, the instance will be billed based on the new instance specifications starting from the next billing cycle.
- Downgrade fees: After downgrade, the instance will be billed based on the new instance specifications starting from the next billing cycle.
For more information, see [Instance Adjustment Fees Description](https://intl.cloud.tencent.com/document/product/238/35799).

### Will the read-only instance configuration be upgraded automatically when the primary instance configuration is upgraded?
Read-only instances can only be upgraded manually.
