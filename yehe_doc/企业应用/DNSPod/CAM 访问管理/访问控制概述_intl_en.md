[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) is used to manage the access permissions for the resources under Tencent Cloud or DNSPod accounts. With CAM, you can use identity management and policy management for granular access control of your Tencent Cloud resources.

Here is an example. Assume that you have several DNS resources under DNSPod that are deployed for different projects. You want to authorize granular access to your resources for better permission control. You can associate an authorization policy to the admin of Project A, stating that only this admin can operate DNS resources for Project A. Most DNSPod APIs support resource-level authorization. For more information, see [Available Resource Authorization Types](https://docs.dnspod.cn/dns/dnspod-cam-manage/).

You can skip this section if you don't need to manage the permissions of DNSPod resources for sub-accounts.

> Note: Both DNSPod APIs and the DNSPod console support access authorization via CAM.

## Basic CAM Concepts
The root account authorizes sub-accounts by associating policies. The policy setting can be specific to the level of **[API, Resource, User/User Group, Allow/Deny, and Condition]**:

### 1. Account
- **DNSPod root account**: the main body that owns Tencent Cloud or DNSPod resources, and bears the obligation to pay corresponding bills. It can be used to log in to Tencent Cloud service consoles.
- **Sub-account**: an account created by the root account. It has a specific ID and identity credentials that can be used to log in to the Tencent Cloud or DNSPod console. A root account can create multiple sub-accounts (users). By default, a sub-account does not own any resources and must be authorized by its root account to access resources.
- **Identity credentials**: including login credentials and credentials for access to DNSPod. Login credentials refer to a user’s login username and password. Credentials for access to DNSPod refer to API keys (SecretId and SecretKey) or DNSPod tokens.
### 2. Resources and permissions
- **Resource**: An object that Tencent Cloud services operate on, such as a CVM instance, a COS bucket, or a VPC instance.
- **Permission**: the ability to allow or forbid users to perform certain operations. By default, the root account has full access to all resources under the account, while a sub-account does not have access to any resources under its root account.
- **Policy**: syntax rules that define and describe one or more permissions. The root account performs authorization by associating policies with users/user groups.
For more information, see [CAM Overview](https://intl.cloud.tencent.com/document/product/598/10583).

## References
| Document Description | Link |
|---------|---------|
| Relationship between policy and user | [Policy Management](https://intl.cloud.tencent.com/document/product/598/10601) |
| Basic structure of policy | [Policy Syntax](https://cloud.tencent.com/document/product/598/10603) |
| More products that support CAM | [CAM-enabled Cloud Services](https://intl.cloud.tencent.com/document/product/598/10588) |