
>! The root account needs to check the **[Roles](https://console.cloud.tencent.com/cam/role)** page to see whether the `SCF_QcsRole` policy is associated. If not, please grant the permissions as instructed in **Roles and Policies** > **Service Authorization**. Otherwise, sub-users will not be able to use the SCF console and call other Tencent Cloud resources through SCF.

## Creating a Sub-user and Granting it All SCF Permissions

### Step 1. Create a sub-user by using the root account
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) and select **Users** > **User List** on the left sidebar.
2. On the **User List** page, select **Create User** > **Custom Create** to access the "Create Sub-user" page.
3. Select **Access Resources and Receive Messages** in the "User Type" step and click **Next**.
4. In the "User Information" step, you can create sub-users and set access modes and console passwords in batches. Please configure the settings as needed and click **Next**.
5. On the "User Permissions" page, set the permissions for the created sub-user as needed and click **Next** to save the settings. You can also change the relevant permission settings later. There are three ways to set permissions:
 - Add the sub-user to an existing or new user group.
 - Copy the permissions of an existing user.
 - Grant permissions from the policy list.
6. On the "Review" page, double check the information and click **Complete**.

>?For more information, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

### Step 2. Create a custom policy
1. Log in to the CAM console and select **[Policies](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
2. On the policy management page, select **Create Custom Policy** > **Create by Policy Generator** to access the creation page.
3. Select the service and action.
   Set the corresponding items as follows and select **Add Statement** > **Next** to move on to the "Edit the Policy" step:
 - **Effect**: allow
 - **Service**: SCF
 - **Action**: all
 - **Resource Description**: `*`
 - **Condition (optional)**: empty
4. Edit the policy name and description (we recommend you use an easy-to-understand name) and click **Done** to complete the policy creation.

### Step 3. Associate a policy with a user/user group
1. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Associate** on the right of the created policy to pop up the prompt box for association.
2. Select the user to be associated with and click **OK** to complete the association. You can also switch between users and user groups for selection.

### Step 4. Add CAM read-only permissions for the sub-user
1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the "User List" page, select the sub-user you want to set permissions for to access the **User Details** page.
3. On the "User Details" page, click **Add Policy**.
4. In the "User Permissions" step, select **Select policies from the policy list**, check `QcloudCamReadOnlyAccess`, and click **Next**.
5. In the "Review User Permissions" step, click **OK** to complete granting the "Read-only access to Cloud Access Management (CAM)" permissions to the sub-user. After the above operations are completed, SCF can get the existing permissions of the root account through the sub-user to complete the authentication process.

### Completion
After the settings above are configured, you can log in to the sub-account to view the permissions.
Log in to the CAM console and select **[Dashboard](https://console.cloud.tencent.com/cam/overview)** on the left sidebar to access the overview page and view the sub-user login address.

## Creating a Sub-user and Granting it Certain SCF Permissions

### Step 1. Create a sub-user by using the root account
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) and select **Users** > **User List** on the left sidebar.
2. On the **User List** page, select **Create User** > **Custom Create** to access the "Create Sub-user" page.
3. Select **Access Resources and Receive Messages** in the "User Type" step and click **Next**.
4. In the "User Information" step, you can create sub-users and set access modes and console passwords in batches. Please configure the settings as needed and click **Next**.
5. On the "User Permissions" page, set the permissions for the created sub-user as needed and click **Next** to save the settings. You can also change the relevant permission settings later. There are three ways to set permissions:
 - Add the sub-user to an existing or new user group.
 - Copy the permissions of an existing user.
 - Grant permissions from the policy list.
6. On the "Review" page, double check the information and click **Complete**.

>?For more information, please see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).


### Step 2. Create a custom policy
1. Log in to the CAM console and select **[Policies](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
2. On the policy management page, select **Create Custom Policy** > **Create by Policy Generator** to access the creation page.
3. Select the service and action.
   Set the corresponding items as follows and select **Add Statement** > **Next** to move on to the "Edit the Policy" step:
 - **Effect**: allow
 - **Service**: SCF
 - **Action**: all
 - **Resource Description**: `*`
 - **Condition (optional)**: empty
4. Edit the policy name and description (we recommend you use an easy-to-understand name) and modify the content of the policy by replacing it with the code in the sample policy in [SCF Policy Syntax](https://intl.cloud.tencent.com/document/product/583/38177).

>! The resource description in `resource` needs to be replaced with the ID of the root account and the names of the functions under it. The `region` needs to be the same as that of the functions.

### Step 3. Associate a policy with a user/user group
1. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Associate** on the right of the created policy to pop up the prompt box for association.
2. Select the user to be associated with and click **OK** to complete the association. You can also switch between users and user groups for selection.

### Step 4. Add CAM read-only permissions for the sub-user
1. Log in to the CAM console and select **Users** > **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the "User List" page, select the sub-user you want to set permissions for to access the **User Details** page.
3. On the "User Details" page, click **Add Policy**.
4. In the "User Permissions" step, select **Select policies from the policy list**, check `QcloudCamReadOnlyAccess`, and click **Next**.
5. In the "Review User Permissions" step, click **OK** to complete granting the "Read-only access to Cloud Access Management (CAM)" permission to the sub-user. After the above operations are completed, SCF can get the existing permissions of the root account through the sub-user to complete the authentication process.

### Completion
After the settings above are configured, you can log in to the sub-account to view the permissions. Click **[Dashboard](https://console.cloud.tencent.com/cam/overview)** on the left sidebar to access the overview page and view the sub-user login address.
>? After the policy takes effect, the current sub-account will be able to see all the function names but will only be able to operate on and view the functions listed in `resource`.









