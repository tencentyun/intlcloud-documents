## Step 1. Sign up and log in[](id:step1)
Sign up as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/10496).
>?You can skip this step if you already have a Tencent Cloud account.

## Step 2. Create a sub-account (optional)[](id:step2)
The account created when you [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) is the root account, which has the management permissions of all resources under it. If you need your team members to assist you in managing resources under your account, you can use the CAM feature to create one or more sub-accounts, bind permission policies to them, and then assign them to team members. For detailed directions, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

A newly created sub-account has no permissions by default and requires the root account or admin to bind a policy to it before it can have the operation permissions of certain resources. You can configure access to CMS with CAM for sub-accounts as instructed in [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1140/44981).

## Step 3. Activate the service[](id:step3)
#### Prerequisites
- You already have a Tencent Cloud root account or sub-account.
- The logged-in account already has the read/write permissions of VM.

#### Directions
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/overview) and select any menu under **VM** on the left sidebar.
2. Click **Activate Now** on the right of the page.
>? After activating the service for the first time, you will be gifted a free trial package of **600 minutes** (equivalent to **36,000 images** and **600 minutes of audio**) valid for **one month**.

3. After the service is activated, the console will pop up a window to ask for resource authorization. Click **Authorize** to enter the role management page.
![](https://qcloudimg.tencent-cloud.cn/raw/d6c19a7491c1b899b9c62bb0ecb7fedf.png)
4. On the role management page, click **Agree**. After completing authentication, you can authorize COS resources and then test or use the VM service normally.


## Step 4. Configure a policy (optional)[](id:step4)
We recommend you configure a recognition policy based on your business needs for a personalized user experience.
>?
>- You can skip this step if you use the preset default policy of Tencent Cloud CMS.
>- The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.

#### Prerequisites
- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated VM.

#### Directions
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/overview) and select **VM** > **Policy Management** on the left sidebar.
2. On the **Policy Management** page, click **Create Policy** to enter the **Create Policy** page.
![](https://qcloudimg.tencent-cloud.cn/raw/1463e63f8aaf8338d3395e2848a8eeac.png)
3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/665cb8a91726adf874d7c6dab8f6777f.png)

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

4. On the **Recognition Policy Configuration** page, configure recognition policies for audio and captured images, select whether to recognize different types of content based on your business needs, and click **Next**.
5. On the **Custom Library Configuration** page, select a custom dictionary for content recognition in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 5. Configure a custom dictionary](#step5).
![](https://qcloudimg.tencent-cloud.cn/raw/6f54aa40563ba65ce8741cbfe0189ae3.png)
6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.
7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/1d7e948004669cf781f87bd564858332.png)

## Step 5. Configure a global task template (optional)[](id:step5)
Task templates are used to manage how files are processed for recognition tasks. You can skip this step if the default template is used.
#### Prerequisites
- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated VM.

#### Directions
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/srvconfig) and select **VM** > **Service Management** on the left sidebar.
2. On the service management page, click **View Details** to enter the template details page.
>? Currently, only the default template can be edited for template configuration.

![](https://qcloudimg.tencent-cloud.cn/raw/bb660b4bec6e52a0cb7f1c51c639124e.png)
3. On the template details page, click **Edit** in the top-right corner to modify parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/52b6ced759c7b0e34598556020fbbedd.png)

Parameter description:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Template Name</td>
<td>Text description of the template, which can contain up to 30 letters, digits, and underscores.</td>
</tr>
<tr>
<td>Screencapture Interval</td>
<td>Set the time interval for screencapturing the video file, which can be 1s, 5s, 10s, 15s, or 30s (default).</td>
</tr>
<tr>
<td>Service Status</td>
<td>Select whether to recognize audio at the same time.<ul><li>Enable: yes.</li><li>Disable: no.</li></ul></td>
</tr>
<tr>
<td>Audio Stream or Large File Segment Duration</td>
<td>Set the time length for audio stream or large file segmentation, which can be 15s, 30s (default), or 60s.</td>
</tr>
<tr>
<td>Callback Address</td>
<td>The risky content can be returned to this optional address (if entered).</td>
</tr>
<tr>
<td>Enable Full Callback for Live Streaming</td>
<td>Set whether to enable full callback for live streaming. <ul><li>Enable: both normal and non-compliant video content will be returned to the callback address. </li><li>Disable: only the non-compliant video content will be returned to the callback address.</li></ul></td>
</tr>
</tbody></table>

