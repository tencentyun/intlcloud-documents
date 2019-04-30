Task flow settings can be used to transcode, screencapture, watermark, or ausit a video based on the created templates in a routine manner.

Log in to the [VOD console](https://console.cloud.tencent.com/video) and click **Video Processing** > **Task Flow Settings** in the left navigation pane to go to the task flow list page:
1. The task flow list displays the task names and task flow IDs, which can be sorted by created time or modified time. Click a button in the **Operation** column to view, edit, or delete the specified task flow.
2. Click **Create Task Flow** in the upper left corner to add a task flow template.

![Task Flow](https://main.qcloudimg.com/raw/a47ba19d0719ea474a640790b2a8b26d.png)

Within the task flow template, you can customize the task flow name and select a configuration item, including five options, i.e., transcoding task, screencapturing task, cover creating task, animated image generating task, and video audit. In order to configure a task flow, you have to select at least one configuration item.
![Create Task Flow](https://main.qcloudimg.com/raw/f1a66053364891b0f283c13e9364bb73.png)
Click **Submit** after the configuration item is completed. The information about the task flow will be displayed in the task flow list, and the system will prompt that the task flow is created successfully.

## Transcoding Task Configuration

You can configure a transcoding task by clicking "Transcoding task" in the configuration item.
![Create Task Flow - Transcoding](https://main.qcloudimg.com/raw/91912e7700e005c31758aeedf194381c.png)
The transcoding rule can configure the transcoding template and watermarking template, while the task flow only supports selecting the configured templates.

- Transcoding template: Select from the list of created templates. Each task configuration supports adding one or more transcoding templates. If the existing templates do not meet the usage requirements, click "Template settings - Transcoding template" to go to the template settings. After a template is created, click "Refresh" to view the newly added template.
- Watermarking template: Each transcoding template supports adding up to four watermarks. If the existing watermarks do not meet the usage requirements, click "Template Settings - Watermarking Template" to go to the watermark settings. After a template is created, click "Refresh" to view the newly added template.

## Screencapturing Task Configuration

You can configure a screencapturing task by clicking "Screencapturing task" in the configuration item.
![Create Task Flow - Screencapturing](https://main.qcloudimg.com/raw/bae5e7848a2b8799393790cbbec48c3c.png)
The screencapturing rule can configure the screencapturing template and watermarking template, while the task flow only supports selecting the configured templates.

- Screencapturing template: There are three types of screenshots, namely, point-in-time screenshot, sampling screenshot, and sprite screenshot. For each screenshot type, you can only select the configured templates for the corresponding type. For the point-in-time screenshot type, you need to select the time point. If the existing templates do not meet the usage requirements, click "Template settings - Screencapturing template" to go to the template settings. After a template is created, click "Refresh" to view the newly added template.
- Watermarking template: Each template supports adding up to four watermarks. If the existing watermarks do not meet the usage requirements, click "Template settings - Watermarking template" to go to the watermark settings. After a template is created, click "Refresh" to view the newly added template.

## Cover Creating Task Configuration

You can configure a cover creating task by clicking "Task of capturing cover screenshot" in the configuration item.
![Create Task Flow - Cover Creating](https://main.qcloudimg.com/raw/52f13aa3c546f9931cf9eeb085a0ef6e.png)
The cover creating rule can only configure the point-in-time screencapturing template and watermarking template, while the task flow only supports selecting the configured templates.

- Cover creating template: Only point-in-time screencapturing templates are supported. For the sampling time point, you can select time offset or percentage setting. If the existing templates do not meet the usage requirements, click "Template Settings - Screenshot Template" to go to the template settings. After a template is created, click "Refresh" to view the newly added template.
- Watermarking template: Each template supports adding up to four watermarks. If the existing watermarks do not meet the usage requirements, click "Template Settings - Watermarking Template" to go to the watermark settings. After a template is created, click "Refresh" to view the newly added template.

## Dynamic Image Generating Task Configuration

You can configure a dynamic image generating task by clicking "Dynamic Image Task" in the configuration item.
![Create Task Flow - Dynamic Image generating](https://main.qcloudimg.com/raw/35b391f6394e1f2b4b5fc0f816fef42b.png)
The dynamic image generating rule can configure the template, while the task flow only supports selecting the configured templates.

Dynamic image generating template: You can add multiple dynamic image generating templates and reconfigure the time period for dynamic image generating. If the existing templates do not meet the usage requirements, click "Template Settings - Dynamic Image Template" to go to the template settings. After a template is created, click "Refresh" to view the newly added template.

## Video Audit Task Configuration

You can configure a video audit task by clicking "Video Audit" in the configuration item. This feature is the content audit mechanism provided by Tencent Cloud VOD. You can choose whether to enable it on your own.
![Create Task Flow - Video Audit](https://main.qcloudimg.com/raw/7daa1c7979d0884ea799101cde7efd09.png)


