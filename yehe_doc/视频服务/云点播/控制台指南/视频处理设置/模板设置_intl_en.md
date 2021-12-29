Log in to the [VOD console](https://console.cloud.tencent.com/vod/overview) and select **Video Processing Settings** > **Template Settings** on the left sidebar. Built-in templates there include **video transcoding template**, **TESHD template**, **audio transcoding template**, **adaptive bitrate streaming template**, **watermark template**, **screencapture template**, **animated image generating template**, and **intelligent recognition template**, each of which can be added to a task flow for video processing.


## Video Transcoding Template

You can create a video transcoding template and customize it according to your business needs. Select **Video Transcoding** and click **Create Transcoding Template** to enter the custom template configuration page.
+ Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Container format: MP4, FLV, or HLS
+ Configuration items: video and audio parameters
+ Video parameters:
	+ Codec: H.264, H.265, AOMedia Video1
	+ Video bitrate: 128kbps-35000kbps
	+ Resolution: the value range of the long side/short side (width/height) of the video is 128–4096 px
	+ Frame rate: 1～100fps
+ Audio parameters:
	+ Codec: AAC or MP3
	+ Sampling rate: three default sampling rates, i.e., 32000 Hz, 44100 Hz, and 48000 Hz
	+ Audio bitrate: 26kbps-256kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: specify whether to set it as a common template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.

For details, please see [Preset transcoding templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-transcoding-templates).

## TESHD Template

You can create a TESHD template and customize it according to your business needs. Select **TESHD** and click **Create Transcoding Template** to enter the custom template configuration page.
+ Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Container format: MP4, FLV, HLS
+ Configuration items: video and audio parameters
+ Video parameters:
	+ Codec: H.264, H.265, AOMedia Video1
	+ Average bitrate limit: if it is left empty or 0 is entered, no upper limit is set for video bitrate
	+ Resolution: the value range of the long side/short side (width/height) of the video is 128–4096 px
	+ Frame rate: 1～100fps
+ Audio parameters:
	+ Codec: AAC or MP3
	+ Sampling rate: three default sampling rates, i.e., 32000 Hz, 44100 Hz, and 48000 Hz
	+ Audio bitrate: 26–256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: specify whether to set it as a common template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.
>?You can view the [preset TESHD templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-teshd-templates) in the VOD console.


## <a id="yp"></a>Audio Transcoding Template


You can create an audio transcoding template and customize it according to your business needs. Select **Audio Transcoding** and click **Create Audio Template** to enter the custom template configuration page.

+ Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Container format: MP3, FLAC, OGG, or M4A
+ Audio parameters:
	+ Audio codec: MP3 (when the container format is MP3); FLAC (when the container format is FLAC or OGG); MP3, AAC, or AC3 (when the container format is M4A).
	+ Sampling rate: three default sampling rates, i.e., 32000 Hz, 44100 Hz, and 48000 Hz
	+ Audio bitrate: 26–256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: specify whether to set it as a common template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.

#### List of preset parameter templates

<table>
    <tr>
        <th rowspan=1>
            Template ID                
        </th>
        <th rowspan=1>
            Format
        </th>
        <th>
            Bitrate
        </th>
        <th>
            Codec
        </th>
        <th>
            SoundSystem
        </th>
        <th>
            SampleRate
        </th>
    </tr>
 <tr>
        <td>
            1100
        </td>
        <td>
            M4A
        </td>
        <td>
            24 Kbps
        </td>
        <td>
            AAC
        </td>
        <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            M4A
        </td>
        <td>
            48 Kbps
        </td>
        <td>
            AAC
        </td>
        <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            M4A
        </td>
        <td>
            96 Kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            M4A
        </td>
        <td>
            192 Kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            M4A
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1010
        </td>
        <td>
            MP3
        </td>
        <td>
            128 Kbps
        </td>
        <td>
            MP3
        </td>
       <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1020
        </td>
        <td>
            MP3
        </td>
        <td>
            320 Kbps
        </td>
        <td>
            MP3
        </td>
       <td>
            Stereo
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
</table>

## Adaptive Bitrate Streaming Template

You can use the preset adaptive bitrate streaming template or create custom templates according to your business needs.
+ **Basic info**
	+ Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
	+ Muxing Format: HLS, MPEG-DASH
	+ Encryption: no encryption or SimpleAES
	+ Switch from Low Resolution to High Resolution: enable or disable
+ **Substream info**
	+ Video codec: H.264 or H.265.
	+ Video bitrate: 128–35,000 Kbps
	+ Video resolution: the value range of the short/long side of the video is 128–4,096 px
	+ Video frame rate: 1-100fps
	+ Audio codec: AAC or MP3
	+ Audio sampling rate: 32,000 Hz, 44,100 Hz, or 48,000 Hz
	+ Audio bitrate: 26–256 Kbps
	+ Sound channel: mono-channel or dual-channel

The created template will be displayed in the template list. You can view, edit, or delete the template.
>?
>- You need to add the information of at least one substream when creating a template.
>- You can view the [preset adaptive bitrate streaming templates](https://intl.cloud.tencent.com/document/product/266/33932#preset-adaptive-bitrate-streaming-templates) in the VOD console.

## Watermark Template

You can create a watermark template by uploading images according to your business needs and customize the watermark configuration and its location in the video.

+ Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Watermark type: image watermark
+ Watermark image: PNG and APNG images are supported. We recommend you use transparent images in PNG format for best results. The image is up to 200 KB in size and 200x200 px in dimensions.
+ Watermark location: top-left corner by default. You can also choose bottom-left, top-right, or bottom-right corner.
+ Horizontal offset: the horizontal offset percentage is the ratio of the horizontal distance between the watermark and the top-left corner to the horizontal width. This is used to set the horizontal location of the watermark.
+ Vertical offset: the vertical offset percentage is the ratio of the vertical distance between the watermark and the top-left corner to the vertical height. This is used to set the vertical location of the watermark.
+ Watermark size: you can choose to resize the watermark by percentage (%) or pixel (px). If % is selected, the original size will be scaled by percentage. If px is selected, the watermark will be scaled according to the enter values.

In the management list of created watermark templates, you can view the name of a watermark template, preview a watermark file, and view the format, type, position, and size of a watermark. You can also view, edit, or delete a watermark template, or set it as the default template.
>?For example, if the horizontal offset is 0% and vertical offset is 0%, then the watermark will be in the top-left corner of the video. If the horizontal offset is 90% and the vertical offset is 90%, then the watermark will be in the bottom-right corner of the video.


## Screencapture Template
You can create a screencapture template according to your business needs for uploaded videos. Currently, the VOD console supports three types of screenshots: time point screenshot, sampled screenshot, and image sprite screenshot.

The template name, screenshot type, and image dimensions are displayed in the screencapture template. You can view, edit, or delete the template in the **Operation** column.

### Time point screenshot
Select **Time Point Screenshot** as the screenshot type. **You can only use the template to set the screenshot type. To specify sample timestamps, please go to screenshot task configuration.** For more information on the configuration of a time point screencapture task, please see [Task Configuration](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow).

- Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Image format: JPG
- Image dimensions: 128–4,096 px

#### List of preset parameter templates

| Template ID | Format | Width | Height | FillType |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

### Sampled screenshot
Select **Sampled Screenshot** as the screenshot type.

- Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Image format: JPG
- Image dimensions: 128–4,096 px
- Sample interval: percentage (up to 100%) or duration (s).

#### List of preset parameter templates

| Template ID | Format | Width | Height | SampleType | Interval | FillType |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG    | Same as source   | Same as source     | By percent  | 10%   | Stretch     |



### Image sprite screenshot
Select **Image Sprite Screenshot** as the screenshot type.

- Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Image format: JPG
- Image dimensions: 128–4,096 px
- Sample interval: percentage (up to 100%) or duration (s).
- Rows: enter a positive integer. The number of subimage rows multiplied by the number of subimage columns cannot exceed 100.
- Columns: enter a positive integer. the number of subimage rows multiplied by the number of subimage columns cannot exceed 100.



#### List of preset parameter templates

| Template ID | Format | Width | Height | Rows | Columns | SampleType | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80              | 10               | 10                  | By interval             | 10s                 |


## Animated Image Generating Template
You can create an animated image generating template to take screenshots within the specified time period and generate an animated image. **You can only use the template to set the screenshot type. To specify time periods for generating animated image, please go to task configuration.** For more information on the configuration of an animated image generating task, please see [Task Configuration](https://intl.cloud.tencent.com/document/product/266/14058#custom-task-flow).

- Image type: WebP or GIF
- Frame rate: 1–30 fps
- Image quality: 1–100
- Image dimensions: 128px-4, 096px

#### List of preset parameter templates

| Template ID | Format | Resolution | FPS |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | 320 * proportionally scaled             | 2           |



## Intelligent Recognition Template
You can create an intelligent video recognition template and customize it according to your business needs. Click **Create Template** to enter the custom template configuration page.

- Template name: enter up to 64 characters. Only letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Sampling interval: it indicates at which interval in seconds the video under intelligent recognition is sampled for check. Default value: 1. Minimum value: 0.5
- Intelligent recognition item: valid values include image recognition, speech recognition, and text recognition. The selected intelligent recognition subitems will appear in the "Selected" column on the right
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >Intelligent Recognition Item</th>
<th align="center" nowrap="nowrap">Intelligent Recognition Subitem</th>
<th align="center">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td align="center">Porn information</td>
<td align="center">Includes intelligent recognition subitems of porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Terrorism information</td>
<td align="center">Includes intelligent recognition subitems of militants, weapons and guns, bloody scenes, police force, and crowd gathering</td>
</tr>
<tr>
<td align="center">Politically sensitive information</td>
<td align="center">Includes intelligent recognition subitems of particular people, icons, and celebrities in sports and the entertainment industry</td>
</tr>
<tr>
<td rowspan = 3>Speech recognition</td>
<td align="center">Porn information</td>
<td align="center">Recognizes porn words in audios</td>
</tr>
<tr>
<td align="center">Politically sensitive information</td>
<td align="center">Recognizes politically sensitive words in audios</td>
</tr>
<tr>
<td align="center">Illegal</td>
<td align="center">Recognizes abusive or illegal words and words about gambling in audios</td>
</tr>
<tr>
<td rowspan = 4>Text recognition</td>
<td align="center">Porn information</td>
<td align="center">Recognizes porn words in text</td>
</tr>
<tr>
<td align="center">Politically sensitive information</td>
<td align="center">Recognizes politically sensitive words in text</td>
</tr>
<tr>
<td align="center">Terrorism information</td>
<td align="center">Recognizes terrorism words in text</td>
</tr>
<tr>
<td align="center">Illegal</td>
<td align="center">Recognizes abusive or illegal words and words about gambling in text</td>
</tr>
</tbody></table>

For each intelligent recognition subitem, you can set a **certainty confidence threshold** and a **suspicion confidence threshold** to adjust the intelligent recognition criteria. If left empty, the default values in VOD will be used for intelligent video recognition.
 - Certainty Confidence Threshold: VOD scores an uploaded video after intelligently recognizing it. If the score is above the threshold, VOD will label the intelligent recognition item as "confirmed". If you have no special requirements, we recommend you use the default value range (0–100).
 - Suspicion Confidence Threshold: VOD scores an uploaded video after intelligently recognizing it. If the score is above the threshold, VOD will label the intelligent recognition item as "suspected", and you can initiate human review on the intelligent video recognition page. If you have no special requirements, we recommend you use the default value range (0–100).
 
The created template will be displayed in the template list. You can view, edit, or delete the template.

>?You can view the [preset intelligent recognition templates](https://intl.cloud.tencent.com/document/product/266/33932#video-ai) in the VOD console.
