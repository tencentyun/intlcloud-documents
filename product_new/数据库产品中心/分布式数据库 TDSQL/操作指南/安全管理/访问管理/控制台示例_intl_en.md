## Sample CAM Policies for TencentDB
You can grant a user the permission to view and use specific resources in the TencentDB Console by using a CAM policy. The sample below shows how to allow a user to use certain policies in the console.

>As TDSQL was formerly known as DCDB, its API keyword in CAM is "dcdb". For more information, see [Product Name Change](https://intl.cloud.tencent.com/document/product/1042/33376).

### Syntax for Creating a Custom Policy
1. Enter the policy syntax configuration page and click **Create Custom Policy**.
![](https://main.qcloudimg.com/raw/fc7ff2e20322c74b2e8b5728a483255c.png)
2. Click **Create by Policy Syntax** in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/cda7a1b0ec6256b620bcbd9290fd60fd.png)
2. Select "Blank template" and click **Next**.
![](https://main.qcloudimg.com/raw/9c6bcdc90c02059a5abb67e73a74d739.png)
3. Enter the corresponding policy syntax.
![](https://main.qcloudimg.com/raw/0938ab4115dc67b2e952aa1eaa1283cb.png)

### Associating a Sub-account/Collaborator and Verifying
After the policy is created, associate it with a user/group. After the association is completed, use another browser (or server) to verify whether the sub-account/collaborator can work normally. If the policy syntax is written correctly, you can observe the following:
- You have normal access to the intended target products and resources and can use all the expected features.
- You will be prompted with "You do not have permission to perform this operation" when accessing other unauthorized products or resources.

> To avoid mutual impact of multiple policies, it is recommended to associate only one policy with a sub-account at a time.
> The change to account access permission will take effect within one minute.

## Appendix: Commonly Used Policy Syntax

### Policy for Authorizing Use of All Features in All TencentDB Instances
To grant a user permission to create and manage TencentDB instances, implement the policy named QcloudDCDBFullAccess for the user.

The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dcdb:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```


### Policy for Authorizing Query of All TencentDB Instances
To grant a user permission to view TencentDB instances but not create, delete, or modify them, implement the policy named QcloudDCDBInnerReadOnlyAccess for the user.

The policy syntax is as follows:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dcdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
The above policy achieves its goal by allowing the user to separately authorize the use of all operations beginning with "Describe" in TencentDB with the CAM policy.

>As not all functional APIs are covered in the beta test, you may see that a small number of operations are not included in CAM, which is normal.

### Policy for Granting a User Permission to Manipulate TencentDB Instances in a Specific Region
To grant a user the permission to manipulate databases in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:*",
            "resource": "qcs::dcdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

### Policy for Granting a User Permission to Manipulate TencentDB Instances in Multiple Specific Regions
To grant a user the permission to manipulate databases in a specific region, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances in Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:*",
            "resource": "qcs::dcdb:ap-guangzhou::*","qcs::dcdb:ap-chengdu::*",
            "effect": "allow"
        }
    ]
}
```

### Policy for Granting a User Permission to Manipulate a Specific TencentDB Instance
To grant a user the permission to manipulate a specific database, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instance "dcdb-xxx" in Guangzhou.

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "dcdb:*"
            ],
            "resource": "qcs::dcdb:ap-chengdu::instance/dcdb-fwr62n3i",
            "effect": "allow"
        }
    ]
}

```

### Policy for Granting a User Permission to Manipulate Multiple TencentDB Instances
To grant a user the permission to manipulate TencentDB instances in batches, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances "dcdb-xxx" and "dcdb-yyy" in Guangzhou and "dcdb-zzz" in Beijing.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:*",
            "resource": ["qcs::dcdb:ap-guangzhou::instance/dcdb-xxx", "qcs::dcdb:ap-guangzhou::instance/dcdb-yyy", "qcs::dcdb:ap-beijing::instance/dcdb-zzz"],
            "effect": "allow"
        }
    ]
}
```


### Policy for Granting a User Different Permissions to Manipulate Multiple TencentDB Instances
To grant a user the permission to manipulate TencentDB instances in batches, associate the following policy with the user. For example, the policy below allows the user to manipulate the TencentDB instances "dcdb-xxx" and "dcdb-yyy" in Guangzhou and "dcdb-zzz" in Beijing.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:Describe*","dcdb:Create*",
            "resource": ["qcs::dcdb:ap-guangzhou::instance/dcdb-xxx", "qcs::dcdb:ap-guangzhou::instance/dcdb-yyy", "qcs::dcdb:ap-beijing::instance/dcdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

>For all currently supported APIs, see the list at the end of this document.

### Denying a User Permission to Create TencentDB Accounts
If you want to deny a user permission to upgrade TencentDB instances in batches, configure `"effect": "deny"`.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "dcdb:CreateAccount",
            "resource": "*",
            "effect": "deny"
        }
    ]
}
```


### Other Custom Policies
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


### Supported APIs

| Operation Name | API Name | Effective in Console After Configuration |
| :-------- | :------------------------ |:------------------------ |
| Querying the upgrade price of an instance     | DescribeDCDBUpgradePrice       | No                  |
| Renewing an instance             | RenewDCDBInstance              | No                  |
| Querying the renewal price of an instance     | DescribeDCDBRenewalPrice       | No                  |
| Scaling an instance             | UpgradeDCDBInstance            | No                  |
| Viewing the instance list         | DescribeDCDBInstances          | Yes                  |
| Getting the log list         | DescribeDBLogFiles             | Yes                  |
| Initializing instances           | InitDCDBInstances              | No                  |
| Creating an account             | CreateAccount                  | Yes                  |
| Querying the account list         | DescribeAccounts               | Yes                  |
| Deleting an account             | DeleteAccount                  | Yes                  |
| Setting account permission         | GrantAccountPrivileges         | Yes                  |
| Querying account permission         | DescribeAccountPrivileges      | Yes                  |
| Copying account permission         | CopyAccountPrivileges          | No                  |
| Modifying database account remarks   | ModifyAccountDescription       | No                  |
| Resetting account password         | ResetAccountPassword           | Yes                  |
| Viewing database parameters       | DescribeDBParameters           | No                  |
| Modifying database parameters       | ModifyDBParameters             | No                  |
| Cloning an account             | CloneAccount                   | Yes                  |
| Getting SQL logs          | DescribeSqlLogs                | No                  |
