If you have activated several Tencent Cloud services, such as VPC, CVM and TencentDB, and you let other users to manage these services by sharing your cloud account key, the following problems may arise:
- The possibility of your key being compromised is high because it is shared by several users. 
- The access of other users is not under control. They can introduce security risks caused by misoperations.

To avoid the above problems, you can create sub-accounts for other users to manage different services. By default, a sub-account can not work with VPCs. Therefore, you need to create a policy to grant VPC-related permissions to them.
>? 
>+ VPC supports access control on the resource level, such as an ENI.
>+ Skip this chapter if you don’t need to manage the access permission of sub-accounts for VPC resources.
>

## Overview
Tencent Cloud’s [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598) is a web service that helps you manage the access permissions for resources under your Tencent Cloud accounts. With CAM, you can create, manage, or terminate users (user groups), and manage identities and policies to allow specific users to access and use specific Tencent Cloud resources.

You can use CAM to bind a user or user group to a policy which allows or denies them access to specified resources to complete specified tasks.
- For more information on CAM policy elements, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).
- For more information on how to use CAM policies, see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).



## Getting Started
A CAM policy allows or denies one or more VPC operations. You need to specify the target of the operation. The policy can also include some custom conditions.

Some APIs do not support resource-level permissions, which means that you cannot specify resources when using those APIs.



| Content | Reference|
| -------------------- | -------------------- |
| Basic policy structure | [Authorization Policy Syntax](https://intl.cloud.tencent.com/document/product/576/44374) |
| Defining operations in a policy | [ENI Operations](https://intl.cloud.tencent.com/document/product/576/44374) |
| Defining resources in a policy | ENI Resource Path](https://intl.cloud.tencent.com/document/product/576/44374) |
| Resource-level permissions supported by ENI | [Resource-level Permissions Supported by ENI](https://intl.cloud.tencent.com/document/product/215/31862) |
| CAM examples | [CAM Examples](https://intl.cloud.tencent.com/document/product/576/44375) |
