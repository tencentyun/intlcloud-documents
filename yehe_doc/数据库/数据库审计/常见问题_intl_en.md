
### How is audit billed?
Database audit is billed by the stored log size per clock-hour, and usage duration shorter than one hour is calculated as one hour. For billing details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1102/41313).

### How do I disable audit?
Log in to the [TencentDB for MySQL](https://console.cloud.tencent.com/dls/mysql/policy), [TDSQL-C for MySQL](https://console.cloud.tencent.com/dls/cynosdb/instance), or [TencentDB for MongoDB](https://console.cloud.tencent.com/dls/mongodb) console, click **Configure** on the **Audit Log** page, and select **Disable Audit**.
>!Once the service is disabled, the instance's audit policies, logs, and files will be cleared and cannot be recovered. You need to save the applicable logs and files in advance.

### How long can audit data be retained?
Audit data can be retained for seven days to five years. You can set the retention period when enabling audit in the [TencentDB for MySQL](https://console.cloud.tencent.com/dls/mysql/policy), [TDSQL-C for MySQL](https://console.cloud.tencent.com/dls/cynosdb/instance), or [TencentDB for MongoDB](https://console.cloud.tencent.com/dls/mongodb) console. You can also click **Configure** on the **Audit Log** page after enabling audit to make changes.
