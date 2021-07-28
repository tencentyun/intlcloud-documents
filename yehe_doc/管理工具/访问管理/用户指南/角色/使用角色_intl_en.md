## Overview

You can use roles through the console or APIs. This document describes how to use roles with typical examples.


## Prerequisites

For example:
- Company A wants to outsource its OPS engineer position to company B. The person taking the position needs the access to company A's all CVM resources located in the Guangzhou region.
- Company A has an enterprise account `CompanyExampleA` (ownerUin: 12345).
- Company B has an enterprise account `CompanyExampleB` (ownerUin: 67890).
- Company B has a sub-account `DevB` and wants to use `DevB` to do the work.


## Directions
You can click the following tabs to view the corresponding directions.
<dx-tabs>
::: Using\sthe\srole\sin\sthe\sconsole
1. Company A creates a role (as instructed in [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381)).
Select **Tencent Cloud Account** as the role entity and create a role (`DevOpsRole` for example). Then, set company B's enterprise account "67890" as its role entity and add it the permission to manipulate company A's CVM resources in the Guangzhou region.

2. Company A authorizes the sub-account of company B (as instructed in [Authorizing a Sub-account with the Policy of Assuming a Role](https://intl.cloud.tencent.com/document/product/598/19422)).
Set a policy allowing company B's sub-account `DevB` to use the `DevOpsRole` role of company A (ownerUin: 12345) and grant it the permission of the `sts:AssumeRole` API.

3. Company B uses the role to log in to the console.
Log in to the console with company B's sub-account `DevB` and click **Switch Role** in the drop-down list under the profile photo.
Enter company A's root account "12345" and the role name "DevOpsRole". After confirmation, company B can switch to the `DevOpsRole` role of company A (ownerUin: 12345).
You can also switch to other roles by clicking **Switch Role** in the drop-down list.
If you want to return to the original sub-account after switching the role, you can click **Back to Sub-user** in the drop-down list.
<dx-alert infotype="notice">You can only switch to a role after being authorized to use it, and the role entity must be a Tencent Cloud account. You cannot switch to unauthorized roles.
</dx-alert>

:::

::: Using\sroles\sthrough\sAPI\s
Company A takes the following steps as instructed in [Creating a Role](https://intl.cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA):
1. Create a role and set the role entity to company B's enterprise account `CompanyExampleB`.
2. Call the `CreateRole` API to create a role with the `roleName` as `DevOpsRole` and grant the role the permission to manipulate company A's all CVM resources in the Guangzhou region.

Company B takes the following steps as instructed in [Authorizing a Sub-account with the Policy of Assuming a Role](https://intl.cloud.tencent.com/document/product/598/19422):
1. Authorize the sub-account `DevB` to assume the `DevOpsRole` role.
2. Call the [AssumeRole](https://intl.cloud.tencent.com/document/product/598/35840) API to apply for temporary credentials for the role `DevOpsRole`. Input parameters are as follows: 
<dx-alert infotype="explain">If company B (`CompanyExampleB`) wants to directly manipulate the resources of company A (`CompanyExampleA`), they can also request temporary credentials to perform operations.
</dx-alert>

 ```
roleArn=qcs::cam::uin/12345:roleName/DevOpsRole,
roleSessionName=DevBAssumeTheRole,
durationSeconds=7200
 ```
If this API is called successfully, the response will be as follows:
```
{
	"credentials": {
		"sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
		"tmpSecretId": "AKI***PCl",
		"tmpSecretKey": "Vpx***MqD"
	},
	"expiredTime": 1506433269,
	"expiration": "2018-09-26T13:41:09Z"
}
```
3. `DevB` can perform operations on company A's resources within the scope of permissions during the validity period of the credentials.
For example, if `DevB` wants to call the [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258) API to view the CVM list, then `DevB` needs to replace the values of `SecretId` and `SecretKey` with the values of `tmpSecretId` and `tmpSecretKey` and set the `Token` in [common parameters](https://intl.cloud.tencent.com/document/product/213/31574) to the value of `sessionToken`.
<dx-alert infotype="notice">To stop authorizing company B, company A only needs to delete the `DevOpsRole` role.
</dx-alert>

:::
</dx-tabs>




