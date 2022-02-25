## Overview

In **Task Management**, you can view the progress and details of your VOD tasks. The **Task Management** page only displays the details of executed tasks and only supports querying task status and details within the last 72 hours.

### Basic task information

Log in to the VOD console and click **[Task Management](https://console.cloud.tencent.com/vod/task)**.
![](https://qcloudimg.tencent-cloud.cn/raw/21f4bcbaf40ed173d1ad4444dd7ba36b.png)
Basic information:

| Field     | Description       |
| ---------- | ---------------------- |
| Task ID       | Unique ID generated after a task is created|
| Task Status       |  <li>`Waiting`: The task is waiting.</li><li>`Completed`: The task is completed. Failed tasks and successfully completed tasks are both considered completed.</li><li>`Processing`: The task is being processed.</li>     |
| Creation Time     | Time when the task is created           |
| Start Time     | Time when the task is executed         |
| Completion Time | Time when the task is completed           |
| Operation         | Subtask type and status    |

### Basic subtask information
Click a subtask to view its details.
![](https://qcloudimg.tencent-cloud.cn/raw/91599f6f274cdb336499d524c727446e.png)
Basic information:

| Field     | Description       |
| ------- | --------------------------------------- |
| FileId  | `FileId` of the media on which the task is executed                |
| File Name    | Filename of the media                       |
| Task Type    | Type of task attached to the `FileId`, which can be video processing, video audit, content analysis, or content recognition |
| Task Status    | <li>Processing</li><li>Completed</li>                                 |
| Subtask|  Name of the subtask attached to the `FileId`               |
