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

<img src="https://qcloudimg.tencent-cloud.cn/raw/3a8215d3897533ec756bdd4b04e6b811.png" width="900" />

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
For the features supported by the basic player SDK, see [Feature list](#p1). For the integration method, see [Download and use](#p2).

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

For the features supported by the superplayer SDK, see [Feature list](#p1). For the integration method, see [Download and use](#p2).
To help you quickly integrate the superplayer of VOD, we provide a superplayer [integration guide](https://intl.cloud.tencent.com/document/product/266/38098) to describe the integration steps by way of demos.

## Encrypted Video Playback
Video encryption is a specific scenario of long video playback scenarios, where copyrighted videos such as exclusive TV series and online courses are encrypted to avoid unauthorized download and distribution.
For more information on how video encryption works and the integration methods, see [Video Encryption Overview](https://intl.cloud.tencent.com/document/product/266/38131) and [Video Encryption Integration Guide](https://intl.cloud.tencent.com/document/product/266/38294).

## Player SDK
### Download and use[](id:p2)

| Player Type | SDK Download Address | User Guide |
| -- | -- | -- |
| Superplayer | <ul style="margin:0;"><li>[Android](https://intl.cloud.tencent.com/document/product/266/33975)</li><li>[iOS](https://intl.cloud.tencent.com/document/product/266/33976)</li><li>[Web](https://intl.cloud.tencent.com/document/product/266/33977)</li> <li>[Flutter](https://intl.cloud.tencent.com/document/product/266/42099)</li>| <ul style="margin:0;"><li>[Android](https://intl.cloud.tencent.com/document/product/266/33975)</li><li>[iOS](https://intl.cloud.tencent.com/document/product/266/33976)</li><li>[Web](https://intl.cloud.tencent.com/document/product/266/33977)</li><li>[Flutter](https://intl.cloud.tencent.com/document/product/266/42099)</li> |


### Feature list[](id:p1)

| Feature         | Description                                               | iOS and Android | Web  | Flutter |
| ---------------------- | ------------------------------------------------------------ | ------------- | ---- | ------- |
| Multiple formats        | A rich set of audio/video formats such as RTMP, FLV, HLS, MP4, and WebRTC are supported               | ✓             | ✓    | ✓       |
| Playback through URL | Online videos can be played back at URLs | ✓             | ✓    | ✓       |
| DASH protocol     | Videos in standard DASH format are supported                                  | ×             | ✓    | ✓       |
| Playback through `FileId`   | Videos can be played back through their `FileId` in VOD                               | ✓             | ✓    | ✓       |
| Instant broadcasting and preloading of the first frame     | Videos can be preloaded with the first frame broadcast instantly                                | ✓             | ✓    | ×       |
| Quick seeking     | The specified position can be quickly and accurately located to play back the video image there                               | ✓             | ✓    | ✓       |
| H.265 hardware decoding | Playback based on hardware decoding is supported for H.265 videos | ✓             | ✓    | ✓       |
| Automatic switch between software and hardware decoding | If the device does not support hardware decoding, software decoding will be automatically used | ✓             | -    | ✓       |
| Adaptive bitrate streaming       | If an HLS adaptive bitstream is played back, the bitrate can be manually specified or automatically selected according to the network bandwidth for playback            | ✓             | ✓    | ×       |
| Definition switch       | Multiple definitions can be smoothly switched between with no lags                                 | ✓             | ✓    | ✓       |
| Definition naming       | Names can be customized for different definitions                                   | ✓             | ✓    | ×       |
| Playback control        | Playback control features such as start, end, pause, automatic playback, looped playback, checkpoint restart, and replay are supported                | ✓             | ✓    | ✓       |
| Adjustable-Speed playback        | Videos can be played back at any speed between 0.5 time and 2 times, and the audio tone will stay the same even if the speed changes                      | ✓             | ✓    | ✓       |
| Custom playback start time     | The time when to start the playback of a video is customizable                                     | ✓             | ✓    | ✓       |
| Preview        | Videos with preview enabled can be played back                                      | ✓             | ✓    | ✓       |
| Progress bar operation       | The indicator on the progress bar can be dragged to seek the video                                          | ✓             | ✓    | ✓       |
| Progress bar marking and thumbnail preview | Markers can be added to the progress bar, and thumbnail (sprite) preview is supported                        | ✓             | ✓    | ✓       |
| Player size       | The player size can be customized                                       | ✓             | ✓    | ✓       |
| Screen filling/fitting      | Different display modes can be selected for the video image to match the screen size                             | ✓             | ✓    | ✓       |
| Small window playback        | Videos can be played back in a small window                                          | ✓             | ✓    | ✓       |
| Video mirroring | The video image can be mirrored horizontally or vertically | ✓             | ✓    | ✓       |
| Video rotation        | The video image can be rotated at the specified angle or automatically according to the `rotate` parameter in the video file          | ✓             | -    | ×       |
| Brightness adjustment        | The system brightness can be adjusted during video playback                                      | ✓             | -    | ✓       |
| Volume adjustment        | The system volume can be adjusted or muted during video playback                                 | ✓             | ✓    | ✓       |
| Dual-Channel audio       | Dual-Channel audios can be played back                                          | ✓             | ✓    | ✓       |
| Screen lock        | Screen lock features are supported, including rotation lock and UI element hiding                               | ✓             | -    | ✓       |
| On-screen commenting          | Comments can be displayed above the video                                        | ✓             | ✓    | ✓       |
| Roll image        | A roll image can be added for ad display when the video is paused                                 | ✓             | ✓    | ✓       |
| Video screencapturing        | Any frame of the video can be captured                                      | ✓             | -    | ✓       |
| Subtitles import        | Custom subtitles files can be imported                                        | ✓             | ✓    | ✓       |
| Thumbnail configuration        | The thumbnail of the video to be played back can be set                                        | ✓             | ✓    | ✓       |
| Multi-Instance         | Multiple players can be added on the same page for concurrent playback                                 | ✓             | ✓    | ✓       |
| Buffering | When a video is played back, its rest content can be downloaded and buffered at the same time | ✓             | ✓    | ✓       |
| Referer hotlink protection | The source of a playback request can be identified through the `Referer` field in the request, so as to control the request sources through a blocklist or allowlist | ✓             | ✓    | ✓       |
| Key hotlink protection     | Control parameters can be added in the playback URL, so as to control the URL validity period, preview duration, number of IPs allowed for playback, etc.          | ✓             | ✓    | ✓       |
| HLS encryption      | Video data can be encrypted with a key and HLS-based AES encryption scheme       | ✓             | ✓    | ✓       |
| Proprietary protocol encryption      | Videos can be encrypted over proprietary protocols in the cloud, and the encrypted videos can be decrypted only through the player SDK for playback     | ✓             | ✓    | ×       |
| Offline download        | Encrypted videos downloaded offline can be decrypted only through the player SDK for playback                 | ✓             | -    | ×       |
| Playback callback        | The playback status, first frame, and playback completion or failure can be called back                           | ✓             | ✓    | ✓       |
| Support for HTTPS | HTTPS video resources can be played back | ✓             | ✓    | ✓       |
| Custom HTTP header | HTTP headers in video resource requests are customizable | ✓             | -    | ×       |

  >? "-" in the table indicates that the terminal doesn't need to have the corresponding feature or doesn't have the related concept.
