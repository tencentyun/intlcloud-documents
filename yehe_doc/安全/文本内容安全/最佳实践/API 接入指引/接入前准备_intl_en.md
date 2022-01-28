This document describes how to connect to and use TMS.

## Getting Account Information

### Getting Tencent Cloud account

Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/) to sign up and verify your identity as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985). You can skip this step if you already have a Tencent Cloud account.

### Getting Tencent Cloud API access key

Tencent Cloud uses `secretid` and `secretkey` to verify your identity and permissions. You can get the Tencent Cloud API access key in the following steps:

1. Go to the [TencentCloud API key management](https://console.cloud.tencent.com/cam/capi) page and select **CAM** > **API Key Management** on the left sidebar to enter the API key management page.
2. Click **Create Key** to create a key and save the `secretid` and `secretkey` for subsequent API calls. You can skip this step if you already have a Tencent Cloud key.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/1128fbfe6632d7657bfeeacaed9b601c.png)

## Configuring in Console

### Activating service

Log in to the [CMS console](https://console.cloud.tencent.com/cms) and click **Activate Now**.

### Configuring permission

If you want to call TMS through a sub-account, you need to authorize it by assigning a policy in the following steps:

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) and select **User** > **User List** on the left sidebar to enter the **User List** page.

2. On the **User List** page, find the target sub-account and click **Authorize** in the **Operation** column to pop up the **Associate Policy** window.

   >? For more information on CAM, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1121/43756).

   ![img](https://qcloudimg.tencent-cloud.cn/raw/3459988e65e5f5100e4f5e075b54c51b.png)

3. In the **Associate Policy** pop-up window, select the `QcloudTMSFullAccess` policy and click **OK**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/f60457b2e1e07c2e3965c7e5f395820e.png)

### Configuring custom policy (optional)

>? This step is optional. If you don't use a custom moderation policy, you can use the default policy (by leaving the `Biztype` field empty when calling APIs) for content moderation.

If your business scenarios require a custom moderation policy for text content, you can configure one in **Policy Management** in the following steps:

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/image/lib) and select **TMS** > **Policy Management** on the left sidebar to enter the **Policy Management** page.
2. On the **Policy Management** page, click **Create Policy** in the top-left corner to enter the **Create Policy** page.
3. Enter the policy information based on your business scenario, reserve the `Biztype` field as an API input parameter, and click **Next**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/0f33ebc98c517d170726080396b8129a.png)

Parameter description:

| Parameter | Description |
| :----------- | :----------------------------------------------------------- |
| Policy Name     | Text description of the policy, which can contain up to 30 letters, digits, and underscores. |
| Biztype Name  | Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique. |
| Associated Service Template | Not required currently.                                               |
| Industry Category     | Category of the industry scenario involved in the policy.                                       |
| Use Industry Template | It will be displayed only when **Industry Category** is set. You can select whether to use Tencent Cloud's preset industry templates for moderation. |

4. Select the content to be recognized and filtered in the policy and click **Next**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/f671bacad92169d45c9bed02b24ce8b7.png)

5. If you want to recognize specific text content, you can associate a custom dictionary in the drop-down list and click **Next**.

>? Different colors in a custom dictionary represent different blocking logics, where red represents "blocked", yellow represents "suspected", and green represents "allowed".

![img](https://qcloudimg.tencent-cloud.cn/raw/6a0649111cda862d8dd7671e0fcecf8c.png)

6. After confirming that everything is correct, click **Complete**.

>? You can pass in the `Biztype` of a custom policy as an API input parameter to use the policy for text content moderation.

![img](https://qcloudimg.tencent-cloud.cn/raw/a2c4e83b38df3565735e85bc57d0e5e8.png)