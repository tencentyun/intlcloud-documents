A workflow refers to a set of job tasks performed on a source audio/video file in a process-oriented way, which resemble a physical assembly line. Jobs tasks can be parallel or serial and are generally referred to as tasks in MPS. A workflow is as shown below.
<img src="https://main.qcloudimg.com/raw/9885f9bb3665dbcac1978ed776b7ba5c.png" width = "600px">
- Circle: Indicates the start and end of a task.
- Diamond: Indicates breakdown of a task.
- Rounded rectangle: Indicates an execution unit of a task.
- Dot: Indicates combination or synthesis of tasks.
- Arrow: Indicates the order of executing different tasks or different steps of a task.

An MPS workflow consists of tasks such as transcoding, sampled screencapturing, screencapturing, animated image generating, image sprite generating, and watermarking. Below is an example of a typical MPS workflow:
<img src="https://main.qcloudimg.com/raw/1fee8264c4804a2fa8d69423156ac870.jpg" width = "1000px">
If a transcoding task is of different specifications, such as transcoding to SD and HD and generating screenshots at different sizes, it will be broken down into multiple subtasks that will be executed in parallel. After all transcoding subtasks are completed, MPS will combine their results and end the task.

## How a Workflow Works

Taking video processing as an example, a workflow mainly consists of operations such as configuring a workflow, triggering transcoding, performing a transcoding task, and sending event notifications, as shown below.
<img src="https://main.qcloudimg.com/raw/6ece0c923755b349e470a02df3c1d683.jpg" width = "800px">
1. [Configure a workflow](#p1)
You can configure a workflow in the console as an admin. Before configuring, you must create a CMQ queue and a [COS bucket](https://intl.cloud.tencent.com/document/product/436/6231) and authorize the MPS role.
2. [Trigger transcoding](#p2)
After an audio/video file is uploaded to the created COS bucket in the console or through an SDK, the workflow task (i.e., transcoding task) that is bound to the bucket will be triggered.<!-- You can also use the [ProcessMedia]() API to initiate a transcoding task for a single file.-->
3. [Perform a transcoding task](#3)
Read/write operations such as downloading source files from COS and uploading output files to COS will be performed during the workflow.
4. [Send event notifications](#p4)
After the workflow is completed, MPS will send task completion notifications to the created CMQ queue, and you can receive event notifications through the CMQ API.
>
>- For more information on workflows, please see [Workflow](https://intl.cloud.tencent.com/document/product/1041/33475). For more information on how to set up a workflow, please see [Setting up a Workflow](https://intl.cloud.tencent.com/document/product/1041/33492). 
>- After a file is successfully transcoded, you can proceed to subsequent business logic such as distributing the output video through CDN.

#### <span id="p1"></span>Configuring a workflow
To implement automatic triggering of a transcoding task upon file upload, you need to configure a workflow in advance. The workflow will automatically initiate the specified transcoding task for files uploaded to the specified COS bucket and upload the output files to the same or another COS bucket.

If you do not want to automatically trigger a transcoding task upon file upload, you can call an API to manually trigger a transcoding task for a single file with no need to configure a workflow.

#### <span id="p2"></span>Triggering a transcoding task
A transcoding task can be automatically or manually triggered.
- Automatic triggering: With a configured workflow, a transcoding task will be automatically triggered upon file upload.
<img src="https://main.qcloudimg.com/raw/31c0ac50ecc4a53b4eae6026b3fab6ec.jpg" width = "900px">
- Manual triggering: You can call an API to initiate a transcoding task and receive task completion notifications through CMQ or query the task status through `TaskId`. For more information on manual triggering, please see [Manually Initiating Transcoding](https://intl.cloud.tencent.com/document/product/1041/33493).

	<img src="https://main.qcloudimg.com/raw/e727f9a2703c6bde77e93945133b267f.jpg" width = "900px">

	>
>- Step 5 in the above figure indicates that you can call an API to query the task status with the `TaskId` parameter returned by task initiation.
>- Red boxes indicate optional steps. When you manually trigger a transcoding task, you can use CMQ to receive event notifications or query the task status through an API as shown in step 5.

#### <span id="p3"></span>Performing a transcoding task
A transcoding task includes task processing operations such as transcoding, screencapturing, and watermarking as well as output file uploading. A task will be broken down into several subtasks that will be processed in parallel or serially to speed up the processing.

After the task is completed, MPS will upload the output files to the specified COS bucket. If upload fails, the final task status will be "failed".

#### <span id="p4"></span>Sending event notifications

After a transcoding task is completed, no matter whether the result is successful or failed, MPS will send you a notification of the result and you need to perform further operations as instructed.
