## Overview
You can create a template and add it to a **scheme** to process media files according to preset parameters.

## Directions
Log in to the [MPS console](https://console.cloud.tencent.com/mps) and click **Templates** on the left sidebar. Select the type of template you want to configure and click **Create template**.
![](https://qcloudimg.tencent-cloud.cn/raw/c195de9b941ac6aff0843e302743649b.png)


## Template Types
The table below lists the types of media processing templates you can create and add to a scheme.

>?
>- If a template is modified after being added to a scheme, the new settings will be applied.
>- If a template is deleted after being added to a scheme, its subtasks will fail to be executed.

<table>
    <tr>
        <th width=15%>Template Type</th>
        <th width=17%>Subtype</th>
        <th>Description</th>
    </tr>
    <tr>
        <td rowspan = '5'>Audio/Video transcoding</td>
        <td>General transcoding</td>
        <td>Transcode audio/video files</td>
    </tr>
     <tr>
        <td>TSC transcoding</td>
        <td>Transcode videos according to Top Speed Codec (TSC) standards, reducing video size without compromising quality.</td>
    </tr>
    <tr>
        <td>Adaptive bitrate streaming</td>
        <td>Convert the source file into multi-bitrate streams that are suitable for playback in different scenarios.</td>
    </tr>
    <tr>
        <td>Remuxing</td>
        <td>Change the container format of the source video (to MP4 or HLS) without transcoding.</td>
    </tr>
    <tr>
        <td>Audio transcoding</td>
        <td>Transcode audio files</td>
    </tr>
    <tr>
        <td rowspan = '4'>Screenshot</td>
        <td>Time point screenshot</td>
        <td>Take screenshots at specific time points.</td>
    </tr>
    <tr>
        <td>Sampled screenshot</td>
        <td>Take screenshots at a specified interval (seconds or percentage).</td>
    </tr>
    <tr>
        <td>Image sprite screenshot</td>
        <td>Take screenshots at specified time points and merge them into a sprite.</td>
    </tr>
    <tr>
        <td>Animated screenshot</td>
        <td>Cut out a video clip and make it into an animated screenshot.</td>
    </tr>
    <tr>
        <td rowspan = '1'>Watermark</td>
        <td>Watermark</td>
        <td>Add a text or image watermark to a video.</td>
    </tr>
     <tr>
        <td rowspan = '2'>Content discovery</td>
        <td>Content analysis</td>
        <td>Intelligent labeling, categorization, and thumbnail generation.</td>
    </tr>
    <tr>
        <td>Content recognition</td>
        <td>Recognize faces, text, and speech.</td>
    </tr>
    <tr>
        <td rowspan = '1'>Moderation</td>
        <td>Moderation</td>
        <td>Detect pornographic, terrorist, and politically sensitive content in images, text, and speech.</td>
    </tr>
    <tr>
        <td rowspan = '1'>Audio/Video enhancement</td>
        <td>Audio/Video enhancement</td>
        <td>Enhance audio/video quality.</td>
    </tr>
</table>


