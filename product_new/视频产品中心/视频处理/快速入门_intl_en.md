## Introduction
This document helps you get started with using MPS. The diagram below describes the basic steps:
![](https://main.qcloudimg.com/raw/aed6a4e4f8b3bb99187e0d899ac05338.png)

## Directions
### Step 1. Sign up and log in
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your identity.
2. Log in to Tencent Cloud website and select **Cloud Products** > **Video Services** > [**Media Processing Service**](https://console.cloud.tencent.com/mps) to enter the MPS Console.

### Step 2. Permissions authorization
MPS needs to perform read/write operations, including downloading, transcoding and uploading for files in COS buckets. Therefore, you need to create service roles and grant MPS permissions to operate on COS resources.

Go to the [MPS Console](https://console.cloud.tencent.com/mps). If you have not authorized MPS, click **Go to CAM** to enter the permission management page to authorize MPS.
![](https://main.qcloudimg.com/raw/a3204a6470d3a9740a081849fc7324f3.png)

>If you have not completed authorization, you cannot perform further operations in the MPS Console.



### Step 3. Create a bucket
Because video processing is performed on video files uploaded to COS, you need to first create a bucket in the COS Console.

Go to the Bucket List page in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) and click **Create Bucket** to create a bucket. Then, you can create folders in the bucket and upload files. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

 

### Step 4. Create a workflow
A workflow can help you automatically process video files uploaded to the bucket using created templates. In a workflow, you can set tasks such as transcoding, screencapturing, animated image generating, and watermarking.
1. Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Workflow Management** to enter the workflow management page.
2. Click **Create Workflow** to enter the workflow creation page and set the workflow name, trigger bucket, trigger directory, output bucket, output directory, configuration items, and event notification. For more information, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).
![](https://main.qcloudimg.com/raw/a2b3e7b0e7e41b68221ea1d2b874b06e.png)

Here are the items that need to be configured to create a workflow:

Configuration Item | Required | Description
-----------|-----------|-----
Workflow name | Yes | The name can consist of up to 128 letters, digits, underscores (_), backslashes (\), or hyphens (-), e.g., "MPS".
Trigger bucket | Yes | You can select a bucket under the current APPID as the trigger bucket. When the workflow is enabled, video files uploaded to this bucket will automatically trigger execution of the workflow.
Trigger directory | No | This value must end with a slash (/). If it is left blank, the workflow will take effect for all directories in the trigger bucket.
Output bucket | Yes | This value is the same as the trigger bucket by default. You can select a bucket under the current APPID in the same region as the trigger bucket as the output bucket. After a workflow is completed, the output video file will be stored in this bucket.
Output directory |No | This value must end with a slash (/). If it is left blank, the output directory will be the same as the trigger directory.
Event notification | No | Disabled by default.
Configuration items | Yes | Tasks include transcoding, screencapturing, or animated image generating. You must select at least one task.

### Step 5. Enable the workflow
1. You will see a success message when the workflow is created. Click **Manage Workflow** to go to the [workflow management](https://intl.cloud.tencent.com/document/product/1041/33485) page.
	![](https://main.qcloudimg.com/raw/81ae87468f4c99773278fd6487e39bd4.png)
2. The workflow is disabled by default. Locate the workflow in the list and click the status button to enable it. Uploaded videos in the trigger bucket will auto-trigger workflow execution only when the workflow is enabled.

 

### Step 6. Upload a video
1. After the workflow is enabled, go to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Locate the trigger bucket set in the workflow and click the name. You will be taken to the File List page. Upload the video file to be processed on this page, and MPS will automatically process it according to the workflow settings.
>Automatic execution of a workflow will take effect only for files uploaded to the trigger bucket after the workflow is enabled. Files uploaded before the workflow is enabled will not be touched. 


### Step 7. View the output video
1. After video processing is completed, go to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Locate the output bucket set in the workflow and click the name. You will be taken to the File List page. On this page, you can view the output video file processed according to the workflow task configuration.















