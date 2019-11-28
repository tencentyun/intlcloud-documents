## Introduction
This document describes how to grant permissions to collaborators and how to disassociate them from policies. Collaborators can manage the resources under the root account to the extent allowed by the configured permissions.
## Directions
### Associating a Collaborator with Policies
#### Associating Directly
You can directly associate a policy with a user to give them the permissions included in the policy.
1. Log in to the CAM console and go to [User List](https://console.cloud.tencent.com/cam). Locate the collaborator you want to grant permissions to, and click **Authorize** in the **Operation** column on the right.
2. Select the policies to be associated and click **OK**. You can select more than one. 

#### Associating with Policies by Adding to Groups
You can add the user to a user group to automatically grant the user permissions included in the policies that are associated with the user group. The policy types obtained by the user through this method depend on the policies associated with the user group. If you need to disassociate the user with a policy that is associated with the user group, you must remove the user from the user group.
1. Log in to the CAM console and go to [User List](https://console.cloud.tencent.com/cam). Locate the collaborator you want to grant permissions to, and click **More** > **Add to Group** in the operation column on the right.
2. Select the user group to which you want to add the collaborator to and click **OK**. You can select more than one user group.

### Disassociating a Collaborator from Policies
#### Directly disassociating a Collaborator from Policies
You can directly disassociate a user from policies to remove the permissions granted to the user.
1. Log in to the CAM console and go to [User List](https://console.cloud.tencent.com/cam). Locate the collaborator you want to remove permissions from, and click the user name of the collaborator to enter the collaborator’s details page.
2. Go to **Permissions** and locate the policy. Click **Disassociate** in the operation column on the right.
3. Click **Confirm** to complete the disassociation. This user will no longer have the permissions described in this policy.

#### Removing a Collaborator from a Group
You can remove a collaborator from a group to automatically disassociate the user from the permissions associated with this group.
1. Log in to the CAM console and go to [User List](https://console.cloud.tencent.com/cam). Locate the collaborator you want to remove the permissions from, and click the user name of the collaborator to enter the collaborator’s details page.
2. Click **Groups** and locate the user group. Click **Remove from Group** in the operation column on the right.
3. Click **OK** to remove the collaborator from the user group and disassociate the user from group-associated policies. After the collaborator has been removed, the user will no longer have the permissions associated with the user group.
