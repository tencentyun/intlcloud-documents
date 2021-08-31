## Known Issues
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, TencentDB for PostgreSQL, and other TencentDB products, and they all share your Tencent Cloud account access key, you may face the following problems:

- The risk of your key being compromised is high since multiple users are sharing it.
- Your users might introduce security risks from misoperations due to the lack of user access control.

## Solutions
You can avoid the problems above by allowing different users to manage different services through sub-accounts. By default, a sub-account does not have permissions to use TencentDB for PostgreSQL or its resources. Therefore, you need to create a policy to grant different permissions to the sub-accounts.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a Tencent Cloud service that helps you securely manage and control access to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users and user groups. You can manage identities and policies to allow specific users to access your Tencent Cloud resources.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).

You can skip this section if you do not need to manage permissions to PostgreSQL resources for sub-accounts. This will not affect your understanding and use of the other sections of the document.

### Getting started
A CAM policy is used to allow or deny one or more PostgreSQL instance operations. When configuring a policy, you must specify the target resources of the operations, which can be all resources or specified resources. A policy can also include conditions where the resources can be used.

Some PostgreSQL APIs do not support resource-level permissions, which means that you cannot specify resources when using those APIs.


| Task                        | Link                                                         |
| --------------------------- | ------------------------------------------------------------ |
| Understand the basic structure of policies | [Access Policy Syntax > Policy Syntax](https://intl.cloud.tencent.com/document/product/409/38835#clyf)|
| Define operations in a policy | [Access Policy Syntax > PostgreSQL Operations](https://intl.cloud.tencent.com/document/product/409/38835#cz) |
| Define resources in a policy | [Access Policy Syntax > PostgreSQL Resource Paths](https://intl.cloud.tencent.com/document/product/409/38835#zylj) |
| View supported resource-level permissions | [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/409/38836)|
| View console examples | [Console Examples](https://intl.cloud.tencent.com/document/product/409/38837) |
