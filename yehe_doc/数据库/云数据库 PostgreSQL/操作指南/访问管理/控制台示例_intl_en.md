## Overview
You can grant a user permissions to view and use specific resources in the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/postgres) by using Cloud Access Management (CAM) policies. This document provides examples to describe how to create and use such policies to grant these permissions.


## Directions
>!
>- To grant a user only the permissions of specific APIs, at least the permissions of the following APIs must be granted, or else the console fails to display correctly.
The sample code of `action` is as follows:
```
"action":  [
"postgres:DescribeProductConfig",
"postgres:InquiryPriceCreateDBInstances",
"postgres:DescribeRegions",
"postgres:DescribeZones"
]
```
>! To grant a user the permissions to monitor and view instances, the API permissions related to monitoring needs to be granted. The sample code of `action` is as follows:
```
{"effect": "allow",
"action":  [
"monitor:Get*",
"monitor:Describe*"
],
"resource": "*"
}
```

### Full read/write permission policy for PostgreSQL
To grant a user permissions to create and manage PostgreSQL instances, you can associate the `QcloudPostgreSQLFullAccess` policy with the user.
This policy grants the user permissions to operate all PostgreSQL resources. You can find more details below:
Associate the default policy `QcloudPostgreSQLFullAccess` with the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Read-only permission policy for PostgreSQL
To grant a user permissions to only view PostgreSQL instances, you can associate the `QcloudPostgreSQLReadOnlyAccess` policy with the user. Users assigned will not have the access to create, delete, or modify PostgreSQL instances.
This policy grants the user permissions of all PostgreSQL operations that begin with the word "Describe" or "Inquiry". The detailed steps are as follows:
Associate the default policy `PostgreSQL` with the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Policy for granting a user permissions to operate specific PostgreSQL instances
To grant a user permissions to operate specific PostgreSQL instances, you can associate the following policy with the user. The detailed steps are as follows:
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
   The example policy syntax is as follows. This example policy grants a user permissions of all operations on the PostgreSQL instance whose ID is "postgres-0xxxx8e".
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "postgres:*",
            "resource": "qcs::postgres:ap-shanghai:103xxx1481:DBInstanceId/postgres-0xxxx8e",
            "effect": "allow"
        }
    ]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.


### Policy for granting a user permissions to use all PostgreSQL resources
To grant a user permissions to use all PostgreSQL resources, you can associate the following policy with the user. The detailed steps are as follows:
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
   The example policy syntax is as follows. This example policy grants a user permissions to operate all PostgreSQL resources.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "postgres:*",
            "resource": "qcs::postgres:::*",
            "effect": "allow"
        }
    ]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.


### Policy for denying a user permissions to operate specific PostgreSQL instances
To deny a user permissions to operate specific PostgreSQL instances, you can associate the following policy with the user. The detailed steps are as follows:
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
   The example policy syntax is as follows. This example policy denies a user permissions to operate the PostgreSQL instances whose IDs are "postgres-c8xxxa4" and "postgres-d8xxxb4" respectively.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "postgres:*",
            "resource": [
						"qcs::postgres::16xxx472:DBInstanceId/postgres-c8xxxa4",
						"qcs::postgres::16xxx472:DBInstanceId/postgres-d8xxxb4",
						],
            "effect": "deny"
        }
    ]
}
```
2. Locate the created policy and click **Bind User/Group** in the "Operation" column.
3. In the pop-up window, select the user/group you want to authorize and click **OK**.

<span id="CAMCustomPolicy"></span>
### Custom policies
If preset policies do not meet your requirements, you can create custom policies as needed.
For detailed instructions, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
For more PostgreSQL-related policy syntax, see [Access Policy Syntax](https://intl.cloud.tencent.com/document/product/409/38835).

