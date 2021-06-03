Log in to the [MPS console](https://console.cloud.tencent.com/mps) and click **Template Settings** on the left sidebar. Preset templates in the console include video transcoding, audio transcoding, watermark, screenshot, animated image, and moderation templates. They can be added to a workflow for on-cloud transcoding and audio/video processing.
![](https://main.qcloudimg.com/raw/6c136af8417cbf963d0c75ff50613c2e.png)
>?
>- If a template added to a workflow is edited after the workflow is enabled, the template parameters after editing will be used.
>- If a template added to a workflow is deleted after the workflow is enabled, the task of the template will fail.
## Video Transcoding Template
MPS provides preset video transcoding templates, which can be used in workflows. You can also click **Create Template** to customize your own video transcoding templates.
- Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Container format: MP4, FLV, or HLS
- Configuration item: video parameters and audio parameters
- Video encoding standard: H.264 or H.265
- Video bitrate (kbps): 0 or 128-35000. `0` indicates that the original bitrate is used.
- Video resolution (px): 0 or 128-4096. `0` indicates that the original resolution is used.
- Video frame rate (FPS): 0-60
- Audio encoding standard: AAC or MP3
- Sampling rate (Hz): 32000, 44100, or 48000
- Audio bitrate (kbps): 0 or 26-256. `0` indicates that the original bitrate is used.
- Audio channel: mono-channel or dual-channel

Templates created are displayed in the template list. You can view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.

>? For the container formats MP4, FLV, and HLS, video parameters are required, and audio parameters optional.

#### List of preset templates

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Container Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Bitrate</th><th colspan="1">Frame Rate</th><th colspan="1">Codec</th><th colspan="1">Bitrate</th><th colspan="1">Sample Rate</th><th colspan="1">Sound Channels</th><th colspan="1">Codec</th></tr>
<tr><td colspan="1" rowspan="2">Smooth</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x  360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64 kbps</td><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">Stereo</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 540</td><td colspan="1" rowspan="2">1,000 kbps</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 720</td><td colspan="1" rowspan="2">1,800 kbps</td><td colspan="1" rowspan="4">128 kbps</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 1080</td><td colspan="1" rowspan="2">2,500 kbps</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 1440</td><td colspan="1" rowspan="2">3,000 kbps</td><td colspan="1" rowspan="4">160 kbps</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 2160</td><td colspan="1" rowspan="2">6,000 kbps</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

## TESHD Template
MPS provides preset templates for Tencent Extreme Speed High Definition (TESHD), which can be used in workflows. You can also click **Create Template** to customize your own TESHD templates.

- Template name: up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.)
- Container format: MP4, FLV, or HLS
- Configuration items: video parameters (required) and audio parameters (optional)
- Video encoding standard: H.264 or H.265
- Average bitrate limit: if this parameter is left empty or set to `0`, it means no upper limit is set for the bitrate.
- Video resolution (px): 0 or 128-4096. `0` indicates that the original resolution is used.
- Video frame rate (FPS): 0-60. `0` indicates the original frame rate is used.
- Audio encoding standard: AAC or MP3
- Audio sample rate (Hz): 32000, 44100, or 48000
- Audio bitrate (kbps): 0 or 26-256. `0` indicates that the original bitrate is used.
- Audio channel: mono-channel or dual-channel

>?
> - You can view **preset** TESHD templates in [MPS console > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=tehd).
> - For the container formats MP4, FLV, and HLS, video parameters are required.

Templates created are displayed in the template list. You can filter, view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.




## Audio Transcoding Template
MPS provides preset audio transcoding templates, which can be used in workflows. You can also click **Create Template** to customize your own audio transcoding templates.
 
- Template name: up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.)
- Container format: MP3, FLAC, OGG, or M4A.
- Audio encoding standard: MP3 if the container format is MP3; FLAC if the container format is FLAC or OGG; MP3, AAC, or AC3 if the container format is M4A
- Sampling rate (Hz): 32000, 44100, or 48000
- Audio bitrate (kbps): 0 or 26-256. `0` indicates that the original bitrate is used.
- Audio channel: mono-channel or dual-channel

Templates created are displayed in the template list. You can view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.

#### List of preset templates
 
