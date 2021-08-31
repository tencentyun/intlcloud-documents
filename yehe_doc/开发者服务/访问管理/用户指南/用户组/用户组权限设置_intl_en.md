## Overview
After creating and authorizing a user group, you can associate/unassociate policies with/from it to quickly change its permissions. Sub-accounts in the user group can manage the resources under the root account within the scope of the granted permissions.
- When a policy is associated with a user group, all users in it will have the permissions of the policy.
- When a policy is unassociated from a user group, all users in it will no longer have the permissions of the policy.


## Prerequisites
There is an existing user group (if not, please [create one](https://intl.cloud.tencent.com/document/product/598/33380)).


## Directions
### Associating policy with user group
1. Log in to the CAM console and enter the **[User Group](https://console.cloud.tencent.com/cam/groups)** page.

2. Find the target user group and click its name to enter the user group details page.

3. In the **Permissions** module on the user group details page, click **Associate Policy**.

  ![](https://main.qcloudimg.com/raw/a4cd92bc89b954411292f0abeeba2586.png)

4. Select one or more policies to be associated in the pop-up window and click **OK** to associate the policies with the user group.



### Unassociating policy from user group
1. Log in to the CAM console and enter the **[User Group](https://console.cloud.tencent.com/cam/groups)** page.

2. Find the target user group and click its name to enter the user group details page.

3. In the **Permissions** module on the user group details page, find the policy to be unassociated and click **Unassociate** on the right.

  ![](https://main.qcloudimg.com/raw/f2dbd2d36e5ef396918767785cb72abd.png)

4. Click **OK** to unassociate the policy from the user group.

