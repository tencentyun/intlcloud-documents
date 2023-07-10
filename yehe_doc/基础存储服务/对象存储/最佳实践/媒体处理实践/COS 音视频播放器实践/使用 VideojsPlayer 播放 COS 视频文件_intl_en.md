## Overview
This document describes how to use [VideojsPlayer](https://videojs.com/) together with the rich audio/video capabilities of [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045/46980) to play back video files stored in COS in a web browser.

## Integration Guide

#### Step 1. Import player style and script files into the page
```
<!-- Player style file -->
<link href="https://vjs.zencdn.net/7.19.2/video-js.css" rel="stylesheet" />
<!-- Player script file -->
<script src="https://vjs.zencdn.net/7.19.2/video.min.js"></script>
```

>?We recommend you deploy the above static resources on your own when using the player.

#### Step 2. Set the player container node
Place the player container in the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).
```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
></video>
```

#### Step 3. Get the video file object address
1. [Create a bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. [Upload a video file object](https://intl.cloud.tencent.com/document/product/436/13321).
3. Get the video file object address in the format of `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<video format>`.

>?
> - If cross-origin access is involved, you need to set CORS for the bucket as instructed in [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318).
> - If the bucket permission is private read/write, the object address needs to carry a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

#### Step 4: Set the video address in the player container and pass in the COS video file object URL


```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
>
  <source
    src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
    type="video/mp4"
  />
</video>
```


## Function Guide
[](id:1)
### Playing back video files in different formats
1. Get the object address of the video file in the COS bucket.
>? We recommend you transcode videos for playback because untranscoded videos may experience compatibility issues during playback. You can get video files in different formats with CI's [audio/video transcoding](https://intl.cloud.tencent.com/document/product/1045/49543) feature.
2. For different video formats, in order to ensure the compatibility with different browsers, corresponding dependencies need to be imported.
 - MP4: There is no need to import other dependencies.
 - HLS: If you want to play back HLS videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `hls.min.js` before importing `tcplayer.min.js`.

```
  <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/libs/hls.min.0.13.2m.js"></script>
```

 - FLV: If you want to play back FLV videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `flv.min.js` before importing `tcplayer.min.js`.

```
  <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/libs/flv.min.1.6.2.js"></script>
```

 - DASH: You need to import the `dash.all.min.js` file.

```
  <script src="https://cos-video-1258344699.cos.ap-guangzhou.myqcloud.com/lib/dash.all.min.js"></script>
```

3. Initialize the player and pass in the object address.

```
<!-- MP4 -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
  type="video/mp4"
/>

<!-- HLS -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"
  type="application/x-mpegURL"
/>

<!-- FLV -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.flv"
  type="video/x-flv"
/>

<!-- DASH -->
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mpd"
  type="application/dash+xml"
/>
```


Get code samples:
- [Sample code for MP4 playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/mp4.html)
- [Sample code for FLV playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/flv.html)
- [Sample code for HLS playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/m3u8.html)
- [Sample code for DASH playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/dash.html)

[](id:2)
### Playing back PM3U8 video
PM3U8 refers to private M3U8 video file. COS provides a download authorization API for getting private M3U8 TS resources. For more information, see [Private M3U8 API](https://intl.cloud.tencent.com/document/product/436/47220).

```
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600"
  type="application/x-mpegURL"
/>
```

Get code samples:
- [Sample code for PM3U8 playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/pm3u8.html)

[](id:3)
### Setting thumbnail
1. Get the object address of the thumbnail in the COS bucket.
>!CI's [intelligent thumbnail](https://intl.cloud.tencent.com/document/product/1045/47740) feature can extract optimal frames to generate thumbnails to make the video content more engaging.
2. Initialize the player and set the thumbnail image.

```
<video
  id="my-video"
  class="video-js"
  controls
  preload="auto"
  width="100%"
  height="100%"
  data-setup="{}"
  poster="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/poster.png"
>
  <source
    src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"
    type="video/mp4"
  />
</video>
```

Get code samples:
- [Sample code for thumbnail configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/poster.html)

[](id:4)
### Playing back HLS encrypted video
To ensure the security of video content and prevent unauthorized download and distribution of videos, CI provides the feature of encrypting HLS video content, which is more secure than privately readable files. Encrypted videos cannot be distributed to users without access for playback. Even if they are downloaded, they are still encrypted and cannot be redistributed maliciously. This protects your video copyrights from being infringed upon.
Follow the steps below:
1. Generate an encrypted video as instructed in [Playing back HLS Encrypted Video](https://intl.cloud.tencent.com/document/product/436/48293) and [COS Audio/Video Practice | Encrypting Your Video](https://mp.weixin.qq.com/s/4f-GKyAG0S-FcZ2BZCn7jA).
2. Initialize the player and pass in the video object address.

```
<source
  src="https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"
  type="application/x-mpegURL"
/>
```

Get code samples:
- [Sample code for HLS encrypted playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/videojs/m3u8.html)



