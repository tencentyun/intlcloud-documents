Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and select **Video Processing** > **Templates** on the left sidebar. Built-in templates there include **video transcoding template**, **TESHD template**, **audio transcoding template**, **adaptive bitrate streaming template**, **watermarking template**, **screencapturing template**, **animated image generating template**, and **audit template**, each of which can be added to a task flow for video processing.


## Video Transcoding Template

You can create a video transcoding template based on your business needs and customize it. Select **Video Transcoding Template** and click **Create Transcoding Template** to enter the custom template settings page.
+ Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
+ Container format: MP4, FLV, HLS.
- Configuration item: video parameters or audio parameter.
+ Video parameters:
	+ Codec: H.264, H.265
	+ Video bitrate: 0 or 128–35,000 Kbps
	+ Resolution: video long side (video width) and video short side (video height) are 0 or 128–4096 px
	+ Frame rate: 0–60 fps
+ Audio parameters:
	+ Codec: AAC, MP3
	+ Sample rate: three default sample rates, i.e., 32,000 Hz, 44,100 Hz, and 48,000 Hz
	+ Audio bitrate: 0 or 26–256 Kbps
	+ Sound channel: mono, dual
+ Common template: specify whether to set it as a common template

The created template is displayed in the template list, where you can view, edit, or delete it, or set it as a common template.

#### List of preset parameter templates

<table>
    <tr>
        <th rowspan=2>
            Specification                
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
            Audio Parameters
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
            LD
        </td>
        <td>
            10
        </td>
        <td>
            MP4
        </td>
        <td>
            320 * proportionally scaled
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
            Proportionally scaled * 240
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
            320 * proportionally scaled
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
            Proportionally scaled * 240
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
            320 * proportionally scaled
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
            Proportionally scaled * 240
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
            640 * proportionally scaled
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
            Proportionally scaled * 480
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
            640 * proportionally scaled
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
            Proportionally scaled * 480
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
            640 * proportionally scaled
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
            Proportionally scaled * 480
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
            1280 * proportionally scaled
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
            Proportionally scaled * 720
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
            1280 * proportionally scaled
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
            Proportionally scaled * 720
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
            1280 * proportionally scaled
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
            Proportionally scaled * 720
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
            1920 * proportionally scaled
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
            Proportionally scaled * 1080
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
            1920 * proportionally scaled
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
            Proportionally scaled * 1080
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
            1920 * proportionally scaled
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
            Proportionally scaled * 1080
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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

You can create a TESHD template based on your business needs and customize it. Select **TESHD Template** and click **Create Transcoding Template** to enter the custom template settings page.
+ Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
+ Container format: MP4
- Configuration item: video parameters or audio parameter.
+ Video parameters:
	+ Codec: H.264
	+ Average bitrate upper limit: if this parameter is left empty or 0 is entered, there will be no upper limit for bitrate
	+ Resolution: video long side (video width) and video short side (video height) are 0 or 128–4096 px
	+ Frame rate: 0–60 fps
+ Audio parameters:
	+ Codec: AAC, MP3
	+ Sample rate: three default sample rates, i.e., 32,000 Hz, 44,100 Hz, and 48,000 Hz
	+ Audio bitrate: 0 or 26–256 Kbps
	+ Sound channel: mono, dual
+ Common template: specify whether to set it as a common template

The created template is displayed in the template list, where you can view, edit, or delete it, or set it as a common template.


## <a id="yp"></a>Audio Transcoding Template


You can create an audio transcoding template based on your business needs and customize it. Select **Audio Transcoding Template** and click **Create Audio Template** to enter the custom template settings page.

+ Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
+ Container format: MP3, FLAC, OGG, M4A
+ Audio parameters:
	+ Codec: MP3 if the container format is MP3; FLAC if the container format is FLAC or OGG; MP3, AAC, or AC3 if the container format is M4A
	+ Sample rate: three default sample rates, i.e., 32,000 Hz, 44,100 Hz, and 48,000 Hz
	+ Audio bitrate: 0 or 26–256 Kbps
	+ Sound channel: mono, dual
+ Common template: specify whether to set it as a common template

The created template is displayed in the template list, where you can view, edit, or delete it, or set it as a common template.

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

