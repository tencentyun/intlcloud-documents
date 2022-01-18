Log in to the [MPS console](https://console.cloud.tencent.com/mps) and click **Template Settings** on the left sidebar. Preset templates in the console include video transcoding, audio transcoding, TESHD, watermark, screenshot, animated image, moderation, content analysis, and content recognition. They can be added to a workflow for on-cloud transcoding and audio/video processing.
![](https://main.qcloudimg.com/raw/a6e034f67575726dbdbcfdb462f7de1d.png)
>?
>- If a template added to a workflow is edited after the workflow is enabled, the template parameters after editing will be used.
>- If a template added to a workflow is deleted after the workflow is enabled, the task of the template will fail.

## Video Transcoding Template
MPS provides preset video transcoding templates, which can be used in workflows. You can also click **Create Template** to customize your own video transcoding templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |
|    Container format    |    MP4, FLV, or HLS    |
|    Configuration items    |    Video and/or audio parameters    |
|    Video codec     |    H.264 or H.265    |
|    Video bitrate (Kbps)    | 0 or 128-35000.`0` means to use the original bitrate. |
|    Video resolution (px)    |    0 or 128-4096. `0` means to use the original resolution or resize the video proportionally.    |
|    Video frame rate (fps)    |    0-60    |
|    Audio codec    |    AAC or MP3    |
|    Audio sample rate (Hz)    |    32000, 44100, or 48000    |
|    Audio bitrate (Kbps)    |    0 or 26-256. `0` means to use the original bitrate.    |
|    Sound channels    |    Mono or stereo    |

Templates created are displayed in the template list. You can view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.

>? If the container format is set to MP4, FLV, or HLS, video parameters are required, and audio parameters optional.

#### List of preset templates

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Bitrate (Kbps)</th><th colspan="1">Frame Rate (fps)</th><th colspan="1">Codec</th><th colspan="1">Bitrate (Kbps)</th><th colspan="1">Sample Rate (Hz)</th><th colspan="1">Sound Channels</th><th colspan="1">Codec</th></tr>
<tr><td colspan="1" rowspan="2">Smooth</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 360</td><td colspan="1" rowspan="2">400</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64</td><td colspan="1" rowspan="12">44100</td><td colspan="1" rowspan="12">Stereo</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 540</td><td colspan="1" rowspan="2">1000</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 720</td><td colspan="1" rowspan="2">1800</td><td colspan="1" rowspan="4">128</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 1080</td><td colspan="1" rowspan="2">2500</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 1440</td><td colspan="1" rowspan="2">3000</td><td colspan="1" rowspan="4">160</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 2160</td><td colspan="1" rowspan="2">6000</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

## TESHD Template
MPS provides preset Tencent Extreme Speed High Definition (TESHD) templates, which can be used in workflows. You can also click **Create Template** to customize your own TESHD templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |
|    Container format    |    MP4, FLV, or HLS    |
|  Configuration items    |  Video parameters (required); audio parameters (optional)    |
|    Video codec     |    H.264 or H.265    |
|  Average bitrate limit    |   If this parameter is left empty or set to `0`, it means no upper limit is set for the bitrate.    |
|  Video resolution (px)    |  0 or 128-4096 for either dimension. `0` means to use the original resolution.    |
|  Frame rate (fps)    |  0-60. `0` means to use the original frame rate.    |
|  Audio codec    |  AAC or MP3    |
|  Audio sample rate (Hz)    |  32000, 44100, or 48000    |
|  Audio bitrate (Kbps)    |  0 or 26-256. `0` means to use the original bitrate.    |
|  Sound channels    |  Mono or stereo    |



>?
> - You can view **preset** TESHD templates in [MPS console > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=tehd).
> - If the container format is set to MP4, FLV, or HLS, video parameters are required.

Templates created are displayed in the template list. You can filter, view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.




## Audio Transcoding Template
MPS provides preset audio transcoding templates, which can be used in workflows. You can also click **Create Template** to customize your own audio transcoding templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |
| Container format   | MP3, FLAC, OGG, or M4A   |
| Audio codec   | The codec must be MP3 if the container format is MP3, FLAC if the container format is FLAC or OGG, and can be MP3, AAC, or AC3 if the container format is M4A.   |
| Audio sample rate (Hz)   | 32000, 44100, or 48000   |
| Audio bitrate (Kbps)   | 0 or 26-256. `0` means to use the original audio bitrate.   |
| Sound channels   | Mono or stereo   |

Templates created are displayed in the template list. You can view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.

#### List of preset templates

| Template ID | Container Format | Audio Bitrate (Kbps) | Codec | Sound Channels | Audio Sample Rate (Hz) |
| :------ | :----------------- | :------------------ | :------------ | :-------------------- | :--------------------- |
| 1100    | M4A                | 24              | AAC           | Stereo      | 44100                |
| 1110    | M4A                | 48              | AAC           | Stereo      | 44100                |
| 1120    | M4A                | 96              | AAC           | Stereo      | 44100                |
| 1130    | M4A                | 192             | AAC           | Stereo      | 44100                |
| 1140    | M4A                | 256             | AAC           | Stereo      | 44100                |
| 1010    | MP3                | 128             | MP3           | Stereo      | 44100                |
| 1020    | MP3                | 320             | MP3           | Stereo      | 44100                |



## Watermark Template
MPS does not provide preset watermark templates. You can click **Create Template** to customize watermark templates.

<table>
<tr><th width=13%>Item</th><th>Description</th></tr>
<tr>
<td>Template Name</td>
<td>Max 64 characters; supports Chinese characters, letters, digits, underscores (\_), hyphens (-), and periods</td>
</tr><tr>
<td>Watermark type</td>
<td>Image watermark</td>
</tr><tr>
<td>Image</td>
<td>PNG or JPG images. For better visual experience, transparent images in PNG format are recommended. The image cannot exceed 200 KB in size or 200 × 200 px in dimensions.</td>
</tr><tr>
<td>Reference position</td>
<td>Upper left (default), upper right, lower left, or lower right, based on which you can change the position of the watermark image by adjusting the vertical and horizontal offset</td>
</tr><tr>
<td>Vertical offset</td>
<td>The percentage represents the ratio of the vertical distance between the watermark and reference position to the height of the video, which is used to specify the vertical position of the watermark.</td>
</tr><tr>
<td>Horizontal offset</td>
<td>The percentage represents the ratio of the horizontal distance between the watermark and reference position to the width of the video, which is used to specify the horizontal position of the watermark.</td>
</tr><tr>
<td>Image dimensions</td>
<td>You can choose to resize the watermark by percentage (%) or pixel (px).</td>
</tr></table>   

The watermark templates created can be found in the template list, which displays watermark previews and information including template name, format, type, position, dimension, etc. You can view, edit, and delete a template.

 

## Screenshot Template
MPS provides preset screenshot templates, which can be used in workflows. Three types of screenshots are supported: time point screenshot, sampled screenshot, and image sprite screenshot. You can also click **Create Template** to customize your own screenshot templates.

### Time point screenshot
To create a time point screenshot, select time point screenshot for screenshot type. You can set the template name and screenshot dimensions when creating a template, but the time point must be set in workflows. For detailed instructions, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).

| Item | Description |
| --- | ----|
| Template name | Max 64 characters; supports Chinese characters, letters, digits, underscores (\_), hyphens, and periods (.) |
| Image format | JPG |
| Image dimensions | The width and height of the image must be in the range of 128-4096 px. |

#### List of preset templates

| Template ID | Format | Width | Height | Fill Mode |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Scale to fill                 |

### Sampled screenshot
Select sampled screenshot for screenshot type.

| Item | Description |
| --- | ----|
| Template name | Max 64 characters; supports Chinese characters, letters, digits, underscores (\_), hyphens (-), and periods |
| Image format | JPG |
| Image dimensions | The width and height of the image must be in the range of 128-4096 px. |
| Sampling interval | The interval can be a percent value (%) or a time value (s). If `%` is selected, the value entered cannot exceed 100. |

#### List of preset templates

| Template ID | Format | Width | Height | Interval Measurement | Interval | Fill Mode|
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source            | By percent               | 10%                  | Scale to fill                 |

### Image sprite screenshot
Select image sprite screenshot for screenshot type.

| Item | Description |
| --- | ----|
| Template name | Max 64 characters; supports Chinese characters, letters, digits, underscores (\_), hyphens, and periods (.) |
| Image format| JPG|
| Image dimensions | The width and height of the image must be in the range of 128-4096 px. |
| Sampling interval | The interval can be a percent value (%) or a time value (s). If `%` is selected, the value entered cannot exceed 100. |
| Rows | A positive integer. The number of subimage rows multiplied by subimage columns must not exceed 100.|
| Columns | A positive integer. The number of subimage rows multiplied by subimage columns must not exceed 100.|

The screenshot templates created can be found in the template list, which displays information including template name, screenshot type, image dimensions, and template type. You can view, edit, and delete a template.

#### List of preset templates

| Template ID | Format | Subimage Width | Subimage Height | Subimage Rows | Subimage Columns | Interval Measurement | Interval (s) |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80              | 10               | 10                  | By time             | 10                 |




## Animated Image Generating Template
MPS provides preset animated image generating templates, which can be used in workflows. You can also click **Create Template** to customize your own animated image generating templates.
You can set the image format, frame rate, image dimensions and image quality when creating a template, and the time period for generating animated images in workflows. For detailed instructions, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).

