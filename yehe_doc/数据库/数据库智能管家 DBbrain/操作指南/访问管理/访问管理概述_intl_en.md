## Known Issues
If you use multiple Tencent Cloud services such as CVM, VPC, and TencentDB that are managed by different users sharing your Tencent Cloud account access key, you may face the following problems:
- Your key is shared by multiple users, which means your key runs a high risk of being compromised.
- You cannot limit the access permissions of other users, which poses a security risk due to potential faulty operations.

## Solution
You can allow different users to manage different services through sub-accounts and avoid the above problems. By default, a sub-account doesn't have permission to use a Tencent Cloud service or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups, and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

If you do not need to manage the access permissions to DBbrain resources for sub-accounts, you can skip this chapter. Skipping this chapter will not affect your understanding and usage of other parts in the documentation.

### Getting started
A CAM policy must authorize or deny the use of one or more DBbrain operations. At the same time, it must specify the resources that can be used for the operations (can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

>?
>- We recommend you manage DBbrain resources and authorize DBbrain operations through CAM policies. Although the user experience does not change for existing users who are granted permissions by project, we do not recommend you continue to manage resources and authorize operations in a project-based manner.
>- Currently, DBbrain does not support setting conditions for policies.

| Task | Link | 
|---------|---------|
| Quickly authorize sub-users | [Sub-User Authorization Operations](https://cloud.tencent.com/document/product/1130/39343#gzyhsq) |
| Understand the basic structure of policies | [Policy Syntax](https://cloud.tencent.com/document/product/1130/39343#clyf)|
| Define operations in a policy | [DBbrain Operations](https://cloud.tencent.com/document/product/1130/39343#cz) | 
| Define resources in a policy | [DBbrain Resources](https://cloud.tencent.com/document/product/1130/39343#zylj) |
| View supported resource-level permissions | [Supported Resource-Level Permissions](https://cloud.tencent.com/document/product/1130/39341)|

