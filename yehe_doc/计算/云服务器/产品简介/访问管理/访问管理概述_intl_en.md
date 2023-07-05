If you use multiple Tencent Cloud services such as Cloud Virtual Machine (CVM), VPC, and TencentDB, it is likely they are managed by different users who all your account key. This presents the following challenges:
- Your key is shared by multiple users, leading to high risk of compromise.
- You cannot restrict user access to different resources, which poses a security risk due to potential misoperations.

You can use sub-accounts to solve these issues. Sub-accounts allow you to assign each user a different account so they can perform their duties without the risk of interfering with others. However, sub-accounts by default do not have the permission to access CVM instances and related resources. You need to create appropriate policies for each sub-account to grant them access.

Tencent Cloud provides a web service called Cloud Access Management (CAM) to help customers securely manage access to their resources under their Tencent Cloud accounts. CAM allows you to create, manage, or terminate users and user groups, and provides identity management and policy management to control who is allowed to access and use your Tencent Cloud resources.

You can associate CAM policies with a user or a user group to grant or deny them permissions to use specific resources to perform specific tasks. For more information on CAM policy, see [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603). For more information on how to use CAM policies, see [Policies](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to manage multi-user resource access, you can skip this section. Doing so does not affect your understanding of the rest of the article.

#### Getting started

A CAM policy must allow or deny one or more CVM operations, as well as the resources these actions target. A policy can also include the conditions governing the use of resources.

Some of the CVM APIs do not support resource-level permissions, which means that you must specify all resources, rather than specific resources, when performing such API operations.

| Task | Link | 
|---------|---------|
| Learn more about the basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/213/10313) |
| Define operations in the policy | [CVM Operations](https://intl.cloud.tencent.com/document/product/213/10313) | 
| Define resources in the policy | [CVM Resource Path](https://intl.cloud.tencent.com/document/product/213/10313) |
| Limit the policy with conditions | [CVM Condition Keys](https://intl.cloud.tencent.com/document/product/213/10313) |
| Resource-level permissions supported by CVM | [Resource-level Permissions Supported by CVM](https://intl.cloud.tencent.com/document/product/213/10314) |
| Console samples | [Console Samples](https://intl.cloud.tencent.com/document/product/213/10312) |
