## Overview

This document describes how to use [DPlayer](https://dplayer.js.org/) together with the rich audio/video capabilities of [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045/46980) to play back video files stored in COS in a web browser.

## Integration Guide

#### Step 1. Import player script files and required dependency files into the page
```
<!-- Player script file -->
<script src="https://cdn.jsdelivr.net/npm/dplayer@1.26.0/dist/DPlayer.min.js"></script>
```
>?We recommend you deploy the above static resources on your own when using the player.

#### Step 2. Set the player container node
Place the player container in the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).
```
<div id="dplayer" style="width: 100%; height: 100%"></div>
```

#### Step 3. Get the video file object address
1. [Create a bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. [Upload a video file object](https://intl.cloud.tencent.com/document/product/436/13321).
3. Get the video file object address in the format of `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<video format>`.

>?
> - If cross-origin access is involved, you need to set CORS for the bucket as instructed in [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318).
> - If the bucket permission is private read/write, the object address needs to carry a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

#### Step 4. Initialize the player and pass in the COS video file object URL
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4', // COS video object address
  },
});
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
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4', // COS video object address
  },
});
```

Get code samples:
- [Sample code for MP4 playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/mp4.html)
- [Sample code for FLV playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/flv.html)
- [Sample code for HLS playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/m3u8.html)
- [Sample code for DASH playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/dash.html)

[](id:2)
### Playing back PM3U8 video
PM3U8 refers to private M3U8 video file. COS provides a download authorization API for getting private M3U8 TS resources. For more information, see [Private M3U8 API](https://intl.cloud.tencent.com/document/product/436/47220).
```
 const dp = new DPlayer({
   container: document.getElementById('dplayer'),
   // For more information on pm3u8, visit https://intl.cloud.tencent.com/document/product/436/47220.
   video: {
     url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600' // Relative validity period of the download credential for the private TS resource URL, which is 3,600 seconds.
   }
 });
```
Get code samples:
- [Sample code for PM3U8 playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/pm3u8.html)

[](id:3)
### Setting thumbnail
1. Get the object address of the thumbnail in the COS bucket.
>!CI's [intelligent thumbnail](https://intl.cloud.tencent.com/document/product/1045/47740) feature can extract optimal frames to generate thumbnails to make the video content more engaging.
2. Initialize the player and set the thumbnail image.
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
    url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4',
    pic: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.png',
  },
});
```

Get code samples:
- [Sample code for thumbnail configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/poster.html)

[](id:4)
### Playing back HLS encrypted video
To ensure the security of video content and prevent unauthorized download and distribution of videos, CI provides the feature of encrypting HLS video content, which is more secure than privately readable files. Encrypted videos cannot be distributed to users without access for playback. Even if they are downloaded, they are still encrypted and cannot be redistributed maliciously. This protects your video copyrights from being infringed upon.
Follow the steps below:
1. Generate an encrypted video as instructed in [Playing back HLS Encrypted Video](https://intl.cloud.tencent.com/document/product/436/48293) and [COS Audio/Video Practice | Encrypting Your Video](https://mp.weixin.qq.com/s/4f-GKyAG0S-FcZ2BZCn7jA).
2. Initialize the player and pass in the video object address.
```
 const dp = new DPlayer({
   container: document.getElementById('dplayer'),
   video: {
     url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8' // Encrypted video address
   }
 });
```


Get code samples:
- [Sample code for HLS encrypted playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/m3u8.html)

[](id:5)
### Switching definition

CI's [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/1045/47745) feature can transcode a video and remux it into adaptive bitstreams for output, helping you quickly distribute video content in different network conditions. The player can dynamically select the most appropriate bitrate to play back the video based on the current bandwidth. For more information, see [COS Audio/Video Practice | Playing back Multi-Definition Video with Data Processing Workflow](https://mp.weixin.qq.com/s/THUhur1FV_55T9zzqT2MFQ).

Follow the steps below:
1. Generate the multi-bitrate adaptive HLS or DASH target file with CI's [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/1045/47745) feature.
2. Initialize the player and pass in the video object address.
```
const dp = new DPlayer({
  container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8', //  Multi-bitrate HLS/DASH video
  },
});
```

Get code samples:
- [Sample code for definition switching](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/multiDefinition.html)

[](id:6)
### Setting the top-left logo
The player allows you to set a logo in the top-left corner.
Follow the steps below:
1. Get the object address of the logo in the COS bucket.
2. Initialize the player and set the logo.
```
const dp = new DPlayer({
	container: document.getElementById('dplayer'),
  video: {
  	url: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4',
  },
	logo: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.svg'
});
```

Get code samples:
- [Sample code for setting the top-left logo](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/dplayer/logo.html)


