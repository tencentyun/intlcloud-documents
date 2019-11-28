## Introduction
This document describes how to grant permissions to sub-users and how to disassociate them from policies. Sub-users can manage the resources under the root account to the extent allowed by the configured permissions.
## Directions
### Associating a Sub-User with Policies
#### Associating Directly
You can directly associate a policy with a user to give them the permissions included in the policy.
1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. In the User List management page, locate the sub-user you want to grant permissions to.
3. Click **Authorize** in the operations column on the right.
4. Select the policies to be associated. You can select more than one.
5. Click **OK** to complete associating the policy with the sub-user.

#### Associating with Policies by Adding to Groups
You can add the user to a user group to automatically grant the user permissions included in the policies that are associated with the user group. The policy types obtained by the user through this method depend on the policies associated with the user group. If you need to disassociate the user with a policy that is associated with the user group, you must remove the user from the user group.
1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. In the User List management page, locate the sub-user you want to grant permissions to.
3. Click **More** > **Add to Group** in the operations column on the right.
4. Select the user group to which you want to add the sub-user to. You can select more than one user group.
5. Click **OK** to add the sub-user to the user group and associate them with the group’s policies.

### Disassociating a Sub-User from Policies

#### Directly Disassociating a Sub-User from a Policy
You can directly disassociate a user from policies to remove the permissions granted to the user.
1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. In the User List management page, locate the sub-user you want to remove permissions from. 
3. Click the name of the sub-user to go to the user details page.
4. Click **Permissions**.
5. Locate the policy.
6. Click **Disassociate** > **Confirm** to complete the disassociation.

#### Removing a User from a User Group
You can remove a user from a user group to automatically disassociate the user from the permissions associated with this group.
1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. In the User List management page, locate the sub-user you want to remove permissions from. 
3. Click the name of the sub-user to go to the user details page.
4. Go to **Groups**.
5. Locate the policy that you want to disassociate from.
6. Click **Remove from Group** > **OK** to remove the collaborator from the user group and disassociate the user from group-associated policies.
