1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. By default, you will enter the **Media Assets > Audio/Video Management > Uploaded** page.
4. Select **Video Processing > Template Settings** on the left sidebar to create a **video transcoding template**, **TSC template**, **audio transcoding template**, **remux template**, **adaptive bitrate streaming template**, **watermark template**, **screenshot template**, **animated image template**, or **moderation template**. All templates can be added to video processing workflows.


## Video Transcoding Template

Click **Create Template** under the **Video Transcoding** tab to create a custom video transcoding template.
+ Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
+ Encapsulation format: MP4, FLV, or HLS
+ Configuration items: Video and audio parameters
+ Video parameters:
	+ Codec: H.264 or H.265
	+ Video bitrate: 128-35,000 Kbps
	+ Resolution: Set the long and short sides or width and height of the video. Value range: 128-4096 px.
	+ Frame rate: 1-100 fps
+ Audio parameters:
	+ Codec: AAC or MP3
	+ Sample rate: 32,000 Hz, 44,100 Hz, or 48,000 Hz
	+ Audio bitrate: 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: Whether to mark the template as a common template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.

#### Preset templates
For information about the preset templates, see [Preset transcoding templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-transcoding-templates).

## Top Speed Codec Template

Select the **TSC Template** tab and click **Create a Transcoding Template** to create a custom TSC transcoding template.
+ Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
+ Encapsulation Format: MP4
+ Configuration items: Video and audio parameters
+ Video parameters:
	+ Codec: H.264
	+ Average bitrate limit: If this parameter is left empty or is set to 0, there will be no upper limit for the bitrate.
	+ Resolution: Set the long and short sides or width and height of the video. Value range: 0 or 128-4096 px.
	+ Frame rate: 0-60 fps
+ Audio parameters:
	+ Codec: AAC or MP3
	+ Sample rate: 32,000 Hz, 44,100 Hz, or 48,000 Hz
	+ Audio bitrate: 0 or 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: Whether to mark the template as a common template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.
