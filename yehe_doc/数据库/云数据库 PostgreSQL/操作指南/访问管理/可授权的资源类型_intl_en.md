
## Resource-Level Permission Overview
Resource-level permissions specify resources a user can operate. TencentDB for PostgreSQL supports specific resource-level permissions, i.e., allowing the user to perform operations or use specific resources.
In Cloud Access Management (CAM), the types of PostgreSQL resources that can be authorized are as follows:

| Resource Type                       | Resource Description Method in Access Policies                                     |
| :----------------------------- | ------------------------------------------------------------ |
| [Instance](#PostgreSQLCorrelation) | ` qcs::postgres:$region:$account:DBInstanceId/$DBInstanceId ` <br>` qcs::postgres:$region:$account:DBInstanceId/*  ` |

The [PostgreSQL instance APIs](#PostgreSQLCorrelation) section in this document describes PostgreSQL API operations that currently support resource-level permissions as well as resources and condition keys supported by each operation. When configuring the resource path, you need to replace values of the parameters such as `$region` and `$account` with your actual values. You can also use the wildcard (*) in the path. For more information, please see [Console Examples](https://intl.cloud.tencent.com/document/product/409/38837).

>!For a PostgreSQL API operation that does not support authorization at the resource level, you can still authorize a user to perform the operation. In this case, you must specify `*` as the resource element in the policy statement.

## List of APIs Not Supporting Resource-Level Permissions
| API Operation               | API Description                  |
| :---------------------------- | :------------------- |
| CreateDBInstances             | Creates an instance             |
| CreateServerlessDBInstance    | Creates a PostgreSQL for Serverless instance |
| DescribeOrders                | Obtains order information         |
| DescribeRegions               | Queries available regions         |
| DescribeZones                 | Queries available availability zones       |
| DescribeProductConfig         | Queries product specifications     |
| InquiryPriceCreateDBInstances | Queries prices         |
| DescribeServerlessDBInstances  | Queries the list of PostgreSQL for Serverless instances|


## List of APIs Supporting Resource-Level Permissions
<span id ="PostgreSQLCorrelation"></span>
### [PostgreSQL instance APIs]
**PostgreSQL for Serverless instance APIs**

| API Name                        | API Description                 |
| ------------------------------- | ------------------------ |
| CloseServerlessDBExtranetAccess | Disables the public network access for a PostgreSQL for Serverless instance |
| DeleteServerlessDBInstance      | Deletes a PostgreSQL for Serverless instance     |
| OpenServerlessDBExtranetAccess  | Enables the public network access for a PostgreSQL for Serverless instance |

**Backup and restoration APIs**

| API Name           | API Description         |
| ------------------ | ---------------- |
| DescribeDBBackups  | Queries the list of instance backups |
| DescribeDBErrlogs  | Obtains error logs     |
| DescribeDBSlowlogs | Obtains slow query logs   |
| DescribeDBXlogs    | Obtains the Xlog list |

**Instance APIs**

| API Name                      | API Description           |
| ----------------------------- | ------------------ |
| CloseDBExtranetAccess         | Disables the public network address for an instance   |
| DescribeDBInstanceAttribute   | Queries instance details       |
| DescribeDatabases             | Pulls the instance list     |
| DestroyDBInstance             | Terminates an instance           |
| InitDBInstances               | Initializes an instance         |
| InquiryPriceRenewDBInstance   | Queries the instance renewal price   |
| InquiryPriceUpgradeDBInstance | Queries the instance upgrade price   |
| ModifyDBInstanceName          | Modifies the instance name       |
| ModifyDBInstancesProject      | Transfers an instance to another project |
| OpenDBExtranetAccess          | Enables public network access           |
| RenewInstance                 | Renews an instance           |
| RestartDBInstance             | Restarts an instance           |
| SetAutoRenewFlag              | Sets auto-renewal       |
| UpgradeDBInstance             | Upgrades an instance           |
| DescribeDBInstances            | Queries the instance list|

**Account APIs**

| API Name                      | API Description           |
| -------------------- | ---------------- |
| DescribeAccounts     | Obtains the list of instance users |
| ModifyAccountRemark  | Modifies the account password     |
| ResetAccountPassword | Resets the account password     |
