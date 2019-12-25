## Introduction

You can use roles through CAM APIs. This document describes how to use roles through APIs with a typical use case.

## Prerequisites

For example:
- Company A wants to outsource its OPS Engineer position to Company B. The person taking the position needs the access to all Company A's CVM resources located in the Guangzhou region.
- Company A has an enterprise account, `CompanyExampleA` (ownerUin: 12345).
- Company B has an enterprise account, `CompanyExampleB` (ownerUin: 67890).
- Company B has a sub-account, `DevB`, and wants to use `DevB` to do the work.

## Directions

Company A takes the following steps as directed in [Creating a role > Creating a role using API](https://intl.cloud.tencent.com/document/product/598/19381):
1. Create a role, and set the role entity to Company B’s enterprise account, `CompanyExampleB`.
2. Call the `CreateRole` API to create a role with the `roleName` as `DevOpsRole`, and grant the role the permissions allowing it to operate all Company A’s CVM resources in the Guangzhou region.

Company B takes the following steps as directed in [Assigning role policies to sub-accounts](https://intl.cloud.tencent.com/document/product/598/19422):
1. Authorize the sub-account `DevB` to assume the `DevOpsRole` role.
2. Call the [AssumeRole](https://intl.cloud.tencent.com/document/product/598/13895) API to apply for temporary credentials for the role `DevOpsRole`. Input parameters are as follows: 
> If company B (`CompanyExampleB`) wants to directly operate the resources of company A (`CompanyExampleA`), they can also request temporary credentials to perform operations.
>
```
roleArn=qcs::cam::uin/12345:roleName/DevOpsRole，
roleSessionName=DevBAssumeTheRole，
durationSeconds=7200
```
If this API is called successfully, the response will be as follows:
```
{
	"credentials": {
		"sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
		"tmpSecretId": "AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl",
		"tmpSecretKey": "VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD"
	},
	"expiredTime": 1506433269,
	"expiration": "2018-09-26T13:41:09Z"
}
```
3. `DevB` can perform operations on company A’s resources within the scope of permissions during the validity period of the credentials.
For example, `DevB` wants to call the [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/15728) API to view the CVM list. `DevB` needs to replace the values of `SecretId` and `SecretKey` with the values of `tmpSecretId` and `tmpSecretKey` , and set the `Token` in [Common Parameters](https://intl.cloud.tencent.com/document/product/213/31574) to the value of `sessionToken`. 
> To stop authorizing company B, company A only needs to delete the `DevOpsRole` role.





