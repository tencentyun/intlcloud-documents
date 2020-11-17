
If you do not need to manage the access permissions to SSM resources for sub-accounts, you can skip this chapter. Doing so will not affect your understanding and use of other documentation.
If you use multiple services such as SSM, VPC, CVM, and databases, and these services are managed by different users with a shared cloud account key, there would be a high risk of leakage. Besides, since the access permissions of other users cannot be limited, security risks caused by misoperations may occur.
CAM is used to manage the resource access permissions of a Tencent Cloud account. You can manage the resource operation permissions for sub-accounts using CAM identity management and policy management. For example, if your root account has a secret that you want it to be used only by sub-account A and not by sub-account B, you can configure a policy in CAM to manage the sub-account permissions.

## Basic CAM Concepts
The root account can associate policies to sub-accounts to implement permissions. The policies support multiple dimensions, such as API, resource, user, user group, allowing, forbidding, and condition.
- **Account**
	- **Root account**: the owner of Tencent Cloud resources and the fundamental entity for resource usage, usage calculation, and billing. It can be used to log in to Tencent Cloud services.
	- **Sub-account**: an account created by the root account. It has a specific ID and identity credential that can be used to log in to the Tencent Cloud console. A root account can create multiple sub-accounts (users). By default, a sub-account does not own any resources and must be authorized by its root account.
	- **Identity credential**: includes login credentials and access certificates. Login credential refers to a user’s login name and password. Access certificate refers to Cloud API keys (SecretId and SecretKey).
- **Resource and permission**
	- **Resource**: an object that is operated in Tencent Cloud Services, such as an SSM secret, a CVM instance, a COS bucket, or a VPC instance.
	- **Permission**: an authorization that allows or forbids users to perform certain operations. By default, the root account has full access to all resources under the account, while a sub-account does not have access to any resources under its root account.
	- **Policy**: syntax rule that defines and describes one or more permissions. The root account performs authorization by associating policies with users/user groups.

For more information, please see [Tencent Cloud CAM](https://intl.cloud.tencent.com/product/cam).
