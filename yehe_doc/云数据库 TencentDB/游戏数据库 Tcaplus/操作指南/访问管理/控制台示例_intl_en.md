## Operation Scenarios
You can grant a user the permission to view and use specific resources in the TcaplusDB Console by using a CAM policy. This document describes how to grant the permission to view and use specified resources, thereby showing you how to use certain policies in the console.


## Directions
### Full access policy in TcaplusDB
To grant a user the permission to create and manage TcaplusDB instances, associate the `QcloudTcaplusDBFullAccess` policy with the user.
This policy grants the user the permission to manipulate all resources in TcaplusDB. The steps are as follows:
Authorize the default policy `QcloudTcaplusDBFullAccess` with the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Read-only policy in TcaplusDB
To grant a user the permission to view TcaplusDB instances but not create, delete, or modify them, you can associate the `QcloudTcaplusDBReadOnlyAccess` policy with the user.
This policy grants the user the permissions of all operations in TcaplusDB that begin with the word "Describe" or "Inquiry". The steps are as follows:
Authorize the default policy `TcaplusDB` with the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Policy for granting user permission to manipulate a specific cluster
To grant a user the permission to manipulate a specific TcaplusDB cluster, you can associate the following policy with the user. The steps are as follows:

1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
This policy grants the user the permission to perform all operations on the TcaplusDB cluster whose ID is 19168929215. The policy content can be set by referring to the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:ap-shanghai:uin/1231xxx166:cluster/19168929215",
            "effect": "allow"
        }
    ]
}
```
2. Find the created policy and click **Associate User/Group** in the "Operation" column.
3. In the "Associate User/User Group" window that pops up, select the user/group you want to authorize and click **Confirm**.


### Policy for granting user permission to manipulate all TcaplusDB resources
To grant a user the permission to manipulate all TcaplusDB resources, associate the following policy with the user. The steps are as follows:

1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
This policy grants the user the permission to manipulate all TcaplusDB resources. The policy content can be set by referring to the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:::*",
            "effect": "allow"
        }
    ]
}
```
2. Find the created policy and click **Associate User/Group** in the "Operation" column.
3. In the "Associate User/User Group" window that pops up, select the user/group you want to authorize and click **Confirm**.


### Policy for denying user all permissions of certain TcaplusDB tables
To deny a user the permission to manipulate certain TcaplusDB tables, associate the following policy with the user. The steps are as follows:

1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
This policy denies the user the permission to manipulate tables (ID: tcaplus-c8d1caa4 and tcaplus-d8d1cbb4). The policy content can be set by referring to the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": [
						"qcs::tcaplusdb::uin/16xxx472:table/tcaplus-c8d1caa4",
						"qcs::tcaplusdb::uin/16xxx472:table/tcaplus-d8d1cbb4",
						],
            "effect": "deny"
        }
    ]
}
```
2. Find the created policy and click **Associate User/Group** in the "Operation" column.
3. In the "Associate User/User Group" window that pops up, select the user/group you want to authorize and click **Confirm**.

<span id="CAMCustomPolicy"></span>
### Custom policy
If preset policies cannot meet your requirements, you can create custom policies as needed.
For detailed directions, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
For more TcaplusDB policy syntax, please see [Authorization Policy Syntax](https://intl.cloud.tencent.com/document/product/1016/35751).

