## Overview

For files already in a bucket, you can create a job for media processing, speech recognition, file processing, and other operations. Currently, the following jobs are supported: **audio/video transcoding**, **top speed codec transcoding**, **broadcast media format transcoding**, **highlights generation (also known as video montage)**, **voice separation (also known as voice/sound separation)**, **audio/video splicing**, **video enhancement**, **audio/video segmentation**, **super resolution**, **SDR to HDR**, **video frame capturing**, **video-to-animated image conversion**, **intelligent thumbnail**, **digital watermark extraction**, **image processing**, **text to speech**, **speech recognition**, and **file preview**, some of which can be created by template. You can use the preset templates or customize templates. For more information, see [Template](https://intl.cloud.tencent.com/document/product/436/46411).

>?
> - Currently, jobs can process 3GP, ASF, AVI, DV, FLV, F4V, M3U8, M4V, MKV, MOV, MP4, MPG, MPEG, MTS, OGG, RM, RMVB, SWF, VOB, WMV, WEBM, MP3, AAC, FLAC, AMR, M4A, WMA, and WAV files. When initiating a media processing request, you must enter the complete file name and extension; otherwise, the format cannot be recognized and processed.
> - Currently, the job feature can only manipulate **existing files**. To manipulate files during **upload**, use the workflow feature as described in [Configuring Workflow](https://intl.cloud.tencent.com/document/product/436/46408).
> - After a job is created, feature fees will be charged by CI. For billing details, see Media Processing Fees.
> 

## Viewing Job

On the job page, you can view all jobs in different types for the **specified time period**, click **Job Status** to filter and view jobs in different statuses, and search for jobs by job ID in the **search box**.

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Click **View** on the right of a job to view its information:

 - Job information: Job ID, job status, queue ID, template ID, job creation time, and job end time.
 - Input information: Source file bucket, region, and storage path.
 - Output information: Output file address, bucket, region, and storage path.

>? 
>- A job has six statuses: succeeded, failed, executing, pending, paused, and canceled.
>- You can query the records of jobs for the past month only.

## Creating Audio/Video Transcoding Job

The audio/video transcoding feature converts an audio/video file bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt to different devices and network conditions.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Audio/Video Transcoding** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/9b039ab7eb963c16e50d988e82203f48.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Transcoding Type**: Select **Standard**.
 - **Template Type**: Select preset or custom template.
 - **Template**: Select the specified template.
 - **Digital Watermark**: Add a blind watermark as needed for copyright protection.
 - **Watermark**: Add a visible image or text watermark as needed.
 - **Remove Watermark**: Remove the watermark.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output file.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Top Speed Codec Transcoding Job

The top speed codec technology improves the subjective image quality of a video at the minimum bitrate. Compared with standard transcoding, it makes videos smaller and clearer and delivers a better visual experience with low network resource usage.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Audio/Video Transcoding** as the job type, click **Create Job**, and configure as follows:

 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Transcoding Type**: Select **Top Speed Codec Transcoding**.
 - **Template**: Select the specified template.
 - **Digital Watermark**: Add a blind watermark as needed for copyright protection.
 - **Watermark**: Add a visible image or text watermark as needed.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output file.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Broadcast Media Format Transcoding

This feature produces videos in broadcast media formats such as Apple ProRes and Sony XAVC.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Audio/Video Transcoding** as the job type, click **Create Job**, and configure as follows:

 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Transcoding Type**: Select **Broadcast Media Format**.
 - **Template**: Select the specified template.
 - **Digital Watermark**: Add a blind watermark as needed for copyright protection.
 - **Watermark**: Add a visible image or text watermark as needed.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output file.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Highlights Generation Job

The highlights generation feature accurately extracts highlight segments from a video and outputs them as a new file for use in different scenarios subsequently, such as replay and preview.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Smart Editing > Highlights Generation** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/0414c8e582f5e5b4b9193109e773bb35.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Template**: Select the specified template.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output file.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Voice Separation Job

The voice separation feature separates the voice from the background sound in a video material to generate a new independent audio file. Then, you can apply artistic processing of other styles to the material without accompaniment and noise.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Smart Editing > Voice Separation** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/f67c60a206d904c69f9dcb6ad04d9b0e.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Template**: Select the specified template.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output file.
 - **Voice Filename**: Name of the output voice file.
 - **Background Sound Filename**: Name of the output background sound file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Text-to-Speech Job

The text to speech feature can convert text into natural-sounding and smooth speeches for use in smart customer service and audiobook scenarios.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Smart Editing > Text to Speech** as the job type, click **Create Job**, and configure as follows:

 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Template**: Select the specified template.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output file.
 - **Destination Filename**: Name of the output audio file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Audio/Video Splicing Job

The video/audio splicing feature adds the specified video/audio segment at the beginning or end of a video/audio file to generate a new one.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Audio/Video Splicing** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/53b1bdc8310e59e01e3bc2cdeb10acd4.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Template**: Select a created audio/video splicing template.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the output file.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Audio/Video Segmentation Job

The audio/video segmentation feature splits the specified audio/video file into several segments and outputs them in the specified container format.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Audio/Video Segmentation** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/b6ff7f0119085bed052b705306da4333.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Container Format**: Select the container format for the output segment.
 - **Segment Duration**: Specify the duration of the output segment.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the output file.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Video Frame Capturing Job

Video frame capturing is a screenshot feature provided by CI to capture the frames of a video at specified time points. After the job is enabled in the console, the output screenshots are in JPG format by default. If you enable captured frame compression, screenshots can be output in HEIF or TPG format.

>? A video frame capturing job can be created by template. You can customize the frame capturing start time, frame capturing interval, captured frames, output image size, and output format (captured frame compression needs to be enabled for this option) in a custom video frame capturing template.
>

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Video Frame Capturing** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/9b7322d5facc1b48cef33f9a1a77c729.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Template Type**: You can select preset or custom template. For more information, see [Template](https://intl.cloud.tencent.com/document/product/436/46411).
 - **Template**: Select the specified template.
 - **Output**: If the video frame capturing job is enabled in the console, screenshots in JPG format will be output by default. If captured frame compression is enabled in the template, screenshots in HEIF or TPG format can be output. If you use the video frame capturing API, you can choose to output JPG or PNG screenshots. For more information, see [Getting Media File Screenshot](https://intl.cloud.tencent.com/document/product/436/46912).
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the video screenshots.
 - **Destination Filename**: Name of the output file. Note that as more than one files are output by **smart video frame capturing**, the output filename must contain the ${Number} parameter as the sequence number of the screenshot. For example, if the destination file path is set to `test-${Number}.jpg` and the job captures two screenshots, the actual names of the output files will be `test-0.jpg` and `test-1.jpg`.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).



## Creating Video Enhancement Job

Video enhancement is a video image quality improvement feature provided by CI. You can use it to enhance and beautify image colors and improve the image details.

>? A video enhancement job can be created by template. You can customize the color and detail enhancement settings in a custom video enhancement template.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Image Quality Optimization > Video Enhancement** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/bcec587a60db669cc592a98aa6e2e6a3.png)
>? The input video must be shorter than 30 minutes.
>
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Enhancement Template**: Select a video enhancement template as needed.
 - **Transcoding Template Type**: You can select preset or custom template. For more information, see [Template](https://intl.cloud.tencent.com/document/product/436/46411).
 - **Transcoding Template**: You can select a transcoding template and specify parameters such as resolution, bitrate, and format of the output file.
 - **Digital Watermark**: Add a blind watermark as needed for copyright protection.
 - **Watermark**: Add a visible image or text watermark as needed.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output video.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).


## Creating Super Resolution Job

The super resolution feature reconstructs the details and local features of a video by recognizing its content and contour so as to generate a high-resolution video image through a series of low-resolution video images. It can be used in combination with video enhancement to remaster old videos.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Image Quality Optimization > Super Resolution** as the job type, click **Create Job**, and configure as follows:

 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Super Resolution Template**: Select the destination resolution template as needed.
 - **Transcoding Template Type**: You can select preset or custom template. For more information, see [Template](https://intl.cloud.tencent.com/document/product/436/46411).
 - **Transcoding Template**: You can select a transcoding template and specify parameters such as bitrate and format of the output file.
 - **Digital Watermark**: Add a blind watermark as needed for copyright protection.
 - **Watermark**: Add a visible image or text watermark as needed.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Path of the output video.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating SDR-to-HDR Job

SDR to HDR is a video dynamic range conversion feature provided by CI. You can use it to convert a standard dynamic range (SDR) video to a high dynamic range (HDR) video.

#### Directions


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Image Quality Optimization > SDR to HDR** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/40013de387fbc506b95d4e851825d819.png)
>? The input video must be shorter than 30 minutes.
>
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **HDR Standard**: Select HLG or HDR10.
 - **Transcoding Template**: Select an H.265 transcoding template. If there are no templates, create an audio/video transcoding template and select H.265 as the encoding format. For more information on how to create a template and configure parameters, see [Custom Template](https://intl.cloud.tencent.com/document/product/436/46411#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.A8.A1.E6.9D.BF).
 - **Watermark**: Add a visible image or text watermark as needed.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the destination file after the SDR-to-HDR conversion is completed.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).


## Creating Video-to-Animated Image Conversion Job

You can use the video-to-animated image conversion feature to convert a video to animated images.

>? A video-to-animated image conversion job can be created by template. You can customize the transcoding start time, transcoding duration, frame extraction method, output animated image frame rate, and output animated image size in a custom video to animated image conversion template.
>

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Transcoding > Video-to-Animated Image Conversion** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/12f93dfb3a9a6da63dbbf25ef88fba53.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Template Type**: You can select preset or custom template. For more information, see [Template](https://intl.cloud.tencent.com/document/product/436/46411).
 - **Template**: Select the specified template.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the animated images.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Intelligent Thumbnail Job

The intelligent thumbnail feature intelligently analyzes the quality, brilliance, and content relevance of video frames by understanding the video content with Tencent Media Lab's advanced AI technologies. Then, it extracts optimal frames to generate thumbnails to make the content more engaging.

>?
> - The intelligent thumbnail feature is a paid service and billed by the original video duration. For billing details, see Media Processing Fees.
> - Three optimal keyframes will be output through smart analysis of each video file.
> 

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Smart Editing > Intelligent Thumbnail** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/1c326c11491e108f62f111a72f98951b.png)
 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the smart thumbnails.
 - **Destination Filename**: Name of the output file.
>! As more than one files are output by **intelligent thumbnail**, the output filename must contain the parameter ${Number} as the thumbnail serial number. For example, if the output file path is set to `test-${Number}.jpg`, the actual names of the output files will be `test-0.jpg` and `test-1.jpg`.
>
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Digital Watermark Extraction Job

You can use the media processing service to extract the digital watermark from a watermarked video.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Media Processing** tab, select **Copyright Protection > Digital Watermark Extraction** as the job type, click **Create Job**, and configure as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/d06366d7bea0a7b3d612af4f1bd65090.png)
 - **Source File**: Enter the path of the source file, which must begin with but cannot end with `/`. Different folders are separated with `/`.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queue](https://intl.cloud.tencent.com/document/product/1045/43607).
   
## Creating Speech Recognition Job

The speech recognition feature recognizes a recording file and asynchronously returns the recognized text. It can be used for call center speech quality inspection, video subtitles generation, and meeting recording transcription.

#### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Speech Recognition** tab, click **Create Job**, and configure as follows:

 - **Source File URL**: Enter the path of the source file, which cannot begin or end with `/`.
 - **Recognition Engine**: Select a speech recognition engine. Different engines are as described below:
    - 8k_zh: Applies to telephone recording, 8 kHz audio sample rate, Mandarin.
    - 8k_zh_s: Applies to telephone recording, 8 kHz audio sample rate, Mandarin; supports audio separation by speaker.
    - 16k_zh: Applies to audio/video live streaming and video conferences, 16 kHz audio sample rate, Mandarin.
    - 16k_zh_video: Applies to audio/video live streaming, 16 kHz audio sample rate, Mandarin.
    - 16k_en: Applies to English audio, 16 kHz audio sample rate.
    - 16k_ca: Applies to Cantonese audio, 16 kHz audio sample rate.
 - **Sound Channels**: Select mono-channel or dual-channel.
 - **Recognition Result**: Speech recognition result text output by sentence or word (only supported for the Chinese speech recognition engines at 16 kHZ audio sample rate).
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the recognized text.
 - **Destination Filename**: Name of the output file.
 - **Filter Restricted Words**: Select whether to filter restricted words or replace them with `\*`.
 - **Filter Modal**: Select whether to filter modal.
 - **Smart Speech Conversion**: After it is enabled, recognized Chinese numbers will be converted to Arabic numbers.
 - **Queue**: Currently, only the default speech recognition queue `queue-speech-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
  - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).


## Creating File Preview Job

The file preview feature allows you to preview files of nearly 30 types online through image or HTML, with the source file style preserved as much as possible. This addresses the lack of support for certain file formats on different devices and enables easy online file preview on PC, app, and other terminals.

#### Directions


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **File Preview** tab, click **Create Job**, and configure as follows:

 - **Source File URL**: It cannot begin or end with `/`; for example, `doc/example.doc`.
 - **Preview Setting**: Select to preview whole document or specified page. A job supports up to 5,000 pages. If more pages are input, only the first 5,000 pages can be converted.
 - **Output Format**: Currently, JPG and PNG formats are supported for output images. The PDF format is supported only for whole document preview.
 - **Destination Bucket**: Select a bucket for which the file preview feature has been enabled in the current region.
 - **Destination Path**: It is optional. If it is not set, it will be the same as the input file path.
 - **Destination Filename**: The file preview service converts each page of the original file into an image. Therefore, you need to add a placeholder (`${Number}` or `${Page}`) to the output filename to number the output images. The output numbers are the same as the file page numbers. For example, if you want to preview a file with three pages and set the output filename to `output${Number}.jpg`, then three images `output1.jpg`, `output2.jpg`, `output3.jpg` will be output.
 - **Queue**: Currently, only the default file preview queue `queue-doc-process-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).

