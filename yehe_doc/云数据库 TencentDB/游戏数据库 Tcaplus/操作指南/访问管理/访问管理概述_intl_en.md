If you use multiple Tencent Cloud services such as TcaplusDB, VPC, CVM, and TencentDB which are managed by different users sharing your Tencent Cloud account key, the following problems may exist:
- Your password is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permissions of other users, which poses a security risk due to potential faulty operations.

You can allow different users to manage different services through sub-accounts so as to avoid the above problems. By default, a sub-account does not have permission to use a TcaplusDB service or related resources. Therefore, you need to create a policy to grant the required permission to the sub-account.

Cloud Access Management (CAM) is a web-based Tencent Cloud service that helps you securely manage and control access permissions to your Tencent Cloud resources. Using CAM, you can create, manage, and terminate users (groups), and control the Tencent Cloud resources that can be used by the specified user through identity and policy management.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks. For more information on CAM policies, please see [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603). For more information on how to use CAM policies, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

If you do not need to manage the access permissions to TcaplusDB resources for sub-accounts, you can skip this part. This will not affect your understanding and usage of other parts in the documentation.

#### Getting started

A CAM policy must authorize or deny the use of one or more TcaplusDB operations. At the same time, it must specify the resources that can be used for the operations (which can be all resources or partial resources for certain operations). A policy can also include the conditions set for the manipulated resources.

Certain TencentCloud APIs for TcaplusDB do not support resource-level permissions, which means that for this type of API operations, you cannot specify a given resource for use when they are performed; instead, you must specify all resources for use.

| Task | Link | 
|---------|---------|
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/213/10313)|
| Operation definition in a policy | [TcaplusDB Operations](https://intl.cloud.tencent.com/document/product/213/10313) | 
| Resource definition in a policy | [TcaplusDB Resource Path](https://intl.cloud.tencent.com/document/product/213/10313)|
| Using conditions to limit policies | [TcaplusDB Condition Keys](https://intl.cloud.tencent.com/document/product/213/10313)|
| Resource-level permissions supported by TcaplusDB | [Resource-Level Permissions Supported by TcaplusDB](https://intl.cloud.tencent.com/document/product/213/10314)|
| Console sample | [Console Sample](https://intl.cloud.tencent.com/document/product/213/10312)|
