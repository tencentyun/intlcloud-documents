If you use multiple Tencent Cloud services such as CLB, CVM, and TencentDB that are managed by different users sharing your Tencent Cloud account key, you may face the following problems:
- Your key is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permissions of other users, which poses a security risk due to potential faulty operations.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) is used to manage the access permissions to your Tencent Cloud resources. With CAM, you can use the identity management and policy management features to control which Tencent Cloud resources can be accessed by which sub-accounts.

For example, if you have multiple CLB instances under your account that are deployed in different projects, to manage access permissions and authorize resources, you can bind the admin of project A with an authorization policy, which states that only this admin can use the CLB resources under project A.

If you do not need to manage the access permission to CLB resources for sub-accounts, you can skip this chapter. This will not affect your understanding and usage of other parts in the documentation.

## Basic Concepts in CAM
The root account authorizes sub-accounts by binding policies. The policy setting can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

1. Account
 - **Root account**
 As the fundamental owner of Tencent Cloud resources, a root account acts as the basis for resource usage fee calculation and billing, and can be used to log in to Tencent Cloud services.
 - **Sub-account**
 A sub-account is created by the root account, and it has a specific ID and identity credential that can be used to log in to the Tencent Cloud Console. A root account can create multiple sub-accounts (users). **A sub-account does not own any resources by default; instead, such resources should be authorized by its root account.**
 - **Identity credential**
This includes login credentials and access certificates. **Login credential** refers to the username and password. **Access certificate** refers to the TencentCloud API keys (SecretId and SecretKey).
2. Resources and permissions
 - **Resource**
A resource is an object that is managed in Tencent Cloud services, such as a CVM instance, a bucket in COS, or a VPC instance.
 - **Permission**
Permission is an authorization to allow or forbid certain users to perform certain operations. By default, **a root account has full access to all the resources under it**, while **a sub-account does not have access to any resources under its root account**.
 - **Policy**
Policy is the syntax rule used to define and describe one or multiple permissions. **A root account** performs authorization by **associating policies** with users/user groups.

 For more information, please see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

## Related Documents

| Document Description | Link |
| ----------------------- | ------------------------------------------------------------ |
| Relationship between policy and user | [Policy](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic policy structure | [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603) |
| More products that support CAM | [CAM-enabled Cloud Services](https://intl.cloud.tencent.com/document/product/598/10588) |
