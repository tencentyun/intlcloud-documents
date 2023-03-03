## Overview
After a media processing task is triggered automatically by the upload of a file to COS or initiated manually in the console or by an API call, you can view and manage the task on the [Tasks](https://console.tencentcloud.com/mps/tasks) page.

## Details
### Task list[](id:tlist)
![](https://qcloudimg.tencent-cloud.cn/raw/0123f31fa34d38898ba9eab19ff6ea33.png)

<table border="1">
<tr>
  <th>Header</th>
  <th>Description</th>
</tr>
<tr>
  <td>Task ID</td>
  <td>The ID of the task initiated.</td>
</tr>
<tr>
  <td>Status</td>
  <td>The current status of the task, which may be “waiting”, “in progress”, or “completed”.</li>
    <ul style="margin:0">
			<li><strong>Waiting</strong>: The task is waiting in queue.</li>
			<li><strong>In progress</strong>: A task is considered in progress if at least one of its subtasks is being executed.</li>
			<li><strong>Completed</strong>: A task is considered completed if all its subtasks are completed.</li>
			</ul>
  </td>
</tr>
<tr>
  <td>Creation time</td>
  <td>The time when the task was initiated.</td>
</tr>
<tr>
  <td>End time</td>
  <td>The time when the task ended.</td>
</tr>
<tr>
  <td>Operation</td>
  <td>See <a href="#tquery">Task operations</a> below.</td>
</tr>
</table>

### Querying a task[](id:tquery)
1. Select [Tasks](https://console.tencentcloud.com/mps/tasks) on the left sidebar. The list shows the tasks initiated by the current account.
2. Enter a **task ID** in the search box in the top right corner to search for a task, or click the **Status** header to select the type of tasks you want to view.


### Creating a task[](id:cquery)
1. On the [Tasks](https://console.tencentcloud.com/mps/tasks) page, click **Create task**.
2. Select a file to process and an output path, and specify the transcoding parameters.

### Task operations[](id:operate)
You can view and hide the details of a task, restart and end a task, or play the source video of a task.
- Show details: Click **Show details** to view the information of all the subtasks.
- Restart: For completed tasks, you can click **Restart** to execute its subtasks again.
- End: You can click **End** to cancel tasks whose status is “waiting”.
- Play source video: You can click **Play source video** to play the source video of a task.

### Subtask list[](id:slist)
You can click **Show details** to view the information of the subtasks of a task.

| Header     | Description |
| -------- | -------- |
| Subtask No. | The auto-incrementing sequence of a task. |
| Subtask status | The status of a subtask, which may be waiting, in progress, successful, or failed. |
| Subtask type | The subtask type, which may be audio/video transcoding, screenshot, content discovery, moderation, or audio/video enhancement. |
| Start time   | The time when a subtask started. |
| End time   | The time when a subtask ended. |
| Output   | The output path of a subtask (there are no output paths for content discovery or moderation tasks). |
| Operation | See [Subtask operations](#squery) below. |

### Subtask operations[](id:squery)
You can **view the details** of a subtask as well as **play/view** and **download** its audio/video/images.

| Operation  | Description |
| -------- | -------- |
| Details      | Click “Details” to view the basic information, template, input, and output information of a subtask.                   |
| Play/View | <li>For an audio/video transcoding subtask, you can click “Play” to play the audio/video;</li><br/> <li>for a screenshot subtask, you can click “View” to view the image.</li> |
| Download      | <li>Click **Download** to download the output file of a subtask.</li><br/><li> Only audio/transcoding, screenshot, and audio/video enhancement tasks support this operation. </li><br>**Note: Currently, if multiple screenshots are taken, only the first one can be downloaded. We will add support for package download in the future.** |
