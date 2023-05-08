Cloud Log Service (CLS) provides a one-stop log data solution. You can quickly and conveniently connect to it in five minutes to enjoy a full range of stable and reliable services from log collection, storage, and processing to search, analysis, consumption, shipping, dashboard generation, and alarming, with no need to care about resource issues such as scaling. It helps you improve the problem locating and metric monitoring efficiency in an all-around manner, making log Ops much easier.


## Overview

CLS has the following features.

- Log collection: CLS easily collects logs from different regions, channels, platforms, and data sources (e.g., various Tencent Cloud products) in real time.
- Log storage: CLS offers two storage types: real-time storage and STANDARD_IA storage.
- Log search and analysis: You can search for logs by keyword to quickly locate exception logs and use SQL statements to collect and analyze log statistics. This helps you get statistical metrics such as log quantity change trend over time and proportion of error logs.
- Log data processing: CLS can filter, cleanse, mask, enrich, distribute, and structure logs.
- Log shipping and consumption: CLS can ship logs to Tencent Cloud storage and middleware services and consume logs to stream computing services.
- Dashboard: CLS can quickly generate custom dashboards for search and analysis results.
- Alarming: CLS can trigger alarms for exception logs within seconds and notify you through phone, SMS, email, and custom API callback.

![](https://qcloudimg.tencent-cloud.cn/raw/eb15438795c5f95dc1e3454f05173bae.png)

### Log collection
CLS currently supports multiple methods for data collection, such as LogListener, API, Kafka, and COS import.
- LogListener real-time collection: Use LogListener to collect logs. This method is easy to install, reliable, and secure. It supports most mainstream Linux operating systems, delivering high performance while occupying few resources.
- Collection via API: Call the API to upload logs, without the need to install LogListener. Multiple programming languages are supported.
- Collection over Kafka: Upload logs to CLS by using the Kafka Producer SDK.
- COS import: Import COS data to CLS.

### Log storage
According to users' different requirements for log search latency and log processing capabilities, CLS provides two storage classes:
- Real-time storage: It is suitable for users who require statistical analysis and provides log search within seconds, real-time statistical analysis, real-time monitoring, streaming consumption, and other application capabilities.
- STANDARD_IA storage: It is suitable for infrequently accessed logs that do not require statistical analysis, such as archived audit logs. It provides the full-text log search capability, meeting users' requirements for backtracking and archiving historical logs. The overall usage costs of STANDARD_IA storage are 80% lower than those of real-time storage in the long run.

### Log search and analysis
CLS provides real-time log search and analysis to help you quickly locate exception logs and collect system and business metric statistics.
- Log search: Use keywords to search for logs by full text or field.
- Statistical analysis: Use SQL statements to flexibly collect the system and business metric statistics in logs and display them in charts. This feature is compatible with the SQL-92 standard and supports over 200 SQL functions. It can collect the number of business requests by province and query the request error rate change trend by time.
- Superior performance: Query results can be returned within seconds, and the search and analysis of hundreds of millions of logs are supported.

### Log data processing
- Real-time processing and distribution of log streams: Log streams are processed, and the processing result is generated in real time and can be distributed to multiple topics in different scenarios.
- Log filtering and cleansing: Dirty data is cleansed, logs are filtered by condition, and index is enabled, effectively reducing costs.
- Log structuring: Text logs are processed into structured data for future search, analysis, dashboard generation, and alarming.
- Log masking: Sensitive information in the log text is masked, such as mobile number and ID number.

### Log shipping and consumption
You can ship specified logs to other Tencent Cloud services, such as COS and CKafka. You can also consume CLS logs to Oceanus.
- Log shipping to COS: CLS allows you to ship logs to COS buckets under your account. COS storage is economical and recommended.
- Log shipping to CKafka: It is suitable for scenarios where CKafka is used as the source for data analysis and storage.
- Real-time log consumption: Logs are consumed directly to big data components such as Flink, Oceanus, and Flume.

### Dashboard
A dashboard is a global view of data analysis, where you can view multiple statistical charts of query and analysis results.
- Dashboards: Dashboards save multiple statistical charts of query and analysis results to form a comprehensive scenario-specific view.
- Preset dashboards: CLS provides preset dashboards for Tencent Cloud services such as CLB, TKE, and COS to make common monitoring capabilities out-of-the-box.
- Template variables: Template variables can be data source variables and quickly filtered to switch between statistical analysis objects and dimensions in the charts of dashboards. They can be added to support more complex business scenarios.

### Alarming
Alarms will be triggered within seconds in case of too many error logs or system and business metrics exceeding the threshold, to identify system and business exceptions.
- Notification channels: Notifications can be sent via phone, SMS, email, Weixin, WeCom, and custom API callback (which can be connected to DingTalk and Lark).
- Multi-dimensional analysis: When an alarm is triggered, raw logs can be further searched for and analyzed, and the result can be added to the alarm notification to facilitate root cause discovery.