| Item | Description |
| --- | ----|
| Template name  | Max 64 characters; supports Chinese characters, letters, digits, and underscores (\_) |
| Image format  | WEBP or GIF  |
| Frame rate (fps)  | 1-30  |
| Image quality  | 0-100. The larger the value, the higher the quality and the larger the image size.  |
| Image dimensions (px)  | 0 or 128-4096 for either dimension   |

The templates created can be found in the template list, which displays information including template name, image type, frame rate, image quality, image dimensions, and template type. You can view, edit, or delete a custom template, but preset templates can be viewed only, not edited or deleted.

#### List of preset templates

| Template ID | Format | Resolution | Frame Rate (fps) |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | 320 × Proportionally scaled                 | 2           |

## Moderation Template

MPS provides preset moderation templates, which can be used in workflows. You can also click **Create Template** to customize your own moderation templates.

- Template name: max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.)
- Moderation items: image recognition, speech recognition, or text recognition. The subitems of the selected moderation items will appear in the column on the right.
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
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">Bloodiness, explosion, fire, etc.</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Banned icons, celebrities in sports and the entertainment industry, etc.</td>
</tr>
<tr>
<td rowspan = 2>Speech recognition</td>
<td align="center">Eroticism</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive figures, banned icons, and celebrities (sports and entertainment)</td>
</tr>
<tr>
<td rowspan = 2>Text recognition</td>
<td align="center">Eroticism</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive figures, banned icons, and celebrities (sports and entertainment)</td>
</tr>
</tbody></table>

