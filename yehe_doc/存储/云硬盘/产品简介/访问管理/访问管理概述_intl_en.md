If you are using multiple Tencent Cloud services such as CVM, CBS, VPC, and TencentDB that are managed by different users who share your Tencent Cloud account key, you may face the following problems.
- Your key is shared by multiple users, leading to a high risk of disclosure.
- You cannot control the access permissions of other users, which poses a security risk due to potential misoperations.

In this case, you can use sub-accounts to allow different users to manage different services to avoid these problems. By default, a sub-account does not have the permission to use CVMs or CVM-related resources. Therefore, you need to create a policy to grant the required resources or permissions to the sub-account.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) is a set of web-based Tencent Cloud services that helps you securely manage and control access permissions to your Tencent Cloud resources. By using CAM, you can create, manage, and delete users (groups) and control who can use Tencent Cloud resources and which Tencent Cloud resources they can use through identity and policy management.

When using CAM, you can associate a policy with a user or a user group, which grants or denies them permission to use specified resources to perform specified tasks. For more information on CAM policy basics, see [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603). For more information on the use of CAM policies, see [Policies](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to manage the access permissions of sub-accounts to CBS resources, you can skip this section. This will not affect your understanding and application of the remaining sections of this document.

### Getting Started

A CAM policy must grant or deny the permission to one or more CBS operations. At the same time, it must specify the resources that can be operated on (which can be all resources or some resources for certain operations). A policy can also include the conditions set for the operations of the resources.

| Task | Link |
|---------|---------|
| Learn the basic structure of a policy | [Policy Syntax](https://intl.cloud.tencent.com/document/product/362/34221) |
| Define operations in a policy | [CBS Operations](https://intl.cloud.tencent.com/document/product/362/34221) |
| Define resources in a policy | [CBS Resource Paths](https://intl.cloud.tencent.com/document/product/362/34221) |
| Restrict a policy by conditions | [CBS Condition Keys](https://intl.cloud.tencent.com/document/product/362/34221) |
| Learn the resource-level permissions supported by CBS | [Resource-Level Permissions Supported by CBS](https://intl.cloud.tencent.com/document/product/362/34220) |
| View console examples | [Console Examples](https://intl.cloud.tencent.com/document/product/213/10312) |
