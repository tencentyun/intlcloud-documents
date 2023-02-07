### How is audit billed?
Database audit is billed by the stored log size for every clock-hour, and usage duration shorter than one hour will be calculated as one hour. For more information, see [Database Audit Billing Overview](https://www.tencentcloud.com/document/product/1098/52146).

### How do I disable audit?
Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/dls/cynosdb/instance), find the target instance on the **Audit Instance** page, click the **Edit** icon after **Enabled**, toggle off database audit in the pop-up window, and click **Stop Audit**.

>!Once the service is disabled, the instance's audit policies, logs, and files will be cleared and cannot be recovered. You need to save the applicable logs and files in advance.

### How long can audit data be retained?
Audit data can be retained for seven days to five years. You can set the retention period when enabling audit in the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/dls/cynosdb/instance). You can also click **Configure** on the **Audit Log** page after enabling audit to make changes.
