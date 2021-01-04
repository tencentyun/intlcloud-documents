You can create templates to set task flows for video processing tasks such as transcoding, watermarking, screencapturing, and moderating videos.

Log in to the VOD console and click **Video Processing** > **[Task Flow Settings](https://console.cloud.tencent.com/vod/video-process/taskflow)** on the left sidebar on the non-admin page to view the task flow list which displays the following information:
- Task Flow Name: user-defined task flow name.
- Task Flow Type: **preset** or **custom**.
- Creation Time: creation time of task flow.
- Last Modified Time: last modified time of task flow.
- Operation: tasks added in task flow.


## Preset Task Flow
VOD provides two preset task flows which include adaptive bitrate streaming, screencapturing (image sprite generating), and cover image generating tasks. The detailed parameters are as follows:

<table><tr>
<th>Task Flow Name</td><th>Task Type</td><th>Task Template/ID</td>
</tr><tr>
	<td rowspan=3>LongVideoPreset</td>
	<td>Adaptive bitrate streaming</td>
	<td>Adpative-HLS(10)</td>
</tr><tr>
	<td>Screencapture</td>
	<td>SpriteScreenshot(10)</td>
</tr><tr>
	<td>Cover image generating</td>
	<td>TimepointScreenshot(10)</td>
</tr><tr>
	<td rowspan=3>SimpleAesEncryptPreset</td>
	<td>Adaptive bitrate streaming</td><td>Adpative-HLS-Encrypt(12)</td>
</tr><tr>
	<td>Screencapture</td>
	<td>SpriteScreenshot(10)</td>
</tr><tr>
	<td>Cover image generating</td>
	<td>TimepointScreenshot(10)</td>
</tr></table>


## Custom Task Flow
### Steps<span id = "customize"></span>
1. Go to **[Task Flow Settings](https://console.cloud.tencent.com/vod/video-process/taskflow)**, click **Create Task Flow** above the list to enter the "Create Task Flow" page, and set the following **task flow template** configuration items:
	- **Task Flow Name:** it is customizable and can contain up to 20 letters, digits, hyphens (-), and underscores (_).
	- **Task Type:** options include general transcoding, TESHD transcoding, adaptive bitrate streaming, screencapturing, cover image generating, animated image generating, and video moderation. You must select at least one type before you can configure the task flow template. For more information, please see [Task configuration](#p1).
2. After the configuration items are set, click **Submit** to create the task flow.

### Task configuration<span id = "cust_des"></span>
<table>
<tr><th>Task Type</th><th width="21%">Support for Preset or <br>Custom Templates</th><th>Supported Templates</th>
</tr><tr>
<td>General transcoding</td>
<td>Transcoding template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><ul style="margin:0">
<li/><b>Transcoding template:</b> select one from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Transcoding Template</a> to create a custom template.
<li/><b>Watermark template:</b> all transcoding templates support watermarking. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Watermark Template</a> to create a custom template.</ul></td>
</tr><tr>
<td>TESHD transcoding</td>
<td>Transcoding template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><ul style="margin:0">
<li/><b>Transcoding template:</b> select one from the list of created templates. One or more transcoding templates can be added to each task configuration. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Transcoding Template</a> to create a custom template.
<li/><b>Watermark template:</b> all transcoding templates support watermarking. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Watermark Template</a> to create a custom template.</ul></td>
</tr><tr>
<td>Adaptive bitrate streaming</td>
<td>Adaptive bitrate streaming template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><ul style="margin:0">
<li/><b>Adaptive bitrate streaming template:</b> select one from the list of created templates. One or more adaptive bitrate streaming templates can be added to each task configuration.
<li/><b>Watermark template:</b> all adaptive bitrate streaming templates support watermarking. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Watermark Template</a> to create a custom template.</ul></td>
</tr><tr>
<td>Screencapture</td>
<td>Screencapture template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><ul style="margin:0">
<li/><b>Screencapture template:</b> there are three types of screenshots, namely, time point screenshot, sampled screenshot, and image sprite screenshot. For each screenshot type, you can only select a configured template in the corresponding type. <b>For time point screencapture, you need to configure the time points</b>. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Screencapture Template</a> to create a custom template.
<li/><b>Watermark template:</b> only the time point screencapture template and the sampled screencapture template support watermarking. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Watermark Template</a> to create a custom template.</ul></td>
</tr><tr>
<td>Cover image generating</td>
<td>Screencapture template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><ul style="margin:0">
<li/><b>Screencapture template:</b><b> only time point screencapture templates are supported. </b>For sampled screencapture, you can select a time offset or percent. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Screencapture Template</a> to create a custom template.
<li/><b>Watermark template:</b> all screencapture templates support watermarking. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Watermark Template</a> to create a custom template.</ul></td>
</tr><tr>
<td>Animated image generating</td>
<td>Animated image generating template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><b>Animated image generating template:</b> you can add multiple animated image generating templates and <b>configure the time period for animated image generating</b>. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Animated Image Generating Template</a> to create a custom template.</td>
</tr><tr>
<td>Video moderation</td>
<td>Moderation template:<li/>Preset templates are supported<li/>Custom templates are supported</td>
<td><b>Moderation template:</b> you can add only one moderation template. If the existing templates don't meet your needs, select <a href="https://intl.cloud.tencent.com/document/product/266/14059">Template Settings > Moderation Template</a> to create a custom template.</td>
</tr></table>

>?A task flow only supports the configured templates.
