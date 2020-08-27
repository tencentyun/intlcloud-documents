TencentDB for DBbrain (DBbrain) is a cloud-based database management service for database performance, security, and management. By leveraging machine learning, big data, and expert experience engine, it can quickly replicate sophisticated practices of senior database administrators to automate a large number of traditional manual database OPS tasks, which helps ensure secure, stable, and efficient operations of your database services both in and off the cloud.

DBbrain operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------------|---------|-------------------------------------|
| Creating audit log analysis task             | dbbrain | CreateAuditLogStatsTask             |
| Creating health report analysis task             | dbbrain | CreateDBDiagReportTask              |
| CreateDBDiagReportUrl  | dbbrain | CreateDBDiagReportUrl               |
| Deleting audit log analysis task             | dbbrain | DeleteAuditLogStatsTask             |
| Deleting the analysis task of health diagnosis report            | dbbrain | DeleteDBDiagReportTasks             |
| Getting the timeline-based statistics of specified task | dbbrain | DescribeAuditLogSeriesForSqlTime    |
| Getting current task list               | dbbrain | DescribeAuditLogStatsTasks          |
| Getting the top SQLs of specified task         | dbbrain | DescribeAuditLogTopSqls             |
| Getting exception diagnosis event details             | dbbrain | DescribeDBDiagEvent                 |
| Getting instance exception diagnosis history             | dbbrain | DescribeDBDiagHistory               |
| Querying health diagnosis report               | dbbrain | DescribeDBDiagReport                |
| Getting instance performance curve data             | dbbrain | DescribeDBPerfTimeSeries            |
| Getting the space usage overview of specified time period          | dbbrain | DescribeDBSpaceStatus               |
| Getting health score details               | dbbrain | DescribeHealthScore                 |
| Getting health score curve               | dbbrain | DescribeHealthScoreTimeSeries       |
| Getting process list          | dbbrain | DescribeProcessList                 |
| Getting slow log histogram             | dbbrain | DescribeSlowLogTimeSeriesStats      |
| Getting the list of top SQLs of slow log          | dbbrain | DescribeSlowLogTopSqls              |
| Creating audit log analysis task             | dbbrain | DescribeSqlAdvice                   |
| Getting SQL execution plan              | dbbrain | DescribeSqlExplain                  |
| Getting the latest periodically captured space data of top databases      | dbbrain | DescribeTopSpaceSchemaLatestRecords |
| Getting the daily space usage statistics of specified time period of top databases | dbbrain | DescribeTopSpaceSchemaTimeSeries    |
| Getting the latest periodically captured space data of top tables      | dbbrain | DescribeTopSpaceTableLatestRecords  |
| Getting the statistics of top tables and sorting them in descending order by value    | dbbrain | DescribeTopSpaceTables              |
| Getting the daily space usage statistics of specified time period of top tables | dbbrain | DescribeTopSpaceTableTimeSeries     |