<table>
    <tr>
        <th rowspan=1>
            Template ID                
        </th>
        <th rowspan=1>
            Container Format
        </th>
        <th>
            Bitrate
        </th>
        <th>
            Codec
        </th>
        <th>
            Audio Channels
        </th>
        <th>
            Sample Rate
        </th>
    </tr>
 <tr>
        </td>
            1100
        </td>
        </td>
            M4A
        </td>
        </td>
            24 kbps
        </td>
        </td>
            AAC
        </td>
        </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
 <tr>
        </td>
            1110
        </td>
        </td>
            M4A
        </td>
        </td>
            48 kbps
        </td>
        </td>
            AAC
        </td>
        </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
    <tr>
        </td>
            1120
        </td>
        </td>
            M4A
        </td>
        </td>
            96 kbps
        </td>
        </td>
            AAC
        </td>
       </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
     <tr>
        </td>
            1130
        </td>
        </td>
            M4A
        </td>
        </td>
            192 kbps
        </td>
        </td>
            AAC
        </td>
       </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
    <tr>
        </td>
            1140
        </td>
        </td>
            M4A
        </td>
        </td>
            256 kbps
        </td>
        </td>
            AAC
        </td>
       </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
    <tr>
        </td>
            1010
        </td>
        </td>
            MP3
        </td>
        </td>
            128 kbps
        </td>
        </td>
            MP3
        </td>
       </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
    <tr>
        </td>
            1020
        </td>
        </td>
            MP3
        </td>
        </td>
            320 kbps
        </td>
        </td>
            MP3
        </td>
       </td>
            Dual-channel
        </td>
                </td>
            44100 Hz
        </td>
    </tr>
</table>

## Watermark Template
MPS does not provide preset watermark templates. You can click **Create Template** to customize watermark templates.
 
- Template name: up to 64 Chinese characters, letters, digits, underscores (_), dashes (-), and periods (.)
- Watermark type: image watermark
- Image: PNG and JPG images are supported. For better visual experience, transparent images in PNG format are recommended. The image cannot exceed 200 KB in size or 200 x 200 px in dimensions.
- Reference position: upper left (default), upper right, lower left, lower right, based on which you can change the position of the watermark image by adjusting the vertical and horizontal offset
- Vertical offset: the percentage represents the ratio of the vertical distance between the watermark and reference position to the height of the video, which is used to specify the vertical position of the watermark.
- Horizontal offset: the percentage represents the ratio of the horizontal distance between the watermark and reference position to the width of the video, which is used to specify the horizontal position of the watermark.
- Image dimension: you can choose to resize the watermark by percentage (%) or pixel (px).

The watermark templates created are displayed in the template list, which displays watermark previews and information including template name, format, type, position, dimension, etc. You can also view, edit, and delete a template.

 

## Screenshot Template
MPS supports three types of screenshots: time point screenshot, sampled screenshot, and image sprite screenshot. Preset screenshot templates are provided, which can be used in workflows. You can also click **Create Template** to customize your own screenshot templates.

### Time point screenshot
To create a time point screenshot, select time point screenshot for screenshot type. You can set the template name and screenshot dimension when creating a template, but the time point must be set in workflows. For detailed instructions, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).
 
- Template name: up to 64 Chinese characters, letters, digits, underscores (_), dashes (-), and periods (.)
- Image format: JPG
- Image dimension (px): 128-4096

#### List of preset parameter templates

| Template ID | Format | Width | Height | Fill Mode |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Scale to fill                 |

### Sampled Screenshot
Select sampled screenshot for screenshot type.
 
- Template name: up to 64 Chinese characters, letters, digits, underscores (_), dashes (-), and periods (.)
- Image format: JPG
- Image dimension (px): 128-4096
- Interval: the interval can be a percent value (%) or a time value (s). If `%` is selected, the value entered cannot exceed 100.

#### List of preset templates

| Template ID | Format | Width | Height | Interval Measurement | Interval | Fill Mode|
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source            | By percent               | 10%                  | Scale to fill                 |

### Image sprite screenshot
Select image sprite screenshot for screenshot type.

