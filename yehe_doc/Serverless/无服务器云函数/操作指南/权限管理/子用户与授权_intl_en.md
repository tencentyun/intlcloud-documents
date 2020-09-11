
>! The root account needs to check on the**[Role](https://console.cloud.tencent.com/cam/role)** page whether the `SCF_QcsRole` policy is associated, and if not, please grant the permissions as instructed in **Role and Policy** > **Service Authorization**; otherwise, sub-users will not be able to use the SCF Console and call other Tencent Cloud resources through SCF.

## Creating Sub-user and Granting It All Permissions of SCF

### Step 1. Create a sub-user by using the root account
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and select **Users** > **User List** on the left sidebar.
2. On the **User List** page, select **Create User** > **Custom Create** to enter the "Create Sub-user" page.
3. Select **Access Resources and Receive Messages** in the "User Type" step and click **Next**.
4. In the "User Information" step, you can create sub-users and set access mode and console password in batches. Please configure as needed and click **Next**.
5. On the "User Permissions" page, set the permissions for the created sub-user as needed and click **Next** to save the settings. You can also change the relevant permission settings later. There are three ways to set permissions:
 - Add the sub-user to an existing or new user group.
 - Copy the permissions of an existing user.
 - Authorize in the policy list.
6. On the "Review" page, double check the information and click **Complete**.

>?For more information, please see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

### Step 2. Create a custom policy
1. Log in to the CAM Console and select **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
2. On the policy management page, select **Create Custom Policy** > **Create by Policy Generator** to enter the creation page.
3. Select service and action.
   Set the corresponding items as follows and select **Add Statement** > **Next** to enter the "Edit Policy" step:
 - **Effect**: allowed
 - **Service**: SCF
 - **Action**: all
 - **Resource Description**: `*`
 - **Condition (optional)**: empty
4. Edit the policy name and notes (you are recommended to use an easy-to-understand name) and click **Create Policy** to complete the policy creation.

### Step 3. Associate a policy with a user/user group
1. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Associate** on the right of the created policy to pop up the prompt box for association.
2. Select the user to be associated with and click **OK** to complete the association. You can also switch between users and user groups for selection.

### Step 4. Add CAM read-only permission for the sub-user
1. Log in to the CAM Console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the "User List" page, select the sub-user you want to set permission for to enter the **User Details** page.
3. On the "User Details" page, click **Associate Policy** to enter the **Add Policy** page.
4. In the "User Permissions" step, select **Select policies from the policy list**, check `QcloudCamReadOnlyAccess`, and click **Next**.
5. In the "Review User Permissions" step, click **OK** to complete granting the "user and permissions (CAM) - read-only access permission" to the sub-user. After the above operations are completed, SCF can get the existing permissions of the root account through the sub-user to complete the authentication process.

### Completion
After the settings above are made, you can log in to the sub-account to view the permissions.
Log in to the CAM Console and select **[Overview](https://console.cloud.tencent.com/cam/overview)** on the left sidebar to enter the overview page and view the sub-user login address.

## Creating Sub-user and Granting It Certain Permissions of SCF

### Step 1. Create a sub-user by using the root account
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and select **Users** > **User List** on the left sidebar.
2. On the **User List** page, select **Create User** > **Custom Create** to enter the "Create Sub-user" page.
3. Select **Access Resources and Receive Messages** in the "User Type" step and click **Next**.
4. In the "User Information" step, you can create sub-users and set access mode and console password in batches. Please configure as needed and click **Next**.
5. On the "User Permissions" page, set the permissions for the created sub-user as needed and click **Next** to save the settings. You can also change the relevant permission settings later. There are three ways to set permissions:
 - Add the sub-user to an existing or new user group.
 - Copy the permissions of an existing user.
 - Authorize in the policy list.
6. On the "Review" page, double check the information and click **Complete**.

>?For more information, please see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).


### Step 2. Create a custom policy
1. Log in to the CAM Console and select **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
2. On the policy management page, select **Create Custom Policy** > **Create by Policy Generator** to enter the creation page.
3. Select service and action.
   Set the corresponding items as follows and select **Add Statement** > **Next** to enter the "Edit Policy" step:
 - **Effect**: allowed
 - **Service**: SCF
 - **Action**: all
 - **Resource Description**: `*`
 - **Condition (optional)**: empty
4. Edit the policy name and notes (we recommend you use an easy-to-understand name) and modify the content of the policy by replacing it with the code in the sample policy in [SCF Policy Syntax](https://intl.cloud.tencent.com/document/product/583/38177).

>! The resource description in `resource` needs to be replaced with the ID of the root account and the names of functions under it. The `region` needs to be the same as that of the functions.

### Step 3. Associate a policy with a user/user group
1. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Associate** on the right of the created policy to pop up the prompt box for association.
2. Select the user to be associated with and click **OK** to complete the association. You can also switch between users and user groups for selection.

### Step 4. Add CAM read-only permission for the sub-user
1. Log in to the CAM Console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the "User List" page, select the sub-user you want to set permission for to enter the **User Details** page.
3. On the "User Details" page, click **Associate Policy** to enter the **Add Policy** page.
4. In the "User Permissions" step, select **Select policies from the policy list**, check `QcloudCamReadOnlyAccess`, and click **Next**.
5. In the "Review User Permissions" step, click **OK** to complete granting the "user and permissions (CAM) - read-only access permission" to the sub-user. After the above operations are completed, SCF can get the existing permissions of the root account through the sub-user to complete the authentication process.

### Completion
After the settings above are made, you can log in to the sub-account to view the permissions. Click **[Overview](https://console.cloud.tencent.com/cam/overview)** on the left sidebar to enter the overview page and view the sub-user login address.
>? After the policy takes effect, the current sub-account can see all the function names but can only operate on and view the functions listed in `resource`.









