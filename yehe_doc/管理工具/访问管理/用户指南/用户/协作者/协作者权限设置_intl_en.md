## Overview
This document describes how to associate/disassociate a policy with/from a collaborator. The collaborator can manage the resources under the root account within the scope of the granted permissions.
## Directions
### Associating a policy with a collaborator
#### Direct association
You can directly associate a policy with a user to give them the permissions included in the policy.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam). Locate the collaborator to associate a policy with and click **Grant Permission** in the "Operation" column on the right.
2. Select one or more policies to be associated and click **OK**.

#### Association via group
You can add a user to a user group to automatically grant the user permissions included in the policies that are associated with the user group. The policy types obtained by the user in this method depend on the policies associated with the user group. If you need to disassociate the user from a policy that is associated with the user group, you must remove the user from the user group.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam). Locate the collaborator to associate a policy with and click **More** > **Add to Group** in the "Operation" column on the right.
2. Select one or more user groups to which you want to add the collaborator to and click **OK**.

### Disassociating a collaborator from a policy
#### Direct disassociation
You can directly disassociate a user from a policy to remove the permissions granted.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam). Locate the collaborator to disassociate a policy from and click the **username** of the collaborator to enter the collaborator details page.
2. Go to **Permissions** and locate the policy. Click **Disassociate** in the operation column on the right.
3. Click **OK** to complete the disassociation. This user will no longer have the permissions described in the policy.

#### Removing a collaborator from a group
You can remove a collaborator from a user group to automatically disassociate the user from the permissions associated with the group.
1. 	Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam). Locate the collaborator to disassociate a policy from and click the name of the collaborator to enter the collaborator details page.
2. Go to **Groups** and locate the group. Click **Remove from Group** in the operation column on the right.
3. Click **OK** to remove the collaborator from the user group and disassociate the user from the group-associated policy. After the removal, the collaborator will no longer have the permissions associated with the user group.
