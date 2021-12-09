
You can create templates to set task flows for video processing tasks such as transcoding, watermarking, screencapturing, and recognizing videos.

Log in to the [VOD console](https://console.cloud.tencent.com/vod/video-process/taskflow) and click **Video Processing Settings** > **Task Flow Settings** on the left sidebar to view the task flow list which displays the task flow name, type, creation time, last modified time, and operation information.
- Task Flow Name: user-defined task flow name.
- Task Flow Type: preset or custom.
- Creation Time: creation time of task flow.
- Last Modified Time: last modified time of task flow.
- Operation: tasks added in task flow.

## Preset Task Flow
VOD provides 2 preset task flows which include adaptive bitrate streaming, screencapturing (image sprite generating), and cover image generating tasks. The detailed parameters are as follows:

<table>
   <tr>
        <th>Task Flow Name</td>
        <th>Task Type</td>
        <th>Task Template/ID</td>
    </tr>
    <tr>
        <td rowspan=3>LongVideoPreset</td>
        <td>Adaptive bitrate streaming</td>
        <td>Adpative-HLS(10)</td>
    </tr>
    <tr>
        <td>Screencapture</td>
        <td>SpriteScreenshot(10)</td>
    </tr>
    <tr>
        <td>Cover image generating</td>
        <td>TimepointScreenshot(10)</td>
    </tr>
    <tr>
        <td rowspan=3>SimpleAesEncryptPreset</td>
        <td>Adaptive bitrate streaming</td>
        <td>Adpative-HLS-Encrypt(12)</td>
    </tr>
    <tr>
        <td>Screencapture</td>
        <td>SpriteScreenshot(10)</td>
    </tr>
    <tr>
        <td>Cover image generating</td>
        <td>TimepointScreenshot(10)</td>
    </tr>
</table>



## Custom Task Flow
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod/video-process/taskflow), click **Create Task Flow** above the list to enter the "Create Task Flow" page, and set the following **task flow template** configuration items:
	- Task Flow Name: it is customizable and can contain up to 20 letters, digits, hyphens (-), and underscores (\_).
	- Task Type: options include general transcoding, TESHD transcoding, adaptive bitrate streaming, screencapture, thumbnail generating, animated image generating, and video moderation. You must select at least one type before you can configure the task flow template. For more information, please see [Task Flow Settings
](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow).
2. After the configuration items are set, click **Submit** to create the task flow.

<span id = "p1"></span>**Task configuration**

|Task Type | Support for Preset or Custom Templates | Supported Templates|
|-|-|-|
|General transcoding | Transcoding template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Transcoding template: select one from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates do not meet your needs, select [Template Settings > Transcoding Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template. <br><li>Watermark template: watermarks can be added to a transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|
|TESHD transcoding | Transcoding template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Transcoding template: select one from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates do not meet your needs, select [Template Settings > Transcoding Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template. <br><li>Watermark template: watermarks can be added to a transcoding template. If the existing watermarks do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|
|Remuxing |Remuxing template: preset templates are supported.	  |Remuxing template: select among preset templates. Do not select one template repeatedly.|
|Adaptive bitrate streaming | Adaptive bitrate streaming template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Adaptive bitrate streaming template: select one from the list of preset templates. One or more templates can be added to each task configuration.<br><li>Watermark template: all adaptive bitrate streaming templates support watermark. If the existing templates do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|	
|Screencapture | Screencapture template: <li>Preset templates are supported <br><li>Custom templates are supported |<li>Screencapture template: there are three types of screenshots: time point screenshot, sampled screenshot, and image sprite screenshot. For each screenshot type, you can only select a corresponding configured template. **For time point screencapture, you need to configure the time points.** If the existing templates do not meet your needs, select [Template Settings > Screencapture Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template. <br><li>Watermark template: only time point screenshot and sampled screenshot templates support adding watermark. If the existing watermarks do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|
|Cover generating | Screencapture template: <li>Preset templates are supported<br><li>Custom templates are supported|<li>Screencapture template: **only time point screencapture templates are supported.**. You can use time offset or percentage to decide the time points. If the existing templates do not meet your needs, select [Template Settings > Screencapture Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.<br><li>Watermark template: each screencapture template supports adding watermark. If the existing templates do not meet your needs, select [Template Settings > Watermark Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|
|Animated image generating | Animated image generating template: <li>Preset templates are supported <br><li>Custom templates are supported | Animated image generating template: you can add multiple animated image generating templates and **configure the time period for animated image generating**. If the existing templates do not meet your needs, select [Template Settings > Animated Image Generating Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|
|Intelligent video recognition | Intelligent recognition template: <li>Preset templates are supported<br><li>Custom templates are supported | Intelligent recognition template: you can add only one intelligent recognition template. If the existing templates do not meet your needs, select [Template Settings > Intelligent Recognition Template](https://intl.cloud.tencent.com/document/product/266/14059) to create a custom template.|

>?A task flow only supports the configured templates.
