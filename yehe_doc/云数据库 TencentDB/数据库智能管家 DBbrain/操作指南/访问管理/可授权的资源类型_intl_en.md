Resource-level permission is used to specify which resources a user can manipulate. DBbrain supports certain resource-level permissions. This means that for the TencentDB operations that support resource-level permission, you can control when a user is allowed to perform operations or what resources the user can use. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in the Authorization Policy |
| :-------- |:-------------- |
| TencentDB instance resources |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`

The table below lists the DBbrain API operations that currently support resource-level permission control as well as the resources and condition keys supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

>Any DBbrain API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

| API Operation | Resource Path |
| :------------------------------- | :----------------------------------------------------------- |
| DescribeSlowLogTopSqls           | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeSlowLogTimeSeriesStats   | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeDBDiagHistory            | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeDBDiagEvent              | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| CreateAuditLogStatsTask          | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeAuditLogStatsTasks       | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeAuditLogSeriesForSqlTime | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeAuditLogTopSqls          | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeAuditLogMetricRatio      | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DeleteAuditLogStatsTask          | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeDBSpaceStatus            | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeTopSpaceTables           | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeDBPerfTimeSeries         | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeSqlExplain               | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| CreateDiagUserInstances          | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DeleteDiagUserInstances          | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeProcessList              | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| CreateDBDiagReportTask           | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeDBDiagReportTasks        | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeDBDiagReport             | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DeleteDBDiagReportTasks          | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeSqlAdvice                | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeHealthScoreTimeSeries    | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| DescribeHealthScore              | `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId` |
| CreateDBDiagReportUrl|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
