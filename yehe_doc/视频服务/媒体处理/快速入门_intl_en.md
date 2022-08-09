## Overview
This document helps you get started with MPS. The diagram below describes the basic steps:
![](https://main.qcloudimg.com/raw/aed6a4e4f8b3bb99187e0d899ac05338.png)

## Directions
### Step 1. Sign up and log in
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your identity.
2. Log in to the [MPS console](https://console.cloud.tencent.com/mps).

### Step 2. Grant access to COS
MPS needs read and write access to COS in order to download and transcode videos in COS buckets and upload files to the buckets. Therefore, you need to create a service role and grant the role access to COS.

If you haven’t granted the access yet, go to the [MPS console](https://console.cloud.tencent.com/mps), and click **Go to CAM** to enter the authorization page to grant the access.
![]![](https://main.qcloudimg.com/raw/a3204a6470d3a9740a081849fc7324f3.png)

>!You cannot perform further operations in the MPS console before granting the access.



### Step 3. Create a bucket
Because video processing is performed on video files uploaded to COS, you need to first create a bucket in the COS console.

In the COS console, select [Bucket List](https://console.cloud.tencent.com/cos5/bucket) and click **Create Bucket** to create a bucket. You can then create folders in the bucket and upload files to them. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

 

### Step 4. Create a workflow
With the use of templates, a workflow can automatically process video files uploaded to a specified bucket. You can add tasks such as transcoding, screenshot taking, and animated image generating to a workflow.
1. In the [MPS console](https://console.cloud.tencent.com/mps), click **Workflow Management**.
2. Click **Create Workflow** to enter the workflow creation page and set the workflow name, trigger bucket, trigger directory, output bucket, output directory, event notifications and configuration items. For detailed instructions, please see [workflow configuration](#workflow).
![](https://main.qcloudimg.com/raw/a2b3e7b0e7e41b68221ea1d2b874b06e.png)
The table below lists the information needed to configure a workflow.
<table>
<tr><th>Item<a id="workflow"></a></th><th>Required</th><th>Description</th></tr>
<tr>
<td>Workflow name</td>
<td>Yes</td>
<td>Max 128 characters; supports Chinese characters, letters, digits, underscores, and hyphens<code>（_-）</code>. Example: "MPS"</td>
</tr><tr>
<td>Trigger bucket</td>
<td>Yes</td>
<td>Select a bucket created under the current `APPID`. After the workflow is enabled, videos uploaded to this bucket will be processed automatically.</td>
</tr><tr>
<td>Trigger directory</td>
<td>No</td>
<td>A string that ends with <code>(/)</code>. If it is left empty, the workflow will be applied to all directories under the selected trigger bucket.</td>
</tr><tr>
<td>Output bucket</td>
<td>Yes</td>
<td>By default, the output bucket is the same as the trigger bucket. You can also select a bucket in the same region under the same `APPID`. After a workflow is executed, the processed videos will be stored in this bucket.</td>
</tr><tr>
<td>Output directory</td>
<td>No</td>
<td>A string that ends with <code>(/)</code>. If it is left empty, the output directory will be the same as the trigger directory.</td>
</tr><tr>
<td>Event notifications</td>
<td>No</td>
<td><ul style="margin:0"><li>Disabled by default. For detailed instructions on how to configure event notifications, please see <a href="#recall">callback configuration</a> below. </li><li>To enable CMQ event notifications, you need to activate <a href="https://console.cloud.tencent.com/cmq">CMQ</a> and create a model. After CMQ event notifications are enabled, the specified CMQ will receive notifications about video processing events.</li></ul></td>
</tr><tr>
<td>Configuration items</td>
<td>Yes</td>
<td>From transcoding, screenshot taking, animated image generation, moderation, content recognition, and content analysis, select at least one task for configuration. For details, please see <a href="https://intl.cloud.tencent.com/document/product/1041/33485#p1">task configuration</a>.</td>
</tr></table>
<table>
<tr><th>Callback Method<a id="recall"></a></th><th>Configuration</th></tr>
<tr>
<td>CMQ callback</td>
<td><ul style="margin:0"><li>CMQ model: queue model by default </li><li>CMQ zone: Guangzhou, Shanghai, Beijing, Shanghai Finance, Shenzhen Finance, Hong Kong (China), Chengdu, North America, or West US </li><li>Queue name: a custom value </li></ul></td>
</tr><tr>
<td>SCF callback</td>
<td>Click **Go to SCF Console** to configure the callback in the SCF console. For detailed instructions, please see <a href="https://intl.cloud.tencent.com/document/product/1041/40337">MPS Task Callback Notification</a>. <br>The configuration applies to all workflows and is not saved specifically by one workflow. </td>
</tr></table>


### Step 5. Enable the workflow
1. You will see the toast message "Created workflow successfully" after creating a workflow. Click **Manage Workflow** to go to the [workflow management](https://intl.cloud.tencent.com/document/product/1041/33485) page.
![](https://main.qcloudimg.com/raw/81ae87468f4c99773278fd6487e39bd4.png)
2. Workflows are disabled by default. To enable your workflow, click the toggle in the **Enable** column. A workflow will be executed automatically on videos uploaded to the trigger bucket only after it is enabled.

 

### Step 6. Upload a video
1. After the workflow is enabled, go to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar.
2. Locate the trigger bucket set in the workflow, click its name to enter the **File List** page, and upload a video file. MPS will automatically process the video according to the workflow settings.
>?A workflow will be executed automatically on video files uploaded to the trigger bucket only after it is enabled. Files uploaded before the workflow is enabled will not be processed. 


### Step 7. View the processed video
1. After the video is processed, go to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar.
2. Locate the output bucket set in the workflow and click its name to enter the **File List** page, where you can view the video processed according to the workflow settings.





