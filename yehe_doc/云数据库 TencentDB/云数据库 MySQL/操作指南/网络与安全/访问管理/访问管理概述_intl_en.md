## Known Issues
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

## Solutions
You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account does not have permissions to use Tencent Cloud services or resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups. You can manage identities and policies to allow specific users to access your Tencent Cloud resources.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603).

You can skip this section if you do not need to manage permissions to TencentDB resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

### Getting started
A CAM policy is used to allow or deny one or more TencentDB operations. When configuring a policy, you must specify the target resources of the operations, which can be all resources or specified resources. A policy can also include conditions where the resources can be used.

>?
>- We recommend you manage TencentDB resources and authorize TencentDB operations through CAM policies. Although the user experience does not change for existing users who are granted permissions by project, we do not recommend you continue to manage resources and authorize operations in a project-based manner.
>- Conditions cannot be set in TencentDB for the time being.

| Task | Link | 
|---------|---------|
| Learn more about the basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/236/14466) |
| Define operations in a policy | [TencentDB Operations](https://intl.cloud.tencent.com/document/product/236/14466) | 
| Defines resources in a policy | [TencentDB Resource Path](https://intl.cloud.tencent.com/document/product/236/14466)|
| Resource-level permission supported by TencentDB | [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/236/14467)|
| Console sample | [Console Sample](https://intl.cloud.tencent.com/document/product/236/14468) |
