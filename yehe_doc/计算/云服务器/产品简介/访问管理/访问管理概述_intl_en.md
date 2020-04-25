If you use more than one Tencent Cloud product, such as Cloud Virtual Machine (CVM) instances, VPCs, and cloud databases, it is more than likely that they are managed by different users. These users would all require access to your account, which may present the following problems:
- Your account is shared by multiple users, leading to a high risk of compromise.
- You cannot control the access permissions of other users, which poses a security risk of potential accidental operations.

Sub-accounts allow you to assign each user a different account they can use for access and assign them different permissions so they can perform their duties without the risk of interfering with others. By default, sub-accounts do not have permission to access CVM instances and related resources. You need to create appropriate policies for each sub-account to grant them access.

Cloud Access Management (CAM) is a web service provided by Tencent Cloud that helps customers securely manage and control access to their Tencent Cloud resources. CAM provides identity management and policy management that allows you to create, manage, or terminate users (groups) and to control who is allowed to access and use your Tencent Cloud resources.

CAM enables you to create policies that can be associated with users or user groups. These policies grant or deny users permission to access specific resources. For more information on CAM policies, refer to [Policies](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to manage access permissions to CVM resources for sub-accounts, you can skip this chapter. This will not affect your understanding of the other sections of the documentation.

## Getting Started

A CAM policy must permit or forbid the performance of one or more CVM operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or certain resources for certain operations). A policy can also include the conditions governing the use of resources.

Some CVM API operations support resource-level permissions, which means that you must specify all resources, rather than specific resources, when performing such API operations.

| Task | Link | 
|---------|---------|
| Learn more about the basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/213/10313) |
| Define operations in the policy | [CVM Operations](https://intl.cloud.tencent.com/document/product/213/10313) | 
| Define resources in the policy | [CVM Resource Path](https://intl.cloud.tencent.com/document/product/213/10313) |
| Limit the policy with conditions | [CVM Condition Keys](https://intl.cloud.tencent.com/document/product/213/10313) |
| Resource-level permissions supported by CVM | [Resource-level Permissions Supported by CVM](https://intl.cloud.tencent.com/document/product/213/10314) |
| Console sample | [Console Sample](https://intl.cloud.tencent.com/document/product/213/10312)|
