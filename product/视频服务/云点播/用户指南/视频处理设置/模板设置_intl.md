Log in to the [VOD in the configuration itemConsole](https://console.cloud.tencent.com/video) and click **Video Processing** > **Template Settings** in the left navigation pane. There are five types of built-in templates: **Video Transcoding Template**, **Audio Transcoding Template**, **Watermark Template**, **Screenshot Template**, and **GIF Generating Template**. Each template can be added to the task flow settings for video processing.
![Template Settings](https://main.qcloudimg.com/raw/96105db0ad07f80732df6512ea1dd240.png)

## Video Transcoding Template

You can create video transcoding templates based on your business needs. Click **Create Video Transcoding Template** to customize template settings.
![](https://main.qcloudimg.com/raw/f86b6164d6774745f1483140318fc879.jpg)

+ Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
+ Encapsulation format: MP4, FLV, or HLS.
+ Configuration item: Video parameters and [audio parameters](#yp) (same as the audio transcoding template). If MP4, FLV, or HLS is selected, the video parameters must be configured.
+ Video coding standard: H.264 or H.265.
+ Bitrate (video bitrate): 0 or 128-35000 Kbps.
+ Resolution: 0 or 128-4096 px.
+ Frame rate: 0-60 fps.
+ Common template: Specify whether the template is the common template.

You can view, edit, or delete the created template in the template list. You can also set it as a common template.
![Video Transcoding Template](https://main.qcloudimg.com/raw/bb670eca686cd0e75913fdcc9ec3e07b.png)

## <a id="yp"></a>Audio Transcoding Template


You can create audio transcoding templates based on your business needs. Click **Create Audio Transcoding Template** to customize the template settings.
![Create Audio Transcoding Template](https://main.qcloudimg.com/raw/a3239c32483b8b1bb6cc01bd932b4f90.png)

+ Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
+ Encapsulation format: MP3, FLAC, or OGG.
+ Audio coding standard: MP3 if the encapsulation format is MP3; FLAC if the encapsulation format is FLAC or OGG.
+ Sampling rate: Three default sampling rates, i.e., 32000 Hz, 44100 Hz or 48000 Hz.
+ Bitrate (audio bitrate): 0 or 26-256 Kbps.
+ Channel: 1-channel or 2-channel.
+ Common template: Specify whether the template is the common template.

You can view, edit, or delete the created template in the template list. You can also set it as a common template.
![Audio Transcoding Template](https://main.qcloudimg.com/raw/d4fc0939f4e8aecd158b7ab70aa6ba2a.png)

## Watermarking Template

You can create and customize a watermark template using uploaded images, and configure the default watermark and where it sits in the video.
![Create Watermarking Template](https://main.qcloudimg.com/raw/2ea843e4b6ab0e961ecab92c92a6bacf.png)
+ Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
+ Watermark type: Image or text.
+ Watermark image: PNG and APNG images are supported. For optimal visual effects, transparent images in PNG format are recommended; the image cannot exceed 200 KB in size or 200 * 200 px in dimensions.
+ Watermark position: The default values are upper left, upper right, lower left, and lower right, which cannot be modified.
+ Horizontal offset: The horizontal offset percentage represents the ratio of the horizontal distance between the watermark and the upper left corner to the horizontal width, which is used to configure the horizontal location of the watermark.
+ Vertical offset: The vertical offset percentage represents the ratio of the vertical distance between the watermark and the upper left corner to the vertical height, which is used to configure the vertical location of the watermark.
+ Watermark dimension: You can resize the watermark by percentage (%) or pixel (px). If % is selected, the original size will be scaled by percentage. If px is selected, the watermark will be scaled according to the specified size.

In the list of created watermark templates, you can view the name of a watermarking template, preview a watermark file, and view the format, type, position, and dimension of a watermark. You can also view, edit, or delete a watermarking template, or set it as the default template.
![Watermarking Template](https://main.qcloudimg.com/raw/7537b6bfc2757eeb5325227f31ce7607.png)
>?
- For example, if the horizontal offset is 0% and the vertical offset is 0%, then the watermark is in the upper left corner of the video screen. If the horizontal offset is 90% and the vertical offset is 90%, the watermark is located in the lower right corner of the video screen.
- Once the watermark is set, it will be valid for all subsequently added videos.

## Screenshot Template
You can create a screen capturing template based on your business needs so that users can take screenshots of the uploaded videos in various ways. Currently, the VOD console supports three types of screenshots: time point screenshot, sampling screenshot, and sprite screenshot.

### Point-in-time Screenshot
Select "Point-in-time screenshot" for the screenshot type. You need to specify the sampling time point for the task flow, and you can only configure the type of screenshot for the template. For detailed configuration, see [Task Flow Settings](https://cloud.tencent.com/document/product/266/33819).
![Point-in-time Screenshot](https://main.qcloudimg.com/raw/65b110ceac173767493895721e84f0a0.png)
- Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Image format: JPG.
- Image dimensions: 0 or 128-4096 px.

### Sampling Screenshot
Select "Sampling screenshot" for the screenshot type.
![Sampling screenshot](https://main.qcloudimg.com/raw/d7036db44fa28672a3877ed3a9ebb6b2.png)
- Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Image format: JPG.
- Image dimensions: 0 or 128-4096 px.
- Sampling interval: Percentage (up to 100%) or time (s).

### Image Sprite Screenshot
Select "Image sprite screenshot" for the screenshot type.
![Sprite screenshot](https://main.qcloudimg.com/raw/cb09bcd933ebb2611fc4a5e7cb9dc3ae.png)
- Template name: It can contain up to 64 Chinese characters, letters, digits, spaces, underscores (_), dashes (-), and periods (.).
- Image format: JPG.
- Image dimensions: 0 or 128-4096 px.
- Sampling interval: Percentage (up to 100%) or time (s).
- The number of small image rows: A positive integer. The number of small image rows multiplied by the number of small image columns cannot exceed 100.
- The number of small image columns: A positive integer. The number of small image rows multiplied by the number of small image columns cannot exceed 100.

The template name, screenshot type, and image dimensions are displayed in the screen capturing template. In the **Operation** column, you can view, edit, or delete the template.
![](https://main.qcloudimg.com/raw/4aa06a282c10d8de02abc4d5dc871fd0.jpg)

## Animated Image Converter Template
You can create an animated Image Converter Template based on your business needs,  and convert the screenshot to WEBP or GIF format in a specified time period, which you need to configure in the task flow. You can only configure the image type. For detailed configuration, see [Task Flow Settings](https://cloud.tencent.com/document/product/266/33819).
![](https://main.qcloudimg.com/raw/204a20ba3a501f4ed836aefddb3ffcc7.jpg)
- Image type: WEBP or GIF.
- Frame rate: 1-30 fps.
- Image quality: 1-100.
- Image dimensions: 0-1920 px.
