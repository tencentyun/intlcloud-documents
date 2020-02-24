Log in to the [MPS Console](https://console.cloud.tencent.com/mps) and click **Template Settings** on the left sidebar. There are five types of preset templates: video transcoding template, audio transcoding template, watermark template, screenshot template, and animated image generating template. They can all be can be added to a workflow for cloud-based transcoding and audiovisual processing.
![](https://main.qcloudimg.com/raw/beb249c241648218fd3ae7ca1414b1cd.png)
>
>- If the template used in a workflow is edited after the workflow is enabled, the workflow will use the updated template parameters.
>- If the template used in a workflow is deleted after the workflow is enabled, subtasks associated with the deleted template will fail.
## Video Transcoding Template
MPS provides preset video transcoding templates that can be used in workflows. You can customize these video transcoding templates according to your needs. Click **Create Video Transcoding Template** to enter the custom template settings page.
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

Created templates will be displayed in the template list, where you can view, edit, or delete custom templates. Preset templates can be viewed, but cannot be edited or deleted.

> If MP4, FLV, or HLS is selected, video parameters must be configured, and audio parameters are optional.

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
MPS provides preset audio transcoding templates that can be used in workflows. You can customize these audio transcoding templates according to your needs. Click **Create Template** to enter the custom template settings page.

- Template name: It can contain up to 64 letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Container format: MP3, FLAC, OGG, or M4A.
- Audio codec: MP3 if the container format is MP3; FLAC if the container format is FLAC or OGG; or MP3, AAC, or AC3 if the container format is M4A.
- Sample rate: Three default sample rates, i.e., 32,000 Hz, 44,100 Hz, or 48,000 Hz.
- Audio bitrate: 0 (indicating that the source bitrate is retained) or 26–256 Kbps.
- Sound system: Mono-channel or dual-channel.

Created templates will be displayed in the template list, where you can view, edit, or delete custom templates. Preset templates can be viewed, but cannot be edited or deleted.

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
            Sound System
        </th>
        <th>
            Sample Rate
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
MPS does not provide preset watermarking templates. You can create custom templates according to your needs. Click **Create Template** to enter the custom template settings page.

- Template name: It can contain up to 128 letters, digits, and underscores (_).
- Watermark type: Image watermark.
- Watermark image: PNG and APNG images are supported. For optimal visual effects, transparent images in PNG format are recommended. The image cannot exceed 200 KB in size or 200 * 200 px in dimensions.
- Watermark position: The default position is in the top-left corner, which can be adjusted by vertical and horizontal offsets.
- Vertical offset: The vertical offset percentage represents the ratio of the vertical distance between the watermark and the top-left corner to the vertical height, which is used to configure the vertical position of the watermark.
- Horizontal offset: The horizontal offset percentage represents the ratio of the horizontal distance between the watermark and the top-left corner to the horizontal width, which is used to configure the horizontal position of the watermark.
- Watermark dimension: You can choose to resize the watermark by percentage (%) or pixel (px). If % is selected, the original size will be scaled by percentage. If px is selected, the watermark will be scaled according to the specified size.

Created watermark templates will be displayed in the template list, where you can view their details, including the template names. You can preview the watermarks, and view their format, type, position and dimension. You can also view, edit, or delete templates, and set the default template.

 

## Screenshot Template
Currently, the MPS Console supports three types of screenshots, namely, time point screenshot, sampled screenshot, and image sprite screenshot, and provides preset templates that can be used in workflows. You can customize these screenshot templates according to your needs. Click **Create Template** to enter the custom template settings page.

### Time point screenshot
If time point screenshot is selected as the screenshot type, the time point needs to be configured in the workflow. You can only set the name and image size in the template. For detailed configuration, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).

- Template name: It can contain up to 64 letters, digits, and underscores (_).
- Image format: JPG.
- Image dimension: The value range of the image width or height is 128–4,096 px.

#### List of preset parameter templates

| Template ID | Format | Width | Height | Fill Type |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

### Sampled screenshot
Select sampled screenshot for the screenshot type.

- Template name: It can contain up to 64 letters, digits, and underscores (_).
- Image format: JPG.
- Image dimension: The value range of the image width or height is 128–4,096 px.
- Interval: The interval can be a percent value (%) or be in seconds (s). If a percent value is selected, it cannot exceed 100.

#### List of preset parameter templates

| Template ID | Format | Width | Height | Sample Type | Interval | Fill Type |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG    | Same as source   | Save as source     | By percent  | 10%   | Stretch     |

### Image sprite screenshot
Select image sprite screenshot for the screenshot type.

- Template name: It can contain up to 64 letters, digits, and underscores (_).
- Image format: JPG.
- Image dimension: The value range of the image width or height is 128–4,096 px.
- Interval: The interval can be a percent value (%) or be in seconds (s). If a percent value is selected, it cannot exceed 100.
- Rows: A positive integer. The number of sub-image rows multiplied by the number of sub-image columns cannot exceed 100.
- Columns: A positive integer. The number of sub-image rows multiplied by the number of sub-image columns cannot exceed 100.

Created screenshot templates will be displayed in the template list, where you can view details such as the template name, screenshot type, image dimension, and template type. You can also view, edit, or delete the custom template, or set it as the default template. Preset templates can be viewed, but cannot be edited or deleted.

#### List of preset parameter templates

| Template ID  | Format | Width | Height | Rows | Columns | Sample Type | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80                 | 10               | 10                  | By time             | 10s                 |




## Animated Image Generating Template
MPS provides preset animated image generating templates that can be used in workflows. You can customize these animated image generating transcoding templates according to your needs. Click **Create Template** to enter the custom template settings page.
You can set the image format, frame rate, image dimensions and image quality with the template. Time points needs to be configured in the workflow. For detailed configuration, please see [Workflow Management](https://intl.cloud.tencent.com/document/product/1041/33485).


- Template name: It can contain up to 128 letters, digits, and underscores (_).
- Image format: WEBP or GIF.
- Frame rate: 1–30 fps.
- Image quality: 0–100 (This value is the quality of the generated animated image. The higher the quality, the larger the animated image size.)
- Image dimension: The value of the image width or height should be greater than 0 and less than or equal to 1920 px.

Created animated image generating template will be displayed in the template list, where you can view details such as the template name, image type, frame rate, image quality, image dimension, and template type. You can also view, edit, or delete the custom template, or set it as the default template. Preset templates can be viewed, but cannot be edited or deleted.

#### List of preset parameter templates

| Template ID | Format | Resolution | FPS |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | Same as source                 | 2           |
