## Introduction
This document describes how to create collaborators and set collaborator permissions. Collaborators can manage resources under the root account within the extent of the granted permissions.
## Directions
1. Log in to the Tencent Cloud Console, go to [User List](https://console.cloud.tencent.com/cam). Click **Create User** to enter the user creation page.
2. On the user creation page, click **Create a Collaborator**.
3. Enter the user information and click **Next**.
>
> - Collaborators are allowed to log in to the Tencent Cloud Console by default. This permission cannot be removed for now.
> - To ensure the security of your account, we recommend enabling login and operation protection.
> - The account ID is a unique ID for Tencent Cloud. The collaborator you are adding needs to go to [Account Information](https://console.cloud.tencent.com/developer) in **Account Center** to view the account ID.
> 
4. Set permissions. You can set permissions for the created collaborator using any of the following three ways. The collaborator will be granted permissions described in the policy after they are associated with the policy.
 - Add the collaborator to a group to grant them group permissions: using groups is the best way to manage user permissions by job function. You can use group-associated permissions to grant permissions. Click **Add to Group for Group Permissions** and select the desired user group to add the collaborator to an existing or new user group. The collaborator will then be associated with the policies of the group.
 - Copy existing user policies: click **Copy Existing User Policies** and select the user whose permissions you want to use, and the new collaborator will be associated with the policies of the existing user.
 - Use the policy list: click **Select Policies from Policy List** and select the policies you want to associate with the collaborator.
5. Click **Complete** to complete creating a collaborator.

## Related documents

For more information on how to log in as a collaborator, please see [Collaborator Login](https://intl.cloud.tencent.com/document/product/598/32659).
