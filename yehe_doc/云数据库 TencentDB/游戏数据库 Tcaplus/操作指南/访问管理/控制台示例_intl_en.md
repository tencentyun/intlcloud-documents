## Operation Scenarios

You can grant a user the permission to view and use specific resources in the TcaplusDB Console by using a CAM policy. This document describes how to grant the permission to view and use specified resources, thereby showing you how to use certain policies in the console.

## Operation Examples
### Full access policy in TcaplusDB
To grant a user permission to create and manage TcaplusDB instances, implement the policy named `QcloudTcaplusDBFullAccess` for the user, which achieves its goal by granting the user permission to manipulate all TcaplusDB resources.
The steps are as follows:
Authorize the default policy `QcloudTcaplusDBFullAccess` to the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Read-Only policy in TcaplusDB
To grant a user permission to query TcaplusDB instances but not create, delete, or start/shut down them, implement the policy named `QcloudTcaplusDBReadOnlyAccess` for the user, which achieves its goal by granting the user permission to perform all operations beginning with "Describe" or "Inquiry" in TcaplusDB. The steps are as follows:
Authorize the default policy `TcaplusDB` to the user as instructed in [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### Policy for granting user permission to manipulate specific cluster
To grant a user the permission to manipulate a specific TcaplusDB cluster, associate the following policy with the user. The steps are as follows:
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
This policy grants the user permission to perform all operations on the TcaplusDB cluster whose ID is 19168929215. The policy content can be set by referring to the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:ap-shanghai::cluster/19168929215",
            "effect": "allow"
        }
    ]
}
```
2. Find the created policy and click **Associate User/Group** in the "Operation" column.
3. In the **Associate User/User Group** window that pops up, select the user/group you want to authorize and click **OK**.


### Policy for granting user permission to manipulate all TcaplusDB resources in specific region
To grant a user the permission to manipulate TcaplusDB resources in a specific region, associate the following policy with the user. The steps are as follows:
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
This policy grants the user permission to manipulate all TcaplusDB resources in the Shanghai region. The policy content can be set by referring to the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:ap-shanghai::*",
            "effect": "allow"
        }
    ]
}
```
2. Find the created policy and click **Associate User/Group** in the "Operation" column.
3. In the **Associate User/User Group** window that pops up, select the user/group you want to authorize and click **OK**.


### Policy for granting user permission to manipulate certain TcaplusDB tables in specific region
To grant a user the permission to manipulate certain TcaplusDB tables in a specific region, associate the following policy with the user. The steps are as follows:
1. Create a custom policy as instructed in [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
This policy grants the user permission to manipulate tables whose IDs are tcaplus-c8d1caa4 and tcaplus-d8d1cbb4 in the Shanghai region. The policy content can be set by referring to the following policy syntax:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": [
						"qcs::tcaplusdb:ap-shanghai:uin/164256472:table/tcaplus-c8d1caa4",
						"qcs::tcaplusdb:ap-shanghai:uin/164256472:table/tcaplus-d8d1cbb4",
						],
            "effect": "allow"
        }
    ]
}
```
2. Find the created policy and click **Associate User/Group** in the "Operation" column.
3. In the **Associate User/User Group** window that pops up, select the user/group you want to authorize and click **OK**.

<span id="CAMCustomPolicy"></span>
### Custom policy

If preset policies cannot meet your requirements, you can create custom policies as needed.
For detailed directions, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).
For more TcaplusDB-related policy syntax, please see [Authorization Policy Syntax](https://intl.cloud.tencent.com/document/product/213/10313).

