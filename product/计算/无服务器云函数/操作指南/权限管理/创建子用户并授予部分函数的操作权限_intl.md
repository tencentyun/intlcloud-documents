## I. Creating a Sub-user Using the Master Account
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview), select **User Management** in the navigation pane on the left, and click **Create a user** > **Sub-user** to enter the creation page.

2. Enter the user information. You can create sub-users and set access types and console passwords in batches. Please configure based on your actual needs.
3. Set permissions (required). Make appropriate settings according to different business scenarios, and click **Next** to save the settings. You can also change the relevant permission settings later. There are three ways to set permissions:
 - Add the sub-user to an existing or new user group;
 - Copy the permissions of an existing user;
 - Authorize in the list of policies.

4. After the creation is completed, the console will display the user name, password, TencentCloud API key and other information of the sub-user. Click **Finish** to exit the page.

For more information, see [Creating a Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

## II. Creating a Custom Policy
1. In the CAM console, select **Policy Management** in the navigation pane on the left to enter the **Policy management** page, and click **Create a custom policy** > **Create by policy builder** to enter the creation page.

2. Select services and actions.
   Set the corresponding items as follows, and click **Add a declaration** > **Next** to enter the policy editing steps:
 - Effect: Allowed
 - Service: SCF
 - Action: All
 - Resource description: `*`
 - Condition (optional): Left blank

3. Edit the policy name and remarks (it is recommended to use an easy-to-understand name), and modify the content of the policy by replacing with the code in the sample policy in [Overview of Permission Management](https://cloud.tencent.com/document/product/583/18014).
> **Note:**
> The resource description in "resource" needs to be replaced with the ID of the master account and the names of the functions under the master account. The "region" needs to be the same as that of the function.

## III. Associating a Policy with a User/User Group
1. On the "Policy management" page, click **Associate with a user/user group** on the right of the created policy to bring up the prompt box for association.
2. Select the user to be associated with and click **OK** to finish the association. You can also switch between users and user groups for selection.

## Finishing
After the settings above are made, you can log in to the sub-account to view the permissions. Click **Overview** in the navigation pane on the left to enter the overview page and view the sub-user login address.
**After the policy takes effect, the current sub-account can see all the function names, but can only operate and view the functions listed in "resource".**