## Creating Image Processing Job

The image processing feature supports flexible image editing, such as rotation, cropping, transcoding, and scaling. It provides multiple image downsizing solutions like Guetzli compression, TPG transcoding, and HEIF transcoding, as well as diversified copyright protection solutions like image/text/blind watermarking. This meets your image processing needs in different business scenarios.

#### Directions


1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to manipulate.
4. On the left sidebar, select **Data Processing Workflow** and click **Job** to enter the job management page.
5. Select the **Image Processing** tab, click **Create Job**, and configure as follows:

 - **Input Bucket Name**: It is the current bucket by default.
 - **File Path**: Enter the path of the source file, which must begin with but cannot end with `/`. Different folders are separated with `/`.
 - **Template**: Select the specified template.
 - **Destination Bucket**: Select a bucket for which the media processing feature has been enabled in the current region.
 - **Destination Path**: Storage path of the image processing result.
 - **Destination Filename**: Name of the output file.
 - **Queue**: Currently, only the default queue `queue-1` is supported. For more information, see [Queues and Callbacks](https://intl.cloud.tencent.com/document/product/436/46412).
 - **Queue Callback URL**: Callback URL bound to the queue. You can configure it in the queue in [Common Configuration](https://www.tencentcloud.com/document/product/436/46412).
