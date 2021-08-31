This document describes how to identify the sub-account user type and log in to a sub-account. After successful login, the sub-account can manage resources under the root account within the scope of permissions.

## Identifying Sub-account User Type
Sub-account types include sub-user, collaborator, and message recipient. You can identify the type in the following two methods:
- Identify the account type according to the description in the table in [User Types](https://intl.cloud.tencent.com/document/product/598/32633).
- Enter the [User List](https://console.cloud.tencent.com/cam) page in the console as the root account or a sub-account with the `cam:ListSubAccounts` API permission. The user types of the accounts are listed here.

## Logging in to a Sub-account
### Logging in as collaborator
If your sub-account user type is collaborator, you can use the [Tencent Cloud account login](https://intl.cloud.tencent.com/login) page to login. Login with the associated root account and select the collaborator identity to log in to your sub-account, and you will be able to manage the resources under the root account within the scope of the permissions. For detailed directions, please see [Collaborator Login](https://intl.cloud.tencent.com/document/product/598/32659).
### Logging in as sub-user
- If your sub-account user type is **sub-user**, you can go to the [Tencent Cloud sub-user login](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F598%2F36621) page and enter your root account ID, sub-user name, and login password to log in to the sub-account. For more information, please see [Logging in as Sub-user](https://intl.cloud.tencent.com/document/product/598/34006).

>?A message recipient can only receive message notifications through the associated contact information set by the root account but cannot programmatically access or log in to the Tencent Cloud Console to manage resources under the root account.
