You can create templates to set task flows for video processing to handle tasks such as transcoding, screen capture, watermarks and auditing. 

Log in to the [VOD console](https://console.cloud.tencent.com/video) and click **Video Processing** > **Task Flow Settings** in the left sidebar to see the list of task flows:
1. The task flow list displays the names and IDs of the tasks, and you can sort the tasks by created or modified time. To view, edit, or delete a specified task flow, see the column **Actions**.
2. To create a task flow template, click **Create Task Flow**.

![Task Flow](https://main.qcloudimg.com/raw/a47ba19d0719ea474a640790b2a8b26d.png)

You can create and name a task flow template and select the configurable tasks. You need to select a least one task from transcoding, screen capture, thumbnail downloading, animated image generating, and video auditing to create a task flow.
![Create Task Flow](https://main.qcloudimg.com/raw/f1a66053364891b0f283c13e9364bb73.png)
Click **Submit** to create a task flow. The system will notify you once the task flow is created successfully, and you will see the task flow in the task flow list. 

## Transcoding Task Configuration

You can configure a transcoding task by selecting "Transcoding Task".
![Create Task Flow - Transcoding](https://main.qcloudimg.com/raw/91912e7700e005c31758aeedf194381c.png)
You can select and configure transcoding templates and add a watermark template to create the task flow. Please note that you can only select configured templates.

- Transcoding template: Select from the created templates. You can select one or more transcoding templates for each task. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Transcoding template". To view the new templates, click "Refresh".
- Watermark template: Up to 4 watermarks can be added to each template. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Watermark template". To view the new templates, click "Refresh".

## Screen Capture Task Configuration

You can configure a screen capture task by selecting "Screen Capture Task".
![Create Task Flow - Screencapturing](https://main.qcloudimg.com/raw/bae5e7848a2b8799393790cbbec48c3c.png)
You can select and configure screen capture templates and add a watermark template to create the task flow. Please note that you can only select the configured templates.

- Screenshot template: There are three types of screenshots: point-in-time screenshot, sampling screenshot, and image sprite screenshot. You need to select the corresponding template for each type of screenshot. You need to select the time points for point-in-time screenshots. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Screenshot template". To view the new templates, click "Refresh".
- Watermark template: Up to 4 watermarks can be added to each template. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Watermark template". To view the new templates, click "Refresh".

## Video Thumbnail Downloading Task Configuration

You can configure a video thumbnail downloading task by selecting "Video Thumbnail Downloading Task".
![Create Task Flow - Cover Creating](https://main.qcloudimg.com/raw/52f13aa3c546f9931cf9eeb085a0ef6e.png)
You can select and configure video thumbnail downloading templates and add a watermark template to create the task flow. Please note that you can only select the configured templates.

- Video thumbnail downloading template: Only point-in-time screenshot templates are supported. You can set the sampling time point in terms of time offset or percentage of total time span. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Screenshot template". To view the new templates, click "Refresh".
- Watermark template: Up to 4 watermarks can be added to each template. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Watermark template". To view the new templates, click "Refresh".

## Animated Image Generating Task Configuration

You can configure an animated image generating task by selecting "Animated Image Generating Task".
![Create Task Flow - animated image generating](https://main.qcloudimg.com/raw/35b391f6394e1f2b4b5fc0f816fef42b.png)
You can select and configure animated image generating templates to create the task flow. Please note that you can only select the configured templates.
- Animated image generating template: You can add multiple templates and update the time period for animated image generating task. If the existing templates do not meet the usage requirements, you can edit the templates via "Template settings - Animated Image Generating template". To view the new templates, click "Refresh".

## Video Auditing Task Configuration

You can configure a video auditing task by selecting "Video Auditing Task". Auditing your content on Tencent Cloud VOD is optional.
![Create Task Flow - Video Audit](https://main.qcloudimg.com/raw/7daa1c7979d0884ea799101cde7efd09.png)


