## Cloud Access Management Overview

Cloud Access Management (CAM) is a Tencent Cloud authentication and authorization service, which helps you manage your Tencent Cloud resources access. You can manage authorized objects, resources, and operations, and set policies to control access when granting permissions.

## Features
### Grant access to resources under the primary account
The access to the resources under the primary account can be granted to other users, including sub-accounts or other primary accounts, without sharing the identity credentials of the primary account.

### Refined permission management
Different access permissions to different resources can be granted to different users. For example, some sub-accounts can be granted the read access to a COS storage bucket, while some other sub-accounts or primary accounts can own the write access to a COS object. The above-mentioned resources, access permissions and users can all be managed in batch.

### Eventual consistency
CAM is available in multiple Tencent Cloud regions. Cross-regional data synchronization can be achieved through policy data replication. Modifications to CAM policy can be submitted timely, but cross-regional policy synchronization may delay the time policy takes effect. Additionally, CAM uses cache (currently one minute) to improve performance, and the update does not take effect until cache expires.

## Access Management Use Cases
### Enterprise sub-account permission management
Enterprise employees should have the minimal access permissions to the enterprise's cloud resources, based on their positions.

Scenario: An enterprise has many cloud resources (CVM, VPC instances, CDN instances, COS buckets and objects, etc.) and many employees (developers, testers, OPS personnel, etc.).
Some developers need the read and write permissions to the project-related cloud resources on the development servers. Testers need the read and write permissions to the project-related cloud resources on the test servers. OPS personnel are responsible for the purchase and daily operation of the servers. If the responsibilities of an employee or the projects he involves have changed, the corresponding permissions should be terminated.

### Cross-enterprise permission management
Different enterprises need to share cloud resources.

Scenario: An enterprise that owns many cloud resources focuses on product research and development, and delegates its OPS of cloud resources to another operating enterprise. When their delegation contract terminates, the corresponding permissions should be terminated.

## Policy Syntax
A policy consists of several elements and is used to describe specific information about authorization. Core elements include principal, action, resource, condition, and effect. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

>- The elements must be lowercase. There is no requirement on the description order.
>- If there is no particular condition restrictions on the policy, condition element is optional.
>- It is not allowed to write principal element in the console. You can only use principal in policy management APIs and policy syntax related parameters.

### Core elements
#### version
It describes the version of policy syntax. The only available value is "2.0". This element is required.

#### principal
It describes the entity to be authorized by the policy, including users (developers, sub accounts, anonymous users), and user groups. This element can only be used in policy management APIs and policy syntax related parameters.

#### statement
It describes the detailed information of one or more permissions. This element includes permissions or a permission set of multiple elements such as effect, action, resource and condition. A policy has only one statement. This element is required.

#### action
It describes the action to be allowed or denied. An action can be an API (described using the prefix "name") or a feature set (a set of specific APIs, described using the prefix "permid"). This element is required.

#### resource
It describes the detailed data of authorization. A resource is described using 6-piece format. Detailed resource definition for each product is different. For information on how to specify a resource, see the documentation for the product whose resources you're writing a statement for. This element is required.

#### condition
It describes the condition for the policy to become effective. A condition consists of operator, operational key and operate value. A condition value may include information such as time and IP address. In some services, you can specify other values in condition. This element is optional.

#### effect
It describes the effect of the declaration, which is "allow" or "deny". This element is required.

### Policy limits
| Limited Item | Value |
| ----------------------------------- | --------- |
| Number of user groups in a primary account | 20 |
| Number of sub-users in a primary account | 1000 |
| Number of user groups that a sub-user can be added to | 10 |
| Number of sub-users in a user group | 100 |
| Number of policies for a primary account | 1000 |
| Number of policies associated to a CAM user/user group | 20 |
| Maximum characters allowed for a custom policy | 4096 |

### Policy examples
The policy in this example allows the sub-account with ID 3232523 and the group with ID 18825 that belong to the primary account with ID 1238423 to have permissions to use all COS read APIs and write objects, as well as to send message queues, for the COS bucket "bucketA" in Beijing region and the COS object "object2" in Guangzhou region, on condition that access IP falls within the IP address range of `10.*.*.10/24`.

```json
{     
        "version":"2.0", 
        "principal":
		   {"qcs":["qcs::cam::uin/1238423:uin/3232523", 
                        "qcs::cam::uin/1238423:groupid/18825"]
		   }, 
        "statement": 
        [ 
           { 
              "effect":"allow", 
              "action":["name/cos:PutObject","permid/280655"], 
              "resource":["qcs::cos:ap-beijing:uid/1238423:bucketA-1238423/*", 
                        "qcs::cos:ap-guangzhou:uid/1238423:bucketB-1238423/object2"], 
               "condition": {"ip_equal":{"qcs:ip":"10.*.*.10/24"}} 
           }, 
           { 
             "effect":"allow", 
             "action":"name/cmqqueue:Sendmessages", 
             "resource":"*" 
           } 
       ] 
}
```

