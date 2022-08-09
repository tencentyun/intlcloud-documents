A workflow refers to a set of job tasks performed on a source audio/video file. Job tasks can be parallel or serial and are simply referred to as tasks in MPS. A workflow is as shown below.
<img src="https://main.qcloudimg.com/raw/f327643bd24f9aaa1dec7b9a158fbe60.gif" width = "650px">

| Symbol | Meaning |
|---------|---------|
| Circle | Start and end of a task |
| Diamond | Task breakdown |
| Rectangle | Task unit |
| Dot | Assembly or combination of task units |
| Arrow | Order of executing different tasks or different steps of a task |

An MPS workflow may consist of tasks such as transcoding, sampled screenshot, time point screenshot, animated image generating, image sprite generating, and watermarking. Below is a typical example of an MPS workflow:
<img src="https://main.qcloudimg.com/raw/1fee8264c4804a2fa8d69423156ac870.jpg" width = "750px">
If a task involves multiple outputs, such as transcoding to SD and HD or taking screenshots of different sizes, it will be broken down into multiple subtasks that will be executed simultaneously. After all subtasks are completed, MPS will combine the results, and the task ends.

## How a Workflow Works

The process of executing a workflow involves workflow configuration, task triggering, task execution, and event notification sending, as shown below:
<img src="https://main.qcloudimg.com/raw/6ece0c923755b349e470a02df3c1d683.jpg" width = "900px">

1. [**Workflow configuration**](#p1): You can configure a workflow in the console as an admin. Before configuration, you must create a CMQ queue and a [COS bucket](https://intl.cloud.tencent.com/document/product/436/32955) and grant your MPS service role access to the two services.
2. [**Task triggering**](#p2): After an audio/video file is uploaded via the console or through an SDK to the COS bucket created, the task bound to the bucket will be triggered. You can also use the [ProcessMedia](https://intl.cloud.tencent.com/document/product/1041/33640) API to initiate a task on a specific file.
3. [**Task execution**](#p3): Read/Write operations such as downloading source files from COS and uploading output files to COS will be performed during task execution.
4. [**Event notification sending**](#p4): After the workflow is completed, MPS will send a notification to the CMQ queue created. You can receive the notification through a CMQ API.
>?
>- For more information on workflows, see [Workflow](https://intl.cloud.tencent.com/document/product/1041/33475). For how to set up a workflow, see [Setting Workflow](https://intl.cloud.tencent.com/document/product/1041/33492). 
>- After a file is transcoded successfully, you can proceed with your subsequent business logic, such as distributing the transcoded video through CDNs.

[](id:p1)
### Configuring workflow
You need to configure a workflow if you want a task to be triggered automatically upon file upload. After configuration, the task will be initiated automatically on files uploaded to the specified COS bucket and the output files will be uploaded to the same or a different COS bucket.

You can also call an API to initiate a task on a specific file, in which case workflow configuration is not required.

[](id:p2)
### Triggering task
A transcoding task can be automatically or manually triggered.
- **Automatic triggering**: If a workflow is configured, the transcoding task will be automatically triggered upon file upload.
<img src="https://main.qcloudimg.com/raw/31c0ac50ecc4a53b4eae6026b3fab6ec.jpg" width = "900px">
- **Manual triggering**: You can call an API to initiate a transcoding task and receive task completion notifications through CMQ or query the task status by `TaskId`. For details, see [Manually Initiating Transcoding](https://intl.cloud.tencent.com/document/product/1041/33493).<br>
<img src="https://main.qcloudimg.com/raw/e727f9a2703c6bde77e93945133b267f.jpg" width = "900px">

>?
>- Step 5 is the query of the task status via an API. The request parameter is the `TaskId` returned after task initiation.
>- Steps in the red box are optional. When you manually trigger a transcoding task, you can use CMQ to receive notifications or query the task status through an API as shown in step 5.

[](id:p3)
### Executing task
Task execution may involve transcoding, screenshot taking, watermarking, and output file upload. A task is broken down into several subtasks, which are executed in parallel or in series to speed up the process.

After the task is completed, MPS will upload the output files to the specified COS bucket. If upload fails, the task status will be "failed".

[](id:p4)
### Sending event notification

You will be notified when a task is completed, whether it succeeds or fails. You can determine what to do next depending on the notification.

