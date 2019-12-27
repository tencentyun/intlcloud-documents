## Operation Scenarios
This document helps you get started with and connect to MPS quickly. The process of using MPS is as shown below:
![](https://main.qcloudimg.com/raw/aed6a4e4f8b3bb99187e0d899ac05338.png)

## Directions
### Step 1. Sign up and log in
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your identity.
2. Log in to Tencent Cloud's official website and select **Cloud Products** > **Video Services** > [**Media Processing Service**](https://console.cloud.tencent.com/mps) to enter the MPS Console.

### Step 2. Manage authorization
Because MPS needs to perform read/write operations such as downloading files from, transcoding files in, and uploading files to COS buckets, you need to create service roles and grant MPS permissions to operate on COS resources.

Go to the [MPS Console](https://console.cloud.tencent.com/mps). If you have not authorized MPS, click **Go to CAM** to enter the unified permission management page to authorize MPS.
![](https://main.qcloudimg.com/raw/a3204a6470d3a9740a081849fc7324f3.png)
>If you have not completed authorization, you cannot perform further operations in the MPS Console.



### Step 3. Create a bucket
Because video processing is to perform operations on video files uploaded to COS, such as transcoding or screencapturing, you need to create a bucket in the COS Console first.

Enter the bucket management page in the [COS Console](https://console.cloud.tencent.com/cos5) and click **Create Bucket** to create a bucket. Then, you can create folders in the bucket and upload files to them. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/6232).

 

### Step 4. Create a workflow
A workflow can help you automatically process the latest video files uploaded to the bucket using created templates. In a workflow, you can set tasks such as transcoding, screencapturing, animated image generating, and watermarking.
1. Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Workflow Management** to enter the workflow management page.
2. Click **Create Workflow** to enter the workflow creation page and set the workflow name, triggered bucket, triggered directory, output bucket, output directory, configuration items, and event notification. For more information, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).
![](https://main.qcloudimg.com/raw/a2b3e7b0e7e41b68221ea1d2b874b06e.png)

On the workflow creation page, the information to be configured is as follows:

Configuration Item | Required | Description
-----------|-----------|-----
Workflow name | Yes | You can enter a string consisting of up to 128 letters, digits, underscores (_), backslashes (\), or hyphens (-), e.g., "MPS".
Triggered bucket | Yes | You can select a bucket created under the current APPID as the triggered bucket. After a workflow is enabled, video files uploaded to this bucket will automatically trigger execution of the workflow.
Triggered directory | No | The value of this parameter must end with a slash (/). If it is left blank, all directories in the triggered bucket will be available.
Output bucket | Yes | The value of this parameter is the same as the triggered bucket by default. You can select a bucket under the current APPID in the same region as the triggered bucket as the output bucket. After a workflow is completed, the output video file will be stored in this bucket.
Output directory |	No | The value of this parameter must end with a slash (/). If it is left blank, the output directory will be the same as the triggered directory.
Event notification | No | Disabled by default.
Configuration items | Yes | You can select at least one item for configuration for a transcoding, screencapturing, or animated image generating task.
 
### Step 5. Enable the workflow
1. After the workflow is created, the message "The workflow is successfully created" will be displayed. Click **Manage Workflow** to go to the [workflow management](https://intl.cloud.tencent.com/document/product/1041/33485) page.
	![](https://main.qcloudimg.com/raw/81ae87468f4c99773278fd6487e39bd4.png)
2. The workflow is disabled by default. Click the status button in the row of the workflow to enable it. Only after the workflow is enabled can videos uploaded to the triggered bucket trigger automatic execution of the workflow.

 

### Step 6. Upload a video
1. After the workflow is enabled, go to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the name of the triggered bucket set in the workflow. The file list page will be displayed by default. Upload the video file to be processed on this page, and MPS will automatically process it according to the workflow settings.
>Automatic execution of a workflow will take effect only for files uploaded to the triggered bucket after the workflow is enabled. Files uploaded before the workflow is enabled will be left alone. 
 

### Step 7. View the output video
1. After video processing is completed, go to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the name of the output bucket set in the workflow. The file list page will be displayed by default. On this page, you can view the output video file processed according to task configuration of the workflow.















