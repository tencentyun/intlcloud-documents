After a video processing task is initiated, it takes anywhere from a few minutes to a few hours for the task to complete execution and output the result. Video processing is essentially an offline task. Taking into account the characteristics of video processing tasks, VOD provides a task system allowing you to initiate tasks synchronously and receive task execution result notifications asynchronously.
![](https://main.qcloudimg.com/raw/8941db2138127cc702ead3f856b5b074.png)

- Initiate a task: after a video processing task is submitted, VOD will immediately return a task ID to you and will wait for some time to start executing the task.
- Notify of result: upon task completion, VOD will send you a result notification, which contains the task ID and execution result.
- Query a task: after submitting a task, you can query the execution status and result of the task by task ID at any time.

## Parameter Templates

Video processing parameters are usually quite complicated. For example, video transcoding involves dozens of parameters such as container format, encoder, bitrate, resolution, and frame rate. In order to simplify the parameters of video processing tasks, VOD offers a variety of integrated parameter templates (e.g., [transcoding templates](https://intl.cloud.tencent.com/document/product/266/33938#.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF)), which are identified by template ID.
- Preset parameter templates: as for common video processing parameter sets, VOD provides a batch of preset parameter templates. For more information, please see [List of Preset Parameter Templates](https://intl.cloud.tencent.com/document/product/266/33932).
- Custom parameter templates: VOD supports customizing parameter templates through the console or server API.

## Task Flow
In VOD, the following video processing operations are independent tasks:
- transcoding to MP4 LD video
- transcoding to MP4 SD video
- sampled screencapturing at intervals of 10s
- intelligent porn information detection
- intelligent categorization

If several independent tasks are executed at the same time, there will be multiple task IDs, and you will have to receive and deal with multiple task result notifications. In order to simply the initiation and notification of multiple tasks, VOD offers a task flow scheme. A task flow is essentially a "parent task" composed of multiple subtasks. Initiating a task flow is equivalent to initiating all the subtasks.
![](https://main.qcloudimg.com/raw/eb772f0b31003f3c3325312e3c1584a5.png)
As shown in the figure, the task flow contains three subtasks and ends when the last subtask (subtask 3) is completed. Task flow result notification will be triggered when the task flow ends as well as when each of the subtasks is completed, enabling you to perceive the execution result of any subtask in real time.

Most video processing tasks in VOD are performed in the form of a task flow, which can be regarded as a special type of task. VOD also supports [creating task flow templates](https://intl.cloud.tencent.com/document/product/266/14058) and naming them. When initiating a task flow, you can use the task flow template name to indicate the desired task.

<span id="OriginatingTask"></span>

## Task Initiation

There are three ways to initiate a video processing task, namely, initiating through server API, initiating through the console, and specifying a task upon upload.

#### Initiating through server API

Through server APIs, you can directly initiate a task for a video in VOD or edit it and specify the tasks to be executed for the generated new video.
- [Processing a video](https://intl.cloud.tencent.com/document/product/266/34125)
- [Processing a video at the specified URL](#APIhttps://intl.cloud.tencent.com/document/product/266/33426)
- [Processing a video by using a task flow template](#APIhttps://intl.cloud.tencent.com/document/product/266/11030)
- [Editing a video](#APIhttps://intl.cloud.tencent.com/document/product/266/34783)
- Publishing on WeChat

#### Initiating through the console

You can initiate a task for a video in VOD through the console. For more information, please see [Processing Videos](https://intl.cloud.tencent.com/document/product/266/33892).

#### Specifying a task upon upload

VOD offers three ways to upload a video: upload from client, upload from server, and upload through the console. All of them support specifying the task to be executed upon upload.

- Upload from client: you can specify a task upon upload through the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#p3).
- Upload from server: you can specify a task upon upload through the `procedure` parameter in the [ApplyUpload](#https://intl.cloud.tencent.com/document/product/266/31767#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) API.
- Upload through console: you can upload a video through the console, select **Process Video During Upload**, and specify the task upon upload. For detailed directions, please see [Uploading Videos](https://intl.cloud.tencent.com/document/product/266/33890).

<span id="ResultNotification"></span>

## Result Notification

After initiating a video processing task, you need to perceive the task execution result asynchronously through "result notification".
Video processing result notifications mainly include the following types:

- [Task Flow Status Change](https://intl.cloud.tencent.com/document/product/266/33953)
- [Video Editing Completion](https://intl.cloud.tencent.com/document/product/266/33954)
- [Publishing on WeChat Completion](https://intl.cloud.tencent.com/document/product/266/33955)

Video processing result notifications are a type of "event notifications" in VOD, which can be received in two modes: "HTTP normal callback" and "reliable callback". For more information, please see [Event Notification](https://intl.cloud.tencent.com/document/product/266/33948).

<span id="TaskQuery"></span>

## Querying a Task

In addition to perceiving the task execution result through result notifications, you can poll task execution status by task ID as scheduled, which is called "task query". Currently, VOD only provides the [DescribeTasks](#apihttps://intl.cloud.tencent.com/document/product/266/33430) and [DescribeTaskDetail](https://intl.cloud.tencent.com/document/product/266/34129) server APIs for querying task execution status and execution result.
