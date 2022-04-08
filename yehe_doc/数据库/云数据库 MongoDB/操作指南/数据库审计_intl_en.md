You can activate the database audit service in the TencentDB for MongoDB console to use comprehensive data security diagnosis and management features.

## Background
Database audit is a professional, efficient, and comprehensive database audit service independently developed by Tencent Cloud for monitoring database security in real time. It can record the activities of TencentDB instances in real time, manage the compliance of database operations with fine-grained audit, and alert risky database behaviors such as SQL injections and exceptional operations, improving the security of your data assets. For more information, see [Database Audit Overview](https://intl.cloud.tencent.com/document/product/1102/41315).

## Version Requirement
Currently, only TencentDB for MongoDB 4.0 supports database audit.

## Billing
Database audit is billed by the amount of audit log storage for every clock-hour, and usage duration shorter than one hour will be calculated as one hour. For more information on billing, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1102/41313).

| Region               | Price (USD/GB/Hour) |
| :----------------- | :------------------- |
| China (including finance zones) | 0.00147059 |
| Other countries and regions | 0.00220588 |

## Notes
- After audit is enabled for pay-as-you-go TencentDB instances, when you release an instance, its corresponding audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.
- After audit is enabled for monthly subscribed TencentDB instances, when you release an instance or an instance is released upon expiration, its corresponding audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
### Viewing instance audit status
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **TencentDB for MongoDB** > **Database Audit** on the left sidebar.
3. Above the **Database Audit** page on the right, select the region.
4. In the top-right corner of the audit instance list, select an instance whose **Audit Status** is **Enabled**.
You can view the audit status, audit log retention duration, and log storage size of the instance.

### **Activating audit service**
1. In the top-right corner of the audit instance list, select an instance whose **Audit Status** is **Disabled**.
2. Enter the target instance ID or name in the search box to filter it out.
3. Click the target instance name to enter the **Audit Log** configuration page.
4. On the **Activate Audit Service** tab, view the audit billing description.
5. Click **I agree to the Tencent Cloud Terms of Service** and click **Next**.
6. On the **Audit Service Settings** tab, select an audit **log retention duration**, confirm the order, and click **Activate**.
7. Wait for the audit service to be activated and then you can use it.

### Viewing audit log
In the instance audit list on the **Audit Log** page, select an instance with the **Enabled** **Audit Status** to view its audit log retention duration and log storage size. You can also click instance ID to enter the **Audit Log** page and view audit logs. 

## More Operations
For more information on database audit operations, see [Authorizing Sub-account to Use Database Audit](https://intl.cloud.tencent.com/document/product/1102/41309).

