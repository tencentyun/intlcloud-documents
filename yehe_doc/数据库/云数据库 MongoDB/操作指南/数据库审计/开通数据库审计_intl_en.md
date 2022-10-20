## Background
Database audit is a professional, efficient, and comprehensive database audit service independently developed by Tencent Cloud for monitoring database security in real time. It can record the activities of TencentDB instances in real time, manage the compliance of database operations with fine-grained audit, and alert risky database behaviors such as SQL injections and malicious acquisition of database/table information. It also provides complete security diagnosis and management features. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1102/41315).

### Audit rule

Audit modes include full audit and rule audit.

- Full audit: Records all the access statements and their executions in the database.
- Rule audit: Sets audit rules for attributes of the MongoDB database such as SQL operation statement, database name, collection name, client IP, and username, and then audits part of statements executed in the database accordingly.

### Rule operation

- The different fields in each rule add the conditions; that is, the relationship between field and condition is "AND" (&&).
- The relationship between rules is "OR" (||). You can specify one or more audit rules for an instance, and as long as any one of them is met, the instance should be audited. For example, if rule A specifies that only operations of user1 with an execution time >= 1 second need to be audited, and rule B audits the statements of user1 with an execution time < 1 second, then all statements of user1 need to be audited eventually.

## Version Description
Currently, only TencentDB for MongoDB 4.0 supports database audit.

## Billing
Database audit is billed by the amount of audit log storage for every clock-hour, and usage duration shorter than one hour will be calculated as one hour. For more information on billing, see [Billing Overview](https://www.tencentcloud.com/document/product/1102/49461).

| Region               | Price (USD/GB/Hour) |
| :----------------- | :----------------- |
| China (including finance zones) | 0.00147059 |
| Other countries and regions | 0.00220588 |

## Notes
- After database audit is enabled for a pay-as-you-go TencentDB instance, when you release the instance, its audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.
- After database audit is enabled for a monthly subscribed TencentDB instance, when you release the instance in advance or upon expiration, its audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. Select **TencentDB for MongoDB** > **Database Audit** on the left sidebar.
3. Above the **Database Audit** page on the right, select the region.
4. In the top-right corner of the audit instance list, select an instance with **Audit Status** being **Disabled**.
5. Click the search box and find the target instance by **Instance ID**, **Instance Name**, **Tag Key**, or **Tag** in the drop-down list.
6. Click the target instance name to enter the **Audit Log** configuration page.
7. On the **Enable Audit Service** wizard tab, view the audit billing description.
8. Click **I agree to the Tencent Cloud Terms of Service** and click **Next**.
9. On the **Audit Service Settings** wizard tab, select an **audit log retention period**, and confirm the fees to be paid after **Storage Fees**.
> ?You can select 7 days, 30 days, 3 months, 6 months, 1 year, 3 years, or 5 years as the audit log retention period. You can also modify it in the console after enabling audit. For more information, see [Modifying Audit Log Retention Period](https://www.tencentcloud.com/document/product/240/50656). In order to meet the security compliance requirements for the retention period of audit logs, we recommend you select 180 days or above.
> 
<img src="https://qcloudimg.tencent-cloud.cn/raw/92b9572fe47037db80619d0528deaee6.png" style="zoom:80%;" />
10. Click **Next**. On the **Audit Rule Settings** wizard tab, select the **Rule audit** mode after **Audit Rule**.
You can select **Full audit** (default option) or **Rule audit** as needed.
  - Full audit: Audits all statements when enabled. 
    ![](https://qcloudimg.tencent-cloud.cn/raw/db87cce6437fc99982cf8572c6a004f4.png)      
  - Rule audit: Audits database statements based on the configured audit items, including SQL type, database name, collection name, client IP, and username. Multiple items should be separated by comma.
<img src="https://qcloudimg.tencent-cloud.cn/raw/28f280a0cf61f00f3fa59ea96ac23ea8.png" style="zoom:80%;" />
11. Click **Create Policy**. Wait for the audit service to be enabled and then you can use it.

## More Operations
- For more information on database audit operations, see [Viewing Audit Log](https://intl.cloud.tencent.com/document/product/1102/47772).
- After the audit service is enabled, you can analyze database audit logs at any time for risk management. For detailed directions, see [Viewing Audit Log](https://www.tencentcloud.com/document/product/240/50658).
- As your business scenario changes, you need to adjust audit rules promptly to ensure efficient, accurate, and compliant audit of databases. For detailed directions, see [Modifying Audit Rule](https://www.tencentcloud.com/document/product/240/50657).
- You can [view audit instances](https://www.tencentcloud.com/document/product/240/50659), [disable audit instances](https://www.tencentcloud.com/document/product/240/50655), and [modify the audit log retention period](https://www.tencentcloud.com/document/product/240/50656).