You can use an adaptive bitrate streaming template based on your business needs, which is preset and cannot be customized.
+ Template ID: 10
+ Template type: preset
+ Container type: HLS
+ DRM type: no encryption
+ Filter high bitrate: yes
+ Video specifications: as shown below
<table>
    <tr>
        <th rowspan=1>
            Template ID                
        </th>
        <th rowspan=1>
            Specification
        </th>
        <th>
            Resolution
        </th>
        <th>
            Video Bitrate
        </th>
        <th>
            Video Frame Rate
        </th>
    </tr>
 <tr>
        <td>
          10010
        </td>
        <td>
            LD
        </td>
        <td>
         320 * proportionally scaled
        </td>
        <td>
           256 Kbps
        </td>
        <td>
           24 fps
        </td></tr>
 <tr>
        <td>
            10020
        </td>
        <td>
            	SD
        </td>
        <td>
            640 * proportionally scaled	
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24 fps
        </td>
    </tr>
    <tr>
        <td>
            10030
        </td>
        <td>
            HD
        </td>
        <td>
           1280 * proportionally scaled
        </td>
        <td>
            1,024 Kbps
        </td>
       <td>
          24 fps
        </td></tr>
     <tr>
        <td>
            10040
        </td>
        <td>
            FHD
        </td>
        <td>
           1920 * proportionally scaled
        </td>
        <td>
          2,500 Kbps
        </td>
       <td>
           24 fps
    </tr>
    <tr>
        <td>
            10070
        </td>
        <td>
            2K
        </td>
        <td>
            Proportionally scaled * 1440
        </td>
        <td>
           3,072 Kbps
        </td>
       <td>
            24 fps
        </td>
    </tr>
    <tr>
        <td>
            10080
        </td>
        <td>
            4K
        </td>
        <td>
           Proportionally scaled * 2160
        </td>
        <td>
            6,144 Kbps
        </td>
       <td>
            24 fps
        </td>
    </tr>
</table>
+ Audio specifications: as shown below
<table>
    <tr>
        <th rowspan=1>
            Template ID                
        </th>
        <th rowspan=1>
            Specification
        </th>
        <th>
            Audio Bitrate
        </th>
        <th>
            Codec
        </th>
        <th>
            Audio Sample Rate
        </th>
				<th>
            Sound Channel
					</th>
    </tr>
 <tr>
        <td>
          10010
        </td>
        <td>
            Audio stream
        </td>
        <td>
         48 Kbps
        </td>
        <td>
           AAC
        </td>
        <td>
           44,100 Hz
        </td>
				<td>
           2
        </td>
				</tr>
</table>

## Watermarking Template

You can create a watermarking template by uploading images based on your business needs and customize the watermark configuration and its position in the video.

+ Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
+ Watermark type: image
+ Watermark image: PNG and APNG images are supported. For optimal visual effects, transparent images in PNG format are recommended; the image cannot exceed 200 KB in size or 200 * 200 px in dimensions
+ Watermark position: the default value is top-left and cannot be modified
+ Horizontal offset: the horizontal offset percentage represents the ratio of the horizontal distance between the watermark and the top-left corner to the horizontal width, which is used to configure the horizontal position of the watermark
+ Vertical offset: the vertical offset percentage represents the ratio of the vertical distance between the watermark and the top-left corner to the vertical height, which is used to configure the vertical position of the watermark
+ Watermark size: you can choose to resize the watermark by percentage (%) or pixel (px). If % is selected, the original size will be scaled by percentage. If px is selected, the watermark will be scaled according to the specified size

In the management list of created watermarking templates, you can view the name of a watermarking template, preview a watermark file, and view the format, type, position, and size of a watermark. You can also view, edit, or delete a watermarking template, or set it as the default template.
>
- For example, if the horizontal offset is 0% and vertical offset is 0%, then the watermark will be in the top-left corner of the video. If the horizontal offset is 90% and the vertical offset is 90%, then the watermark will be in the bottom-right corner of the video.
- Once the watermark is set, it will be valid for all subsequently added videos.


## Screencapturing Template
You can create a screencapturing template based on your business needs, so that you can take screenshots of the uploaded videos in various ways. Currently, the VOD Console supports three types of screencapturing: time point screencapturing, sampled screencapturing, and image sprite generating.

### Time point screencapturing
Select "Time Point Screencapturing" for screencapturing type. **The sampling time points need to be specified in the screencapturing task configuration, while the template only configures the screencapturing type.** For detailed configuration of time point screencapturing, please see [Task Configuration Description](https://intl.cloud.tencent.com/document/product/266/14058#p1).

- Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
- Image format: JPG
- Image dimensions: 0 or 128–4,096 px

#### List of preset parameter templates

| Template ID | Format | Width | Height | FillType |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

### Sampled Screencapturing
Select "Sampled Screencapturing" for the screencapturing type.

- Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
- Image format: JPG
- Image dimensions: 0 or 128–4,096 px
- Sampling interval: percentage (up to 100%) or time (in seconds)

#### List of preset parameter templates

| Template ID | Format | Width | Height | SampleType | Interval | FillType |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG    | Same as source   | Save as source     | By percent  | 10%   | Stretch     |



### Image sprite generating
Select "Image Sprite Generating" for the screencapturing type.

- Template name: it can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.)
- Image format: JPG
- Image dimensions: 0 or 128–4,096 px
- Sampling interval: percentage (up to 100%) or time (in seconds)
- Number of subimage rows: a positive integer. The number of subimage rows multiplied by the number of subimage columns cannot exceed 100.
- Number of subimage columns: a positive integer. The number of subimage rows multiplied by the number of subimage columns cannot exceed 100.

