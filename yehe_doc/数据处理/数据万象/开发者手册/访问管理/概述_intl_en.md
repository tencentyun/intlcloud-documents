You can create users or roles by using [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598). By associating CAM preset or custom policies, you can specify which users have which access permissions to which resources. You can also specify that access permissions are only available under certain conditions.

Cloud Infinite (CI) has two major modules: image processing and media processing. For image processing, you can configure persistent permissions for your sub-account to process data when uploading or process COS data already stored in the cloud. To grant permissions to your sub-account to process data when downloading, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=86&source=0&step=1) to contact us. For media processing, CI allows you to grant permissions at the resource level. You can grant permissions to allow a sub-account to manage a single resource through policy syntax.

See the basic concepts below. For more information, see the CAM [User Guide](https://intl.cloud.tencent.com/document/product/598/17848) documentation.

## Accounts

- **Root account**: this account owns all the Tencent Cloud resources and has full access to these resources.
- **Sub-account**: includes sub-users and collaborators.
- **Sub-user**: created by a root account and is subordinate to the root account.
- **Collaborator**: when a root account is added as the collaborator of the current root account, it becomes one of the sub-accounts of the current root account. The account can be switched from collaborator back to root account.
- **Identity credentials**: include login credentials and access certificates.
  - **Login credentials**: refers to usernames and passwords.
  - **Access certificate**: refers to the Cloud API key pairs (SecretId and SecretKey).

## Resources and Permissions

- **Resource**: an object that you can operating on, such as a COS bucket or an image in CI.
- **Permission**: an authorization to allow or forbid some users to perform certain operations. By default, the root account has full access to all resources under it, while a sub-account has no access to any resources under its root account.
- **Policy**: a set of syntax rules that define and describe one or more permissions. A root account grants access for users or user groups by associating policies with them. For more information, see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).



