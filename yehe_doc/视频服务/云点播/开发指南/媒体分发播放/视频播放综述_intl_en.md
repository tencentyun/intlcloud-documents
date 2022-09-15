VOD supports multiple methods to play back uploaded and transcoded videos, and video playback mainly involves three scenarios: short video, long video, and encrypted video playback.

### Short video playback

Short videos generally refer to videos of less than 5 minutes in length, mainly including:

* Videos shared on UGSV social media sites (such as TikTok).
* Product promotion videos shared on ecommerce platforms.
* Videos shared on WeChat Official Account and we media.

<img src="https://qcloudimg.tencent-cloud.cn/raw/3a8215d3897533ec756bdd4b04e6b811.png" width="900" />


### Long video playback

Long videos generally refer to videos produced by professional organizations and published on video websites, mainly including:

* Exclusive TV series and variety shows published on video social media platforms (such as Tencent Video, Youku, and iQIYI).
* Course videos published on online education websites (such as Tencent Class and Penguin Tutoring).
* TV programs replayed on online TV platforms (such as CNTV and Mongo TV).

<img src="https://main.qcloudimg.com/raw/261acb48f5d44c8170d34e60bb3947c2.png" width="800" />

### Encrypted video playback

Video encryption is a specific scenario of long video playback scenarios, where copyrighted videos such as exclusive TV series and online courses are encrypted to avoid unauthorized download and distribution.

<img src="https://main.qcloudimg.com/raw/382d1cece21cb857c71164e905ca02d8.png" width="800" />

## Playback Architecture

For various video playback scenarios, we recommend you use the **Player SDK** to play back the output video of adaptive bitrate streaming in VOD. The overall playback architecture is as follows:

<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="900" />

1. **Upload from server**: The business backend uploads a video to VOD through the console, server API, or other means.
2. **Trigger video processing**: When the video is uploaded, adaptive bitrate streaming is specified. After the video is uploaded, video processing begins.
3. **Transcode to adaptive bitstream and write to storage**: After the video is transcoded to adaptive bitstream, the output video content is written to the VOD storage.
4. **Update the media asset**: The output video information is written into the media asset management module.
5. **Distribute the signature**: The business backend distributes the playback signature generated according to the player signature calculation rule.
6. **Request the download address**: The player gets the download address of the video from VOD's playback service after the video's `FileId` is specified.
7. **Download the content**: The player downloads the content from VOD CDN at the download address.
8. **Play back the video**: The player plays back the output adaptive bitstream.

## Documentation

* For the features supported by the Player SDK, see [Feature Description](https://intl.cloud.tencent.com/document/product/266/42965). For the integration method, see [SDK Download](https://intl.cloud.tencent.com/document/product/266/43035).
* To help you quickly integrate the VOD Player, we provide an [integration guide](https://intl.cloud.tencent.com/document/product/266/38098) for the Player SDK to describe the integration steps by way of demos.
* For more information on how video encryption works and the integration methods in video encryption and playback scenarios, see [Overview](https://intl.cloud.tencent.com/document/product/266/38131) and [Stage 4. Play back an encrypted video](https://intl.cloud.tencent.com/document/product/266/38294).