The template name, screencapturing type, and image dimensions are displayed in the screencapturing template. In the "Operation" column, you can view, edit, or delete the template.

#### List of preset parameter templates

| Template ID | Format | Width | Height | Rows | Columns | SampleType | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | By time   | 10s  |


## Animated Image Generating Template
You can create an animated image generating template based on your business needs to take screenshots within the specified time period and generate an animated image. **The time period needs to be specified in the animated image generating task configuration, while the template only configures the animated image generating type.** For detailed configuration of animated image generating, please see [Task Configuration Description](https://intl.cloud.tencent.com/document/product/266/14058#p1).

- Image type: WebP, GIF
- Frame rate: 1–30 fps
- Image quality: 1–100
- Image dimensions: 0–1,920 px.

#### List of preset parameter templates

| Template ID | Format | Resolution | FPS |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | 320 * proportionally scaled             | 2           |
| 20002   | WebP                | 320 * proportionally scaled | 10          |
| 20003   | WebP               | Proportionally scaled * 360 |  10          |
| 20004   | WebP               | Same as source                 | 10           |
| 20005   | WebP               |540 * 960    | 10         |


## Audit Template
You can create a video audit template based on your business needs and customize it. Click **Create Audit Template** to enter the custom template settings page.

- Template name: it can contain up to 64 letters, digits, spaces, underscores (\_), dashes (-), and periods (.)
- Sampling interval: it indicates at which interval in seconds the video under audit is sampled for check. Default value: 1. Minimum value: 0.5
- Audit item: valid values include image recognition, speech recognition, and text recognition. The selected audit subitems will appear in the "Selected" column on the right
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
<td align="center">Eroticism</td>
<td align="center">Including audit subitems for porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">Including audit subitems for militants, weapons and guns, bloody scenes, explosions and fires, terrorism flags, terrorists, police force, and crowds</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">Including audit subitems for politically sensitive figures, violating photos, entertainment celebrities, and sports celebrities</td>
</tr>
<tr>
<td rowspan = 2>Speech recognition</td>
<td align="center">Eroticism</td>
<td align="center">Same as the eroticism item in image recognition</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">Same as the politics item in image recognition</td>
</tr>
<tr>
<td rowspan = 2>Text recognition</td>
<td align="center">Eroticism</td>
<td align="center">Same as the eroticism item in image recognition</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">Same as the politics item in image recognition</td>
</tr>
</tbody></table>

For each audit subitem, you can set a **confirmed confidence threshold** and a **suspected confidence threshold** to adjust the audit intensity. If they are left empty, the default values in VOD will be used for video audit.
 - Confirmed confidence threshold: VOD scores an uploaded video after auditing it. If the score is above this value, the status of the corresponding audit item will be "confirmed". If there is no special requirement, you are recommended to use the default value range (0–100).
 - Suspected confidence threshold: VOD scores an uploaded video after auditing it. If the score is above this value, the status of the corresponding audit item will be "suspected", and you can initiate human re-audit on the video audit page. If there is no special requirement, you are recommended to use the default value range (0–100).
 
The created template is displayed in the template list, where you can view, edit, or delete it.


#### <span id = "yz"></span>List of preset audit templates
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th nowrap="nowrap">Template ID</th>
<th >Audit Item</th>
<th align="center" nowrap="nowrap">Audit Subitem</th>
<th align="center">Confirmed confidence threshold [0,100]	</th>
<th align="center">Suspected confidence threshold [0,100]	</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">10</td>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td align="center">Eroticism</td>
<td align="center">90</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">90</td>
<td align="center">80</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">97</td>
<td align="center">95</td>
</tr>
<tr>
<tr>
<td rowspan = 7 nowrap="nowrap">20</td>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td align="center">Eroticism</td>
<td align="center">90</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">Terrorism</td>
<td align="center">90</td>
<td align="center">80</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">97</td>
<td align="center">95</td>
</tr>
<tr>
<td rowspan = 2>Speech recognition</td>
<td align="center">Eroticism</td>
<td align="center">100</td>
<td align="center">75</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">100</td>
<td align="center">75</td>
</tr>
<tr>
<td rowspan = 2>Text recognition</td>
<td align="center">Eroticism</td>
<td align="center">100</td>
<td align="center">75</td>
</tr>
<tr>
<td align="center">Politics</td>
<td align="center">100</td>
<td align="center">75</td>
</tr>
</tbody></table>
