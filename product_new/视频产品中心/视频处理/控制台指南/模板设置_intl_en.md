Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Template Settings** on the left sidebar to enter the template settings page. There are five types of built-in templates: video transcoding template, audio transcoding template, watermarking template, screencapturing template, and animated image generating template. Each type of templates can be added to a workflow for cloud-based transcoding and audiovisual processing.
![](https://main.qcloudimg.com/raw/beb249c241648218fd3ae7ca1414b1cd.png)
>
>- If the template used in a workflow is edited after the workflow is enabled, the workflow will use the updated template parameters.
>- If the template used in a workflow is deleted after the workflow is enabled, subtasks associated with the deleted template will fail to be executed.
## Video Transcoding Template
MPS provides preset video transcoding templates that can be used directly in workflow management. In addition, you can customize video transcoding templates based on your business needs. Click **Create Template** to enter the custom template settings page.
- Template name: It can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Container format: MP4, FLV, or HLS.
- Configuration item: Video parameters or audio parameter.
- Video codec: H.264 or H.265.
- Video bitrate: 0 (indicating that the source bitrate is retained) or 128–35,000 Kbps.
- Video resolution: 0 (indicating that the source resolution is retained) or 128–4096 px.
- Video frame rate: 0–60 fps.
- Audio codec: AAC or MP3.
- Audio sample rate: Three default sample rates, i.e., 32,000 Hz, 44,100 Hz, or 48,000 Hz.
- Audio bitrate: 0 (indicating that the source bitrate is retained) or 26–256 Kbps.
- Audio sound system: mono-channel or dual-channel.

A created template will be displayed in the template list, where you can view, edit, or delete custom templates. Preset templates can be viewed only but not edited or deleted.

> If MP4, FLV, or HLS is selected, video parameters must be configured, and audio parameters are optional.

#### Preset parameter template list

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
            Video parameters
        </th>
        <th colspan=1>    
            Audio parameters
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

## Audio Transcoding Template
MPS provides preset audio transcoding templates that can be used directly in workflow management. In addition, you can customize audio transcoding templates based on your business needs. Click **Create Transcoding Template** to enter the custom template settings page.
 
- Template name: It can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Container format: MP3, FLAC, OGG, or M4A.
- Audio codec: MP3 if the container format is MP3; FLAC if the container format is FLAC or OGG; or MP3, AAC, or AC3 if the container format is M4A.
- Sample rate: Three default sample rates, i.e., 32,000 Hz, 44,100 Hz, or 48,000 Hz.
- Audio bitrate: 0 (indicating that the source bitrate is retained) or 26–256 Kbps.
- Sound system: Mono-channel or dual-channel.

A created template will be displayed in the template list, where you can view, edit, or delete custom templates. Preset templates can be viewed only but not edited or deleted.

#### Preset parameter template list

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
            Dual
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
            Dual
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
            Dual
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
            Dual
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
            Dual
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
            Dual
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
            Dual
        </td>
                <td>
            44,100 Hz
        </td>
    </tr>
</table>
 

## Watermarking Template
MPS does not provide preset watermarking templates. You can create custom templates based on your business needs. Click **Create Watermarking Template** to enter the custom template settings page.
 
- Template name: It can contain up to 128 letters, digits, and underscores (_).
- Watermark type: Image watermark.
- Watermark image: PNG and APNG images are supported. For optimal visual effects, transparent images in PNG format are recommended. The image cannot exceed 200 KB in size or 200 * 200 px in dimensions.
- Watermark position: The default position is in the top-left corner, which can be adjusted by vertical and horizontal offsets.
- Vertical offset: The vertical offset percentage represents the ratio of the vertical distance between the watermark and the top-left corner to the vertical height, which is used to configure the vertical position of the watermark.
- Horizontal offset: The horizontal offset percentage represents the ratio of the horizontal distance between the watermark and the top-left corner to the horizontal width, which is used to configure the horizontal position of the watermark.
- Watermark size: You can choose to resize the watermark by percentage (%) or pixel (px). If % is selected, the original size will be scaled by percentage. If px is selected, the watermark will be scaled according to the specified size.

A created watermarking template will be displayed in the template list, where you can view the name of a watermarking template, preview a watermark file, and view the format, type, location, and size of a watermark. You can also view, edit, or delete the watermarking template, or set it as the default template.

 

## Screencapturing Template
Currently, the MPS Console supports three types of screenshots, namely, time point screenshot, sampled screenshot, and image sprite screenshot, and provides preset templates that can be used directly in workflow management. In addition, you can customize screencapturing templates based on your business needs. Click **Create Screencapturing Template** to enter the custom template settings page.

### Time point screenshot
Select time point screenshot for the screenshot type. The time point needs to be configured in the workflow, while the template has only parameters for configuring the template name and image size. For detailed configuration, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).
 
- Template name: It can contain up to 64 letters, digits, and underscores (_).
- Image format: JPG.
- Image size: The value range of the image width or height is 128–4,096 px.

#### Preset parameter template list

| Template ID | Format | Width | Height | FillType |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

### Sampled screenshot
Select sampled screenshot for the screenshot type.
 
- Template name: It can contain up to 64 letters, digits, and underscores (_).
- Image format: JPG.
- Image size: The value range of the image width or height is 128–4,096 px.
- Interval: The interval can be set to a percent value (%) or second value (s). If a percent value is selected, it cannot exceed 100.

#### Preset parameter template list

| Template ID | Format | Width | Height | SampleType | Interval | FillType |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG    | Same as source   | Save as source     | By percent  | 10%   | Stretch     |

### Image sprite screenshot
Select image sprite screenshot for the screenshot type.

- Template name: It can contain up to 64 letters, digits, and underscores (_).
- Image format: JPG.
- Image size: The value range of the image width or height is 128–4,096 px.
- Interval: The interval can be set to a percent value (%) or second value (s). If a percent value is selected, it cannot exceed 100.
- Rows: A positive integer. The number of small image rows multiplied by the number of small image columns cannot exceed 100.
- Columns: A positive integer. The number of small image rows multiplied by the number of small image columns cannot exceed 100.

A created screencapturing template will be displayed in the template list, where you can view information such as the template name, screenshot type, image size, and template type. You can also view, edit, or delete the custom template, or set it as the default template. Preset templates can be viewed only but not edited or deleted.

#### Preset parameter template list

| Template ID  | Format | Width | Height | Rows | Columns | SampleType | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80                 | 10               | 10                  | By time             | 10s                 |


 

## Animated Image Generating Template
MPS provides preset animated image generating templates that can be used directly in workflow management. In addition, you can customize animated image generating templates based on your business needs. Click **Create Animated Image Generating Template** to enter the custom template settings page.
The time point needs to be configured in the workflow, while the template has only parameters for configuring the image type, frame rate, image quality, and image size. For detailed configuration, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).
 

- Template name: It can contain up to 128 letters, digits, and underscores (_).
- Image type: WEBP or GIF.
- Frame rate: 1–30 fps.
- Image quality: 0–100 (This value is the quality of the generated animated image. The higher the quality, the larger the animated image size.)
- Image size: The value of the image width or height should be greater than 0 and less than or equal to 1920 px.

A created animated image generating template will be displayed in the template list, where you can view information such as the template name, image type, frame rate, image quality, image size, and template type. You can also view, edit, or delete the custom template, or set it as the default template. Preset templates can be viewed only but not edited or deleted.

#### Preset parameter template list

| Template ID | Format | Resolution | FPS |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | Same as source                 | 2           |
