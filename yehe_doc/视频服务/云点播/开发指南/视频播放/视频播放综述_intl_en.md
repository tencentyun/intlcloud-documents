VOD supports multiple methods to play back uploaded and transcoded videos, and video playback mainly involves the following three scenarios:

| Scenario | Description | Recommended Playback Method |
| -- | -- | -- |
| Short video playback | Playback of videos of less than 5 minutes in length | Basic player |
| Long video playback | Playback of videos produced by professional organizations and published on video websites | Superplayer |
| Encrypted video playback | Playback of long videos requiring encryption for copyright protection | Superplayer |

This document describes the three scenarios' characteristics and recommended playback methods.

## Short Video Playback

Short videos generally refer to videos of less than 5 minutes in length, mainly including:

* Videos shared on UGSV social medias (such as WeSee, Kuaishou, and TikTok).
* Product promotion videos shared on ecommerce platforms (such as JD.com and Pinduoduo).
* Videos shared on WeChat Official Account and we media.



### Playback architecture
For short video playback scenarios, VOD provides the **basic player SDK**, which uses the URL as a parameter to play back the selected video on demand.

<img src="https://main.qcloudimg.com/raw/a9d4a24cefcdb3ccba1b316ea6be9ee0.png" width="700" />

The overall architecture of playback with the basic player SDK is as follows:
1. **Upload from server**: the business backend uploads a video to VOD through the console, server API, or other means.
2. **Trigger video processing**: when the video is uploaded, transcoding can be specified. After the video is uploaded, the transcoding process begins.
3. **Transcode and write to storage**: after the video is transcoded, the output video content is written to the VOD storage.
4. **Download the content**: the basic player downloads the content from VOD CDN at the download address.
5. **Play back the video**: the basic player plays back the video.

