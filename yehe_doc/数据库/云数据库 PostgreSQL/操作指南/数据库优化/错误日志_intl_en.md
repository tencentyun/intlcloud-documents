## Overview
Error logs refer to logs generated due to operation, SQL, and system errors during database running. Error logs are usually used by developers to find out the causes of errors in business systems or databases.

You can log in to the TencentDB for PostgreSQL console, click an instance ID/name in the instance list to access the instance management page, and select the **Performance Optimization** tab to view error logs as shown below.
![](https://main.qcloudimg.com/raw/4af3667ea509689c4f795b879f777ebe.png)


## Error Log Default Configurations
- Error log feature: enabled by default.
- Error log level: `log_min_error_statement=ERROR`.
- Analyzed data output delay: 1–5 minutes.
- Log retention period: 7 days (up to the last 10,000 records).
