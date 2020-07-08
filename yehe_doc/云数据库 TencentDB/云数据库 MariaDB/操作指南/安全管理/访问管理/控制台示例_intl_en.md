## Sample CAM Policies for TencentDB
You can grant a user the permission to view and use specific resources in the TencentDB Console by using a CAM policy. The sample below shows how to allow a user to use certain policies in the console. Currently, you can configure TencentDB for MariaDB to support the CAM feature only by using the "creation by policy syntax" method. You can do so in **[CAM](https://console.cloud.tencent.com/cam/policy)** > **Policy** > **Create Custom Policy** > **Create by Policy Syntax** > **Custom**.
>!The API keyword in CAM of TencentDB for MariaDB is "mariadb".

### Step 1. Create custom policy syntax
1. Enter the policy syntax configuration page.
![](https://main.qcloudimg.com/raw/4af838f8bb42d48ddb7836345e5b81fc.png)
![](https://main.qcloudimg.com/raw/c75a0306c187c5754d30dd3b77891ffa.png)
2. Select "Blank Template" and click **Next**.
![](https://main.qcloudimg.com/raw/9c26e03dab484b6787c57a2b243e19d6.png)
3. Enter the corresponding policy syntax.
![](https://main.qcloudimg.com/raw/bcf53e1eecb4c6f76f133bd6fa7dfeec.png)

### Step 2. Associate a sub-account/collaborator and verify
After the policy is created, associate it with a user/group. After the association is completed, use another browser (or server) to verify whether the sub-account/collaborator can work normally. If the policy syntax is written correctly, you can observe the following:
- You have normal access to the intended target products and resources and can use all the expected features.
- You will be prompted with "You do not have permission to perform this operation" when accessing other unauthorized products or resources.

>!
- To avoid mutual impact of multiple policies, it is recommended to associate only one policy with a sub-account at a time.
- The change to account access permission will take effect within 1 minute.

## Appendix: Commonly Used Policy Syntax

### Policy for authorizing use of all features in all TencentDB instances
To grant a user permission to create and manage TencentDB instances, implement the policy named `QcloudMariaDBFullAccess` for the user.

The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "mariadb:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```


### Policy for authorizing query of all TencentDB instances
To grant a user permission to query TencentDB instances but not create, delete, or modify them, implement the policy named `QcloudMariaDBInnerReadOnlyAccess` for the user.

The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "mariadb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
The above policy achieves its goal by allowing the user to separately authorize the use of all operations beginning with "Describe" in TencentDB with the CAM policy.

>? As not all functional APIs are covered currently, you may see that a small number of operations are not included in CAM, which is normal.

### Policy for granting a user permission to manipulate TencentDB instances in a specific region
To grant a user the permission to manipulate TencentDB instances in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "mariadb:*",
            "resource": "qcs::mariadb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

### Policy for granting a user permission to manipulate TencentDB instances in multiple specific regions
To grant a user the permission to manipulate TencentDB instances in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "mariadb:*",
            "resource": "qcs::mariadb:ap-guangzhou::*","qcs::mariadb:ap-chengdu::*",
            "effect": "allow"
        }
    ]
}
```

### Policy for granting a user permission to manipulate a specific TencentDB instance
To grant a user the permission to manipulate a specific database, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instance "tdsql-xxx" in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "mariadb:*"
            ],
            "resource": "qcs::mariadb:ap-chengdu::instance/tdsql-fwr62n3i",
            "effect": "allow"
        }
    ]
}

```
### Policy for granting a user permission to manipulate multiple TencentDB instances
To grant a user the permission to manipulate TencentDB instances in batches, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances "tdsql-xxx" and "tdsql-yyy" in Guangzhou and "tdsql-zzz" in Beijing.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": "mariadb:*",
            "resource": ["qcs::mariadb:ap-guangzhou::instance/tdsql-xxx", "qcs::mariadb:ap-guangzhou::instance/tdsql-yyy", "qcs::mariadb:ap-beijing::instance/tdsql-zzz"],
            "effect": "allow"
        }
    ]
}
```


### Policy for granting a user different permissions to manipulate multiple TencentDB instances
To grant a user the permission to manipulate TencentDB instances in batches, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances "tdsql-xxx" and "tdsql-yyy" in Guangzhou and "tdsql-zzz" in Beijing.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "mariadb:Describe*","mariadb:Create*",
            "resource": ["qcs::mariadb:ap-guangzhou::instance/tdsql-xxx", "qcs::mariadb:ap-guangzhou::instance/tdsql-yyy", "qcs::mariadb:ap-beijing::instance/tdsql-zzz"],
            "effect": "allow"
        }
    ]
}
```

>?For all currently supported APIs, please see the list at the end of this document.

### Denying a user permission to create TencentDB accounts
To deny a user permission to create TencentDB accounts, configure `"effect": "deny"` as shown below.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "mariadb:CreateAccount",
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```



### Other custom policies
If preset policies cannot meet your requirements, you can create custom policies as shown below:
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



