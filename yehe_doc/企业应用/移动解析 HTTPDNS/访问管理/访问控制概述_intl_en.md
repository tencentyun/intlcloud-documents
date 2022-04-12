
[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) is used to manage the access permissions for the resources under Tencent Cloud accounts. With CAM, you can use the identity management and policy management features to control which Tencent Cloud resources can be accessed by which sub-accounts.

For example, if your account has HTTPDNS domains deployed in different projects, to strengthen access control, you can authorize resources and assign the admin of project A an authorization policy, specifying that only the admin can manipulate the HTTPDNS domain resources under project A.

You can skip this section if you don't need to manage the permissions of HTTPDNS resources for sub-users.
>!Currently, CAM-based access authorization is only supported in the console.
## Basic CAM Concepts
A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

1. **Account**
 - **Root account**: The owner of Tencent Cloud resources and the fundamental entity for resource usage, usage calculation, and billing. It can be used to log in to Tencent Cloud services.
 - **Sub-account**: An account created by the root account. It has a specific ID and identity credential that can be used to log in to the Tencent Cloud console. A root account can create multiple sub-accounts (users). **By default, a sub-account does not own any resources and must be authorized by its root account.**
 - **Identity credential**: Includes login credentials and access certificates. **Login credential** refers to a user's login name and password. **Access certificate** refers to Tencent Cloud API keys (`SecretId` and `SecretKey`).
2. **Resources and permissions**
 - **Resource**: An object that is operated in Tencent Cloud services, such as a CVM instance, a COS bucket, or a VPC instance.
 - **Permission**: An authorization that allows or forbids users to perform certain operations. By default, **the root account has full access to all resources under the account, while a sub-account does not have access to any resources under its root account.**
 - **Policy**: Syntax rule that defines and describes one or more permissions. The **root account** performs authorization by **associating policies** with users/user groups.
 
For more information, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

## Relevant Documentation
| Document Description | Link | 
|---------|---------|
| Relationship between policy and user | [Policy](https://intl.cloud.tencent.com/document/product/598/10601) | 
| Basic policy structure | [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10603) | 
| CAM-enabled products | [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588) | 


