# Overview

StreamLive is a premium stream processing platform newly launched by Tencent Cloud, which provides broadcast-grade live stream processing services. It enables you to create high-quality video streams and distribute them to various types of devices.

StreamLive uses Tencent Cloud's proprietary high-performance video encoding and compression algorithms to reduce transfer traffic consumption while delivering a better watch experience. In addition, it guarantees a 24/7 availability.

![](https://main.qcloudimg.com/raw/b007110c97f491fb447302763ad85b20.png)

# Features

**Multi-Protocol and Multi-Format Stream Input**

StreamLive supports multiple streaming protocols such as RTP, RTMP, UDP, HLS, HTTP-MP4, and RTP-FEC. It provides both pull and push input methods. When RTP MPEG-TS is used, StreamLive allows the video stream input with multiple audio tracks (language type) and can transcode each track separately.

**High-Quality and Multi-Format Transcoding**

StreamLive supports transcoding at different resolutions (SD, HD, UHD, 2K, 4K, etc.), bitrates, and frame rates. It also provides high-performing Top Speed Codec Transcoding. After this feature is enabled, AI algorithms can calculate the optimal dynamic encoding parameters in real time based on business scenarios, and implement low-bitrate as well as high-quality transcoding services.

**Digital Rights Management (DRM)**

StreamLive offers a specialized digital rights management (DRM) solution to fully protect your video assets. It supports FairPlay and Widevine encryption technologies, meeting the needs for digital copyright protection.

**Multi-Protocol and Multi-Method Output**

StreamLive supports various output muxing types, such as adaptive bitrate HLS, DASH, COS ARCHIVE, and StreamPackage.

**Flexible Configuration for Independent Channels and Diverse Output Combinations**

StreamLive provides services based on channel management, where the same channel can be configured with different inputs and outputs. You can associate an output with existing audio and video transcoding templates, configuring flexible output combinations to implement adaptive bitrate video delivery.

**Stream Quality Monitoring**

StreamLive offers detailed health reports about the running status of each channel and displays alerts, allowing you to check video stream quality in real time.

**High Performance**

Under the dual standards of SSIM and VMAF, Tencent Cloud Top Speed Codec Transcoding greatly outperforms AWS Elemental MediaLive Quality-Defined Variable Bitrate.

**Low Costs**

The characteristics of Top Speed Codec Transcoding meet the needs of customers for reducing the CDN bandwidth costs, which can still deliver a leading performance when the bitrate is reduced by about 10%.

**Architecture Design**

Each StreamLive channel supports dual-pipeline input configuration at the beginning of the input configuration, where pipeline A is required and pipeline B is optional.

Pipeline A and pipeline B operate independently, that is, the streams from input A will be output to the destination A of each output group, while the streams from input B will be output to the destination B of each output group.

![](https://main.qcloudimg.com/raw/ec3ea24ca723cdb08f3b8f35d339b6ff.png)