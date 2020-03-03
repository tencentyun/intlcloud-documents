Cloud Infinite (CI) provides data processing services, and its storage feature is based on Cloud Object Storage (COS). Therefore, for a sub-account to use CI services, you must configure CI read-write access and relevant COS read-write access for it.
Granting CI operation permissions to a sub-account involves three steps: **creating a sub-account and configuring CI permissions**, **granting permissions to the sub-account**, and **using the sub-account to process data**.


## Step 1: Create a Sub-Account

You can create a sub-account in CAM Console and grant access permissions for it. The specific procedure is as follows:
 
1. Log in to [CAM Console](https://console.cloud.tencent.com/cam). In the left sidebar, choose **Users** > **User List**.
2. Go to the user list page, and click **Create User**.
3. On the **Select User Type** page, choose **Sub-user** > **Custom Create**<!--, as shown below: 
![](https://main.qcloudimg.com/raw/526186d4c4a69ddf7f3b59717b27b777.png)-->
4. Enter user information. Here, you can create sub-users in batches, set the access type and console password, or perform other operations<!--, as shown below:
![](https://main.qcloudimg.com/raw/198df4e123c4e4ccd1b2362abd6ae5ce.png)-->
5. From the system policy list, select the CI full Read/Write permission **QcloudCIFullAccess** and associate it with the sub-account.
<!--![](https://main.qcloudimg.com/raw/66e417e6e1d5ee90d5e0cb34b885a673.png)-->
6. After confirming that the information is correct, click **OK** to create the sub-account.


## Step 2: Grant Permissions to a Sub-Account

To grant **COS resource access permissions** to the sub-account, associate a preset policy to it as follows:
1. Log in to [CAM Console](https://console.cloud.tencent.com/cam). In the left sidebar, choose **Users** > **User List**.
2. Go to the user list page, find the sub-user to which you want to associate the policy, and click **Authorize** for the account.
3. To configure CI operation permissions for a sub-account, you must grant permissions to read and write COS resources. In the list, select the policies that you need to authorize, and click **OK** to associate the selected policies with the sub-users<!--, as shown below:
![](https://main.qcloudimg.com/raw/766f7bb53479da06dc5f47c27f5e58fb.png)-->

You can also authorize sub-accounts by creating custom policies. For more information, see the [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) document and policy examples.

## Step 3: Use a Sub-Account to Process Data
To use a sub-account to process data, you need the APPID of the root account and the SecretId and SecretKey of the sub-account.

After logging in to CAM Console with the root account, click **User List** to view the API key of the sub-account to obtain its SecretId and SecretKey.
<!--![](https://main.qcloudimg.com/raw/b6cd45d8b8d9d5605417f951e6512f2e.png)-->

You can also grant the sub-account the CAM read access and log in to the console with the sub-account to view key information.