- Template name: up to 64 Chinese characters, letters, digits, underscores (_), dashes (-), and periods (.)
- Image format: JPG
- Image dimension (px): 128-4096
- Interval: the interval can be a percent value (%) or a time value (s). If `%` is selected, the value entered cannot exceed 100.
- Rows: a positive integer. The number of subimage rows multiplied by subimage columns must not exceed 100.
- Columns: a positive integer. The number of subimage rows multiplied by subimage columns must not exceed 100.

The screenshot templates created are displayed in the template list, which displays information including template name, screenshot type, image dimension, and template type. You can also view, edit, and delete a template.

#### List of preset templates

| Template ID | Format | Subimage Width | Subimage Height | Subimage Rows | Subimage Columns | Interval Measurement | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80              | 10               | 10                  | By time             | 10s                 |


 

## Animated Image Generating Template
MPS provides preset animated image generating templates, which can be used in workflows. You can also click **Create Template** to customize your own animated image generating templates.
You can set the image format, frame rate, image dimensions and image quality when creating a template, and the time period for generating animated images when creating workflows. For detailed instructions, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).
 

- Template name: up to 64 letters, digits, and underscores (_)
- Image format: WebP or GIF
- Frame rate (FPS): 1-30
- Image quality: 0-100. The higher the value, the higher the image quality and the more space the image takes up.
- Image dimension (px): 128-4096

The templates created are displayed in the template list, which displays information including template name, image type, frame rate, image quality, image dimensions, and template type. You can view, edit, or delete a custom template, but preset templates can be viewed only, not edited or deleted.

#### List of preset templates

| Template ID | Format | Resolution | Frame Rate |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | x 320                 | 2           |

## Moderation Template

MPS provides preset moderation templates, which can be used in workflows. You can also click **Create Template** to customize your own moderation templates.

- Template name: up to 64 Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.)
- Moderation items: image recognition, speech recognition, or text recognition. The subitems of the selected moderation items will appear in the column on the right.
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >Moderation Item</th>
<th align="center" nowrap="nowrap">Moderation Subitem</th>
<th align="center">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td align="center">Porn</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">Militants, weapons, bloodiness, explosions and fires, terrorist flags, terrorists, police, and crowds</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive figures, banned icons and celebrities</td>
</tr>
<tr>
<td rowspan = 2>Speech recognition</td>
<td align="center">Porn</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive figures, banned icons and celebrities</td>
</tr>
<tr>
<td rowspan = 2>Text recognition</td>
<td align="center">Porn</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Politically sensitive figures, banned icons and celebrities</td>
</tr>
</tbody></table>

For each subitem, you can set a **Confirm Threshold** and a **Suspicion Threshold**, which determine the degree of moderation. If they are left empty, the default values will be used.
 - Confirm threshold: MPS analyzes the videos uploaded and gives them scores. If the score of a video exceeds the confirm threshold, the video will be marked confirmed. The value range of the threshold is 0-100. Unless you have special requirements, we recommend you use the default value.
 - Suspicion threshold: MPS analyzes the videos uploaded and gives them scores. If the score of a video exceeds the suspicion threshold, the video will be marked suspicious. You can initiate human moderation tasks for suspicious videos on the video moderation page. The value range of the threshold is 0-100. Unless you have special requirements, we recommend that you use the default value.
 
 
 >? You can view the **preset** moderation templates in [MPS console > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=audit).


The templates created are displayed in the template list, where you can view, edit, or delete a template.

## Content Analysis Template
MPS provides preset content analysis templates, which can be used in workflows. You can also click **Create Template** to customize your own content analysis templates.

- Template name: up to 64 Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.)
- Content analysis items: **Smart tag**, **Intelligent classification**, **Intelligent cover**, and **Tag by frame**

>? You can view the **preset** content analysis templates in [MPS > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=analysis).


The templates created are displayed in the template list, where you can view, edit, or delete a template.

## Content Recognition Template

MPS provides preset content recognition templates, which can be used in workflows. You can also click **Create Template** to customize your own content recognition templates.

- Template name: up to 64 Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.)
- Content recognition items: **Face recognition**, **Text recognition**, and **Speech recognition**

>?You can view the **preset** content recognition templates in [MPS console > Template Settings](https://console.cloud.tencent.com/mps/templates?tab=recognization).


The templates created are displayed in the template list, where you can view, edit, or delete a template.
