## Overview

Adaptive bitrate streaming (ABR streaming) involves creating audio/video files with various bitrates. After using adaptive bitrate streaming, a player can dynamically select and play back the most appropriate bitrate based on the viewer’s current bandwidth. VOD can convert videos to mainstream adaptive bitrate streaming formats such as HLS and DASH.

| Capability | Description |
| -- | -- |
| Supported formats | HLS and DASH. |
| Ultra low-latency playback start | An adaptive bitrate stream contains multiple resolutions. The player generally starts playback at a low resolution to help playback start faster. |
| Smart resolution switch | The player dynamically selects the most appropriate resolution for playback based on the current bandwidth. |
| Zero-lag switch | The frames of each resolution in the adaptive bitrate stream are aligned, so there is no lag when resolution is switched. |
| FHD image and audio | <li>Up to 8K FHD resolution is supported.</li><li>Stereo is supported.</li><li>HDR is supported.</li>|
| Advanced encoding technology | You can use advanced encoding formats such as H.265, H.266, and AV1 and Top Speed Codec transcoding to reduce the video bitrate. |
| Support for encryption and DRM | DRM copyright protection schemes such as media encryption, Widevine, and FairPlay all depend on adaptive bitrate streaming. |


>! Differences between **adaptive bitrate streaming** and **transcoding**:
>- An adaptive bitrate streaming URL contains outputs in multiple resolutions, while a transcoding URL contains an output in only one resolution.
>- When adaptive bitstreams are played back, the player will switch to the optimal resolution in real time based on current network conditions, while videos output by transcoding do not support intelligent resolution switching during playback.

## Use Cases

| Use Case | Description |
| -- | -- |
| Online education | In online education scenarios such as subject teaching and training courses, videos usually need to be encrypted or copyright protected based on DRM. |
| Video website | Video websites have rich video resources, and adaptive bitrate streaming can deliver a smoother viewing experience.  |
| Online TV | Online TV platforms may need to protect their resources. In addition, viewers may want to switch to a higher resolution while watching a video. |

## Directions

For detailed directions, see [Transcoding to Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942).
