
You can create users or roles by using [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598). By associating with CAM preset or custom policies, you can specify which users have which access permissions, to which resources they can have these permissions, and you can also specify those are available only under certain conditions.

Currently, Cloud Infinite (CI) allows you to configure data persistence permissions for sub-accounts to process data in transit or stored in COS buckets. To authorize your sub-accounts to perform certain operations during downloading, [submit a ticket](https://console.cloud.tencent.com/workorder).

The following describes the involved basic concepts. For more information, see the CAM [User Guide](https://intl.cloud.tencent.com/document/product/598/17848).

## Accounts
- **Root account**: the owner of all its Tencent Cloud resources and has full access to these resources.
- **Sub-account**: includes sub-users and collaborators.
 - **Sub-user**: created by a root account and is subordinate to the root account.
 - **Collaborator**: when a root account is added as the collaborator of the current root account, it becomes one of the sub-accounts of the current root account. The account can be switched from collaborator back to root account.
- **Identity credentials**: include login credentials and access certificates.
  - **Login credentials**: contain login names and passwords.
  - **Access certificate**: indicate the Cloud API key pairs (SecretId and SecretKey).


## Resources and Permissions
- **Resource**: an object that you can work with. For example, a COS bucket or an image in CI.
- **Permission**: an authorization to allow or forbid some users to perform certain operations. By default, a root account has full access to all resources under it, while a sub-account has no access to any resources under its root account.
- **Policy**: a set of syntax rules that define and describe one or more permissions. A root account grants access for users or user groups by associating policies with them. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).