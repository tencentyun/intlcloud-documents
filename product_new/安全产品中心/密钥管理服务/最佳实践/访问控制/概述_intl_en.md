
If you use multiple services such as KMS, VPC, CVM, and TencentDB, and these services are managed by different users that all share your Tencent Cloud account key, you would be facing the following issues:

- Your password is shared by multiple users, leading to high risk of compromise.
- You cannot limit the access permission of other users, which makes it vulnerable to operational errors and poses a security risk.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) is used to manage the access permissions for the resources under Tencent Cloud accounts. With CAM, you can use identity management and policy management for granular access control of your Tencent Cloud resources.

For example, if you have a master key under your root account, and you want it to be used by sub-account A but not sub-account B, you can control the permissions of the sub-accounts by configuring a corresponding policy in CAM.

If you do not need to manage the access permission to KMS resources for sub-accounts, you can skip this section. This does not affect the use of the remaining documentation.


### Basic CAM Concepts
The root account authorizes sub-accounts by binding policies. The policy setting can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

- **Account**
 - **Root account**: As the fundamental owner of Tencent Cloud resources, a root account acts as the basis for resource usage fee calculation and billing and can be used to log in to Tencent Cloud services.
 - **Sub-account**: An account created by the root account, which has an ID and identity credential and can be used to log in to Tencent Cloud console. A root account can create multiple sub-accounts (sub-users). **A sub-account does not own any resources by default and needs to be authorized by its root account to access resources.**
 - **Identity credential**: This includes login credentials and access certificates. **Login credential** refers to user login name and password. **Access certificate** refers to the Cloud API keys (SecretID and SecretKey).
- **Resources and Permissions**
 - **Resource**: A resource is an object that is managed in Tencent Cloud services, such as a master key in KMS, a CVM instance, a bucket in COS, or a VPC instance.
 - **Permission**: Permissions allow or forbid users to perform operations. By default, **a root account has full access to all the resources in its account**, while **a sub-account does not have access to any resources in its root account**.
 - **Policy**: Policy is the syntax rule used to define and describe one or more permissions. **A root account** performs authorization by **associating policies** with users/user groups.

For more information, see the [CAM](https://intl.cloud.tencent.com/document/product/598/10583) product documentation.

### Related Documents
| Document description | Link |
|---------|---------|
| Relationship between policy and user | [Policy Management](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) |
| More products that support CAM | [List of Cloud Services that Support CAM](https://intl.cloud.tencent.com/document/product/598/10588) |
