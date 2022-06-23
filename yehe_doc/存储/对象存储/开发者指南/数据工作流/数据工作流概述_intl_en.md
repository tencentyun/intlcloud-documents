## Overview

Data workflow is a new data processing service launched by COS. It offers two features: workflow and task.

- Workflow: With the workflow feature, you can quickly and flexibly create data processing processes as needed. A workflow is bound to a path of an input bucket. When a file is **uploaded** to the path, the workflow will be **automatically triggered** to perform the specified processing operation, with the processing result automatically saved to the specified path of the output bucket.
- Task: For files in a bucket, you can create tasks to perform data processing operations.
- Template: When using data workflows, you usually need to set a series of parameters, which can be combined through a template. This **simplifies your operations** and allows you to reuse the configured parameters with no need to enter them repeatedly.
>? For audio/video transcoding, audio/video splicing, video frame capturing, and animated image generation, you need to specify a template when creating a task or workflow, which can be either a **preset** or **custom** one.
>
- Queue and callback: When you activate the data workflow service, the system will **automatically create** a user queue for you. When you submit a task, the task will be arranged in the queue first and executed in sequence according to the priority and order of submission. You can also set a **callback rule** to stay up to date with the task or workflow progress, and the system will send the processing result and status information to the specified address.

The processing operations currently supported by data workflow include:

| Operation   | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| Audio/Video transcoding | Converts an audio/video file bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt to different devices and network conditions. |
| TESHD transcoding   | Provides transcoding capabilities that make videos smaller and clearer. It integrates a complete set of video processing solutions such as image remastering and enhancement, adaptive content parameter selection, and V265 encoder to deliver a better visual experience with guaranteed low network resource usage. |
| Professional media format transcoding   |  Can transcode special formats such as XAVC and ProRes.  |
| Video enhancement       | Optimizes the video image quality and enhances the visual effect through a series of features, including details enhancement, color enhancement, and SDR to HDR conversion. |
| Super-resolution       | Reconstructs the details and local features of a video by recognizing its content and contour so as to generate a high-resolution video image through a series of low-resolution video images. It can be used in combination with video enhancement to remaster old videos. |
| Highlight generation       | Accurately extracts highlights from a video by recognizing and aggregating the video content, postures, and scenes and quickly clipping them professionally. |
| Voice/Sound separation       | Separates the human voice and background sound in a specified video (or audio) to generate audio materials for subsequent artistic processing of other styles. |
| Adaptive HLS muxing  | Generates a multi-bitrate adaptive file from a raw video to adapt the video to different devices and network conditions. |
| HDR to SDR conversion | Makes the image details of the output video as close as possible to those of the original video to adapt to different types of devices and avoid image distortion and darkness.    |
| Video frame capturing   | Captures the frames of a video at specified time points. You can customize the start time point of frame capturing, frame capturing interval, number of frames to be captured, and output image size and format to meet your diversified needs. |
| Audio/Video splicing | Adds a video/audio segment at the beginning or end of a video/audio file to generate a new one. |
| Audio/Video segmentation | Divides a video/audio file into several segments of the specified duration. |
| Animated image generation | Converts a video file into an animated image file. You can specify the video segment for conversion, frame sampling method, as well as the frame rate, size, and format of the output animated image to meet your different needs. |
| Intelligent thumbnail generation   | Intelligently analyzes the quality, brilliance, and content relevance of video frames by understanding the video content with Tencent Cloud's advanced AI technologies. Then, it extracts optimal frames to generate thumbnails to make the content more engaging. |
| Speech recognition   | Recognizes an audio recording file and returns the recognized text asynchronously. Currently, the supported languages include Mandarin, English, and Cantonese. Meanwhile, Cloud Infinite (CI) can help you process the recognition result, such as blocking impolite words, filtering interjections, and intelligently converting numbers to words, meeting your various speech recognition needs. |
| File preview   | Allows you to preview files of nearly 30 types through image or HTML online, with the source file style preserved as much as possible. This addresses the lack of support for certain file formats on different devices and enables online file preview on PC, app, and other terminals. |
| Image processing   | Supports flexible image editing, such as rotation, cropping, transcoding, and zooming. It provides multiple image downsizing solutions like Guetzli compression, TPG transcoding, and HEIF transcoding, as well as diversified copyright protection solutions like image/text/blind watermarking. This meets your image processing needs in different business scenarios. |

## Use Cases

#### Multi-device adaptability

As content platforms are generally intended for multiple types of devices, they need to provide media files in different formats for different users. The audio/video transcoding feature covers most transcoding needs and provides diversified compression capabilities to increase the compression efficiency and downsize files. This reduces lags, storage space usage, and traffic fees.

#### Video platform

For traditional video platforms, reviewers need to watch videos and then manually select thumbnails, which is labor consuming and slows down video release.

The intelligent thumbnail generation feature can quickly select the most striking frames as thumbnails, which saves labor resources and accelerates video release.

The animated image generation feature allows you to select the highlights in a video to convert them into an animated image for video preview, so that users can get a glimpse of the video without playing it back. Compared with traditional static video thumbnails, animated image thumbnails increase the click rate and video playbacks.

#### Video subtitles generation

A list of words and corresponding timestamps can be generated for audio files, which makes it easier to subtitle corresponding videos.

#### Meeting recording transcription

The minutes of large meetings are complex. If a meeting is lengthy and attended by many people, it would be more difficult to keep the complete minutes. The speech recognition feature of COS can recognize Mandarin, English, and Cantonese, which reduces the workload of taking meeting minutes and improves the meeting effect.

#### Online education

The file preview feature enables viewing various types of files such as courseware and handouts in online education, which delivers an easier user experience.

#### Website transcoding

The display of file content at websites is subject to browser rules. The file preview feature of COS allows generating images from multiple types of files for preview. This addresses the display problems of file content on webpages.

## Directions

### Through COS console

You can use the data workflow service in the COS console. For more information, see the documentation for [workflow](https://intl.cloud.tencent.com/document/product/436/46408)  and [task configuration](https://intl.cloud.tencent.com/document/product/436/46409).

### Through RESTful APIs

You can use APIs to manage workflows and tasks. For more information, see the data workflow API documentation.
