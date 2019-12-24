## Overview
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you with the security management of access permissions for resources under your Tencent Cloud account. With CAM, you can create, manage, and terminate users or user groups, and can use identity and policy management to control the permissions other users have to use Tencent Cloud resources. Policies can be used to authorize or block the use of specified resources by users to complete specified tasks. When you use CAM, you can associate policies with a user or user group to perform permissions control.

BatchCompute is already integrated with CAM. You can use CAM to control the permissions for resources related to BatchCompute.


## Related concepts
#### CAM users
[CAM users](https://intl.cloud.tencent.com/document/product/598/32633) are entities that you create in Tencent Cloud, and each CAM user is associated with only one Tencent Cloud account. The Tencent Cloud account you register is the **root account**. You can also create **sub-accounts** with different permissions in [Cloud Access Management](https://console.cloud.tencent.com/cam). There are 3 types of sub-accounts: [sub-users](https://intl.cloud.tencent.com/document/product/598/13674), [collaborators](https://intl.cloud.tencent.com/document/product/598/32639), and [message recipients](https://intl.cloud.tencent.com/document/product/598/13667).

#### Policies
[The policy](https://intl.cloud.tencent.com/document/product/598/10601) is the syntax rule used to define and describe one or more permissions. CAM supports two types of policies: preset policy and custom policy.
 - Preset policies: Policies created and managed by Tencent Cloud. These are some common permission sets that are frequently used by users, such as full read and write permissions for resources. Preset policies have a wide range of operation objects, coarse operation granularity, and are preset by the system. They cannot be edited by users.
 - Custom policies: Policies created by users. These permit fine-grained division of permissions. For example, a usage policy is associated with a sub-account that gives the sub-account management permissions for the computing environment of BatchCompute, but no management permissions for TencentDB instances.

#### Resources
[Resource](https://intl.cloud.tencent.com/document/product/598/10606) is an element of policies that describes one or multiple operation objects. For example, BatchCompute computing environment or jobs.


## Preset policies of BatchCompute

| Preset Policies                  | Permissions Granted                                                 |
| :-------------------------- | :----------------------------------------------------------- |
| QcloudBatchFullAccess       | Users associated with this policy will have full read and write access permissions to all BatchCompute resources.                   |
| QcloudBatchReadOnlyAccess   | Users associated with this policy will have read-only permission to all BatchCompute resources.                     |
| QcloudFullAccessForBatchRole| Users associated with this policy will have access to other Tencent Cloud products while using BatchCompute. This includes access permissions for products such as CVM, VPC, COS, CMQ Topic, CMQ Queue, CLS, and Cloud Monitor.  |


## Authorizable resource types
Resource-level permissions specify which resources a user can operate. For example, you can authorize a user to have operation permissions for computing environments in Guangzhou region.
The resource types of BatchCompute that can be authorized through CAM are as follows:

| Resource Type | Resource Description Method in Authorization Policy |
| :------------| :------------------------------------------ |
| Job-related    | `qcs::batch:$region:$account:job/*`           |
| Computing environment-related| `qcs::batch:$region:$account:computeenv/*`    |
| Task template-related| `qcs::batch:$region:$account:tasktemplate/*`  |


The following table lists the resource-level permissions operations APIs that BatchCompute supports, as well as the resource path supported by each operation.
When setting the resource path, you must modify variable parameters such as `$region`, `$account`, `$EnvId`, `$JobId`, and `$TaskTemplateId` according to your actual parameter information. You can also use `*` in the path as a wildcard character.
For information about related concepts in CAM policies such as region, action, account, and resource, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).
>Any BatchCompute API operation not listed in the table does not support resource-level permission. For such operations, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

| API: action                |  Resource path: resource                                            |
| :---------------------------- | :------------------------------------------------------------ |
| CreateCpmComputeEnv          |`qcs::batch:$region:$account:computeenv/*`                     |
| CreateComputeEnv            |`qcs::batch:$region:$account:computeenv/*`                     |
| DeleteComputeEnv            |`qcs::batch:$region:$account:computeenv/$EnvId`                |
| ModifyComputeEnv            |`qcs::batch:$region:$account:computeenv/$EnvId`                |
| TerminateComputeNode        |`qcs::batch:$region:$account:computeenv/$EnvId`                |
| TerminateComputeNodes        |`qcs::batch:$region:$account:computeenv/$EnvId`                |
| DescribeComputeEnv          |`qcs::batch:$region:$account:computeenv/$EnvId`                |
| DescribeComputeEnvActivities|`qcs::batch:$region:$account:computeenv/$EnvId`                |
| DescribeComputeEnvCreateInfo  |`qcs::batch:$region:$account:computeenv/$EnvId`                |
| DescribeComputeEnvCreateInfos|`qcs::batch:$region:$account:computeenv/*`<br>`qcs::batch:$region:$account:computeenv/$EnvId`               |
| DescribeComputeEnvs          |`qcs::batch:$region:$account:computeenv/*`<br>`qcs::batch:$region:$account:computeenv/$EnvId`               |
| SubmitJob                    |`qcs::batch:$region:$account:job/*`                            |
| DeleteJob                    |`qcs::batch:$region:$account:job/$JobId`                       |
| TerminateJob                |`qcs::batch:$region:$account:job/$JobId`                       |
| TerminateTaskInstance        |`qcs::batch:$region:$account:job/$JobId`                       |
| DescribeJob                  |`qcs::batch:$region:$account:job/$JobId`                       |
| DescribeJobs                  |`qcs::batch:$region:$account:job/*`<br>`qcs::batch:$region:$account:job/$JobId`                             |
| DescribeJobSubmitInfo        |`qcs::batch:$region:$account:job/$JobId`                       |
| DescribeTask                |`qcs::batch:$region:$account:job/$JobId`                       |
| DescribeTaskLogs            |`qcs::batch:$region:$account:job/$JobId`                       |
| CreateTaskTemplate          |`qcs::batch:$region:$account:tasktemplate/*`                   |
| DeleteTaskTemplates          |`qcs::batch:$region:$account:tasktemplate/*`<br>`qcs::batch:$region:$account:tasktemplate/$TaskTemplateId`  |
| ModifyTaskTemplate          |`qcs::batch:$region:$account:tasktemplate/$TaskTemplateId`      |
| DescribeTaskTemplates        |`qcs::batch:$region:$account:tasktemplate/*`<br>`qcs::batch:$region:$account:tasktemplate/$TaskTemplateId`  |


## BatchCompute CAM policy example
The following section provides two specific examples that display how to use CAM to control permissions for BatchCompute:

- Create a policy to prohibit access to any computing environment in Guangzhou region.
	


```
# In this example, `$account` must be substituted with the account information, and `$EnvId` must be substituted with the corresponding `EnvId`
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/batch:*"
            ],
            "resource": [
                "qcs::batch:ap-guangzhou:$account:computeenv/*"
            ]
        },
        {
            "effect": "deny",
            "action": [
                "name/batch:*"
            ],
            "resource": [
                "qcs::batch:ap-guangzhou:$account:computeenv/$EnvId"
            ]
        }
    ]
}
```
- Policy created: grant access permissions on jobs' reading APIs  in all regions.	
```
# In this example, `$account` must be substituted with the account information
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/batch:DescribeJobs",
                "name/batch:DescribeJobSubmitInfo",
                "name/batch:DescribeJob",
                "name/batch:DescribeTask",
                "name/batch:DescribeTaskLogs"
            ],
            "resource": [
                "qcs::batch::$account:job/*"
            ]
        }
    ]
}
```