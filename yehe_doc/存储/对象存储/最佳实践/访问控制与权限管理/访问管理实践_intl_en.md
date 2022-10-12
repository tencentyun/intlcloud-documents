## Overview

Cloud Access Management (CAM) is a Tencent Cloud authentication and authorization service, which helps you manage the access to your Tencent Cloud resources. You can manage authorized objects, resources, and operations, and set policies to control access when granting permissions.

## Features
#### Granting access to resources under the root account
You can grant the access to the resources under your root account to other users, including sub-accounts and other root accounts, without sharing the identity credentials of your root account.

#### Granular permission management
Different access permissions to different resources can be granted to different users. For example, some sub-accounts can be granted the read access to a COS bucket, while some other sub-accounts or root accounts can own the write access to a COS object. The above-mentioned resources, access permissions and users can all be managed in batch.

#### Eventual consistency
CAM currently supports data synchronization across Tencent Cloud regions by copying policies. CAM policies can be modified timely, but it may take some time for those policies synced across regions to take effect. Additionally, CAM uses cache (currently valid for one minute) to improve performance, and any policy update does not take effect until cache expires.

## Use Cases

**Enterprise sub-account access permission management**

Enterprises may need to grant the minimal access permission for their cloud resources to all kinds of employees. Assume that an enterprise owns many cloud resources (CVM, VPC instances, CDN instances, COS buckets and objects, etc.) and many employees (developers, testers, OPS personnel, etc.).
The developers need the read and write permissions to the project-related cloud resources on the development servers. Testers need the read and write permissions to the project-related cloud resources on the test servers. OPS personnel are responsible for the purchase and daily operation of the servers. If the duty or project of an employee changes, the corresponding permissions should be terminated.

**Cross-enterprise access permission management**

There are cases where enterprises may need to share their cloud resources. For example, a company which has many cloud resources wants to focus on product R&D and outsource the operation of its cloud resources to another company. It also need to revoke all permissions that have been granted as soon as the outsourcing service contracts are terminated.

## Policy Syntax
A CAM policy consists of several elements and is used to describe specific information about authorization. Core elements include principal, action, resource, condition, and effect. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

>?
>- There is no particular sequence in the description of policy syntax. However, please note that the `action` element is case-sensitive.
>- If there are no particular conditions required, the `condition` element is optional.
>- You cannot define the `principal` element in the console, but only through the policy management APIs or policy syntax parameters.

#### Core elements

| Core Element           | Description                                                         | Required                                          |
| ------------------ | ------------------------------------------------------------ | ----------------------------------------------------- |
| version       | Specifies the version of the policy syntax. Valid value: 2.0 | Yes                |
| principal   | Describes the entity to be authorized by the policy, including users (developers, sub-accounts, anonymous users), and user groups | This element can only be used in policy management APIs and policy syntax-related parameters |
| statement     | Describes the details on a permission or a permission set defined by other elements including effect, action, resource, and condition. One policy has only one statement. | Yes |
| action        | Describes the action to be allowed or denied. It can be an API operation or a set of API operations. This element is case-sensitive, e.g. `name/cos:GetService` | Yes |
| resource  | Describes the resource to which the permission applies. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for | Yes   |
| condition | Describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may be time, IP address, etc. Some services allow you to specify additional values in a condition  | No   |
| effect        | Describes whether the statement result is "allow" or "deny" | Yes     |

#### Policy limits

| Limit | Value | 
|---------|---------|
|Number of user groups in a root account | 300| 
| Number of sub-accounts in a root account | 1000 | 
| Number of roles in a root account | 1000 | 
|Number of user groups that a sub-account can be added to | 10 | 
| Number of root accounts with which a collaborator can be associated | 10 | 
| Number of sub-accounts in a user group | 100 | 
| Number of custom policies created for a root account | 1500 | 
| Number of policies associated to a CAM user/user group/role| 200 | 
|Maximum characters allowed for a policy syntax | 4096 |

#### Example policy
The policy in this example allows the sub-account with ID 100000000011 under the root account with ID 100000000001 (APPID: 1250000000) to **PUT Object** and **GET Object** on the bucket "examplebucket-bj" in Beijing region and the object “exampleobject” in the bucket “examplebucket-gz” in Guangzhou region, on condition that the access IP falls within the IP address range `10.*.*.10/24`.

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

