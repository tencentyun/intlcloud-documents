A root account or other accounts with AdministratorAccess permissions can assign collaborator accounts with GAAP read-write or read-only access permission by configuring access management permissions.

There are two ways the user can authorize the collaborator account: by associating a policy with a user, or by associating a user with a policy. For more information, see [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583).

## Preparation
1. Log in to the root account or other account with AdministratorAccess permissions on [Tencent Cloud Console](https://console.cloud.tencent.com/).
2. In the top navigation, select **Cloud Products** > **Manage and Audit** > **[Cloud Access Management](https://console.cloud.tencent.com/cam/policy)** to enter the CAM console.
>? You can also enter the access management console by selecting **Your Account Name** > **Access Management** in the upper-right corner of the console.

## Directions
### Associating a User with a Policy
1. In the left sidebar, click **Policy** to enter the management page.
2. In the search bar, enter **GAAP**. 2 results are found. Select Policy Permissions, and click **Associate user/group**.
![1](https://main.qcloudimg.com/raw/06fc88f33dbc935ca2b65948fb3343e3.png)
3. Select the user to be authorized, and click **OK**. The user is authorized.
![](https://main.qcloudimg.com/raw/cc41715cfe649f76ff15ae49bc3485a6.png)

### Associating a Policy with a User
1. In the left sidebar, click **User** > **User List** to enter the management page.
2. Find the line in the list that contains the user to be authorized. In the operation column, click **Authorize**.
![](https://main.qcloudimg.com/raw/64eccc12058f227c789a4153d92fddc6.png)
3. Search for **GAAP** in the association list. Select the policy to be authorized and click **OK**. The user is authorized.
![](https://main.qcloudimg.com/raw/7a602d2eefa9ed3ba69ca72df39616a7.png)

### Checking and Removing Permissions
Authorized users can check and remove permissions by clicking the user names in the [User List](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/0880fdaaef1f97acb7d0d2401ffdff43.png)
