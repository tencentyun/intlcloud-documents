Task flows help you create templates in accordance with the logical flow of video processing to transcode the video, capture screens, add watermarks to the video, and audit the video files. 
Log in to the [VOD console](https://console.cloud.tencent.com/video) and click **Video Processing** > **Task Flow Settings** in the left navigation pane, then you will see a list of task flows:
1. A task flow list shows information such as the names and IDs of the tasks, and you can sort the tasks by created time or modified time. To view, edit, or delete a specified task flow, go to **Operation**.
2. To create a task flow template, click **Create Task Flow**.

![Task Flow](https://main.qcloudimg.com/raw/a47ba19d0719ea474a640790b2a8b26d.png)

You can create a name and configure tasks for the task flow template. You need to select a least one task from transcoding, screen capturing, thumbnail downloading, animated image generating, and video auditing to configure a task flow.
![Create Task Flow](https://main.qcloudimg.com/raw/f1a66053364891b0f283c13e9364bb73.png)
Click **Submit** to create a task flow. The system will notify you once the task flow is created successfully, then you will see information about the task flow in the task flow list. 

## Transcoding Task Configuration

You can configure a transcoding task by clicking "Transcoding task" in the configurable task.
![Create Task Flow - Transcoding](https://main.qcloudimg.com/raw/91912e7700e005c31758aeedf194381c.png)
According to the rule, you can configure transcoding templates with an added  watermark template for task flow. Please note that you can only select the configured templates for the task flow.

- Transcoding template: Select one from the created templates. You can configure one or more transcoding templates for each task. If the existing templates do not meet the usage requirements, change the settings at "Template settings - Transcoding template". To view the newly added template, click "Refresh".
- Watermark template: Up to 4 watermarks can be added to each transcoding template. If the existing watermarks do not meet the usage requirements, change the settings at "Template Settings - Watermark Template". To view the newly added template, click "Refresh".

## Screen Capturing Task Configuration

You can configure a screen capturing task for the task flow by selecting "Screencapturing task" in the configurable task.
![Create Task Flow - Screencapturing](https://main.qcloudimg.com/raw/bae5e7848a2b8799393790cbbec48c3c.png)
According to the rule, you can configure screen-capturing templates with an added watermark template for task flow. Please note that you can only select the configured templates for the task flow.

- Screen capturing template: There are three types of screenshots: point-in-time screenshot, sampling screenshot, and sprite screenshot. For each type of screenshot, you can only select the template that has been configured for that type. You need to select the time points for point-in-time screenshots. If the existing templates do not meet the usage requirements, change the settings at "Template settings - Screencapturing template". To view the newly added template, click "Refresh".
- Watermark template: Up to 4 watermarks can be added to each template. If the existing templates do not meet the usage requirements, change the settings at "Template settings - Watermark template". To view the newly added template, click "Refresh".

## Video Thumbnail Downloading Task Configuration

You can configure a video thumbnail downloading task by clicking "Video Thumbnail Downloading Task" in the configurable task.
![Create Task Flow - Cover Creating](https://main.qcloudimg.com/raw/52f13aa3c546f9931cf9eeb085a0ef6e.png)
According to the rule, you can configure video thumbnail downloading templates with an added watermark template for task flow. Please note that you can only select the configured templates for the task flow.

- Video thumbnail downloading template: Only point-in-time screen-capturing are supported. You can set the sampling time point in terms of time offset or percentage of total time span. If the existing templates do not meet the usage requirements, change the settings at "Template settings - Screenshot template". To view the newly added template, click "Refresh".
- Watermark template: Up to 4 watermarks can be added to each template. If the existing templates do not meet the usage requirements, change the settings at "Template settings - Watermark template". To view the newly added template, click "Refresh".

## Animated Image Generating Task Configuration

You can configure  Fgenerating task by clicking "Animated Image Generating Task" in the configurable task.
![Create Task Flow - animated image generating](https://main.qcloudimg.com/raw/35b391f6394e1f2b4b5fc0f816fef42b.png)
According to the rule, you can configure animated image generating templates for task flow. Please note that you can only select the configured templates for the task flow.
animated image generating template: You can add multiple templates and update the time period for animated image generating task. If the existing templates do not meet the usage requirements, change the settings at "Template settings - animated image generating template". To view the newly added template, click "Refresh".

## Video Auditing Task Configuration

You can configure a video auditing task by clicking "Video Auditing Task" in the configurable task. Auditing your content on Tencent Cloud VOD is optional.
![Create Task Flow - Video Audit](https://main.qcloudimg.com/raw/7daa1c7979d0884ea799101cde7efd09.png)


