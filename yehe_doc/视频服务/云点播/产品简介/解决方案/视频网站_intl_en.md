## Video Encryption Scenarios
### Background
Almost all scenarios throughout the video service industry, including video websites, video portals, and online education, require secure and reliable video on demand services. This is especially true with the rising awareness of copyright protection and the growing need for video encryption. Tencent Cloud VOD provides a video encryption solution that can be built quickly and delivers a smooth viewer experience.



In video encryption scenarios, VOD combines hotlink protection, encrypted adaptive bitrate streaming, and the Player SDK. You can quickly integrate the player into your mobile and web clients, which gives you capabilities such as resolution switching, thumbnail preview, video preview, and encrypted playback. Backed by the powerful backend of VOD, you can easily provide end-to-end video services ranging from video upload and transcoding to playback and acceleration. In addition, VOD also provides the following features:
- Hotlink protection can be enabled to restrict video playback and guarantee video security.
- VOD provides adaptive bitrate streaming that supports various resolutions and bitrates, allowing video players to dynamically switch to appropriate video streams based on the network bandwidth.
- Encrypted adaptive bitrate streaming and hotlink protection can be configured for the VOD Player SDK to further enhance the security.

### Scheme architecture
![](https://main.qcloudimg.com/raw/18310d428c77267d247246059ced7ece.png)

### Playing back an encrypted video on a video website
#### Directions
1. Sign up for a Tencent Cloud account and activate the VOD service. For details, see [Getting Started - Step 1. Activate VOD](https://intl.cloud.tencent.com/document/product/266/8757).
2. Initiate the video upload and transcoding services in VOD as instructed in [Uploading Video](https://intl.cloud.tencent.com/document/product/266/33890).
3. Add the player configuration, select the encrypted adaptive bitstream for playback, select the image sprite used for preview, and set the playback control parameters (such as preview duration and number of IPs allowed for playback) as instructed in [Superplayer Configuration](https://intl.cloud.tencent.com/document/product/266/38261).
4. Preview the video and player and get the corresponding player code as instructed in [Managing Video](https://intl.cloud.tencent.com/document/product/266/33896).


## More Information
- For more information on hotlink protection, see [Overview](https://intl.cloud.tencent.com/document/product/266/33984).
- For more information on adaptive bitrate streaming, see [Transcoding to Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942).
- For more information on the Player SDK, see [Overview](https://intl.cloud.tencent.com/document/product/266/7836).
- For more information on video encryption, see [Overview](https://intl.cloud.tencent.com/document/product/266/38131).
