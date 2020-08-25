
You can create templates to [set task flows](https://console.cloud.tencent.com/vod/video-process/taskflow) for video processing tasks such as transcoding, watermarking, screencapturing, and auditing videos.


## Preset Task Flow
VOD provides a preset task flow which includes adaptive bitrate streaming, screencapturing (image sprite generating), and cover image generating tasks. The detailed parameters are as follows:

- Task Flow Name: user-defined task flow name.
- Task Flow Type: preset or custom.
- Creation Time: creation time of task flow.
- Last Modified Time: last modified time of task flow.
- Operation: tasks added in task flow.

## Custom Task Flow
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/video-process/taskflow), click **Create Task Flow** above the list to enter the "Create Task Flow" page, and set the following **task flow template** configuration items:
	- Task Flow Name: it is customizable and can contain up to 20 letters, digits, hyphens (-), and underscores (\_).
	- Task Type: its options include general transcoding, TESHD transcoding, adaptive bitrate streaming, screencapturing, cover generating, animated image generating, and video audit. You must select at least one type before you can configure the task flow template. For more information, please see [Task configuration](#p1).
2. After the configuration items are set, click **Submit** to create the task flow.

<span id = "p1"></span>**Task configuration**

Task Type | Support for Preset or Custom Templates | Supported Templates
-|-|-
 General transcoding | Transcoding template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Transcoding template: select one from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates do not meet your needs, select [Template Settings > Transcoding Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template. <br><li>Watermark template: watermarks can be added to a transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.
  TESHD Transcoding | Transcoding template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Transcoding template: select one from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates do not meet your needs, select [Template Settings > Transcoding Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template. <br><li>Watermark template: watermarks can be added to a transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.
  Adaptive bitrate streaming | Adaptive bitrate streaming template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Adaptive bitrate streaming template: select one from the list of preset templates. One or more templates can be added to each task configuration.<br><li>Watermark template: all adaptive bitrate streaming templates support watermarking. If the existing templates do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.	
 Screencapturing | Screencapturing template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Screencapturing template: there are three types of screenshots, namely, point-in-time screenshot, sampled screenshot, and image sprite screenshot. For each screenshot type, you can only select a configured template in the corresponding type. **For time point screencapturing, you need to configure the time points.** If the existing templates do not meet your needs, select [Template Settings > Screencapturing Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template. <br><li>Watermark template: up to four watermarks can be added to a transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.
 Cover generating | Screencapturing template: <li>Preset templates are supported<br><li>Custom templates are supported|<li>Screencapturing template: **only point-in-time screencapturing templates are supported.** For sampled screencapturing, you can select time offset or percent. If the existing templates do not meet your needs, select [Template Settings > Screencapturing Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.<br><li>Watermark template: up to four watermarks can be added to one transcoding template. If the existing templates do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.
Animated image generating | Animated image generating template: <li>Preset templates are supported <br><li>Custom templates are supported | Animated image generating template: you can add multiple animated image generating templates and **configure the time period for animated image generating**. If the existing templates do not meet your needs, select [Template Settings > Animated Image Generating Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.
Video audit | Audit template: <li>Preset templates are supported<br><li>Custom templates are supported | Audit template: you can add only one audit template. If the existing templates do not meet your needs, select [Template Settings > Audit Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.

>?A task flow only supports selecting the configured templates.
