
## Sample CAM Policies for TencentDB
You can grant a user the permission to view and use specific resources in the TencentDB console by using a CAM policy. The sample below shows how to allow a user to use certain policies in the console. Currently, you can configure TencentDB for MariaDB to support the CAM feature only by using the **creation by policy syntax** method.
>!The API keyword of TencentDB for MariaDB in CAM is `mariadb`.

### Step 1. Create a custom policy
1. Enter the [Policy Syntax](https://console.cloud.tencent.com/cam/policy) configuration page and click **Create Custom Policy**.
2. Click **Create by Policy Syntax** in the pop-up window.
![](https://main.qcloudimg.com/raw/c75a0306c187c5754d30dd3b77891ffa.png)
3. Select **Blank Template** and click **Next**.
![](https://main.qcloudimg.com/raw/9c6bcdc90c02059a5abb67e73a74d739.png)
4. Enter the corresponding policy syntax.
![](https://main.qcloudimg.com/raw/bcf53e1eecb4c6f76f133bd6fa7dfeec.png)

### Step 2. Associate the sub-account/collaborator and verify
After the policy is created, associate it with a user/group. After the association is completed, use another browser (or server) to verify whether the sub-account/collaborator can work normally. If the policy syntax is written correctly, you can observe the following:
- You have normal access to the intended target products and resources and can use all the expected features.
- You will be prompted that "You do not have permission to perform this operation" when accessing other unauthorized products or resources.

>!
- To avoid mutual impact of multiple policies, we recommend you associate only one policy with a sub-account at a time.
- The change to account access permission will take effect within 1 minute.

## Appendix. Commonly Used Policy Syntax
### Policy for authorizing the use of all features in all TencentDB instances
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

### Policy for authorizing the query of all TencentDB instances
To grant a user permission to view TencentDB instances but not create, delete, or modify them, implement the policy named `QcloudMariaDBInnerReadOnlyAccess` for the user.

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

>?Because not all functional APIs are now supported, a limited number of operations may be excluded from CAM, which is normal.

### Policy for granting user permission to manipulate TencentDB instances in one specific region
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

### Policy for granting user permission to manipulate TencentDB instances in multiple specific regions
To grant a user the permission to manipulate TencentDB instances in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou and Chengdu.
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

### Policy for granting user permission to manipulate one specific TencentDB instance
To grant a user the permission to manipulate a specific database, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instance "tdsql-xxx" in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "mariadb:*"
            ],
            "resource": "qcs::mariadb:ap-guangzhou::instance/tdsql-xxx",
            "effect": "allow"
        }
    ]
}
```

### Policy for granting user permission to manipulate multiple TencentDB instances
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

### Policy for granting user different permissions to manipulate multiple TencentDB instances
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

### Denying user permission to create TencentDB accounts
To deny a user permission to create TencentDB accounts, configure `effect": "deny"`.
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
