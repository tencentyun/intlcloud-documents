## Issues
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the following problems:
- Your key will be easily compromised because it is shared by several users.
- You cannot restrict the access from other users and your service will be vulnerable to the security risks caused by their maloperations.

## Solution
You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account does not have permissions to use Tencent Cloud services or resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

You can skip this section if you do not need to manage permissions to TencentDB resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

### Getting started
A CAM policy must authorize or deny the use of one or more TencentDB operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

>?
>- We recommend that you manage TencentDB resources and authorize TencentDB operations through CAM policies. Although the user experience does not change for existing users who are granted permissions by project, we do not recommend that you continue to manage resources and authorize operations in a project-based manner.
>- Effectiveness conditions cannot be set in TencentDB for the time being.

| Task | Link | 
|---------|---------|
| Basic policy structure | [Authorization Policy Syntax > Policy syntax](https://intl.cloud.tencent.com/document/product/236/14466)|
| Operation definition in a policy | [Authorization Policy Syntax > Operations in TencentDB](https://intl.cloud.tencent.com/document/product/236/14466)| 
| Resource definition in a policy | [Authorization Policy Syntax > TencentDB resources](https://intl.cloud.tencent.com/document/product/236/14466)|
| Resource-level permission supported by TencentDB | [Authorizable Resource Types > List of APIs supporting authorization at resource level](https://intl.cloud.tencent.com/document/product/236/14467)|
| Console examples | [Console Examples](https://intl.cloud.tencent.com/document/product/236/14468) |
