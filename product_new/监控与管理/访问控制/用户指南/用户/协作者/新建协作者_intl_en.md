## Introduction
This document describes how to create collaborators and set collaborator permissions. Collaborators can manage resources under the root account within the extent of their permissions.
## Directions
1. Log in to the CAM console and go to [User List](https://console.cloud.tencent.com/cam). Click **Create User**, and click **Go to create a Collaborator**.
2. Enter the user information, and click **Next**.
>
> - To ensure the security of your account, we recommend enabling login and operation protection.
> - The account ID is a unique ID for Tencent Cloud. The collaborator you’re adding needs to go to [Account Center - Account Information](https://console.cloud.tencent.com/developer) to view their account ID.
> 
3. Set permissions. You can set permissions for the created collaborator using any of the following three ways. The collaborator will be granted permissions described in the policy after they are associated with the policy.
 - Add the collaborator to a group to give them the group permissions: Using groups is a best practice for managing user permissions by job function. You can use group-associated permissions to give users permissions. Click **Add to Group for Group Permissions** and select the desired user group to add the collaborator to an existing user group or to create a new user group. The collaborator will then be associated with the policies of the group.
 - Copy the permissions of an existing user: By clicking **Copy Existing User's Policies** and selecting the user whose permissions you want to copy, you can associate the collaborator with the policies of the user.
 - Use the policy list: Click **Select Policies to Associate from Policy List**, and then select the policies that you want to associate with the collaborator.
4. Click **Complete** to finish creating a collaborator.
