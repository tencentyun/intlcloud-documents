Cloud Infinite (CI) provides a suite of data processing services, among which CI storage is based on COS. Therefore, for a sub-account to use all CI services, it must be granted necessary read/write permissions both for CI and COS.
Granting CI operation permissions to a sub-account involves three steps: **[Create a Sub-Account and Grant CI Permissions](#step1)**, **[Grant COS permissions to the Sub-Account](#step2)**, and **[Use the Sub-Account to Process Data](#step3)**.

> !
> A sub-account may need the following permissions to view data or change settings in the CI console:
>
> | Operation     | Permission                            |
> | :----------- | :---------------------------------- |
> | Create a bucket   | cos:PutBucket permission for COS bucket    |
> | Unbind a bucket   | cos:DeleteBucket permission for COS bucket |
> | View feature configuration | cos:GetBucket permission for COS bucket    |
> | Modify feature configuration | cos:PutObject permission for COS bucket    |

<span id="step1"></span>

## Step 1. Create a Sub-Account and Grant CI Permissions

You can create a sub-account in CAM Console and grant CI access permissions for it. The specific procedure is as follows:

1. Log in to [CAM Console](https://console.cloud.tencent.com/cam). In the left sidebar, choose **Users** > **User List**.
2. In the user list page, click **Create User**.
3. Click **Custom Create** to open the **Select Type** page.
4. Click **Access to resources and receive messages** > **Next** to enter the **Enter user info** page.
5. Enter user information. Here, you can create multiple sub-users, set the access type and console password, or perform other operations.

6. Click **Next** to set user permissions. Choose **Select policies from the policy list**, and then **QcloudCIFullAccess** for full CI access from the policy list. Click **Next**.

7. After confirming that the information is correct, click **OK** to create the sub-account.

<span id="step2"></span>

## Step 2. Grant COS Permissions to the Sub-Account

To grant **COS resource access permissions** to the sub-account, associate a preset policy with it as follows:

1. Log in to [CAM Console](https://console.cloud.tencent.com/cam). In the left sidebar, choose **Users** > **User List**.
2. In the user list page, find the sub-user that you just created, and click **Grant Permission** under **Operation**.
3. In the policy list, select the appropriate permission policy, and click **OK** to associate it with the sub-user

You can also grant COS permissions to a sub-account using a custom policy. For more information, see the [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602) document and policy examples.

<span id="step3"></span>

## Step 3. Use the Sub-Account to Process Data

To use a sub-account to process data, you need the APPID of the root account and the SecretId and SecretKey of the sub-account.

1. Log in to [CAM Console](https://console.cloud.tencent.com/cam) with your root account. In the left sidebar, choose **Users** > **User List**.
2. Click on the name of the sub-account whose SecretId and SecretKey you want.
3. Select the **API Key** tab where you can get the SecretId and SecretKey.


You can also get the API Key from the CAM console using a sub-account by granting it CAM read permission.
