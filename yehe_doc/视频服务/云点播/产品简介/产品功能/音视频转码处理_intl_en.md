## System Architecture
<img src="https://mc.qcloudimg.com/static/img/962be55d993d07eee39c66d27fd778fe/image.png" width="650">

## Features
### Audio/Video transcoding
The transcoding feature converts a video bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, for playback on different devices in various network environments. For more information, please see [Transcoding](https://intl.cloud.tencent.com/document/product/266/33938). The following benefits can be achieved with transcoding:
- The distributed transcoding system of VOD supports multipart transcoding, elastic scalability of transcoding resources, and dynamic capacity expansion to meet the needs of custom transcoding in various scenarios.
- VOD supports all mainstream formats, multiple resolutions, and multiple bitrates. It features flexibly configurable transcoding templates and custom watermarking.
- VOD can intelligently analyze video metadata to select the optimal transcoding template accordingly and call back the transcoding result promptly.
- VOD supports H.265 transcoding, 4K transcoding, HDR transcoding, and video transcoding to GIF.


### Audio/Video editing
Audio/Video editing includes video splicing and editing features as detailed below:
- VOD enables you to create audio/video clips of a specified duration starting at a specified time point and splice multiple video files.
- VOD supports time point screencapturing, sampled screencapturing, and image sprite generating.
- VOD supports deleting audio track from video.


### Video DRM encryption
The digital rights management (DRM) feature of VOD supports commercial-grade encryption of videos as detailed below:
- VOD supports DRM encryption for protecting digital copyright and encrypts video content with the AES-128 algorithm.
- VOD supports encryption in all HLS players and provides customized and personalized video encryption services.


### Video AI
The video AI of VOD has various AI-powered features such as video audit, intelligent video recognition, and intelligent video analysis as detailed below:
- VOD leverages YouTu's DeepEye intelligent porn detection technology to identify porn images and videos on your video platform, helping you greatly improve the coverage and efficiency of your fight against pornography and avoid the risk of being involved in distributing porn information in your business.
- Currently, the accuracy of porn image recognition by the DeepEye engine has reached over 65% at a 0.01% FAR and over 80% at a 0.1% FAR.
- Based on in-depth understanding of audio/video content, VOD is capable of searching for multiple elements such as tags, figures, phrases, scenes, and objects, helping you improve the availability of media assets and quickly locate desired video content.
- VOD can generate distinctive tags and covers quickly for your audio/video content to increase the efficiency of recommendation service.


### Adaptive bitrate streaming
Adaptive bitrate streaming refers to the process of transcoding a video and muxing it into adaptive bitstream for output. It involves audio/video files with various bitrates and a descriptive file (manifest).

A player can dynamically select the most appropriate bitrate for playback based on the current bandwidth. The adaptive bitrate streaming parameters can specify "video transcoding parameter" and "audio transcoding parameter" of each substream. VOD uses an adaptive bitrate streaming template to represent the set of parameters for easy configuration. For more information, please see [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942). Specifically,
- VOD can dynamically select the appropriate bitrate for playback based on the changes in the network bandwidth of devices, helping you conserve bandwidth while delivering a smoother viewing experience.
- VOD supports customizing video and audio parameters to meet your diverse needs.
- VOD supports multi-resolution, multi-bitrate substream modes that can be configured easily and flexibly.


### TESHD
The Tencent Extreme Speed High Definition (TESHD) feature of VOD uses video AI algorithms to recognize videos based on video scene category and selects the optimal encoding parameters by accessing various factors such as original bitrate, frame rate, resolution, texture, motion variation, server load, and ROI detection, which can effectively improve the video quality and reduce bandwidth loss.

Leveraging the intelligent dynamic encoding technology integrated with intelligent scenario recognition, dynamic encoding matching, and image quality restoration and enhancement, TESHD enables video businesses such as live video broadcasting and video on demand to provide higher-definition streaming services at lower bitrates, thereby delivering a new HD video experience.
