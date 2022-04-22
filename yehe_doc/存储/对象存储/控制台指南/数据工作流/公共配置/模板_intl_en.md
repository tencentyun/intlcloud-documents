## Overview

When using the data processing workflow feature, you usually need to set a series of parameters, which can be combined through a template. This **simplifies your operations** and allows you to reuse the configured parameters with no need to enter them repeatedly.

For media processing features such as audio/video transcoding, audio/video splicing, video frame capturing, and video to animated image conversion, you need to specify a template when creating a job or workflow. The template page provides **system templates**, and you can also **customize templates** based on your business needs.

## System Templates

The system combines common parameters in advance into system templates, so that you can use them directly. When creating a job or workflow, you can select such a template by the template name.

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to operate.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration** > **Template** to view templates of different processing types.
![](https://qcloudimg.tencent-cloud.cn/raw/be779fe02687118951c896008de7649f.png)
Click **View** in the **Operation** column to view template details.
>?
> - Currently, the system provides 15 **audio/video transcoding**, 3 **video frame capturing**, and 18 **video to animated image conversion** templates.
> - You can view the information of system templates but cannot edit or delete them.
> 

#### System templates for audio/video transcoding

| Template ID | Template Name | Container Format | Video Encoding Format | Resolution | Video Bitrate | Audio Encoding Format | Audio Bitrate |
| ---------------------------------- | -------- | -------- | ------------ | ------------------ | --------- | ------------ | -------- |
| t02db40900dc1c43ad9bdbd8acec6075c5 | MP4\-FLU | MP4      | H\.264       | 640 \* auto-scaled  | 512 Kbps  | AAC          | 128 Kbps |
| t04e1ab86554984f1aa17c062fbf6c007c | MP4\-SD  | MP4      | H\.264       | 720 \* auto-scaled  | 1024 Kbps | AAC          | 128 Kbps |
| t02d06d8ad881648e69f9ca95b2e7e4b6a | MP4\-HD  | MP4      | H\.264       | 1280 \* auto-scaled | 2000 Kbps | AAC          | 128 Kbps |
| t064fb9214850f49aaac44b5561a7b0b3b | MP4\-FHD | MP4      | H\.264       | 1920 \* auto-scaled | 3500 Kbps | AAC          | 128 Kbps |
| t077211ea3e0e74168b8ed921fcb2d5a6b | MP4\-2K  | MP4      | H\.264       | 2048 \* auto-scaled | 4800 Kbps | AAC          | 128 Kbps |
| t0c9cfaffb5055467691b85eed1242cd03 | FLV\-FLU | FLV      | H\.264       | 640 \* auto-scaled  | 512 Kbps  | AAC          | 128 Kbps |
| t0b612860a293f410785b3e672465dca38 | FLV\-SD  | FLV      | H\.264       | 720 \* auto-scaled  | 1024 Kbps | AAC          | 128 Kbps |
| t0b6a845f5e42847bd810ee9cbf337f83c | FLV\-HD  | FLV      | H\.264       | 1280 \*auto-scaled  | 2000 Kbps | AAC          | 128 Kbps |
| t08571e1f229094eb79817f8474987a479 | FLV\-FHD | FLV      | H\.264       | 1920 \* auto-scaled | 3500 Kbps | AAC          | 128 Kbps |
| t0f52244b7f3c743eb9f9080b15e5fe2f8 | FLV\-2K  | FLV      | H\.264       | 2048 \* auto-scaled | 4800 Kbps | AAC          | 128 Kbps |
| t06e5246d8bf694c88b16ae7512e83962a | HLS\-FLU | M3U8     | H\.264       | 640 \* auto-scaled  | 512 Kbps  | AAC          | 128 Kbps |
| t03ed6a4e1b374429eadec266bd6859347 | HLS\-SD  | M3U8     | H\.264       | 720 \* auto-scaled  | 1024 Kbps | AAC          | 128 Kbps |
| t0e09a9456d4124542b1f0e44d501d7182 | HLS\-HD  | M3U8     | H\.264       | 1280 \* auto-scaled | 2000 Kbps | AAC          | 128 Kbps |
| t088613dea8d564a9ba7e6b02cbd5de877 | HLS\-FHD | M3U8     | H\.264       | 1920 \* auto-scaled | 3500 Kbps | AAC          | 128 Kbps |
| t08e7237a0975c427cabfa3d958f29aa58 | HLS\-2K  | M3U8     | H\.264       | 2048 \* auto-scaled | 4800 Kbps | AAC          | 128 Kbps |

#### System templates for video frame capturing

| Template ID | Template Name | Frame Capturing Start Time | Frame Capturing Interval | Max Frame Count Per Video | Output Image Size | Output Format |
| ---------------------------------- | ---------------------- | -------------- | -------- | ---------------- | ----------------- | -------- |
| t01d40e440761448fc8c538fb8d5a5b81e | snapshot\_320 \* 180\_1  | 0s            | 2s      | 5                | 320 \* 180 px  | JPEG     |
| t0a60a2bc71a4b40c7b3d7f7e8a2779a81 | snapshot\_640 \* 360\_2  | 0s            | 10s     | 5                | 640 \* 360 px  | JPEG     |
| t07740e32081b44ad7a0aea03adcffd54a | snapshot\_1280 \* 720\_3 | 0s            | 10s     | 5                | 1280 \* 720 px | JPEG     |

#### System templates for video to animated image conversion

| Template ID | Template Name | Transcoding Start Time | Transcoding Duration | Frame Extraction Method | Output Animated Image Frame Rate | Output Animated Image Size | Output Format | Output Animated Image Quality |
| ---------------------------------- | --------------- | ------------ | -------- | ----------------- | -------------------- | -------------- | -------- | ------------ |
| t04373959a69c04d47b62fd214dd13d8e9 | gif_320 \* 180_1   | 0s          | 600s    | Only keyframes are extracted      | Adaptive               | 320 \*  180 px  | GIF      | \            |
| t0341b0ab2b8a340ff826e9cb4f3a7baea | gif_320 \* 180_2   | 0s          | 600s    | One frame is extracted every 10s | Adaptive (0.1 FPS) | 320 \* 180 px  | GIF      | \            |
| t046b1d8e5bdf842c6a58d8028b48eafee | gif_320 \* 180_3   | 0s          | 600s    | Ten frames are extracted per second | Adaptive (10 FPS)   | 320 \* 180 px  | GIF      | \            |
| t0ef2077f215864c018a2fca73614ceca6 | gif_640 \* 360_4   | 0s          | 600s    | Only keyframes are extracted      | Adaptive               | 640 \* 360 px  | GIF      | \            |
| t0d21406ca737a40869973a37a5daa349a | gif_640 \* 360_5   | 0s          | 600s    | One frame is extracted every 10s | Adaptive (0.1 FPS) | 640 \* 360 px  | GIF      | \            |
| t0878a9c9c1f054cb5bca68b8b06e556c2 | gif_640 \* 360_6   | 0s          | 600s    | Ten frames are extracted per second | Adaptive (10 FPS)   | 640 \* 360 px  | GIF      | \            |
| t0dae821708cea4ba5b3e271810ac80a21 | gif_1280 \* 720_7  | 0s          | 600s    | Only keyframes are extracted      | Adaptive               | 1280 \* 720 px | GIF      | \            |
| t03fef67ad94d2466b9c0c89252ed72e87 | gif_1280 \* 720_8  | 0s          | 600s    | One frame is extracted every 10s | Adaptive (0.1 FPS) | 1280 \* 720 px | GIF      | \            |
| t030a64e9f9f5a4f53a9ef64bb7ce490b5 | gif_1280 \* 720_9  | 0s          | 600s    | Ten frames are extracted per second | Adaptive (10 FPS)   | 1280 \* 720 px | GIF      | \            |
| t03b0e9eca4fc34e2cba9da89d9c7c13a2 | webp_320 \* 180_1  | 0s          | 60s     | Only keyframes are extracted      | Adaptive               | 320 \* 180 px  | WEBP     | 75           |
| t016fcddf6bc3c44b793e9b7b07119b4ee | webp_320 \* 180_2  | 0s          | 600s    | One frame is extracted every 10s | Adaptive (0.1 FPS) | 320 \* 180 px  | WEBP     | 75           |
| t0bf1f1ce6d2404b258c0f81fbb9aaece1 | webp_320 \* 180_3  | 0s          | 600s    | One frame is extracted every 10s | Adaptive (10 FPS)   | 320 \* 180 px  | WEBP     | 75           |
| t098d6d3fcfd2c45309a408594a42559f6 | webp_640 \* 360_4  | 0s          | 60s     | Only keyframes are extracted      | Adaptive               | 640 \* 360 px      | WEBP     | 75           |
| t0169a6a9c2eec4b51972eb63bafcbf08d | webp_640 \* 360_5  | 0s          | 600s    | One frame is extracted every 10s | Adaptive (0.1 FPS) | 640 \* 360 px      | WEBP     | 75           |
| t0ef9ba537011e4876b8777aebc19d10a5 | webp_640 \* 360_6  | 0s          | 600s    | One frame is extracted every 10s | Adaptive (10 FPS)   | 640 \* 360 px      | WEBP     | 75           |
| t02743d344b5e74c579e50e9e135b432b8 | webp_1280 \* 720_7 | 0s          | 60s     | Only keyframes are extracted      | Adaptive               | 1280 \* 720 px     | WEBP     | 75           |
| t0dd27c136ff2741538bec96981e058868 | webp_1280 \* 720_8 | 0s          | 600s    | One frame is extracted every 10s | Adaptive (0.1 FPS) | 1280 \* 720 px     | WEBP     | 75           |
| t00ad05235d67a45a9a697b553052b7346 | webp_1280 \* 720_9 | 0s          | 600s    | One frame is extracted every 10s | Adaptive (10 FPS)   | 1280 \* 720 px     | WEBP     | 75           |



## Custom Templates

If system templates cannot meet your needs, use custom templates. Currently, you can create custom templates for **audio/video transcoding**, **top speed codec transcoding**, **highlights generation**, **video frame capturing**, **video to animated image conversion**, **video watermark**, **audio/video splicing**, **voice/sound separation**, **video enhancement**, **super-resolution**, **image processing**, and **broadcast media format transcoding**.

### Audio/Video transcoding

The audio/video transcoding feature converts an audio/video file bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt to different devices and network conditions. You can customize the template parameters in a custom audio/video transcoding template.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Audio/Video Transcoding** and click **Create Transcoding Template**.
![](https://main.qcloudimg.com/raw/44fd00fb33e98e396482b564a7bbf91f.png)
6. In the **Create Transcoding Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Transcoding Type: You can select video or audio transcoding.
 - Container Format: Video transcoding supports the MP4, FLV, HLS, TS, MKV, and WebM formats. Audio transcoding supports the MP3, AAC, AMR, FLAC, and WebM formats.
 - Transcoding Duration: You can select the input file duration or customize the duration.
 - Audio/Video Parameters: You can customize audio/video parameters as needed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating an audio/video transcoding job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>

### Top speed codec transcoding

The top speed codec transcoding feature improves the subjective image quality of a video at a low bitrate. Compared with regular audio/video transcoding, it outputs smaller files and clearer video images and delivers a better visual experience with guaranteed low network resource usage. You can customize parameters such as codec, resolution, and bitrate in a custom top speed codec transcoding template.


#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Top Speed Codec Transcoding** and click **Create Top Speed Codec Transcoding Template**.
<img src="https://main.qcloudimg.com/raw/2c30fe3def5a1d823308fd8197053cbc.png" style="zoom:67%;" />
6. In the **Create Top Speed Codec Transcoding Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Transcoding Type: It is video transcoding by default.
 - Container Format: Supported formats include MP4 and HLS.
 - Transcoding Duration: You can select the input file duration or customize the duration.
 - Audio/Video Parameters: You can customize audio/video parameters as needed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a top speed codec transcoding job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>

### Broadcast media format transcoding

This feature processes special formats such as XAVC and ProRes.


#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Broadcast Media Format Transcoding** and click **Create Broadcast Media Format Transcoding Template**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5704ca5edb3bd3c2e8d8adb199870a46.png" style="zoom:67%;" />
6. In the **Create Broadcast Media Format Transcoding Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Preset Encoder Configuration: Select the default values of encoder parameters such as sample rate.
 - Container Format: Supported formats include MXF.
 - Transcoding Duration: You can select the input file duration or customize the duration.
 - Audio/Video Parameters: You can customize audio/video parameters as needed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a broadcast media format transcoding job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).


### Highlights generation

The highlights generation feature automatically extracts highlights from a video. You can use a custom template to set the highlights generation template name and specify the maximum duration, resolution, and format of the output highlight video.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Highlights Generation** and click **Create Highlights Generation Template**.
<img src="https://main.qcloudimg.com/raw/55654c6c7d2975647c5e64c483d42596.png" style="zoom:80%;" />
6. In the **Create Highlights Generation Template** window, configure the following items:
>? Currently, highlights generation can be used only for landscape, food, street, and vlog scenarios and will support more scenarios in the future. If you want to customize this feature, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
>
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Container Format: Supported formats include MP4, FLV, HLS, TS, and MKV.
 - Highlight Video Duration: You can select the duration of the complete output highlight video after automatic analysis or customize the duration.
 - Audio/Video Parameters: You can customize audio/video parameters as needed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a highlights generation job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>



### Video frame capturing

The video frame capturing feature captures the frames of a video at specified time points. The output screenshots are in JPG format by default. If you enable captured frame compression, screenshots can be output in HEIF or TPG format. You can customize the template name, frame capturing start time, frame capturing interval, captured frames, and output image size and format in a custom video frame capturing template.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Video Frame Capturing** and click **Create Video Frame Capturing Template**.
![](https://main.qcloudimg.com/raw/158fccdefdbdb21850eb751e9e27c9a5.png)
6. In the **Create Video Frame Capturing Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Frame Capturing Start Time: You can select any time point within the full video length.
 - Frame Capturing Method:
    - All frames will be captured by default: Every video frame will be captured.
    - Custom Frame Capturing Interval: Frames will be captured at specified time intervals from the frame capturing start time to the end of the video.
    - Even Frame Capturing: Frames will be captured at even intervals calculated based on the specified **number of captured frames** from the frame capturing start time to the end of the video.
    - Capture Keyframes: Capture only keyframes.
 - Max Frame Count Per Video: This parameter is required if you select **All frames will be captured by default**, **Custom Frame Capturing Interval**, or **Capture Keyframes** as the frame capturing method.
 - Captured Frames: This parameter is required if you select **Even Frame Capturing** as the frame capturing method. Frames will be captured at even intervals calculated based on the specified number of frames captured from the frame capturing start time to the end of the video.
 - Output Image Size: The default output screenshot size is the same as that of the original video image. If you select custom image size, you must enter an integer between 128 and 4096 for the width and height respectively.
 - Video Frame Compression: If it is enabled, captured images can be compressed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a video frame capturing job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>

### Video to animated image conversion

The video to animated image conversion feature converts a video to animated images. You can customize the template name, transcoding start time, transcoding duration, frame extraction method, output animated image frame rate, and output animated image size in a custom video to animated image conversion template.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Video to Animated Image Conversion** and click **Create Video to Animated Image Conversion Template**.
![](https://main.qcloudimg.com/raw/1c17fcb61438b2f33f95b4bc922318fb.png)
6. In the **Create Video to Animated Image Conversion Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Transcoding Start Time: You can select any time point within the full video length.
 - Transcoding Duration: It specifies the duration of video transcoding after the **transcoding start time**. You can select **Original Video Duration** or **Custom Duration**.
 - Frame Extraction Method:
     - Extract all frames: Every video frame will be extracted.
     - Frame Extraction Frequency: You can set the number of frames to be extracted per second (an integer between 1 and 50).
     - Frame Extraction Interval: Frame will be extracted at the specified intervals in seconds.
     - Extract key frames only: The system will intelligently identify and extract the optimal set of frames based on AI understanding of the video content and output them as an animated image.
 - Output Animated Image Frame Rate: If **Adaptive** is selected, the system will automatically select an appropriate frame rate based on the settings of the above parameters. You can also select **Custom Playback Frame Rate** to restrict the frame rate to 1–60 FPS.
 - Output Animated Image Format: The output animated image is in GIF format by default. If you select the WEBP format, you need to select the animated image quality, which ranges from 1 to 99 and is 75 by default.
 - Output Animated Image Size: The default output animated image size is the same as that of the original video. If you select custom width and height, you must enter an integer between 128 and 4096 for the width and height respectively. 
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a video to animated image conversion job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>

### Video watermark

The video watermark feature adds a text or image watermark to a video during transcoding.

>? Currently, you can add up to three watermarks in the console or five via API at a time. To add more watermarks, [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.
>

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Video Watermark** and click **Create Video Watermark Template**.
![](https://main.qcloudimg.com/raw/f94daf7e8ad67c4616f6cf3ba17b8bb1.png)
6. In the **Create Video Watermark Template** window, configure the following items:
 - **Common parameters**
    - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (\*).
    - Watermark Type: Select image or text watermark.
    - Origin Point: Select the top-left, top-right, bottom-left, or bottom-right corner.
    - Opacity: Select a value between 1% and 100%.
    - Offset Method: The watermark offset is based on the origin point. You can select offset by ratio or fixed position.
    - Watermark Duration: Select **Same as video duration** or **Specified period**. If you select the latter, you can set the watermark start time and end time. If you set the start time only, the watermark will be displayed until the video ends by default.
 - **Image watermark parameters**
    - Select Image: If you select image watermark, you need to select its source. Currently, only a watermark image in the same bucket can be selected. If the bucket doesn't have desired images, you need to upload a new one.
    - Image Layer: Select whether to place the image on top of or underneath the video.
      - If the image is placed on top of the video, the effect is as shown below:
     ![img](https://main.qcloudimg.com/raw/b3d8ba30e161104704076329338fe364.png)
       - If the image is placed underneath the video (as the background), the effect is as shown below:
     ![img](https://main.qcloudimg.com/raw/5e6a97ccd0f178f52ea52e93e4ad9f4c.png)
    - Watermark Dimensions:
      - Input image size: The original watermark image size will be retained without any processing. Note that if the watermark image is larger than the video image, the watermark cannot be completely displayed.
      - By ratio: You can set the percentage (1–100) of only the width or height or both of them. If the width or height is not set, it will be scaled proportionally. Suppose the width ratio is `a` and height ratio is `b`, then the watermark width will be `w = W * a`, and the watermark height will be `h = H * b` (here, `W` and `H` are the video width and height respectively).
      - Fixed size: You can specify the watermark width and height between 8 and 4096 px.
    - Offset Method (On top of video):
      - By ratio: You can set the percentage (0–100) of the width or height. As shown below, suppose the horizontal offset ratio is `a` and the vertical ratio is `b`, then the horizontal offset will be `Dx = W * a`, and the vertical offset will be `Dy = H * b` (here, `W` and `H` are the video width and height respectively).
      - Fixed position: Select a value between 0 and 4096 px. The horizontal offset is `Dx`, and the vertical offset is `Dy`.
     - Watermark Dimensions:
       - Input image size: The original watermark image size will be retained without any processing. Note that if the watermark image is smaller than the video image, the watermark cannot be completely displayed.
       - By ratio: You can set the percentage (100–300) of only the width or height or both of them. If the width or height is not set, it will be scaled proportionally. Suppose the width ratio is `a` and height ratio is `b`, then the watermark width will be `w = W * a`, and the watermark height will be `h = H * b` (here, `W` and `H` are the video width and height respectively).
      - Fixed size: You can specify the watermark width and height between 8 and 4096 px.
    - Offset Method (Underneath video):
      - By ratio: You can set the percentage (-300–0) of the width or height. As shown below, suppose the horizontal offset ratio is `a` and the vertical ratio is `b`, then the horizontal offset will be `Dx = W * a`, and the vertical offset will be `Dy = H * b` (here, `W` and `H` are the video width and height respectively).
      - Fixed position: Select a value between -4096 and 0 px. The horizontal offset is `Dx`, and the vertical offset is `Dy`.
 - **Text watermark parameters**
    - Watermark Text: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
    - Font Size: Select a value between 5 and 100 px.
    - Font: Select Ariblk, Arial, Ahronbd, Helvetica, or HelveticaNeue.
    - Font Color: It is in the format of `0xRRGGBB`.
7. Click **OK**.
 - After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
 - You can click **Preview** to view the position and dimensions of the watermark in videos of three common resolutions and quickly adjust the template.

>? You can use the template when [creating an audio/video transcoding, SDR to HDR, video enhancement, or super-resolution job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>

### Audio/Video splicing

The video/audio splicing feature adds the specified video/audio segment at the beginning or end of a video/audio file to generate a new one.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Audio/Video Splicing** and click **Create Audio/Video Splicing Template**.
![](https://main.qcloudimg.com/raw/b865a18aec0626bc08c309bfc9487df1.png)
6. In the **Create Audio/Video Splicing Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (\*).
 - Container Format: Supported formats include AAC, MP3, MP4, FLV, HLS, and TS.
 - Splicing Position: Select whether to add the file at the beginning or end of the source file.
 - Other parameters: You can customize the audio/video parameters as needed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating an audio/video splicing job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>


### Voice separation

You can separate the same audio file into a voice file and a background sound file for subsequent video editing and playback.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Voice Separation** and click **Create Voice Separation Template**.
<img src="https://main.qcloudimg.com/raw/03d049a8fe3ef91821501e82be1a6190.png" style="zoom:67%;" />
6. In the **Create Voice Separation Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Output Audio Format: Supported formats include MP3, AAC, AMR, and FLAC.
 - Output Audio: Specify to output voice or background sound.
 - Sample Rate: Select an option as needed.
 - Audio Bitrate: Enter a value as needed.
 - Channels: Select an option as needed.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a voice separation job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).



### Video enhancement

The video enhancement feature uses AI to improve the video quality and enhance the video colors and details visually.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Video Enhancement** and click **Create Video Enhancement Template**.
![](https://main.qcloudimg.com/raw/11a7381c7a634048f0b317940806bb53.png)
6. In the **Create Video Enhancement Template** window, configure the following items:
> ? 
> - Currently, video enhancement supports color and detail enhancement. Other features will be provided in the future.
> - The input video for enhancement must be shorter than 30 minutes.
> 
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Color Enhancement: Select automatic system analysis for color enhancement or customize the color enhancement parameters.
 - Detail Enhancement: Select automatic system analysis for detail enhancement or customize the detail enhancement parameters.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a video enhancement job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>

### Super-resolution

The super-resolution feature reconstructs the details and local features of an image by recognizing its content and contour so as to generate a high-resolution image through a series of low-resolution images.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Super-Resolution** and click **Create Super-Resolution Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/6f0634a392449df73a2d937515242bfb.png)
6. In the **Create Super-Resolution Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Version: Select Basic or Enhanced. The latter delivers greater image reconstruction and restoration effects.
 - Target Resolution: Select the output resolution.
 - Target Zoom: After it is enabled, the output video will be zoom to the selected target resolution or three times the input video resolution.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating a super-resolution job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>


### Image processing

Image processing is a rich-featured, cost-effective, and high-reliability image processing service provided by CI. It supports flexible image editing, such as rotation, cropping, transcoding, and zooming. It provides multiple image downsizing solutions like Guetzli compression, TPG transcoding, and HEIF transcoding, as well as diversified copyright protection solutions like image/text/blind watermarking. This meets your image processing needs in different business scenarios.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Select **Bucket List** on the left sidebar.
3. Click the name of the bucket for video storage.
4. On the left sidebar, select **Data Processing Workflow** > **Common Configuration**. Then, select the **Template** tab to go to the template configuration page.
5. Select **Video Processing** and click **Create Video Processing Template**.
![](https://qcloudimg.tencent-cloud.cn/raw/36a2f7f47b7e8dac12e5f128e7ea7c81.png)
6. In the **Create Video Processing Template** window, configure the following items:
 - Template Name: It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).
 - Editing Mode: Select Basic or Enhanced. The latter delivers greater image reconstruction and restoration effects.
 - Basic Processing: Select the output target resolution.
 - Text Watermark: After it is enabled, you can add a single or tiled watermark to the image.
 - Image Watermark: After it is enabled, you can add an animated or static watermark at the specified position on the image.
 - Preview: You can preview the processing effect.
7. Click **OK**.
After successfully creating the template, you can **view**, **edit**, or **delete** it in the custom template list.
>? You can use the template when [creating an image processing job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408).
>
