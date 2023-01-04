## Overview
Monitoring and alarm are important features to help you maintain your database and provide reliability, availability, and performance support to troubleshooting. Monitoring enables you to stay on top of the resource utilization, performance, and status of TDSQL-C for MySQL, while alarm keeps you informed of database exceptions, so you can handle them promptly. Ultimately, this increases the system stability, improves the Ops efficiency, and reduces Ops costs.

The TDSQL-C for MySQL console has a visual **Monitoring and Alarms** page, which offers a wide variety of performance monitoring metrics and convenient monitoring features. As soon as any business exception occurs, alarm messages will be pushed to you according to the alarm rules you set. In this way, you can stay up to date with your database status, performance, and resource usage comprehensively, with no additional development required.


## Concepts
**Metric**
Metric is a fundamental concept in CM. A metric represents a time-ordered set of data points sent to CM, such as CPU utilization and memory utilization. You can retrieve the statistics of those data points in time series. A metric can be seen as a variable to monitor, and the data points represent the values of the variable over time.

**Unit**
Unit refers to the measurement unit of the raw metric data; for example, the unit of CPU utilization is %.

**Time granularity**
Time granularity refers to a statistical period in CM. Timestamp data represents the result of aggregating all the data collected in the specified time granularity.

**Alarm**
Alarm management is a feature in the Cloud Monitor Alarm service. It triggers alarms for exceptions of Tencent Cloud resources and allows you to view alarm messages, customize alarm thresholds, and subscribe to alarms.

## Supported monitoring types

| Supported Monitoring Type | Description |
|---------|---------|
| Instance | Read-write and read-only instances can be monitored. |
| Database proxy | Database proxy nodes can be monitored. For more information, see [Viewing Database Proxy Monitoring Data](https://www.tencentcloud.com/document/product/1098/49995). |


## Monitoring granularities
In TDSQL-C for MySQL, the monitoring time granularity is automatically adjusted based on the monitoring time range as follows:

| Query Time Range | Time Between Query Start Time and Current Time | Default Time Granularity | Optional Time Granularities |
|-------|-------|--------|----|
| (0h, 1h]   | (0d, 1d]     | 5s | 5s/1min/5min | 
| (0h, 1h]   | (1d, 15d]   | 1min | 1min/5min | 
| (0h, 1h]   | (15d, 31d]  | 5min | 5min |
| (1h, 24h] | (0d, 15d]    | 1min | 1min/5min/1h |
| (1h, 24h] | (15d, 31d]   | 5min | 5min/1h |
| (24h, 7d] | (0d, 31d]     | 5min | 5min/1h/1d |
| (7d, 31d] | (0d, 31d]    | 1h | 1h/1d | 

>?Currently, you can view monitoring data of TDSQL-C for MySQL in the past 31 days.

## Monitoring metrics
TDSQL-C for MySQL offers a rich set of monitoring metrics to help you better track your database resource utilization, performance, and status. For more information, see [Supported Monitoring Metrics](https://www.tencentcloud.com/document/product/1098/50193).

