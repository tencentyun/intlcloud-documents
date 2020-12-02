Log in to [VOD Console](https://console.cloud.tencent.com/vod/overview), select **Video Processing** > **Template Setting** on the left sidebar. Then you can see built-in templates including **Video Transcoding**, **TESHD**, **Audio Transcoding **, **Adaptive Bitrate Streaming**, **Watermark**, **Screenshot**, **Dynamic Image*, and **Audit**templates. You add them to task flow for video processing.


## Video Transcoding Template

You can create a video transcoding template and customize it according to your business needs. Select **Video Transcoding** and click **Create Transcoding Template** to enter the custom template configuration page.
+ Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Encapsulation format: MP4, FLV, or HLS
+ Configuration items: video and audio parameters.
+ Video parameters:
	+ Codec: H.264, H.265
	+ Bitrate: 0 or 128-35,000 Kbps
	+ Resolution: the value range of the long side/short side (width/height) of the video is 0 or 128-4096 px
	+ Frame rate: 0-60 fps.
+ Audio parameters:
	+ Codec: AAC, MP3
	+ Sample rate: three default sampling rates, i.e., 32000 Hz, 44100 Hz or 48000 Hz.
	+ Audio bitrate: 0 or 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common Template: specify whether to set it as a frequently used template.

The created template will be displayed in the template list, where you can view, edit, or delete the template, or set it as a frequently used template.

#### List of preset templates

<table>
    <tr>
        <th rowspan=2>
            Video Type                
        </th>
        <th rowspan=2>
            Template ID                
        </th>
        <th rowspan=2>
            Format
        </th>
        <th colspan=4>    
            Video Parameters
        </th>
        <th colspan=1>    
            Audio Parameter
        </th>
    </tr>
    <tr>
        <th>
            Resolution
        </th>
        <th>
            Bitrate
        </th>
        <th>
            FPS
        </th>
        <th>
            Codec
        </th>
        <th>
            Codec
        </th>
    </tr>
    <tr>
        <td rowspan=6>
            FLU
        </td>
        <td>
            10
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (320) x long side (proportionally scaled) of the screen
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            510
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (240) of the screen
        </td>
        <td>
            250 Kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            210
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (320) x long side (proportionally scaled) of the screen
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            610
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (240) of the screen
        </td>
        <td>
            250 Kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10046
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (320) x long side (proportionally scaled) of the screen
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            710
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (240) of the screen
        </td>
        <td>
            250 Kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            SD
        </td>
        <td>
            20
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (640) x long side (proportionally scaled) of the screen
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            520
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (480) of the screen
        </td>
        <td>
            600 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            220
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (640) x long side (proportionally scaled) of the screen
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            620
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (480) of the screen
        </td>
        <td>
            600 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10047
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (640) x long side (proportionally scaled) of the screen
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            720
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (480) of the screen
        </td>
        <td>
            600 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            HD
        </td>
        <td>
            30
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (1280) x long side (proportionally scaled) of the screen
        </td>
        <td>
            1,024 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            530
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (720) of the screen
        </td>
        <td>
            800 Kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            230
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (1280) x long side (proportionally scaled) of the screen
        </td>
        <td>
            1,024 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            630
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (720) of the screen
        </td>
        <td>
            800 Kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10048
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (1280) x long side (proportionally scaled) of the screen
        </td>
        <td>
            1,024 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            730
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (720) of the screen
        </td>
        <td>
            800 Kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            FHD
        </td>
        <td>
            40
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (1920) x long side (proportionally scaled) of the screen
        </td>
        <td>
            2,500 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            540
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (1080) of the screen
        </td>
        <td>
            1,400 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            240
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (1920) x long side (proportionally scaled) of the screen
        </td>
        <td>
            2,500 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            640
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (1080) of the screen
        </td>
        <td>
            1,400 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10049
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (1920) x long side (proportionally scaled) of the screen
        </td>
        <td>
            2,500 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            740
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (1080) of the screen
        </td>
        <td>
            1,400 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            2K
        </td>
        <td>
            70
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (1440) of the screen
        </td>
        <td>
            3,072 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            570
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (1440) of the screen
        </td>
        <td>
            2,048 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            270
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (1440) of the screen
        </td>
        <td>
            3,072 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            670
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (1440) of the screen
        </td>
        <td>
            2,048 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            370
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (1440) of the screen
        </td>
        <td>
            3,072 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            770
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (1440) of the screen
        </td>
        <td>
            2,048 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            4K
        </td>
        <td>
            80
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (2160) of the screen
        </td>
        <td>
            6,144 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            580
        </td>
        <td>
            MP4
        </td>
        <td>
            Short side (proportionally scaled) x long side (2160) of the screen
        </td>
        <td>
            4,096 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            280
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (2160) of the screen
        </td>
        <td>
            6,144 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            680
        </td>
        <td>
            HLS
        </td>
        <td>
            Short side (proportionally scaled) x long side (2160) of the screen
        </td>
        <td>
            4,096 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            380
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (2160) of the screen
        </td>
        <td>
            6,144 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            780
        </td>
        <td>
            FLV
        </td>
        <td>
            Short side (proportionally scaled) x long side (2160) of the screen
        </td>
        <td>
            4,096 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
</table>

## TESHD Template

You can create a TESHD template and customize it according to your business needs. Select **TESHD** and click **Create Transcoding Template** to enter the custom template configuration page.
+ Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Encapsulation Format: MP4
+ Configuration items: video and audio parameters.
+ Video parameters:
	+ Codec: H.264
	+ Average bitrate upper limit: if this parameter is left empty or 0 is entered, there will be no upper limit for bitrate
	+ Resolution: the value range of the long side/short side (width/height) of the video is 0 or 128-4096 px
	+ Frame rate: 0-60 fps
+ Audio parameters:
	+ Codec: AAC, MP3
	+ Sample rate: three default sampling rates, i.e., 32000 Hz, 44100 Hz or 48000 Hz.
	+ Audio bitrate: 0 or 26–256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: specify whether to set it as a frequently used template.

The created template will be displayed in the template list, where you can view, edit, or delete the template, or set it as a frequently used template.
>?You can view [Preset TESHD Templates](https://console.cloud.tencent.com/vod/video-process/template/tehd) on VOD Console.


## <a id="yp"></a>Audio Transcoding Template


You can create an audio transcoding template and customize it according to your business needs. Select **Audio Transcoding** and click **Create Audio Template** to enter the custom template configuration page.

+ Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Encapsulation Format: MP3, FLAC, OGG, or M4A.
+ Audio parameters:
	- Audio codec: MP3 (when the container format is MP3); FLAC (when the container format is FLAC or OGG); MP3, AAC, or AC3 (when the container format is M4A).
	+ Sample rate: Three default sampling rates, i.e., 32000 Hz, 44100 Hz or 48000 Hz.
	+ Audio bitrate: 0 or 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel
+ Common template: specify whether to set it as a frequently used template

The created template will be displayed in the template list. You can view, edit, or delete the template, or set it as a common template.

#### List of preset templates

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
            44100 Hz
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
            44100 Hz
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
            44100 Hz
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
            44100 Hz
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
            44100 Hz
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
            44100 Hz
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
            44100 Hz
        </td>
    </tr>
</table>

## Adaptive Bitrate Streaming Template

You can use the preset adaptive bitrate streaming template or create custom templates.
+ **Basic Info**
	+ Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
	+ Encapsulation Format: HLS
	+ Encryption: no encryption or SimpleAES
	+ Transcoding a low-resolution video to a high-resolution one: enable or disable
+ **Substream info**
	+ Video codec: H.264 or H.265.
	+ Video bitrate: 0 or 128–35,000 Kbps
	+ Video bitrate: value range of the short/long side of the video is 0 or 128-4,096 px
	+ Video frame rate: 0-60 fps
	+ Audio codec: AAC or MP3.
	+ Audio sampling rate: 32000 Hz, 44100 Hz and 48000 Hz
	+ Audio bitrate: 0 or 26-256 Kbps
	+ Sound channel: mono-channel or dual-channel

The created template will be displayed in the template list. You can view, edit, or delete the template.
>?
>- You need add at least one piece of substream information when creating a template.
>- You can view [Preset Adaptive Bitrate Streaming Templates](https://console.cloud.tencent.com/vod/video-process/template/ads) on VOD Console.

## Watermark Template

You can upload images to create a watermark template, set watermark settings and location of the watermark in the video.

+ Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
+ Watermark type: image watermark.
+ Watermark image: PNG and APNG images are supported. We recommend you use transparent images in PNG format for best results. The image is up to 200 KB in size and 200 x 200 in dimensions.
+ Watermark location: top-left corner by default. You can also choose bottom-left, top-right or bottom-right corner.
+ Horizontal offset: the horizontal offset percentage is the ratio of the horizontal distance between the watermark and the upper left corner to the horizontal width. This is used to set the horizontal location of the watermark.
+ Vertical offset: the vertical offset percentage is the ratio of the vertical distance between the watermark and the upper left corner to the vertical height. This is used to set the vertical location of the watermark.
+ Image size: you can choose to resize the watermark by percentage (%) or pixel (px). If % is selected, the original size will be scaled by percentage. If px is selected, the watermark will be scaled according to the entered values.

In the list of created watermark templates, you can view the name of a watermark template, preview a watermark file, and view the format, type, location, and dimensions of a watermark. You can also view, edit, or delete a watermark template, or set it as the default template.
>?
- For example, if the horizontal offset is 0% and vertical offset is 0%, then the watermark will be on the top-left corner of the video. If the horizontal offset is 90% and the vertical offset is 90%, then the watermark will be on the bottom-right corner of the video.
- Once configured, the watermark will be added on all subsequent videos.


## Screenshot Template
You can create a screenshot template for uploaded videos. VOD Console provides three types of screenshot settings: point-in-time screenshot, sampling screenshot, and image sprite screenshot.

The template name, screenshot type, and image dimensions are displayed in the screenshot template. You can view, edit, or delete the template in the operation column.

### Point-in-time screenshot
Select "Point-in-Time Screenshot" as the screenshot type. **You can only use the template to set the screenshot type. To specify sample timestamps please go to screenshot task configuration.** For more information about the configuration of a point-in-time screenshot, please see [Task Configuration](https://intl.cloud.tencent.com/document/product/266/14058).

- Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Image format: JPG.
- Image size: 0 or 128-4096 px.

#### List of preset templates

| Template ID | Format | Width | Height | FillType |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as the source file          | Same as the source file           | Stretch                 |

### Sampling Screenshot
Select "Sampling Screenshot" as the screenshot type.

- Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Image format: JPG.
- Image size: 0 or 128-4096 px.
- Sample interval: percentage (up to 100%) or duration (s).

#### List of parameters of a preset template

| Template ID | Format | Width | Height | SampleType | Interval | FillType |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | Same as the source file          | Save as the source file            | By percentage               | 10%                  | Stretch                 |



### Image sprite screenshot
Select "Image Sprite Screenshot" as the screenshot type.

- Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Image format: JPG.
- Image size: 0 or 128-4096 px.
- Sampling interval: percentage (up to 100%) or duration (s).
- Row: enter a positive integer. The number of small image rows multiplied by the number of small image columns cannot exceed 100.
- Column: enter a positive integer. the number of small image rows multiplied by the number of small image columns cannot exceed 100.



#### List of preset templates

| Template ID | Format | Width | Height | Rows | Columns | SampleType | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80              | 10               | 10                  | By interval             | 10 s                 |


## Dynamic Image Generating Template
You can create an animated image generating template to take screenshots within the specified time period and generate an animated image. **You can only use the template to set the screenshot type and need to specify time periods for generating animated image in task configuration.** For more information about the configuration of an dynamic image generating task, please see [Task Configuration](https://intl.cloud.tencent.com/document/product/266/14058).

- Image type: WEBP or GIF
- Frame rate: 1-30 fps
- Image quality: 1-100
- Image size: 0-1920 px

#### List of preset templates

| Template ID | Format | Resolution | FPS |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as the source file                 | 2           |
| 20001   | WebP               | Short side (320) x long side (proportionally scaled) of the screen             | 2           |



## Audit Template
You can create a video audit template and customize it. Click **Create Template** to enter the custom template configuration page.

- Template name: enter up to 64 characters. Only Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.) are supported
- Sampling interval: the interval in seconds at which the video is sampled for audit. Default value: 1; minimum value: 0.5
- Audit items: you can select image recognition, speech recognition, and text recognition as audit items. The selected subitems will be displayed in the "Selected" column on the right
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >Audit Item</th>
<th align="center" nowrap="nowrap">Audit Subitem</th>
<th align="center">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td align="center">Pornographic</td>
<td align="center">Including audit subitems of porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">Including audit subitems of militants, weapons and guns, bloody scenes, explosions and fires, terrorist flags, terrorists, police force, and crowds</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Including audit subitems of politically sensitive figures, images that violate rules and regulations, pop stars, and sports celebrities</td>
</tr>
<tr>
<td rowspan = 3>Speech recognition</td>
<td align="center">Pornographic</td>
<td align="center">Recognizing pornographic words in audios </td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Recognizing politically sensitive words in audios</td>
</tr>
<tr>
<td align="center">Illegal</td>
<td align="center">Recognizing abusive, illegal words and words about gambling in audios</td>
</tr>
<tr>
<td rowspan = 4>Text recognition</td>
<td align="center">Pornographic</td>
<td align="center">Recognizing pornographic words in text</td>
</tr>
<tr>
<td align="center">Politically sensitive</td>
<td align="center">Recognizing politically sensitive words in text</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">Recognizing terrorism-related words in text</td>
</tr>
<tr>
<td align="center">Illegal</td>
<td align="center">Recognizing abusive, illegal words and words about gambling in text</td>
</tr>
</tbody></table>

For each audit subitem, you can set a **certainty confidence threshold** and a **suspicion confidence threshold** to adjust the audit criteria. If left empty, the default values in VOD will be used for video audit.
 - Confidence threshold for confirmed cases: VOD scores an uploaded video after auditing it. If the score is above the threshold, VOD will label the audit item as "confirmed". If you have no special requirements, we recommend you use the default value range (0-100).
 - Confidence threshold for suspected cases: VOD scores an uploaded video after auditing it. If the score is above the threshold, VOD will label the audit item as "suspected", and you can initiate manual re-audit on the video audit page. If you have no special requirements, we recommend you use the default value range (0-100).
 
The created template will be displayed in the template list, where you can view, edit, or delete the template.

>?You can view [Preset Audit Templates](https://console.cloud.tencent.com/vod/video-process/template/audit) on VOD Console.
