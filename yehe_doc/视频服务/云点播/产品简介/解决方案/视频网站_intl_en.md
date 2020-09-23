## Video Encryption Scenario
### Foreword
The entire video service industry (including various scenarios such as video website, video portal, and online education) requires secure and reliable video on demand services. In addition, as users are getting more and more aware of copyright protection, the needs for video encryption also grows. To this end, Tencent Cloud VOD provides a video encryption scheme that can be built quickly and deliver a smooth watch experience.

In video encryption scenarios, VOD combines hotlink protection, encrypted adaptive bitrate streaming, and superplayer features, enabling you to quickly integrate the player into your mobile and web clients for easy implementation of various capabilities such as definition switch, thumbnail preview, video preview, and encrypted playback. Backed by the powerful backend of VOD, you can easily provide end-to-end video services ranging from video upload and transcoding to delivery acceleration and playback. In addition, VOD also has the following features:
- Hotlink protection can be enabled for playback control before video playback at video websites so as to guarantee video security.
- The network environments of applications are complex and ever-changing. When videos with a high bitrate are played back in a poor network environment, lags may occur. VOD provides adaptive bitrate streaming that supports various resolutions and bitrates, allowing the players to dynamically switch to appropriate video streams based on the network bandwidth.
- Encrypted adaptive bitrate streaming and hotlink protection can be configured for the VOD superplayer to further enhance the security.

### Scheme architecture
![](https://main.qcloudimg.com/raw/18310d428c77267d247246059ced7ece.png)

### Playing back encrypted video at video website
#### Directions
1. Sign up: sign up for a Tencent Cloud account and activate the VOD service as instructed in [Getting Started - Step 1. Activate VOD](https://intl.cloud.tencent.com/document/product/266/8757).
2. Process: initiate video upload and transcoding services in VOD as instructed in [Uploading Video](https://intl.cloud.tencent.com/document/product/266/33890).
3. Configure parameters: add superplayer configuration, select the encrypted adaptive bitstream for playback, select the image sprite used for preview, and set the playback control parameters (such as preview duration and number of IPs allowed for playback) as instructed in [Superplayer Configuration](https://intl.cloud.tencent.com/document/product/266/38261).
4. Preview: preview the video and player and get the corresponding player code as instructed in [Superplayer Preview](https://intl.cloud.tencent.com/document/product/266/33896).


## Relevant Information
- For more information on hotlink protection, please see [Overview](https://intl.cloud.tencent.com/document/product/266/33984).
- For more information on adaptive bitrate streaming, please see [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942).
- For more information on superplayer, please see [Superplayer](https://intl.cloud.tencent.com/document/product/266/38296).
- For more information on video encryption, please see [Overview](https://intl.cloud.tencent.com/document/product/266/38131).

