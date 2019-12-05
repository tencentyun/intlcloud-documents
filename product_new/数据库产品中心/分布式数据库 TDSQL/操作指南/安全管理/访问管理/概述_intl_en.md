If you use multiple Tencent Cloud services such as TencentDB, CVM, and VPC that are managed by different users sharing your Tencent Cloud account key, you may face the following problems:
- Your password is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permission of other users, which is easy to pose a security risk due to faulty operations.

This is exactly why CAM has been developed.
For a detailed description of CAM, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

After connecting to CAM, you can allow different users to manage different services through sub-accounts so as to avoid the above problems. By default, a sub-account doesn't have permission to use a TencentDB instance or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.

A policy is a syntax rule used to define and describe one or more permissions. It can authorize or deny the use of the designated resources by a user or user group. For more information on CAM policy, see [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603). For more information on how to use a CAM policy, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to manage the access permission to TencentDB resources for sub-accounts, you can skip this chapter. This will not affect your understanding and usage of other parts in the documentation.

### Getting Started
A CAM policy must authorize or deny the use of one or more TencentDB operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

>
> - You are recommended to manage TencentDB resources and authorize TencentDB operations through CAM policies. Although the experience stays the same for existing users who are granted permission by project, it is not recommended to continue managing resources and authorizing operations in a project-based manner.
>- Effectiveness conditions cannot be set for TencentDB for the time being.

