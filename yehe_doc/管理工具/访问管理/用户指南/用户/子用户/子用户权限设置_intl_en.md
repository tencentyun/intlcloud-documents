## Overview
This document describes how to associate/disassociate a policy with/from a sub-user. The sub-user can manage the resources under the root account within the scope of the granted permissions.
## Directions
### Associating a policy with a sub-user
#### Direct association
You can directly associate a policy with a user to give them the permissions included in the policy.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam).
2. Locate the sub-user you want to grant permission to.
3. Click **Grant Permission** in the "Operation" column on the right.
4. In the "Associate Policies" window that pops up, select one or more policies to be associated.
5. Click **OK** to associate the policies with the sub-user.

#### Association via group
You can add a user to a user group to automatically grant the user permissions included in the policies that are associated with the user group. The policy types obtained by the user in this method depend on the policies associated with the user group. If you need to disassociate the user from a policy that is associated with the user group, you must remove the user from the user group.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam).
2. Locate the sub-user you want to grant permission to.
3. Click **More** > **Add to Group** in the "Operation" column on the right.
4. Select one or more user groups you want to add the sub-user to.
5. Click **OK** to add the sub-user to the user groups and associate the sub-user with the group-associated policies.

### Disassociating a sub-user from a policy

#### Direct disassociation
You can directly disassociate a user from a policy to remove the permissions granted.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam).
2. Locate the sub-user you want to remove permission from.
3. Click the name of the sub-user to enter the user details page.
4. Go to **Permissions** and locate the policy.
5. Click **Disassociate** in the operation column on the right.
6. Click **OK** to complete the disassociation. This user will no longer have the permissions described in the policy.

#### Removing a user from a group
You can remove a user from a user group to automatically disassociate the user from the permissions associated with the group.
1. Log in to the CAM Console and enter [User List](https://console.cloud.tencent.com/cam).
2. Locate the sub-user you want to remove permission from.
3. Click the name of the sub-user to enter the user details page.
4. Go to **Group** and locate the policy to be disassociated from.
5. Click **Remove from Group** > **Confirm** in the "Operation" column on the right to remove the sub-user from the user group.
6. After the removal, the user will no longer have the permissions associated with the user group.
