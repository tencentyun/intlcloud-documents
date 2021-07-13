CTSDB supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include:
>?CTSDB API operations not listed here do not support resource-level permissions. You can still authorize a user to perform such an API operation, but you must specify `*` as the resource element of the policy statement.

| API Name | Description | Six-Segment Example of Resource |
| ----------------------- | ------------------------ |---------------------------------------------------- |
| ModifyDBInstanceUserPassword | Modifies the user password of database instance   |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| DescribeDBInstances   | Queries instance list |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| InitDBInstance     | Initializes database instance |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| ModifyDBInstanceName     | Renames database instance |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| ModifyDBInstanceProject | Modifies the project of database instance         |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| RecycleDBInstance       | Repossesses database instance      |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| DescribeDBInstanceMetricInfo    | Queries the metric information of database instance     |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| DescribeDBInstanceMetricList  | Queries the metric list of database instance   |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |
| DescribeDBInstanceMetricQuery        | Queries the metric queries of database instance |  `qcs::ctsdb:$region:$account:instanceId/*`    `qcs::ctsdb:$region:$account:instanceId/$instanceId` |

