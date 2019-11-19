## Operation Scenario
You can grant a user the permission to view and use specific resources in the TencentDB Console by using a CAM policy. The sample below shows how to allow a user to use certain policies in the console.

## Directions
#### Full Read/Write Permission Policy for TencentDB
To grant a user permission to create and manage TencentDB instances, implement the policy named QcloudCDBFullAccess for the user.

Enter the [policy management page](https://console.cloud.tencent.com/cam/policy). Click **Service Type** and select **TencentDB for MySQL** in the drop-down list. Then, you can see this policy in the results.
![Alt text](https://main.qcloudimg.com/raw/c3a7dd4dae2d82da3d3c702a5188fe9e.png)
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
The above policy achieves its goal by allowing the user to separately authorize the use of TencentDB, VPC, security group, COS, KMS, and all resources available in the monitor with the CAM policy.

### Read-only Permission Policy for TencentDB
To grant a user permission to view TencentDB instances but not create, delete, or modify them, implement the policy named QcloudCDBInnerReadOnlyAccess for the user.

>You are recommended to configure the read-only policy for TencentDB.

Enter the [policy management page](https://console.cloud.tencent.com/cam/policy). Click **Service Type** and select **TencentDB for MySQL** in the drop-down list. Then, you can see this policy in the results.

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

### Read-only Permission Policy for TencentDB-related Resources
To grant a user permission to view TencentDB instances and related resources (VPC, security group, COS, and monitor) but create, delete, or modify them, implement the policy named QcloudCDBReadOnlyAccess for the user.

Enter the [policy management page](https://console.cloud.tencent.com/cam/policy). Click **Service Type** and select **TencentDB for MySQL** in the drop-down list. Then, you can see this policy in the results.

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
The above policy achieves its goal by allowing the user to separately authorize the use of the following operations with the CAM policy.
- All operations in TencentDB that begin with "Describe".
- All operations in VPC that begin with "Describe", "Inquiry", or "Get".
- All operations in security groups that begin with "DescribeSecurityGroup".
- All operations in COS that begin with "List", "Get", and "Head" as well as the "OptionsObject" operation.
- All operations in the monitor.

### Policy for Granting a User Permission to Manipulate a Specific TencentDB Instance
To grant a user the permission to manipulate a specific database, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instance "cdb-xxx" in Guangzhou.
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

### Policy for Granting a User Permissions to Manipulate TencentDB Instances in Batches
To grant a user the permission to manipulate databases in batches, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances "cdb-xxx" and "cdb-yyy" in Guangzhou and "cdb-zzz" in Beijing.
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

### Policy for Granting a User Permission to Manipulate TencentDB Instances in a Specific Region
To grant a user the permission to manipulate databases in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou.
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

### Custom Policy
If the preset policies cannot meet your needs, you can also customize policies. To grant a user the permission to manipulate certain projects, associate the QcloudCDBProjectToUser policy with the user at the same time.
The syntax of a custom policy is as follows:
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
