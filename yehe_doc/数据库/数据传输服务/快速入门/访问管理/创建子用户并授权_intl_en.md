
## Overview  
If you have multiple users managing different Tencent Cloud services such as CVM, VPC, and TencentDB, and they all share your Tencent Cloud account access key, you may face the risk of your key being compromised. Therefore, we recommend you create sub-users and let them manage different services to avoid such risk.

By default, sub-users have no permission to use DTS. Therefore, you need to create policies to allow them to use it.

You can skip this section if you don't need to manage permissions to TencentDB resources for sub-users.

## Creating and Authorizing Sub-user 
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as the root account.
2. On the left sidebar, select **User** > **User List** to enter the user list management page. 
3. Click **Create User** to enter the user creation page.
4. On the user creation page, select the creation method. 
6. On the **Quick User Creation** page, set the sub-user name, access method, user permission, etc.
![](https://qcloudimg.tencent-cloud.cn/raw/2b1ebd82f776467bec5d173d530eeea0.png)
   - Console Login: select **Console access** or **Programming access**.
   - User permission: select the permission as needed. If you select **QcloudDTSFullAccess**, the sub-user will be granted all read/write permissions of the DTS service. If you select **QcloudDTSReadOnlyAccess**, only the read-only permission will be granted.
7. Click **Create User**.
8. You will be redirected to the page prompting that the user is successfully created, and you can get the sub-user information in the following two methods:
  - Click **Copy** to directly get and copy the login information of the sub-user.
  - Click **Send**, enter the email address, and the system will send the complete sub-user information to the specified email address.

## Authorizing Existing Sub-user
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) as a root account, select the target sub-user in the user list, and click **Authorize**.
![](https://qcloudimg.tencent-cloud.cn/raw/7afe15f6ae3fab3ccad803127d532925.png)
2. In the pop-up window, select the **QcloudDTSFullAccess** preset policy and click **OK** to complete the authorization.
![](https://qcloudimg.tencent-cloud.cn/raw/d63b4700d77fa9505f0154468203703a.png)
