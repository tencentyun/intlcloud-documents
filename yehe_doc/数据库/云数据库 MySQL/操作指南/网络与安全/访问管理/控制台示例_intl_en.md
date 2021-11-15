
This document provides examples about how to grant a user permissions to view and use specific resources in the TencentDB console by using a CAM policy.

## Full Access Policy for TencentDB
To grant a user permissions to create and manage TencentDB instances, implement the QcloudCDBFullAccess policy for the user.

Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), select **Policies** on the left sidebar, and search QcloudCDBFullAccess in the upper right corner.
![](https://main.qcloudimg.com/raw/5ec89e71595a5edd3e7f723a19c01a6a.png)
The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:*"
            ],
            "resource": "qcs::cvm:::sg/*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        },
        {
            "action": [
                "kms:CreateKey",
                "kms:GenerateDataKey",
                "kms:Decrypt",
                "kms:ListKey"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
The above CAM policy syntax grants the user permissions to use all the resources of TencentDB, VPC, security groups, COS, KMS, and Cloud Monitor.

## Read-only Permission Policy for TencentDB
To grant a user permissions to view TencentDB instances but not create, delete, or modify them, implement the QcloudCDBInnerReadOnlyAccess policy for the user.

>?You are recommended to configure the read-only policy for TencentDB.

Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), select **Policies** on the left sidebar, click **Service Type** in the policy list and select **TencentDB for MySQL** in the drop-down list, and then you can see this policy in the results.

The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Read-only Permission Policy for TencentDB-related Resources
To grant a user permissions to view TencentDB instances and related resources (VPC, security groups, COS, and Cloud Monitor) but not create, delete, or modify them, implement the QcloudCDBReadOnlyAccess policy for the user.

Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), select **Policies** on the left sidebar, click **Service Type** in the policy list and select **TencentDB for MySQL** in the drop-down list, and then you can see this policy in the results.

The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:DescribeSecurityGroup*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```
The above CAM policy syntax grants the user permissions of the following operations:
- All operations in TencentDB that begin with "Describe".
- All operations in VPC that begin with "Describe", "Inquiry", or "Get".
- All operations in security groups that begin with "DescribeSecurityGroup".
- All operations in COS that begin with "List", "Get", and "Head" as well as the "OptionsObject" operation.
- All operations in the Cloud Monitor.

## Policy for Granting a User Permissions to Use APIs not at the Resource Level
To grant a user permissions to use only APIs not at the resource level, implement the QcloudCDBProjectToUser policy for the user.
Log in to the [CAM console](https://console.cloud.tencent.com/cam/policy), select **Policies** on the left sidebar, click **Service Type** in the policy list and select **TencentDB for MySQL** in the drop-down list, and then you can see this policy in the results.
The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:BalanceRoGroupLoad",
                "cdb:CancelBatchOperation",
                "cdb:CreateBatchJobFiles",
                "cdb:CreateDBInstance",
                "cdb:CreateDBInstanceHour",
                "cdb:CreateMonitorTemplate",
                "cdb:CreateParamTemplate",
                "cdb:DeleteBatchJobFiles",
                "cdb:DeleteMonitorTemplate",
                "cdb:DeleteParamTemplate",
                "cdb:DescribeBatchJobFileContent",
                "cdb:DescribeBatchJobFiles",
                "cdb:DescribeBatchJobInfo",
                "cdb:DescribeProjectSecurityGroups",
                "cdb:DescribeDefaultParams",
                "cdb:DescribeMonitorTemplate",
                "cdb:DescribeParamTemplateInfo",
                "cdb:DescribeParamTemplates",
                "cdb:DescribeRequestResult",
                "cdb:DescribeRoGroupInfo",
                "cdb:DescribeRoMinScale",
                "cdb:DescribeTasks",
                "cdb:DescribeUploadedFiles",
                "cdb:ModifyMonitorTemplate",
                "cdb:ModifyParamTemplate",
                "cdb:ModifyRoGroupInfo",
                "cdb:ModifyRoGroupVipVport",
                "cdb:StopDBImportJob",
                "cdb:UploadSqlFiles"
            ],
            "effect": "allow",
            "resource": "*"
        }
    ]
}
```

## Policy for Granting a User Permissions to Manipulate a Specific TencentDB Instance
To grant a user permissions to manipulate a specific database, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instance "cdb-xxx" in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::instanceId/cdb-xxx",
            "effect": "allow"
        }
    ]
}
```

## Policy for Granting a User Permissions to Manipulate TencentDB Instances in Batches
To grant a user permissions to manipulate TencentDB instances in batches, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances "cdb-xxx" and "cdb-yyy" in Guangzhou and "cdb-zzz" in Beijing.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": ["qcs::cdb:ap-guangzhou::instanceId/cdb-xxx", "qcs::cdb:ap-guangzhou::instanceId/cdb-yyy", "qcs::cdb:ap-beijing::instanceId/cdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

## Policy for Granting a User Permissions to Manipulate TencentDB Instances in a Specific Region
To grant a user permissions to manipulate TencentDB instances in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

## Custom Policies
If preset policies cannot meet your requirements, you can create custom policies as shown below. If permissions are granted by resources, for a TencentDB API operation that does not support authorization at the resource level, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.
     
The syntax of custom policies is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```
- Replace "Action" with the operation to be allowed or denied.
- Replace "Resource" with the resources that you want to authorize the user to manipulate.
- Replace "Effect" with "Allow" or "Deny".
