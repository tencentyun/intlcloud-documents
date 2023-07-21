### How do I view the monitoring data of a TencentDB for SQL Server instance?
TencentDB for SQL Server supports 38 common metrics of SQL Server. For more information, see [Monitoring Metrics](https://intl.cloud.tencent.com/document/product/238/46502). You can also collect statistics of other metrics by configuring the counters of SSMS.
You can view and stay up to date with instance conditions on monitoring charts as instructed in [Viewing Monitoring Charts](https://www.tencentcloud.com/document/product/238/46503). You can also [set alarm policies](https://intl.cloud.tencent.com/document/product/238/46501), [configure alarm notifications](https://intl.cloud.tencent.com/document/product/238/46500), and [view alarm records](https://intl.cloud.tencent.com/document/product/238/46499) in Tencent Cloud Observability Platform (TCOP) for 38 monitoring metrics about CPU, memory, storage, network, connection, access, and lock. For example, you can configure alarms in **Alarm Management** > **Policy Management** > **Create Policy** in the [TCOP console](https://console.cloud.tencent.com/monitor/alarm2/policy/create).

### Where can I view monitoring charts in TencentDB for SQL Server?
We provide a wide variety of performance monitoring metrics and convenient monitoring features (such as custom view, time comparison, and merged monitoring metrics). You can view and stay up to date with instance conditions by going to the **System Monitoring** page in the TencentDB for SQL Server console, as instructed in [Viewing Monitoring Charts](https://www.tencentcloud.com/document/product/238/46503).

### What monitoring metrics are supported by TencentDB for SQL Server?
TencentDB for SQL Server supports 38 common metrics of SQL Server. For more information, see [Monitoring Metrics](https://intl.cloud.tencent.com/document/product/238/46502). You can also collect statistics of other metrics by configuring the counters of SSMS.

### How do I set an alarm policy for TencentDB for SQL Server?
You can create an alarm policy in the TCOP console. An alarm will be triggered and notifications will be sent if the status of a monitoring metric of TencentDB for SQL Server becomes abnormal. For more information, see [Setting Alarm Policies](https://intl.cloud.tencent.com/document/product/238/46501).

### How do I associate an alarm policy with an alarm object in TencentDB for SQL Server?
You can create an alarm policy in the TCOP console and associate it with an alarm object. If the object meets the alarm trigger condition, an alarm will be triggered. For more information, see [Setting Alarm Policies](https://intl.cloud.tencent.com/document/product/238/46501).

[](id:SZGJTZ)
### How do I set alarm notifications for TencentDB for SQL Server?
After creating an alarm policy, you can configure an alarm notification template and alarm notifications in the TCOP console. After the configuration is completed, if an alarm is triggered by an exception, the system will send notifications to the recipients via the specified channels (email, SMS, and phone call). For more information, see [Setting Alarm Notification](https://intl.cloud.tencent.com/document/product/238/46500).

### How do I view alarm records in TencentDB for SQL Server?
You can view detailed alarm records in the console and quickly locate specific problems through alarm messages for further troubleshooting. For more information, see [Viewing Alarm Records](https://intl.cloud.tencent.com/document/product/238/46499).

### What is the minimum monitoring granularity in TencentDB for SQL Server?
The minimum monitoring granularity in TencentDB for SQL Server is 10 seconds, and the time range automatically changes with the granularity.

### Which monitoring metrics of a TencentDB for SQL Server instance should I stay up to date with?
You need to pay attention to the following monitoring metrics: CPU utilization, memory utilization, and percentage of remaining disk space. You can configure alarm notifications based on your actual business scenario, so that alarms will be triggered and notifications will be sent if the status of a monitoring metric of TencentDB for SQL Server becomes abnormal. When receiving an alarm, you can take applicable measures to resolve it. For more information, see [Setting Alarm Policies](https://intl.cloud.tencent.com/document/product/238/46501).
Sample configuration: If the CPU utilization reaches a certain value (such as 80%) for multiple times (such as five times) within a certain period of time (such as five minutes), an alarm will be triggered (once an hour, for example).