For each subitem, you can set a **Confirm Threshold** and a **Suspicion Threshold**, which determine the degree of moderation. If they are left empty, the default values will be used.
 - Confirm threshold: MPS analyzes the videos uploaded and gives them scores. If the score of a video exceeds the confirm threshold, the video will be marked confirmed. The value range of the threshold is 0-100. The default value is recommended.
 - Suspicion threshold: MPS analyzes the videos uploaded and gives them scores. If the score of a video exceeds the suspicion threshold, the video will be marked suspicious. You can initiate human moderation tasks for suspicious videos on the video moderation page. The value range of the threshold is 0-100. The default value is recommended.


>? You can view the **preset** moderation templates in [MPS console > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=audit).


The templates created are displayed in the template list, where you can view, edit, or delete a template.

## Content Analysis Template
MPS provides preset content analysis templates, which can be used in workflows. You can also click **Create Template** to customize your own content analysis templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |
| Content Analysis Items  | **Smart Tag**, **Intelligent Classification**, **Intelligent Thumbnail**, **Tag by Frame**  |

>? You can view the **preset** content analysis templates in [MPS > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=analysis).


The templates created are displayed in the template list, where you can view, edit, or delete a template.

## Content Recognition Template

MPS provides preset content recognition templates, which can be used in workflows. You can also click **Create Template** to customize your own content recognition templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |
| Content Recognition Items  | **Face Recognition**, **Text Recognition**, **Speech Recognition**  |

>?You can view the **preset** content recognition templates in [MPS console > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=recognization).


The templates created are displayed in the template list, where you can view, edit, or delete a template.
