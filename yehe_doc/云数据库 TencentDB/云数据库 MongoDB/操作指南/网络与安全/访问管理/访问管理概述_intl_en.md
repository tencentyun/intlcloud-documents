## Known Issues
If you use multiple Tencent Cloud services such as CVM, VPC, and TencentDB that are managed by different users sharing your Tencent Cloud account access key, you may face the following problems:
- Your key is shared by multiple users, which means your key runs a high risk of being compromised.
- Your users might introduce security risks from misoperations due to the lack of user access control.

## Solutions
These problems can be eliminated by the use of [sub-accounts](https://intl.cloud.tencent.com/document/product/598/32633) which allow you to authorize different users to manage your different services. By default, a sub-account has no access to Tencent Cloud services or resources. To grant a sub-account such access, you need to create a CAM policy.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups, and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Syntax Logic](https://intl.cloud.tencent.com/document/product/598/10603).

If you do not need to manage access permissions to TencentDB resources for sub-accounts, you can skip this chapter. This will not affect your understanding and use of the other sections of the document.

### Getting started
A CAM policy must authorize or deny the use of one or more MongoDB operations. At the same time, it must specify the resources that can be used for the operations (can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

> ?
>- We recommend you manage MongoDB resources and authorize MongoDB operations through CAM policies. Although the user experience does not change for existing users who are granted permissions by project, we do not recommend you continue to manage resources and authorize operations in a project-based manner.
>- Effectiveness conditions cannot be set for MongoDB for the time being.

| Relevant Information         | Link                                                         |
| ---------------- | ------------------------------------------------------------ |
| Basic policy structure | [CAM Policy Syntax](https://intl.cloud.tencent.com/document/product/240/32840) |
| Define operations in a policy | [TencentDB for MongoDB Operations](https://intl.cloud.tencent.com/document/product/240/32840) |
| Define resources in a policy | [TencentDB for MongoDB Resource Path](https://intl.cloud.tencent.com/document/product/240/32840) |
| Resource-level permissions | [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/240/32841) |

