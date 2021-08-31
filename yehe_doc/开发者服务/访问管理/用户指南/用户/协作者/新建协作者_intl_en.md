## Overview
If you are an admin user and have purchased CVM, VPC, COS, and other Tencent Cloud resources, you can set the Tencent Cloud accounts of other members of your team as collaborators and allow them to access your resources.

This document describes how to use the admin account to create a collaborator in the CAM console and bind the collaborator to a permission policy.
>?Both collaborators and sub-users are sub-accounts. For related definitions and permission descriptions, please see [User Types](https://intl.cloud.tencent.com/document/product/598/32633).

## Prerequisites
- [An admin user has been created](https://intl.cloud.tencent.com/document/product/598/40985).
- There is an existing Tencent Cloud account that can be set as a collaborator (if not, [sign up for one](https://intl.cloud.tencent.com/document/product/378/17985) first).

## Directions
1. Log in to the Tencent Cloud console, go to [User List](https://console.cloud.tencent.com/cam), and click **Create User** to enter the user creation page.
2. On the user creation page, click **Create a Collaborator**.
![](https://main.qcloudimg.com/raw/ea3983994fe7646429e0d8b499e5bf41.png)
3. Enter the user information and click **Next**.
>?
> - Collaborators are allowed to log in to the Tencent Cloud console by default. Cancellation of this permission is not supported currently.
> - To ensure the security of your account, we recommend you enable login protection and operation protection.
> - The account ID is a unique ID for Tencent Cloud. The collaborator you are adding needs to go to [Account Center - Account Info](https://console.cloud.tencent.com/developer) to view the account ID.
> 
4. Set permissions. You can set permissions for the created collaborator in any of the following three ways. After the collaborator is associated with a policy, they can get the permissions described in the policy.
 - Use group permissions: using groups is the best way to manage user permissions by job function. You can use group-associated permissions to grant permissions. Click **Use group permissions** and select the desired user group to add the collaborator to an existing or new user group. The collaborator will then be associated with the policies of the group.
 - Copy existing user policies: click **Copy existing user policies** and select the user whose permissions you want to use, and the new collaborator will be associated with the policies of the existing user.
 - Select policies from the policy list: click **Select policies from the policy list** and select the policies you want to associate with the collaborator.
5. Click **Done**.

## Related Documents

For more information on how to log in as a collaborator, please see [Logging in as Sub-account - Logging in as collaborator](https://intl.cloud.tencent.com/document/product/598/38248).
