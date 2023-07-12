## Overview

Cloud Access Management (CAM) is a Tencent Cloud authentication and authorization service that helps you manage the access to your Tencent Cloud resources. You can manage authorized objects, resources, and operations and set policies to control access when granting permissions.

## Features
#### Granting access to resources under the root account
You can grant the access to resources under your root account to other users, including sub-accounts and other root accounts, without sharing the identity credentials of your root account.

#### Granular permission management
Different access permissions of different resources can be granted to different users. For example, some sub-accounts can be granted the read access to a COS bucket, while some other sub-accounts or root accounts can be granted the write access to a COS object. Such resources, access permissions, and users can all be managed in batch.

#### Eventual consistency
CAM currently supports data sync across Tencent Cloud regions by copying policies. CAM policies can be modified timely, but it may take some time for those policies synced across regions to take effect. In addition, CAM uses cache (currently valid for one minute) to improve the performance, and any policy update does not take effect until the cache expires.

## Use Cases

**Enterprise sub-account permission management**

Enterprises may need to grant the minimal access permission of their cloud resources to all kinds of employees. Assume that an enterprise owns many cloud resources (CVM/VPC/CDN instances, COS buckets/objects, etc.) and many employees (developers, testers, Ops engineers, etc.).
Developers and testers need the read/write permissions of project-specific cloud resources on development servers and test servers respectively, while Ops engineers are responsible for the purchase and daily operations of such servers. If the duty or project of an employee changes, the corresponding permissions should be terminated.

**Cross-enterprise permission management**

There are cases where enterprises may need to share their cloud resources. For example, enterprise A has many cloud resources and wants to focus on product R&D, so it outsources the operations of its cloud resources to enterprise B, and it needs to revoke all the granted permissions as soon as the outsourcing service contract is terminated.

## Policy Syntax
A CAM policy consists of several elements and is used to describe specific information on authorization. Core elements include principal, action, resource, condition, and effect. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/18023).

>?
>- There is no particular sequence in the description of policy syntax. However, note that the action element is case-sensitive.
>- If there are no particular conditions required, the condition element is optional.
>- You can define the principal element only through policy management APIs or policy syntax parameters but not in the console.

#### Core elements

| Core Element           | Description                                                         | Required                                          |
| ------------------ | ------------------------------------------------------------ | ----------------------------------------------------- |
| version       | Specifies the version of the policy syntax. Valid value: `2.0`. | Yes                |
| principal   | Describes the entity to be authorized by the policy, including users (developers, sub-accounts, anonymous users) and user groups | This element can be used only in policy management APIs and policy syntax parameters. |
| statement     | Describes the details of a permission or a permission set defined by other elements including effect, action, resource, and condition. One policy has only one statement. | Yes |
| action        | Describes the action to be allowed or denied, which can be an API operation or a set of API operations. This element is case-sensitive, such as `name/cos:GetService`. | Yes |
| resource  | Describes the resource to which the permission applies. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation of the product for which you are writing a resource statement. | Yes   |
| condition | Describes the condition for the policy to take effect. A condition consists of the operator, action key, and action value. A condition value may be time, IP address, etc. Some services allow you to specify additional values in a condition.  | No   |
| effect        | Describes whether the statement result is "allow" or "deny". | Yes     |

#### Policy limits

| Item | Upper Limit | 
|---------|---------|
| Number of user groups under a root account | 300 | 
| Number of sub-accounts under a root account | 1,000 | 
| Number of roles under a root account | 1,000 | 
| Number of user groups that a sub-account can be added to | 10 | 
| Number of root accounts with which a collaborator can be associated | 10 | 
| Number of sub-accounts in a user group | 100 | 
| Number of custom policies that can be created under a root account | 1,500 | 
| Number of policies that can be directly associated with a user, user group, or role | 200 | 
| Number of characters in a policy syntax | 4,096 |

#### Sample policy

The policy in this example allows the sub-account with ID 100000000011 under the root account with ID 100000000001 (APPID: 1250000000) to **upload** and **download** objects regarding the `examplebucket-bj` bucket in Beijing region and the `exampleobject` object in the `examplebucket-gz` bucket in Guangzhou region, on condition that the access IP falls within the IP range `10.*.*.10/24`.

```json
{
			"version": "2.0",
			"principal": {
				"qcs": ["qcs::cam::uin/100000000001:uin/100000000011"]
			},
			"statement": [{
				"effect": "allow",
				"action": ["name/cos:PutObject", "name/cos:GetObject"],
				"resource": ["qcs::cos:ap-beijing:uid/1250000000:examplebucket-bj-1250000000/*",
					"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-gz-1250000000/exampleobject"
				],
				"condition": {
					"ip_equal": {
						"qcs:ip": "10.*.*.10/24"
					}
				}
			}]
}
```

