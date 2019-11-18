

Log topic is a basic management unit of the Cloud Log Service (CLS). A [logset](https://intl.cloud.tencent.com/document/product/614/35676) can contain multiple log topics. A log topic corresponds to a project or application. It is recommended to collect logs of the same type from different servers under the same log topic. For example, a business project may have 3 types of logs, operation logs, application logs, and access logs. You should create a log topic for each log type.

The CLS system manages different log data based on each log topic. Each log topic can be configured with different data sources, index rules, and shipping rules. Therefore, log topic is the basic unit for configuring and managing log data on the CLS system. You need to configure corresponding rules after creating a log topic to perform log collection, search, analysis, and shipping.

In terms of functions, the log topic service can:

- Collect logs to log topics.
- Store and manage logs based on log topics.
- Search and analyze logs by log topics.
- Ship logs to other platforms based on log topics.
- Download and consume logs from log topics.

