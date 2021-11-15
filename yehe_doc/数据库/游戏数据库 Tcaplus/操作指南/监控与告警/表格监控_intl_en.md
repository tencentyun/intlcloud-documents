To help you view and stay up to date with TcaplusDB running information, TcaplusDB provides various performance monitoring metrics. It supports table monitoring and offers an independent monitoring view for each table for easy query.
You can log in to the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/table), click a table ID to enter the table management page, and enter the **Table Monitoring** tab to view the monitoring view.

>
>- You can also get instance monitoring metrics by calling the TcaplusDB monitoring data API in Cloud Monitor.
>- Currently, you can view the monitoring data of TcaplusDB for the last 60 days.

## Table Monitoring Metrics
Tencent Cloud Monitor provides the following monitoring metrics for TcaplusDB tables:

| Metric Name | Parameter | Description | Unit |
| ----------------- | ---------------- | ------------------------------------------------------------ | -------- |
| Average error rate | Average Error Rate | Average percentage of table operation errors | % |
| General error rate | General Error Rate | Percentage of general table operation errors | % |
| Actual read capacity units | Actual Read Capacity Units | Number of actual read capacity units of table | Unit/s |
| Average read latency | Average Read Latency | Average latency in data read | us |
| System error rate | System Error Rate | Percentage of system errors | % |
| Storage capacity | Storage Capacity | Storage capacity used by table | KB |
| Average write latency | Average Write Latency | Average latency in data write | us |
| Actual write capacity units | Actual Write Capacity Units | Number of actual write capacity units of table | Unit/s |