>? For information about the preset templates, see [Preset TSC templates](https://intl.cloud.tencent.com/document/product/266/33932).


## Audio Transcoding Template[](id:yp)
Select the **Audio Transcoding** tab and click **Create Audio Template** to create a custom audio transcoding template.

+ Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
+ Encapsulation Format: MP3, FLAC, OGG, or M4A.
+ Audio parameters:
	+ Codec: MP3 if the container format is MP3; FLAC if the container format is FLAC or OGG; MP3, AAC, or AC3 if the container format is M4A.
	+ Sample rate: 32,000 Hz, 44,100 Hz, or 48,000 Hz
	+ Audio bitrate: 0 or 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: Whether to mark the template as a common template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.

#### Preset templates
For information about the preset templates, see [Preset transcoding templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-transcoding-templates).


## Adaptive Bitrate Streaming Template

You can use the preset adaptive bitrate streaming template or create custom templates.
+ **Basic Info**
	+ Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
	+ Encapsulation Format: HLS
	+ Encryption type: No encryption or SimpleAES
	+ Transcoding a low-resolution video to a high-resolution one: enable or disable
+ **Substream info**
	+ Video codec: H.264 or H.265
	+ Video bitrate: 0 or 128-35,000 Kbps
	+ Resolution: Set the long and short sides or width and height of the video. Value range: 0 or 128-4096 px.
	+ Frame rate: 0-60 fps
	+ Audio codec: AAC or MP3
	+ Sample rate: 32,000 Hz, 44,100 Hz, or 48,000 Hz
	+ Audio bitrate: 0 or 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel

The templates created are displayed in the template list, where you can view, edit, or delete a template.
>?
>- You need to add at least one substream to create an adaptive bitrate streaming platform.
>- For the preset templates, see [Preset adaptive bitrate streaming templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-adaptive-bitrate-streaming-templates).

## Watermark Template

You can create a custom watermark template to add the watermark you upload to a specific position of the video.

+ Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
+ Watermark type: Image watermark
+ Image: PNG and APNG images are supported. For better visual experience, transparent images in PNG format are recommended. The image cannot exceed 200 KB in size or 200 x 200 px in dimensions.
+ Watermark position: Upper left (default), upper right, lower left, or lower right
+ Horizontal offset: The percentage indicates the ratio of the horizontal distance between the watermark and the origin (top-left corner by default) to the video width.
+ Vertical offset: The percentage indicates the ratio of the vertical distance between the watermark and the origin (top-left corner by default) to the video height.
+ Image size: You can resize the watermark by specifying the width and height in pixels or as a percentage of the original dimensions.

The watermark template list shows information including template name, format, type, position, and size. You can also preview watermarks or click the buttons in the operation column to view, edit, delete, or set a template as the default.
>? If the horizontal offset and vertical offset are both 0%, the watermark will be in the top-left corner of the video. If the horizontal offset and vertical offset are both 99%, the watermark will be in the bottom-right corner of the video.

## Screenshot Template
You can create screenshot templates to take different types of screenshots (time point, sampled, or image sprite) of uploaded videos.

The screenshot template list shows information including template name, screenshot type, and image size. You can click the buttons in the operation column to view details or edit or delete a template.

### Time point screenshot
Select time point screenshot as the screenshot type and **specify the time points to take screenshots in task flow settings.** For detailed directions, see [Task Flow Settings](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow).

- Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
- Image format: JPG
- Image dimension: 0 or 128-4096 px

#### Preset templates
For information about the preset templates, see [Preset time point screenshot templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-time-point-screenshot-templates).

### Sampled screenshot
Select sampled screenshot as the screenshot type.

- Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
- Image format: JPG
- Image dimension: 0 or 128-4096 px
- Sampling interval: Specify the interval as a percentage (up to 100%) of the total video duration, or specify the number of seconds between screenshots.

#### Preset templates
For information about the preset templates, see [Preset sampled screenshot templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-sampled-screenshot-templates).


### Image sprite screenshot
Select image sprite screenshot as the screenshot type.

- Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
- Image format: JPG
- Image dimension: 0 or 128-4096 px
- Sampling interval: Specify the interval as a percentage (up to 100%) of the total video duration, or specify the number of seconds between screenshots.
- Rows: Enter a positive integer. The number of subimage rows multiplied by subimage columns must not exceed 100.
- Columns: Enter a positive integer. The number of subimage rows multiplied by subimage columns must not exceed 100.



#### Preset templates
For information about the preset templates, see [Preset image sprite templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-image-sprite-templates).

## Animated Image Template
You can create an animated image template to take an animated screenshot with a specific duration. **You need to specify the time period for taking the screenshot in task flow settings.** For detailed directions, see [Task Flow Settings](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow).

- Image type: WEBP or GIF
- Frame rate: 1-30 fps
- Image quality: 1-100
- Image dimension: 0-1920 px

#### Preset templates
For information about the preset templates, see [Preset animated image generating templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-animated-image-generating-templates).



## Moderation Template
Select the **Moderation Template** tab and click **Create Template** to create a custom moderation template.

- Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
- Sampling interval: The interval (seconds) at which frames are checked. Default value: 1; minimum value: 0.5.
- Moderation items: You can choose image recognition, speech recognition, and text recognition. Selected items will appear in the "Selected" column on the right.
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >Moderation Item</th>
<th align="center" nowrap="nowrap">Subitem</th>
<th align="center">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td align="center">Eroticism</td>
<td align="center">Porn, vulgar, intimacy, and sexy</td>
</tr>
<tr>
<td align="center">Violence</td>
<td align="center">Militants, weapons, bloody scenes, police force, and crowds</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive people, banned icons, and celebrities (sports and entertainment)</td>
</tr>
<tr>
<td rowspan = 3>Speech recognition</td>
<td align="center">Eroticism</td>
<td align="center">Erotic words in speech</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive words in speech</td>
</tr>
<tr>
<td align="center">Illegal</td>
<td align="center">Abusive, gambling-related, and other illegal content in speech</td>
</tr>
<tr>
<td rowspan = 4>Text recognition</td>
<td align="center">Eroticism</td>
<td align="center">Pornographic words in text</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive words in text</td>
</tr>
<tr>
<td align="center">Violence</td>
<td align="center">Violence-related words in text</td>
</tr>
<tr>
<td align="center">Illegal</td>
<td align="center">Abusive, gambling-related, and other illegal content in text</td>
</tr>
</tbody></table>

For each subitem, you can specify a **certainty confidence threshold** and a **suspicion confidence threshold** to control the strictness of moderation. If you leave them empty, the default values will be used.
 - Certainty confidence threshold: VOD analyzes the videos uploaded and gives them scores. If the certainty score of a video exceeds the certainty confidence threshold, the video will be marked confirmed. The value range of the threshold is 0-100. The default value is recommended.
 - Suspicion confidence threshold: VOD analyzes the videos uploaded and gives them scores. If the suspicion score of a video exceeds the suspicion threshold, the video will be marked suspicious. You can initiate human moderation tasks for suspicious videos on the video moderation page. The value range of the threshold is 0-100. The default value is recommended.

The templates created are displayed in the template list, where you can view, edit, or delete a template.

>? For the preset templates, see [Preset video moderation templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-video-moderation-templates.3Ca-id.3D.22verify.22.3E.3C.2Fa.3E).