### Integration with basic player
For the features supported by the basic player SDK, please see [Feature list](#p1). For the integration method, please see [Download and use](#p2).

## Long Video Playback

Long videos generally refer to videos produced by professional organizations and published on video websites, mainly including:

* Exclusive TV series and variety shows published on video social media (such as Tencent Video, Youku, and iQIYI).
* Course videos published on online education websites (such as Tencent Class and Penguin Tutoring).
* TV programs replayed on online TV platforms (such as CNTV and Mongo TV).

<img src="https://main.qcloudimg.com/raw/261acb48f5d44c8170d34e60bb3947c2.png" width="800" />
<img src="https://main.qcloudimg.com/raw/382d1cece21cb857c71164e905ca02d8.png" width="800" />

### Playback architecture

For long video playback scenarios, VOD provides the **superplayer SDK**, which uses the `FileId` as a parameter to play back the selected video on demand.

<img src="https://main.qcloudimg.com/raw/f6b52d9429111812b0ee0e78654f2e34.png" width="700" />

The overall architecture of playback with the superplayer SDK is as follows:
1. **Upload from server**: the business backend uploads a video to VOD through the console, server API, or other means.
2. **Trigger video processing**: when the video is uploaded, adaptive bitrate streaming is specified. After the video is uploaded, video processing begins.
3. **Transcode to adaptive bitstream and write to storage**: after the video is transcoded to adaptive bitstream, the output video content is written to the VOD storage.
4. **Update the media asset**: the output video information is written into the media asset management module.
5. **Request the download address**: the superplayer gets the download address of the video from VOD's playback service after the video's `FileId` is specified.
6. **Download the content**: the superplayer downloads the content from VOD CDN at the download address.
7. **Play back the video**: the superplayer plays back the output adaptive bitstream.

If [key hotlink protection](https://intl.cloud.tencent.com/document/product/266/33986) is enabled for the video to be played back, the [superplayer signature](https://intl.cloud.tencent.com/document/product/266/38099) needs to be specified during the playback. In this case, the architecture is as follows:

1. The "signature distribution" service needs to be built on the business backend, and a signature is generated according to the [player signature calculation rule](https://intl.cloud.tencent.com/document/product/266/38099#.E7.AD.BE.E5.90.8D.E8.AE.A1.E7.AE.97).
2. The superplayer gets the player signature before playing back the video (as shown in step 5 below).
3. When the superplayer requests the download address (as shown in step 6 below), the playback service will return the download address only after verifying that the signature is valid.

<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

### Integration with superplayer

For the features supported by the superplayer SDK, please see [Feature list](#p1). For the integration method, please see [Download and use](#p2).
To help you quickly integrate the superplayer of VOD, we provide a superplayer [integration guide](https://intl.cloud.tencent.com/document/product/266/38098) to describe the integration steps by way of demos.

## Encrypted Video Playback
Video encryption is a specific scenario of long video playback scenarios, where copyrighted videos such as exclusive TV series and online courses are encrypted to avoid unauthorized download and distribution.
For more information on how video encryption works and the integration methods, please see [Video Encryption Overview](https://intl.cloud.tencent.com/document/product/266/38131) and [Video Encryption Integration Guide](https://intl.cloud.tencent.com/document/product/266/38294).

## Player SDK
### Download and use[](id:p2)

| Player Type | SDK Download Address | User Guide |
| -- | -- | -- |
| Superplayer | <ul style="margin:0;"><li>[Android](https://intl.cloud.tencent.com/document/product/266/33975)</li><li>[iOS](https://intl.cloud.tencent.com/document/product/266/33976)</li><li>[Web](https://intl.cloud.tencent.com/document/product/266/33977)</li><li>[Flutter](https://intl.cloud.tencent.com/document/product/266/42099)</li> | <ul style="margin:0;"><li>[Android](https://intl.cloud.tencent.com/document/product/266/33975)</li><li>[iOS](https://intl.cloud.tencent.com/document/product/266/33976)</li><li>[Web](https://intl.cloud.tencent.com/document/product/266/33977)</li><li>[Flutter](https://intl.cloud.tencent.com/document/product/266/42099)</li> |


### Feature list[](id:p1)
#### Basic player
| Feature | Description | Mobile (Android and iOS) | Web |
| -- | -- | -- | -- |
| Wide variety of formats | A wide variety of formats such as RTMP, FLV, HLS, and MP4 are supported | &#10003;  | &#10003; |
| Instant streaming of the first frame | The first frame of videos can be streamed instantly | &#10003; | &#10003; |
| Seamless switch of resolution | Different resolutions can be switched between with no lags | &#10003; | × |
| Quick seeking | The specified position can be quickly located to play back the video image there | &#10003; | &#10003; |
| H.265 hardware decoding | Playback based on hardware decoding is supported for H.265 videos | &#10003; | × |
| Automatic switch between software and hardware decoding | If the device does not support hardware decoding, software decoding will be automatically used | &#10003; | × |
| Custom HTTP header | The HTTP headers in video resource requests are customizable | &#10003; | × |
| Adaptive bitrate | If an HLS adaptive bitstream is played back, the bitrate is adaptive to the network bandwidth | &#10003; | &#10003; |
| Small window playback | Videos can be played back in a small window | &#10003; | × |
| Adjustable-speed playback | Videos can be played back at different speeds, without changing the audio tone | &#10003; | × |
| Playing video while downloading | When a video is played back, its remaining content is downloaded and buffered at the same time | &#10003; | &#10003; |
| On-screen commenting | Comments can be displayed above video | &#10003; | × |
| Mute | Audio can be muted during video playback | &#10003; | &#10003; |
| Video screencapturing | The video image can be captured as screenshots | &#10003; | × |
| Video rotation | The video image can be rotated by a specified angle | &#10003; | × |
| Video mirroring | The video image can be mirrored horizontally or vertically | &#10003; | × |
| Screen filling/fitting | Different display modes can be selected for the video image to match the screen size | &#10003; | × |
| Custom streaming start time | The time when streaming starts is customizable | &#10003; | &#10003; |
| Cover configuration | The cover of the video to be played back can be set | &#10003; | &#10003; |
| Player dimensions configuration | The player's width and height can be set | &#10003; | &#10003; |
| Support for HTTPS | HTTPS video resources can be played back | &#10003; | &#10003; |
| Playback through URL | Online videos can be played back at URLs | &#10003; | &#10003; |
| Live streaming recording | Recorded live streaming videos can be played back | &#10003; | &#10003; |
| Custom video rendering | After being decoded, videos can be rendered onto the screen | &#10003; | × |
| Seamless loop playback | A single video can be looped | &#10003; | &#10003; |
| Interactive floating window | Videos can be played back in a floating window | &#10003; | × |
| Automatic video rotation | Videos can be rotated according to the internal `rotate` parameter | &#10003; | × |
| Custom progress callback interval | The progress callback interval is customizable | &#10003; | × |

#### Superplayer
| Feature | Description | Mobile (Android and iOS) | Web |
| -- | -- | -- | -- |
| Instant streaming of the first frame | The first frame of videos can be streamed instantly | &#10003; | &#10003; |
| Seamless switch of resolution | Different resolutions can be switched between with no lags | &#10003; | &#10003; |
| Quick seeking | The specified position can be quickly located to play back the video image there | &#10003; | &#10003; |
| H.265 hardware decoding | Playback based on hardware decoding is supported for H.265 videos | &#10003; | × |
| Automatic switch between software and hardware decoding | If the device does not support hardware decoding, software decoding will be automatically used | &#10003; | × |
| Hotlink protection | Videos with hotlink protection enabled are supported | &#10003; | &#10003;  |
| Preview | Videos with preview enabled are supported | &#10003; | &#10003;  |
| Playback of encrypted video | Encrypted videos can be played back on demand | &#10003; | &#10003;  |
| Custom HTTP header | The HTTP headers in video resource requests are customizable | &#10003; | × |
| Adaptive bitrate | If an HLS adaptive bitstream is played back, the bitrate is adaptive to the network bandwidth | &#10003; | &#10003; |
| Custom substream specification name | During the playback of a custom bitstream, the specification name of each substream is customizable | &#10003; | &#10003; |
| Small window playback | Videos can be played back in a small window | &#10003; | × |
| Adjustable-speed playback | Videos can be played back at different speeds, without changing the audio tone | &#10003; | × |
| Playing video while downloading | When a video is played back, its remaining content is downloaded and buffered at the same time | &#10003; | &#10003; |
| On-screen commenting | Comments can be displayed above video | &#10003; | × |
| Mute | Audio can be muted during video playback | &#10003; | &#10003; |
| Video screencapturing | The video image can be captured as screenshots | &#10003; | × |
| Video rotation | The video image can be rotated by a specified angle | &#10003; | × |
| Video mirroring | The video image can be mirrored horizontally or vertically | &#10003; | &#10003; |
| Screen filling/fitting | Different display modes can be selected for the video image to match the screen size | &#10003; | × |
| Custom streaming start time | The time when streaming starts is customizable | &#10003; | &#10003; |
| Gesture | The brightness, volume, and progress can be adjusted through gestures | &#10003; | × |
| Cover configuration | The cover of the video to be played back can be set | &#10003; | &#10003; |
| Thumbnail preview | Thumbnails can be displayed on the progress bar for preview | &#10003; | &#10003; |
| Progress bar timestamp | Timestamp information can be added to the progress bar | &#10003; | &#10003; |
| Playback list | Videos in the playback list can be played back in sequence | &#10003; | × |
| Player dimensions configuration | The player's width and height can be set | &#10003; | &#10003; |
| File download | Online videos can be downloaded | &#10003; | × |
| Support for HTTPS | HTTPS video resources can be played back | &#10003; | &#10003; |
| Playback through `FileId` | Videos can be played back through their `FileId` values in VOD | &#10003; | &#10003; |
| Custom video rendering | After being decoded, videos can be rendered onto the screen | &#10003; | × |
| Seamless loop playback | A single video can be looped | &#10003; | &#10003; |
| Interactive floating window | Videos can be played back in a floating window | &#10003; | × |
| Automatic video rotation | Videos can be rotated according to the internal `rotate` parameter | &#10003; | × |
| Custom progress callback interval | The progress callback interval is customizable | &#10003; | × |
