A root account or other accounts with AdministratorAccess permissions can assign collaborator accounts with GAAP read-write or read-only access permission by configuring access management permissions.

There are two ways the user can authorize the collaborator account: by binding a policy with a user, or by binding a user with a policy. For more information, see [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583).

## Preparation
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) with a root account or an account with AdministratorAccess permissions. 
2. In the top navigation, select **Cloud Products** > **Manage and Audit** > **[Cloud Access Management](https://console.cloud.tencent.com/cam/policy)** to open the CAM console.
>You can also open the CAM console by selecting **Your Account Name** > **Access Management** in the upper-right corner of the console.

## Directions
### Bind a User with a Policy
1. In the left sidebar, click **Policy** to enter the management page.
2. In the search bar, enter **GAAP**. 2 results are found. Select Policy Permissions, and click **Bind User/Group**.
![1](https://main.qcloudimg.com/raw/06fc88f33dbc935ca2b65948fb3343e3.png)
3. Select the user to be authorized, and click **OK**. The user is authorized.
![](https://main.qcloudimg.com/raw/61df6a1fd920c302c0f2b2f68c79f4a2.png)

### Bind a Policy with a User
1. In the left sidebar, click **User** > **User List** to enter the management page.
2. Find the line in the list that contains the user to be authorized. In the operation column, click **Authorize**.
![](https://main.qcloudimg.com/raw/740bfd484b9df92eb13bb9517c6238e1.png)
3. Search for **GAAP** in the association list. Select the policy to be authorized and click **OK**. The user is authorized.
![](https://main.qcloudimg.com/raw/7a602d2eefa9ed3ba69ca72df39616a7.png)

### Check and Remove Permissions
Authorized users can check and remove permissions by clicking the user names in the [User List](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/da41405cfc21806881e2c86d9bc2823e.png)
