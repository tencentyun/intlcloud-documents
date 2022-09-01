
## Issues
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from maloperations due to the lack of user access control.

## Solution
You can avoid the above problems by allowing different users to manage different services through sub-accounts. By default, sub-accounts don't have permissions to use Tencent Cloud services or resources. Therefore, you need to create policies to grant them different permissions.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions of your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

If you do not need to manage the access permissions to DBbrain resources for sub-accounts, you can skip this chapter. Skipping this chapter will not affect your understanding and usage of other parts in the documentation.

### Getting started
A CAM policy must authorize or deny the use of one or more DBbrain operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

>?
>- We recommend you manage DBbrain resources and authorize DBbrain operations through CAM policies. Although the user experience does not change for existing users who are granted permissions by project, we do not recommend you continue to manage resources and authorize operations in a project-based manner.
>- Currently, DBbrain does not support setting conditions for policies.

| Task | Document |
|---------|---------|
| Quickly authorize a sub-user | [Authorizing a sub-user](https://intl.cloud.tencent.com/document/product/1035/48610#gzyhsq) |
| Learn more about the basic policy structure | [Policy syntax](https://intl.cloud.tencent.com/document/product/1035/48610#clyf) |
| Define operations in a policy | [DBbrain operations](https://intl.cloud.tencent.com/document/product/1035/48610#cz) |
| Define resources in a policy | [Resources that can be manipulated by DBbrain](https://intl.cloud.tencent.com/document/product/1035/48610#zylj) |
| View supported resource-level permissions | [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/1035/36052)|

