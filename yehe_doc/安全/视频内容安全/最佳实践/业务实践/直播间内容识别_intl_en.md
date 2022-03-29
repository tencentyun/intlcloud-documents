After activating [VM](https://console.cloud.tencent.com/cms/video/package), you can directly call **VM** APIs to batch recognize video stream content (such as live rooms and video meetings).
>?
>- Before calling the API, make sure that the current account **has at least the access permission of VM**. For more information on how to configure the permission, see [CAM Authorization Guide](https://intl.cloud.tencent.com/document/product/1140/44981).
>- If you cannot access the service, you will need to activate the service/check the billing information (for root account) or request the corresponding permission from the admin or root account (for sub-account/collaborator).


## Step 1. Configure a policy (optional)[](id:step1)
We recommend you configure a recognition policy based on your business needs for a personalized user experience.
>?
>- You can skip this step if you use the preset default policy of Tencent Cloud CMS.
>- The default policy is developed by TenDI based on models for multiple industries. It is suitable for most content security requirements.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/overview) and select **VM** > **Policy Management** on the left sidebar.
2. On the **Policy Management** page, click **Create Policy** to enter the **Create Policy** page.
![](https://qcloudimg.tencent-cloud.cn/raw/17c5d3d4e582324fd882766818649de3.png)
3. On the **Policy Configuration** page, enter the relevant information of the policy and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/80fa8771fc76a001becd8c7779fba829.png)

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
5. On the **Custom Library Configuration** page, select a custom dictionary for content recognition in the **Custom Dictionary** drop-down list. If there are no custom libraries, you can click **Next** or save the current policy and go to [Step 3. Configure a custom dictionary](#step3).
![](https://qcloudimg.tencent-cloud.cn/raw/dcd57f63e8d9482bfa42c45ab15e4877.png)
6. On the **Creation Completion** page, you can view the policy configuration information. After confirming it, click **Complete**.
7. The policy just created will be displayed in the list on the right of the **Policy Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/17c5d3d4e582324fd882766818649de3.png)

## Step 2. Configure a global task template (optional)[](id:step2)
Task templates are used to manage how files are processed for recognition tasks.
>? You can skip this step if the default template is used.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/srvconfig) and select **VM** > **Service Management** on the left sidebar.
2. On the service management page, click **View Details** to enter the template details page.
>?Currently, only the default template can be edited for template configuration.

![](https://qcloudimg.tencent-cloud.cn/raw/8dbaa385139993cb985e6b3ff34e121f.png)
3. On the template details page, click **Edit** in the top-right corner to modify parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/a530cd081bf816aa6cd788334f73fc3c.png)

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

## Step 3. Configure a custom dictionary (optional)[](id:step3)
You can configure a custom dictionary.
>? You can skip this step if you don't need to configure a custom dictionary.

1. Log in to the [CMS console](https://console.cloud.tencent.com/cms/video/lib) and select **VM** > **Custom Library Management** > **Custom Dictionary** on the left sidebar.
2. On the **Custom Dictionary** page, click **Add Dictionary** to pop up the **Create Dictionary** window.
![](https://qcloudimg.tencent-cloud.cn/raw/a5cab3158d386825f5ff04b3ac24f169.png)
3. In the **Create Dictionary** pop-up window, configure a custom library based on your business needs.
![](https://qcloudimg.tencent-cloud.cn/raw/c88c26512d3c63f5d629f6858e177bc7.png)

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
<td>You can select <strong>Non-compliant</strong> or <strong>Suspected</strong>.<ul><li><strong>Non-compliant</strong>: the information is identified as non-compliant information</li><li><strong>Suspected</strong>: the information may be non-compliant and requires manual recognition</li></ul></td>
</tr>
<tr>
<td>Match Mode</td>
<td>You can select <strong>Exact match</strong> or <strong>Fuzzy match</strong>.<ul><li><strong>Exact match</strong>: it <strong>exactly</strong> matches the entered text</li><li> <strong>Fuzzy match</strong>: it detects variants of the entered keyword to fuzzily match similar words such as split words, homographs, homophones, upper and lower cases, and numbers in words</li></ul></td>
</tr>
</tbody></table>

4. Click **OK**.
5. The dictionary just created will be displayed in the list below the **Custom Dictionary** tab.
>? Different colors in a custom dictionary represent different blocking logics, where red represents "non-compliant", and orange represents "suspected".

![](https://qcloudimg.tencent-cloud.cn/raw/7404d269257fc18e37b6309392a23cf9.png)
6. On the **Custom Dictionary** page, select the dictionary just created and click **Manage** in the **Operation** column to enter the dictionary management page.
![](https://qcloudimg.tencent-cloud.cn/raw/a6c45d646c24a1d8fae62a24103a6244.png)
7. On the dictionary management page, click **Add Sample** to pop up the **Add Sample** window.
8. In the **Add Sample** pop-up window, select the handling suggestion, enter keywords, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/178d44db27e4ae7522bfad6d0d900c67.png)
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

>? After configuring the custom dictionary, you can associate it with the policy created in [Step 1. Configure a policy](#step1).


## Step 4. Create a VM task 
After completing the above steps, you can call the **CreateVideoModerationTask** API to create a video live room recognition task as instructed below: 
- Make sure that the video meets the [file format requirements](https://intl.cloud.tencent.com/document/product/1140/46113#1.-.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) of the API.
- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1140/46113#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
- If the task is created successfully, you can use the task query API to query task details, and you can refer to the [example of creating video recognition task](https://intl.cloud.tencent.com/document/product/1140/46113#.E7.A4.BA.E4.BE.8B1-.E5.88.9B.E5.BB.BA.E8.A7.86.E9.A2.91.E5.AE.A1.E6.A0.B8.E4.BB.BB.E5.8A.A1) for more information on sample response parameters. If task creation fails, the API will return an error code, and you can refer to [Business Error Codes](https://intl.cloud.tencent.com/document/product/1140/46113#6.-.E9.94.99.E8.AF.AF.E7.A0.81) and [Common Error Codes](https://intl.cloud.tencent.com/document/product/1140/46108#.E9.94.99.E8.AF.AF.E8.BF.94.E5.9B.9E.E7.BB.93.E6.9E.9C) for troubleshooting.

>? When connecting to the service, you can use API Explorer for online debugging.

## Step 5. Get the VM task result
After creating the video recognition task, you can call the **DescribeTaskDetail** API to query the details of the task as instructed below: 
- Enter the input parameters as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1140/46112).
- If the API call is successful, you will receive the response output from the API, including the task details. You can refer to the [example of viewing task details](https://intl.cloud.tencent.com/document/product/1140/46112#.E7.A4.BA.E4.BE.8B1-.E6.9F.A5.E7.9C.8B.E4.BB.BB.E5.8A.A1.E8.AF.A6.E6.83.85) for more information on sample response parameters.
