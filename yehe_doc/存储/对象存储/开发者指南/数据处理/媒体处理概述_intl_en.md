## Overview

Media processing is a multimedia file processing service provided by COS based on CI. It offers diverse features empowered by Tencent Cloud's cutting-edge AI technology, such as audio/video transcoding, video frame capturing, and intelligent thumbnail.

| Feature | Description |
| -------------- | ------------------------------------------------------------ |
| Audio/Video transcoding | Converts an audio/video file bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt to different devices and network conditions. |
| TESHD transcoding   | Provides transcoding capabilities that make videos smaller and clearer. It integrates a complete set of video processing solutions such as image remastering and enhancement, adaptive content parameter selection, and V265 encoder to deliver a better visual experience with guaranteed low network resource usage. |
| Professional media format transcoding   |  Can transcode special formats such as XAVC and ProRes.  |
| Video montage       | Accurately extracts highlights from a video by recognizing and aggregating the video content, postures, and scenes and quickly clipping them professionally. |
| Video enhancement       | Optimizes the video image quality and enhances the visual effect through a series of features, including details enhancement, color enhancement, and SDR-to-HDR. |
| Super resolution       | Reconstructs the details and local features of a video by recognizing its content and contour so as to generate a high-resolution video image through a series of low-resolution video images. It can be used in combination with video enhancement to remaster old videos. |
| Custom function processing | Helps you flexibly and quickly implement customized services on demand, accelerate the development, reduce costs, and increase the efficiency. |
| Video encryption | Encrypts video data through HLS standard encryption to ensure the video security. |
| Video tagging | Accurately recognizes video content and automatically outputs multidimensional content tags by analyzing the visuals, scenes, behaviors, and objects in the video based on multi-modal information fusion and alignment technologies. |
| Text to speech | Converts text to natural-sounding and smooth speeches in a variety of voices through advanced deep learning technology. |
| Voice/Sound separation       | Separates the human voice and background sound in a specified video (or audio) to generate audio materials for subsequent artistic processing of other styles. |
| Adaptive HLS muxing  | Generates a multi-bitrate adaptive file from a raw video to adapt the video to different devices and network conditions. |
| HDR-to-SDR | Makes the image details of the output video as close as possible to those of the original video to adapt to different types of devices and avoid image distortion and darkness.    |
| Video frame capturing   | Captures the frames of a video at specified time points. You can customize the start time point of frame capturing, frame capturing interval, number of frames to be captured, and output image size and format to meet your diversified needs. |
| Audio/Video splicing | Adds a video/audio segment at the beginning or end of a video/audio file to generate a new one. |
| Audio/Video segmentation | Divides a video/audio file into several segments. |
| Video to animated image conversion | Converts a video file into an animated image file. You can specify the video segment for conversion, frame sampling method, as well as the frame rate, size, and format of the output animated image to meet your different needs. |
| Intelligent thumbnail | Intelligently analyzes the quality, brilliance, and content relevance of video frames by understanding the video content with Tencent Cloud's advanced AI technologies. Then, it extracts optimal frames to generate thumbnails to make the content more engaging. |
| Video metadata acquisition | Gets the metadata of media files such as videos, audios, and subtitles stored in COS, including video file's encoding format, codec, pixel format, duration, bitrate, frame rate, width, and height, audio file's bitrate, sample format, sample rate, number of channels, and duration, as well as subtitles' language. This helps meet your needs for various media information. |



## Use Cases

#### Multi-device adaptability

As content platforms are generally intended for multiple types of devices, they need to provide media files in different formats for different users. The audio/video transcoding feature covers most transcoding needs and provides diversified compression capabilities to increase the compression efficiency and downsize files. This reduces lags, storage space usage, and traffic fees.

#### Video platform

For traditional video platforms, reviewers need to watch videos and then manually select thumbnails, which is labor consuming and slows down video release.

The intelligent thumbnail feature can quickly select the most striking frames as thumbnails, which saves labor resources and accelerates video release.

The video to animated image conversion feature allows you to select the highlights in a video on your video platform to convert them into an animated image for video preview, so that users can get a glimpse of the video without playing it back. Compared with traditional static video thumbnails, animated image thumbnails increase the click rate and video playbacks.

## How to Use

You can use media processing features through [job](https://intl.cloud.tencent.com/document/product/436/46409) or [workflow](https://intl.cloud.tencent.com/document/product/436/46408). To increase the efficiency and reduce repeated operations, for the features of audio/video transcoding, audio/video splicing, video frame capturing, and video to animated image conversion, you can specify a template when creating a job or workflow. The template page provides [preset system templates](https://intl.cloud.tencent.com/document/product/436/46411), and you can also [customize templates](https://intl.cloud.tencent.com/document/product/436/46411) based on your business needs.

### Job

You can create a media processing job for existing data stored in COS.

#### Managing job

- Console: You can create jobs visually in the COS console as instructed in [Configuring Job](https://intl.cloud.tencent.com/document/product/436/46409).
- API: You can create, delete, query, and search for media processing jobs through APIs as instructed in [Job APIs](https://www.tencentcloud.com/document/product/436/49192).

### Workflow

With a media processing workflow, you can quickly and flexibly create audio/video processing flows as needed. A workflow is bound to a path of an input bucket. When a file is **uploaded** to the path, the media workflow will be **automatically triggered** to perform the specified processing operation, with the processing result automatically saved to the specified path of the output bucket. You can set **audio/video splicing**, **audio/video transcoding**, **video frame capturing**, **video to animated image conversion**, and **intelligent thumbnail** jobs in a workflow.

#### Managing workflow

- Console: You can create workflows visually in the COS console as instructed in [Configuring Workflow](https://intl.cloud.tencent.com/document/product/436/46408).
- API: You can create, delete, query, and search for media processing workflows through APIs as instructed in the API documentation.

