
Assume that you are using multiple Tencent Cloud services, such as Game Server Engine (GSE), VPC and TencentDB. These services are managed by different users who all share your Tencent Cloud account key. Then, the following problems may exist:

- Your key is shared by multiple users, which means your key runs a high risk of being compromised.
- You cannot restrict the access permissions of other users, which poses a security risk due to potential misoperations.

These problems can be eliminated by the use of CAM, which allows you to authorize sub-accounts to manage your different services. By default, a sub-account has no access to GSE service or its resources. To grant a sub-account such access, you need to create a CAM policy. For more information on CAM, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

A policy is a syntax specification that defines one or more permissions. It allows or denies the access to a specified resource by authorizing a user or a group of users.
For more information on CAM policy elements, please see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603).
For more information on how to use CAM policies, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601).

>?If you do not need to manage access permissions to GSE resources for sub-accounts, you can skip this part. This will not affect your understanding and use of other parts of the documentation.

## Getting Started

A CAM policy must permit or deny one or more GSE operations. Besides, you must specify some (or all) resources to operate on.

Some GSE APIs support resource-level permissions, which means that you can choose to specify either specific or all resources when calling these APIs.

| Task | Link |
| -------------------- | ---------------------------------------------- |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/1055/37778) |
| Defining operations in a policy | [GSE Operations](https://intl.cloud.tencent.com/document/product/1055/37778#test5) |
| Defining resources in a policy | [GSE Resource Path](https://intl.cloud.tencent.com/document/product/1055/37778#test6) |
| Resource-level permissions for GSE | [Authorizable Resource Types](https://intl.cloud.tencent.com/document/product/1055/37777)              |
| Console Demo | [Access Control Examples](https://intl.cloud.tencent.com/document/product/1055/37779) |
