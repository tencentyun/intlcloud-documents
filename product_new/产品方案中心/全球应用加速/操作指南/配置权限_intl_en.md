A root account with GAAP permissions or other accounts with AdministratorAccess permissions can assign collaborator accounts with GAAP read-write or read-only permissions by configuring access management.

The user can grant permissions to collaborator accounts by two methods: associating a policy with a user, or associating a user with a policy. For more information, see [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/597/17989).

## Preparation
1. Log into the [Tencent Cloud Console](https://console.cloud.tencent.com/) using the root account with GAAP permissions or other accounts with AdministratorAccess permissions.
2. In the top navigation, select **Products**>**Management & Audit**>**[Cloud Access Management](https://console.cloud.tencent.com/cam/policy)** to enter the CAM console.
>? You can also enter the CAM console by selecting **Your Account Name**>**Cloud Access Management** in the upper-right corner of the console.

### Steps
### Associating a user with a policy
1. In the left sidebar, click **Policies** to enter the management page.
2. In the search bar, enter **GAAP**, 2 results are found. Select policy permissions, and click **Bind User/Group**.
![1](https://main.qcloudimg.com/raw/06fc88f33dbc935ca2b65948fb3343e3.png)
3. Select the user to be bound, and click **OK** to grant the user permissions.
![](https://main.qcloudimg.com/raw/61df6a1fd920c302c0f2b2f68c79f4a2.png)

### Associating a policy with a user
1. In the left sidebar, click **Users** > **User List** to enter the management page.
2. In the list, find the row of the user who needs to be granted permission. In the operation column, click **Grant Permission**.
![](https://main.qcloudimg.com/raw/740bfd484b9df92eb13bb9517c6238e1.png)
3. Search for **GAAP** in the select policy list. Select the policy to be associated and click **OK**.
![](https://main.qcloudimg.com/raw/7a602d2eefa9ed3ba69ca72df39616a7.png)

### Checking and removing permissions
Users who have been granted permissions can check and remove permissions by clicking the user names in [User List](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/da41405cfc21806881e2c86d9bc2823e.png)
