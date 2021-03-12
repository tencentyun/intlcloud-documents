# Product Features
This document describes the product features of MediaLive.
#### Multi-Protocol and multi-method stream input
MediaLive supports multiple streaming protocols such as RTP, RTP-FEC, RTMP, UDP, HLS, and HTTP-MP4. It provides both pull and push input methods. When RTP-MPEGTS is used, MediaLive allows inputting the video stream with multiple audio tracks and can transcode each track separately.


#### Authentication with security group
MediaLive provides protection policies for input streams at the CIDR security group level. A security group can verify the input’s IPv4 address and enhance the security of MediaLive channels.


#### Diversified transcoding
MediaLive supports transcoding at different resolutions (SD, HD, UHD, 2K, 4K, etc.), bitrates, and frame rates. It also provides high-performing top speed codec transcoding. After this feature is enabled, AI algorithms can calculate the optimal dynamic encoding parameters in real time based on business scenarios, and implement low-bitrate as well as high-quality transcoding services.


#### Remuxing in multiple formats
MediaLive supports various output muxing types, such as adaptive bitrate muxing protocols of HLS and DASH.


#### Live stream archiving
 MediaLive supports exporting HLS files to COS for archiving. After configuring the output type, you can output the specified live stream to be archived in COS for video processing later on.


#### DRM
MediaLive features a professional digital rights management (DRM) solution to comprehensively protect the security of your video assets. Currently, it supports the FairPlay and Widevine encryption schemes to satisfy most needs in digital copyrights protection.


#### Flexible configuration for independent channels and diverse output combinations
MediaLive provides services based on channel management, where the same channel can be configured with different inputs and outputs. You can associate an output with existing audio and video transcoding templates, configuring flexible output combinations to implement adaptive bitrate video delivery.


#### Stream quality monitoring
MediaLive offers detailed health reports on the running status of each channel and displays various types of alerts, making it easy for you to monitor the stream quality in real time.


#### Easy Integration with Tencent Cloud Services
MediaLive supports outputting live stream to specified destination and can also integrate with Tencent Cloud services (MediaPackage, MediaConnect, LVB CDN, etc.) to implement broadcast-grade one-stop media services at large-scales.
