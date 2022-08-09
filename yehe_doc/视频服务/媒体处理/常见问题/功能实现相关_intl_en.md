[](id:que1)

### How to obtain media metadata?
Please see [DescribeMediaMetaData](https://intl.cloud.tencent.com/document/product/1041/37461).

[](id:que2)

### How to configure a time point screenshot task?

#### Through an API

For details, please see [CreateSnapshotByTimeOffsetTemplate](https://intl.cloud.tencent.com/document/product/1041/33672).

#### Via the console

1. Log in to the [MPS console](https://console.cloud.tencent.com/mps/workflows/add) and click **Workflow Management** on the left sidebar.
2. Click **Create Workflow** to enter the workflow creation page and set the workflow name, trigger bucket, trigger directory, output bucket, output directory, event notifications and configuration items.
3. Select **Time point screenshot** for **Screencapturing Method**. Please note that you can set the template name and screenshot dimensions in template settings, but the time point must be configured in workflow settings.
![](https://qcloudimg.tencent-cloud.cn/raw/751f3dd9ea1c03ed9dce47a83d13008b.png)
 - Screenshot template: You can choose time point screenshot, sampled screenshot, or image sprite screenshot and select from the existing templates for each mode. For time point screenshot, you must also specify the time point. If existing templates do not meet your needs, you can create new ones in [**Template Settings** > **Screenshot Template**](https://console.cloud.tencent.com/mps/templates?tab=snapshot).
 - Watermark template: You can add up to 4 watermarks to each transcoding task. If existing watermarks do not meet your needs, you can create new ones in [**Template Settings** > **Watermark Template**](https://console.cloud.tencent.com/mps/templates?tab=watermark).

[](id:que3)
### How to create a video analysis template?
MPS provides [preset video analysis templates](https://intl.cloud.tencent.com/document/product/1041/33476). You can also use a [server API](https://intl.cloud.tencent.com/document/product/1041/37470) to create and manage custom video analysis templates.

[](id:que4)
### How to use video analysis templates?
1. Initiate a video analysis task. You can **call an API** to initiate a task or configure **automatic triggering of a task upon video upload**.
2. After initiating a task, you can query the result synchronously or get the result asynchronously in the callback.

[](id:que5)
### Can I query newly finished tasks using `ScrollToken`?
You may not be able to query newly finished tasks using the pagination flag parameter `ScrollToken` because the tasks returned are sorted by creation time.
>? The pagination flag parameter `ScrollToken` is used when you paginate your queries. If it’s impossible to query all tasks with one request, the API will return `ScrollToken`, which should be passed in for the next request so that it starts from the record following `ScrollToken`.

[](id:que6)
### How to query the task list?
For detailed directions, see the [DescribeTasks](https://intl.cloud.tencent.com/document/product/1041/33643) API.

[](id:que7)
### How are the tasks returned sorted?
The tasks returned are sorted by **creation time**. For details, see [DescribeTasks](https://intl.cloud.tencent.com/document/product/1041/33643).

[](id:que8)
### How to add animated watermarks?
Convert animated images into APNG format, and add them as watermarks in workflow settings.

[](id:que9)
### How to modify a watermark template?
For details, see the [ModifyWatermarkTemplate](https://intl.cloud.tencent.com/document/product/1041/33646) API.

[](id:que10)
### How to associate MPS with COS buckets?
When configuring a workflow, select a trigger bucket, and videos uploaded to the selected bucket will be processed automatically. For more information, see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).

[](id:que11)

### OCR results are generated for a video frame. How do I get the frame in question?
Use the `ProcessMedia` API to take a screenshot of the video at the specified time point.
1. Note the time point when OCR results are generated.
2. Pass the time point to the request parameter of `ProcessMedia`: [MediaProcessTaskInput](https://intl.cloud.tencent.com/document/product/1041/33640) > [SnapshotByTimeOffsetTaskInput](https://intl.cloud.tencent.com/document/product/1041/33690).

[](id:que12)

### How to grant access to COS?

MPS needs read and write access to COS in order to download and transcode videos in COS buckets as well as upload files to buckets. Therefore, you need to create a service role and grant the role access to COS.
Directions:
1. Log in to the [MPS console](https://console.cloud.tencent.com/mps) and click **Authorization Management** on the left sidebar. Click **Go to CAM** to go to the permission management page to grant the access. After MPS is authorized, the system will create a preset service role and grant MPS relevant access.
![](https://qcloudimg.tencent-cloud.cn/raw/acd667fb5514bc01da3deaf0f84fbcc8.png)

>! You cannot perform further operations in the MPS console before granting the access.
2. After authorization, return to the authorization management page, and you will see that the access has been granted successfully. You can revoke the access granted by clicking **Cancel Authorization** to go **CAM** and deleting the [service role](https://intl.cloud.tencent.com/document/product/598/19388).
![](https://qcloudimg.tencent-cloud.cn/raw/f880511bc91dfbda8bde68990c93adcc.png)
