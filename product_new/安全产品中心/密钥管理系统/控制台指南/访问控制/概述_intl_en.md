
If you use multiple services such as KMS, VPC, CVM, and TencentDB, which are managed by different users sharing your Tencent Cloud account key, the following problems may exist:

- Your key is shared by multiple users, leading to high risk of compromise.
- You cannot control the access permissions of other users, which poses a security risk due to potential accidental operations.

[Cloud Access Management (CAM)](https://cloud.tencent.com/document/product/598/17848) is used to manage the access permissions for the resources under Tencent Cloud accounts. With CAM, you can use the identity management and policy management features to control which Tencent Cloud resources can be accessed by which sub-accounts.

For example, if you have a CMK under your root account, and you want it to be used by sub-account A but not sub-account B, you can control the permissions of the sub-accounts by configuring a corresponding policy in CAM.

If you do not need to manage the access to KMS resources by sub-accounts, you can skip this chapter. This will not affect your understanding and usage of other parts in the documentation.


### Basic CAM Concepts
The root account authorizes sub-accounts by binding policies. The policy setting can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

- **Account**
 - **Root account**: As the fundamental owner of Tencent Cloud resources, a root account acts as the basis for resource usage fee calculation and billing and can be used to log in to Tencent Cloud services.
 **Sub-account**: An account created by the root account, which has a specific ID and identity credential that can be used to log in to the Tencent Cloud Console. A root account can create multiple sub-accounts (users). **A sub-account does not own any resources by default; instead, such resources should be authorized by its root account.**
 - **Identity credential**: This includes login credentials and access certificates. **Login credential** refers to user login name and password. **Access certificate** refers to the TencentCloud API keys (SecretId and SecretKey).
- **Resources and permissions**
 - **Resource**: A resource is an object that is managed in Tencent Cloud services, such as a CMK in KMS, a CVM instance, a bucket in COS, or a VPC instance.
 - **Permission**: Permission is an authorization to allow or forbid certain users to perform certain operations. By default, **a root account has full access to all the resources under it**, while **a sub-account does not have access to any resources under its root account**.
 - **Policy**: Policy is the syntax rule used to define and describe one or multiple permissions. **A root account** performs authorization by **associating policies** with users/user groups.

For more information, please see the [CAM](https://intl.cloud.tencent.com/document/product/598/10583) product documentation.

### Related Documents
| Document Description | Link | 
|---------|---------|
| Relationship between policy and user | [Policy Management](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) | 
| More products that support CAM | [List of Tencent Cloud Services that Support CAM](https://intl.cloud.tencent.com/document/product/598/10588)|
