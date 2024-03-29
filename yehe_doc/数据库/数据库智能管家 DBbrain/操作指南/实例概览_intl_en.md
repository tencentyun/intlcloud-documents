The instance overview page displays the summary of your instances, which is customizable. You can view information such as task execution, region distribution, real-time performance, and health assessment of all connected instances.

>?Currently, instance overview is supported only for TencentDB for MySQL (excluding basic single-node instances), TDSQL-C for MySQL, TencentDB for Redis, self-built MySQL, and TencentDB for MongoDB.
>

Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/board), select **Instance Overview** on the left sidebar, and select a database on the right. You can view **Real-Time** and **Historical** data of all regions or a specific region.

## Recommended Features
The navigation bar at the top highlights popular features recommended by DBbrain. You can quickly access the details of the corresponding feature.

#### Self-built instance access
The self-built database instance access page displays the number of self-built database instances that access the DBbrain service through the Agent and direct connection under the current account. You can click **Quick Access** to redirect to the self-built database instance access page.

## Custom Settings
DBbrain provides custom settings. Click **Custom Settings** to enter the instance management page, select the instances to be displayed, and configure them. For more information, see [Instance Management](https://intl.cloud.tencent.com/document/product/1035/36033).

## Exception Alarming
DBbrain's 24/7 exception diagnosis module can detect problems in database instances in real time and provide optimization plans accordingly. This module displays the total number of exception alarms in the last 3 hours and in the last 24 hours. You can click to access the exception alarm page and view more details.

## Health Rankings
DBbrain periodically performs health checks on all instances and scores them accordingly. On this page, you can view the health scores (current and historical) of all instances. You can click an instance to access the exception diagnosis page and view more details.

## Monitoring Status Rankings
The resource consumption rankings of selected monitoring metrics are displayed. You can click an instance to view details about its exception diagnosis.
- MySQL metrics: CPU, memory, disk utilization, TPS, QPS, number of slow queries, connected threads, and running threads.
- TDSQL-C metrics: CPU, memory, storage utilization, TPS, QPS, number of slow queries, connected threads, and running threads.
- Redis metrics: CPU utilization, memory utilization, connection utilization, inbound traffic utilization, outbound traffic utilization, and read request hit rate.
