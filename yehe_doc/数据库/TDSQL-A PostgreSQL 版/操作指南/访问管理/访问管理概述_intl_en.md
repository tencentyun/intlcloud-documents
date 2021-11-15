
## Issues
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the following problems:
- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

## Solution
You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account does not have permissions to use Tencent Cloud services or resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

[Cloud Access Management (CAM)](https://cloud.tencent.com/document/product/598/10583) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the specified Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Policy Syntax](https://cloud.tencent.com/document/product/598/10603). For detailed directions, please see [Policy](https://cloud.tencent.com/document/product/598/10601).

You can skip this section if you do not need to manage permissions to TDSQL-A resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

### Getting started
A CAM policy must authorize or deny the use of one or more TDSQL-A for PostgreSQL operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.
>?
>- We recommend you manage TDSQL-A for PostgreSQL resources and authorize TDSQL-A for PostgreSQL operations through CAM policies. Although the user experience does not change for existing users who are granted permissions by project, we do not recommend you continue to manage resources and authorize operations in a project-based manner.
>- Effectiveness conditions cannot be set for TDSQL-A for PostgreSQL for the time being.


