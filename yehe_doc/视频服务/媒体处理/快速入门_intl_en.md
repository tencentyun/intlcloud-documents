## Overview

This document helps you get started with MPS. The diagram below describes the basic steps:

## Directions

### Step 1. Log in

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your identity.
2. Log in to the [MPS console](https://console.tencentcloud.com/mps).

### Step 2. Grant permission to access COS

MPS needs to be able to download files from your COS buckets, transcode the files, and upload the files to your COS buckets after transcoding. Therefore, you need to create a service role to grant MPS the required permissions to access COS.

To grant the permissions, go to the [MPS console](https://console.tencentcloud.com/mps), and click **Go to CAM** to enter the authorization page.
![img](https://qcloudimg.tencent-cloud.cn/raw/29d478d02a8cfcc701ef9ab67daaea38.png)

>! You cannot perform further operations in the MPS console until you have granted the permissions.

### Step 3. Set a template

During media processing, you need to perform audio/video transcoding, watermarking, screencapturing, and other operations. You can control different operations by configuring different templates on the **Templates** page in the console.

### Step 4. Create a scheme

A scheme helps automatically process new media files uploaded to your bucket according to the preconfigured processes and steps. In a scheme, you can set transcoding and screencapturing rules, processing workflows, callback notifications, etc.

1. Log in to the [MPS console](https://console.tencentcloud.com/mps) and go to the **Workflow** > **Schemes** page.
2. Click **Create scheme** to enter the **Create scheme** page. Then, set the **Scheme name**, **Trigger bucket**, **Trigger directory**, **Output bucket**, **Output directory**, **Actions**, and **Enable event notifications**. For more information on how to configure a scheme, see [Scheme Configuration Description](https://intl.cloud.tencent.com/document/product/1041/48780).
![](https://qcloudimg.tencent-cloud.cn/raw/984a8ce5935f4e0263abcf1d10b55227.png)

The table below lists the information needed to configure a scheme.

| Configuration Item       | Required | Description                                                     |
| :----------- | :------- | :----------------------------------------------------------- |
| Scheme name | Yes       | The name can contain up to 128 letters, digits, underscores (_), and hyphens (-), such as "MPS". |
| Trigger bucket  | Yes       | Select a bucket created under the current `APPID`. After the scheme is enabled, videos uploaded to this bucket will be processed automatically. |
|Trigger directory | No | This value must end with a slash (/). If it is left blank, the scheme will take effect for all directories in the trigger bucket. |
|Output bucket | Yes | By default, the output bucket is the same as the trigger bucket. You can also select a bucket in the same region under the same `APPID`. After a scheme is executed, the processed videos will be stored in this bucket. |
|Output directory |No | This value must end with a slash (/). If it is left empty, the output directory will be the same as the trigger directory. |
| Enable event notifications | No       | Event notifications are disabled by default. For more information on how to configure event notifications, see [Getting Started](https://intl.cloud.tencent.com/document/product/1041/33482#recall). To enable TDMQ-CMQ event notifications, go to the [TDMQ console](https://console.tencentcloud.com/tdmq/cmq-queue?rid=1) to activate the service and create a model. After event notifications are enabled, the specified CMQ queue/topic will receive the event notifications of MPS. |
| Actions       | Yes       | Select at least one task from transcoding, screencapturing, animated screenshot generating, moderation, content recognition, and content analysis tasks to configure the scheme. |

| Callback Method Type  | Configuration Description                                                     |
| :------------ | :----------------------------------------------------------- |
| TDMQ-CMQ callback | TDMQ-CMQ model: Select **Queue Model** or **Topic Model**. **Queue Model** is selected by default. TDMQ-CMQ region: Select **Guangzhou**, **Shanghai**, **Beijing**, **Shanghai Finance**, **Shenzhen Finance**, **Hong Kong (China)**, **Chengdu**, **North America**, or **West US**. Queue Name/Topic Name: Customize a name. |
| HTTP callback     | When you call the [TaskNotifyConfig](https://intl.cloud.tencent.com/document/product/1041/33690#TaskNotifyConfig) API of the task, set `NotifyType` to `URL` and `NotifyUrl` to the HTTP callback URL. |
| SCF callback      | You can click [Go to SCF Console](https://console.tencentcloud.com/scf/list-create?rid=1&ns=default&keyword=mps) for configuration. For more information on how to configure the callback, see [MPS Task Callback Notification](https://intl.cloud.tencent.com/document/product/1041/40337). SCF callback configuration takes effect for all schemes. The configuration will not be retained for the current scheme. |

### Step 5. Enable the scheme

1. After a scheme is created, the **Created successfully** message will appear, and you will be automatically redirected to the Schemes page. In the scheme list, you can manage the scheme you just created.
2. A scheme is not enabled by default. To enable a scheme, click the status button on the row of the scheme. Only after the scheme is enabled will it be automatically executed when a video is uploaded to the trigger bucket.

### Step 6. Initiate a task

Currently, you can initiate a task by calling a task initiation API, uploading a video file to the COS directory bound to a scheme, or manually creating a task in **Tasks** > [**Create task**](https://console.tencentcloud.com/mps/tasks/create).

- **Manual task creation:**
  1. Go to the [Tasks](https://console.tencentcloud.com/mps/tasks) page.
  2. Click [Create task](https://console.tencentcloud.com/mps/tasks/create).
  3. Select the target video file, output path, and transcoding template and initiate the task.
- **Automatic trigger for video uploaded to COS:**
  1. After the scheme is enabled, go to the [COS console](https://console.tencentcloud.com/cos5) and click **Bucket List** on the left sidebar.
  2. Locate the trigger bucket set in the scheme, click its name to enter the **File List** page, and upload a video file. MPS will automatically process the video according to the scheme settings.

>?A scheme will be executed automatically only on video files that are uploaded to the trigger bucket after the scheme is enabled. Files uploaded before the scheme is enabled will not be processed.

### Step 7. Manage tasks

1. Go to the [Tasks](https://console.tencentcloud.com/mps/tasks) page to view the list of all initiated tasks.
2. You can filter tasks to be processed by field such as **Status** and **Task ID**. You can also click **View details** to view the subtask information, click **Restart** to restart tasks queuing up, play back the source video, and perform other operations.
3. You can expand the subtask list to view the subtask information. You can also play back/view subtask files, download subtask output files, view subtask details, and perform other operations.
![img](https://qcloudimg.tencent-cloud.cn/raw/74e5076bc92486b61de0cce1283d6d58.png)
