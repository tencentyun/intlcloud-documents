## CAM Introduction

### Basic concepts
The root account authorizes sub-accounts by binding policies. The policy setting can be accurate to **"API, Resource, User/User Group, Allow/Deny, Condition"**.

#### Account

**Root account**: As the fundamental owner of Tencent Cloud resources, root account acts as the basis for resource usage fee calculation and billing, and can be used to log in to Tencent Cloud services.
**Sub-account**: An account created by the root account, which has a specific ID and identity credential that can be used to log in to Tencent Cloud console. A root account can create multiple sub-accounts (users). **A sub-account does not own any resources by default, and must be authorized by its root account.**
**Identity credential**: Includes login credential and access certificate. **Login credential** refers to a user’s login name and password, while **access certificate** refers to the Cloud API key (SecretID and SecretKey).

#### Resources and permission
- **Resource**: Resources are objects that the cloud services operate on, such as the CVM instance, COS bucket and VPC instance.
- **Permission** : Permission is an authorization to allow or forbid users to perform certain operations. By default, **root account has full access to all resources under the account**, while **sub-accounts do not have access to any resources under its root account**.
- **Policy** : Policy is the syntax rule used to define and describe one or more permissions. **Root account** performs authorization by **associating policies** with users/user groups.

### Related Documents
| Content                     | Link                                                         |
| ------------------------ | ------------------------------------------------------------ |
| Relationship between policy and user | [Policy Management](https://intl.cloud.tencent.com/document/product/598/10603)
| Basic structure of policy | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) |
| More products that support CAM | [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588) |

[Click to learn more about CAM](https://intl.cloud.tencent.com/document/product/598)

## API Gateway Resources
```
- qcs::APIgateway:_`region`_:uin/_`uin—id`_:service/_`serviceid`_
- qcs::APIgateway:_`region`_:uin/_`uin—id`_:service/_`serviceid`_/API/_`apiid`_
- qcs::APIgateway:_`region`_:uin/_`uin—id`_:usagePlan/_`usagePlanid`_
- qcs::APIgateway:_`region`_:uin/_`uin—id`_:secret/_`secretid`_
- qcs::APIgateway:_`region`_:uin/_`uin—id`_:IPStrategy/_`IPStrategyId`_
- qcs::APIgateway:_`region`_:uin/_`uin—id`_:logRule/_`logRuleId`_
```
All creation APIs are at account level, while other APIs are at resource level.

## CAM Policy Examples 

### Full read-write policy for any API Gateway resources
The following policy statement gives the sub-user permission to fully manage (creating, managing, etc.) any API services.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "apigw:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

You can also configure the system's [full read-write policy](https://console.cloud.tencent.com/cam/policy/createV2) to support this permission.
![](https://main.qcloudimg.com/raw/e008d17424a460d631754dffe36903f7.png)

### Full management policy for single API Gateway service 
The following policy statement gives the sub-user permission to fully manage (creating, managing, etc.) a specified API service:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "apigw:*"
            ],
            "resource":"qcs::apigw:ap-guangzhou:uin/{ownerUin}:service/service-id/API/api-id",
            "effect": "allow"
        }
    ]
}
```

### Read-only policy for single API Gateway service 
1. Create a policy with policy generator, and grant the permissions to list information for all resources and product monitoring. The following policy statement will grant read-only permission to all resources of the account.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "apigw:Describe*",
                "apigw:GenerateApiDocument"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

2. Grant read-only permission to a single API.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "ckafka:Get*",
                "ckafka:List*"
            ],
            "resource": "qcs::apigw:ap-guangzhou:uin/{ownerUin}:service/service-id/API/api-id",
            "effect": "allow"
        }
    ]
}
```
