This document describes how to connect to and use VM.
## Getting Account Information
### Getting Tencent Cloud account
Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/) to sign up and verify your identity as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985). You can skip this step if you already have a Tencent Cloud account.

### Getting Tencent Cloud API access key
Tencent Cloud uses `secretid` and `secretkey` to verify your identity and permissions. You can get the Tencent Cloud API access key in the following steps:
1. Go to the [TencentCloud API key management](https://console.cloud.tencent.com/cam/capi) page and select **CAM** > **API Key Management** on the left sidebar to enter the API key management page.
2. Click **Create Key** to create a key and save the `secretid` and `secretkey` for subsequent API calls. You can skip this step if you already have a Tencent Cloud key.
![](https://qcloudimg.tencent-cloud.cn/raw/83e1ef822beff460d607f7f7338f4f6c.png)

## Configuring in Console
### Activating service
Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/overview) and click **Activate Now**. You will be gifted a free trial package of **600 minutes** (equivalent to **36,000 images** and **600 minutes of audio**) valid for **one month**.
### Configuring permission
If you want to call VM through a sub-account, you need to authorize it by assigning a policy in the following steps:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) and select **User** > **User List** on the left sidebar to enter the **User List** page.
2. On the **User List** page, find the target sub-account and click **Authorize** in the **Operation** column to pop up the **Associate Policy** window.
>? For more information on CAM, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1140/44981). 

![](https://qcloudimg.tencent-cloud.cn/raw/a6241d11d5c891e0ab2ec5053515051c.png)
3. In the **Associate Policy** pop-up window, select the `QcloudVMFullAccess` policy and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/4106b3a94143d4effaa399c34ba9235e.png)

### Configuring custom policy (optional)
>? This step is optional. If you don't use a custom recognition policy, you can use the default policy (by leaving the `Biztype` field empty when calling APIs) for content recognition.

If your business scenarios require a custom recognition policy for video content, you can configure one in **Policy Management** in the following steps:
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/strategy) and select **VM** > **Policy Management** on the left sidebar to enter the **Policy Management** page.
2. On the **Policy Management** page, click **Create Policy** in the top-left corner to enter the **Create Policy** page.
3. Enter the policy information based on your business scenario, reserve the `Biztype` field as an API input parameter, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/6908d857071825c254fa80c92bfa8507.png)

Parameter description:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Policy Name</td>
<td>Text description of the policy, which can contain up to 30 letters, digits, and underscores.</td>
</tr>
<tr>
<td>Biztype Name</td>
<td>Specific policy number used for API calls, which can contain 3–32 letters, digits, and underscores and must be unique.</td>
</tr>
<tr>
<td>Associate Service Template</td>
<td>Currently, only the default template can be used for configuration.</td>
</tr>
<tr>
<td>Industry Category</td>
<td>Category of the industry scenario involved in the policy.</td>
</tr>
<tr>
<td>Use Industry Template</td>
<td>It will be displayed only when <strong>Industry Category</strong> is set. You can select whether to use Tencent Cloud's preset industry templates for recognition.</td>
</tr>
</tbody></table>

4. On the **Recognition Policy Configuration** page, select whether to recognize different types of content based on your business needs and click **Next**.
5. You can choose to associate a custom dictionary you configured in the drop-down list and click **Next**.
>? Different colors in a custom dictionary represent different blocking logics, where red represents "blocked", yellow represents "suspected", and green represents "allowed".

![](https://qcloudimg.tencent-cloud.cn/raw/6eb0132e5d1556ca599339d4786f192b.png)
6. After confirming that everything is correct, click **Complete**.
>? You can pass in the `Biztype` of a custom policy as an API input parameter to use the policy for video content recognition.
