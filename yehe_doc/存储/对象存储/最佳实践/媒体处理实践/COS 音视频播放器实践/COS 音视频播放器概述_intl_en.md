This document describes how to process COS audio/video files in the cloud and play back them on the client. Examples in this document cover protocols and features supported for audio/video processing and offer you more ideas on using the product features based on the rich audio/video processing capabilities of the [media processing service](https://www.tencentcloud.com/document/product/1045/46980) in CI to help you improve the playback performance.

## Supported protocols

|   Audio/Video Protocol    | URL Format                                                 | PC Browser | Mobile Browser |
| :-------------: | ------------------------------------------------------------ | --------- | ------------ |
|       MP3       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.mp3 | Supported      | Supported         |
|       MP4       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.mp4 | Supported      | Supported         |
| HLS<br/>(M3U8) | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.m3u8 | Supported      | Supported         |
|       FLV       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.flv | Supported      | Supported         |
|      DASH       | https://&lt;BucketName-APPID&gt;.cos.&lt;Region&gt;.myqcloud.com/xxx.mpd | Supported      | Supported         |

>!In some browser environments, HLS, FLV, and DASH video playback depends on <a href="https://caniuse.com/?search=Media Source Extensions">Media Source Extensions</a>.

## Supported features

| Feature                       | TCPlayer | DPlayer | VideojsPlayer |
| -------------------------- | --------------- | -------------- | -------------- |
| MP4 video playback          | View details        | View details       | View details       |
| HLS video playback          | View details        | View details       | View details       |
| FLV video playback          | View details        | View details       | View details       |
| DASH video playback         | View details        | View details       | View details       |
| PM3U8 (private M3U8) video playback | View details        | View details       | View details       |
| Thumbnail configuration                 | View details        | View details       | View details       |
| Standard HLS encryption configuration          | View details        | View details       | View details       |
| Definition switch                 | View details        | View details       | -              |
| Dynamic watermark configuration               | View details        | -              | -              |
| Top-left logo configuration            | -               | View details       | -              |
| Progress preview image configuration             | View details        | -              | -              |
| Subtitles configuration                   | View details        | -              | -              |
| Multilingual configuration                 | View details        | -              | -              |
| Roll image ad configuration               | View details        | -              | -              |

>? The player is compatible with mainstream browsers and can automatically select the optimal playback scheme depending on the browser used. For example, for modern browsers such as Chrome, the player uses the HTML5 technology for playback, and for mobile browsers, it uses the HTML5 technology or the browser's built-in capabilities.

## Usage guide
- Playing back COS Video File with TCPlayer
- Playing back Video in COS with DPlayer
- Playing back Video in COS with VideojsPlayer


