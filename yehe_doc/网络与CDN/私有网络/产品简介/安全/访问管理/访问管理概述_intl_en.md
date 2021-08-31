If you are using multiple Tencent Cloud services such as VPC, CVM, and TencentDB that are managed by different users sharing your Tencent Cloud account key, you may encounter the following problems:
- Your key is shared by multiple users, which poses a high risk of leakage.
- You cannot limit the access permissions of other users, which poses a security risk due to potential misoperation.

To prevent these problems, you can use sub-accounts to allow different users to manage different services. By default, a sub-account has no permission to use a CVM or CVM-related resources. Therefore, you need to create a policy to grant the required resources or permissions to sub-accounts.

## Overview
Cloud Access Management (CAM) is a web service provided by Tencent Cloud to help customers manage the permissions to access resources under their Tencent Cloud accounts in a secure way. You can use CAM to create, manage, and terminate users (or user groups), and use identity management and policy management to control Tencent Cloud resources that can be used by each user.

When using CAM, you can associate a policy to a user or a group of users. The policy can authorize or deny users’ requests of using specified resources to complete specified tasks.
- For more basic information on CAM policies, see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603).
- For more usage information on CAM policies, see [Policies](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to manage the access permissions of sub-accounts for VPC resources, you can skip this section. This will not affect your understanding and usage of other parts in the document.



## Getting Started
A CAM policy must authorize or deny the use of one or more VPC operations. At the same time, it must specify the resources (which can be all resources or partial resources for certain operations) that can be used for the operations. The policy can also include the conditions set for the operation resources.

Some VPC API operations support resource-level permissions. That is, when calling these APIs, you cannot specify some resources for the operations. Instead, you must specify all resources for the operations.


| Task | Link |
| -------------------- | -------------------- |
| Basic structure of a policy | Policy Syntax |
| Define operations in the policy | VPC Operations|
| Define resources in the policy | VPC Resource Paths |
| Resource-level permissions supported by VPC | [Resource-Level Permissions Supported by VPC](https://intl.cloud.tencent.com/document/product/215/31862) |
| Console example | [Console Example](https://intl.cloud.tencent.com/document/product/215/31861) |
