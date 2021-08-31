
TDSQL-A for PostgreSQL supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

APIs supporting resource-level authorization include:
>?TDSQL-A for PostgreSQL API operations not listed here do not support resource-level permissions. You can still authorize a user to perform such an API operation, but you must specify `*` as the resource element of the policy statement.

| API Name | Description | Six-Segment Example of Resource |
| ----------------------- | ------------------------ |---------------------------------------------------- |
| DescribeAccounts        | Queries TencentDB instance account     |  `qcs::tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| DescribeBackupDetails   | Queries TencentDB instance backup details |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| DescribeBackupLists     | Queries TencentDB instance backup list |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| DescribeBackupRules     | Queries TencentDB instance backup rule |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| DescribeInstanceDetails | Queries instance details         |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| DescribeInstances       | Queries instance list                  |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| ModifyInstanceName    | Renames TencentDB instance     |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| ResetAccountPassword  | Resets TencentDB account password   |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |
| SetBackupRules        | Sets TencentDB instance backup rule |  `qcs:: tdapg:gz:uin/2113345772:instance/tdapg-i8edslnn` |

