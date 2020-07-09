## Step 1. Create a sub-user by using the root account
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview) and select **Users** > **User List** on the left sidebar.
2. On the **User List** page, select **Create User** > **Custom Creation** to enter the sub-user creation page.
3. Select a user type and click **Access resources and receive messages**.
4. Enter the user information. You can create sub-users and set access type and console password in batches. Please configure based on your actual needs.
5. Set the permissions (required). Make appropriate settings according to different business scenarios and click **Next** to save the settings. You can also change the relevant permission settings later. There are three ways to set permissions:
	- Add the sub-user to an existing or new user group.
	- Copy the permissions of an existing user.
	- Authorize in the list of policies.
6. After the creation is completed, the console will display the username, password, TencentCloud API key and other information of the sub-user. Click **Complete** to exit the page.
>?For more information, please see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

## Step 2. Create a custom policy
1. Log in to the CAM Console and select **[Policy](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
2. On the policy management page, select **Create Custom Policy** > **Create by Policy Builder** to enter the creation page.
3. Select services and operations.
   Set the corresponding items as follows and click **Add Statement> **Next** to enter the policy editing steps:
 - **Effect**: allowed
 - **Service**: SCF
 - **Action**: all
 - **Resource**: `*`
 - **Condition (optional)**: empty
4. Edit the policy name and remarks (you are recommended to use an easy-to-understand name) and modify the content of the policy by replacing it with the code in the sample policy in [Permission Management Overview](https://intl.cloud.tencent.com/document/product/583/18014).
>! The resource description in `resource` needs to be replaced with the ID of the root account and the names of functions under it. The `region` needs to be the same as that of the functions.

## Step 2. Associate a policy with a user/user group
1. On the [Policy Management](https://console.cloud.tencent.com/cam/policy) page, click **Associate User/User Group** on the right of the created policy to pop up the prompt box for association.
2. Select the user to be associated with and click **OK** to complete the association. You can also switch between users and user groups for selection.

## Completion
After the settings above are made, you can log in to the sub-account to view the permissions. Click **[Overview](https://console.cloud.tencent.com/cam/overview)** on the left sidebar to enter the overview page and view the sub-user login address.
**After the policy takes effect, the current sub-account can see all the function names but can only operate on and view the functions listed in `resource`.**