4. Click **Save** to save the current template, which will take effect immediately for all VM services under the account.

## Step 6. Configure a custom dictionary (optional)[](id:step6)
You can configure a custom dictionary.
>? You can skip this step if you don't need to configure a custom dictionary.

#### Prerequisites
- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated VM.

#### Directions
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/lib) and select **VM** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
![](https://qcloudimg.tencent-cloud.cn/raw/6896c3af337b4b078c97e820188be28a.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
![](https://qcloudimg.tencent-cloud.cn/raw/7bbd49b00613b5c2059e86303cd0db5c.png)

Parameter description:
<table>
<thead>
<tr>
<th><strong>Parameter</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>Dictionary Name</td>
<td>Text description of the dictionary, which can contain up to 32 letters, digits, and underscores.</td>
</tr>
<tr>
<td>Handling Suggestion</td>
<td>You can select <strong>Non-compliant</strong> or <strong>Suspected</strong>.<ul><li><strong>Non-compliant</strong>: the information is identified as non-compliant information</li><li><strong>Suspected</strong>: the information may be non-compliant and requires manual review</li></ul></td>
</tr>
<tr>
<td>Match Mode</td>
<td>For Chinese characters, both exact matching and fuzzy matching are supported. For alphabet letters, only fuzzy matching is supported.<li>Exact match: it exactly matches the entered text</li><li>Fuzzy match: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li></td>
</tr>
</tbody></table>

4. Click **OK**.
5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.
>?Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

![](https://qcloudimg.tencent-cloud.cn/raw/12f6f3b80a87f173a59c9d1615effc88.png)
6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
![](https://qcloudimg.tencent-cloud.cn/raw/676934ca615ba9014250dc96cd6a5e12.png)
7. On the dictionary management page, click **Add Sample** to pop up the **Add Sample** window.
8. In the **Add Sample** pop-up window, select the handling suggestion, enter keywords, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/799215292cfcdeea20c6ba65bc557b7b.png)

Parameter description:
<table>
<thead>
<tr>
<th><strong>Parameter</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>Handling Suggestion</td>
<td>Violation type that corresponds to the recognition model.</td>
</tr>
<tr>
<td>Keyword</td>
<td><ul><li>Keywords are separated by line breaks, and each keyword can contain up to 20 letters. </li><li>You can add up to 500 keywords at a time.</li><li>You can add up to 2,000 keywords in total.</li></ul></td>
</tr>
</tbody></table>

>? After configuring the custom dictionary, you can associate it with the policy created in [Step 4. Configure a policy](#step4).

## Step 7. Try out the service[](id:step7)
After completing the above steps, you can select the created recognition policy and recognize videos to try out the VM service.

#### Prerequisites
- You already have a Tencent Cloud root account or sub-account.
- The logged-in account has activated VM.


#### Directions
1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/experience) and select **VM** > **Demo** on the left sidebar to enter the **Demo** page.
2. On the **Demo** page, select the desired policy and specify the video to be recognized in any of the following ways:
 - Local Upload: click **Click to Upload** and select the local file to be uploaded.
 - URL Upload: enter the URL or COS storage address of the content to be recognized in the input box.
>? The video file must meet the following requirements:
>- Video file name: below 64 characters.
>- Video file size: below 100 MB.
>- Video file duration: below 3 minutes.
>- Video file format: FLV, MKV, MP4, RMVB, AVI, WMV, 3GP, TS (only supported for recognition of URL-uploaded videos), or MOV.
>- Video resolution: the recommended optimal resolution is 1920x1080 (1080p). Videos in a higher resolution can be transcoded by calling the on-cloud transcoding service before they are submitted for review.
3. Click **Recognize Now**, and the recognition result will be displayed at the bottom of the page after the system recognizes the video.

## Step 8. Connect the service[](id:step8)
To connect to VM, you need to call APIs.

>? Before calling APIs, you need to get the Tencent Cloud API access key in the following steps. Tencent Cloud uses `SecretId` and `SecretKey` to verify your identity and permissions.
>Go to the [TencentCloud API key management](https://console.cloud.tencent.com/cam/capi) page, select **CAM** > **API Key Management** on the left sidebar, click **Create Key** to create a key, and save the `SecretId` and `SecretKey` for subsequent API calls.
