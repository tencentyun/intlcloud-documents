
### How is audit billed?
- Database Audit (except for finance regions) is billed by the amount of audit log storage at 0.00220588 USD/GB/hour.
- Fees are billed for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.
>?For TencentDB for MySQL instances in finance regions, you cannot add new audit policies currently. You can use existing policies normally. After the optimization of the audit policy feature for finance regions is completed, the audit feature in finance regions will be commercialized as a paid service. Please check the notices and pop-up messages in the console regularly to stay tuned.

### How do I disable audit?
Log in to the [console](https://console.cloud.tencent.com/dls/mysql/policy), click **Configure** on the **Audit Policy** page, and select **Disable SQL Audit**.
>!After it is disabled, the instance's audit policies, log records, and generated log files will be cleared and cannot be recovered. Please save the corresponding logs and files in advance.

### How long can audit data be retained?
Audit data can be retained for 30 days to 5 years. You can set the retention period when enabling audit in the [console](https://console.cloud.tencent.com/dls/mysql/policy). You can also click **Configure** on the **Audit Policy** page after enabling audit to make changes.
