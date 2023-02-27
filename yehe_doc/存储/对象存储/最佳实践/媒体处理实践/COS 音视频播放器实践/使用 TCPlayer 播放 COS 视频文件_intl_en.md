## Overview
This document describes how to use the TCPlayer integrated in the TCToolkit SDK together with the rich audio/video capabilities of [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045/46980) to play back video files stored in COS in a web browser.


## Integration Guide
#### Step 1. Import player style and script files into the page
```
<!--Player style file-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.min.css" rel="stylesheet">
<!--Player script file-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.0/tcplayer.v4.5.0.min.js"></script>
```
>?
>- We recommend you deploy the above static resources on your own when using the player SDK. Click [here](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip) to download the player resources.
>- Deploy the folder generated after decompression. Do not adjust the directories in the folder; otherwise, resource import exceptions may occur.

#### Step 2. Set the player container node
Place the player container in the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
> - The player container must be a `<video>` tag.
> - The `player-container-id` in the sample is the ID of the player container, which can be customized.
> - We recommend you set the size of the player container zone through CSS, which is more flexible than the attribute and can achieve effects such as fit to full screen and container adaption.
> - The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster playback start. Other options include `meta` (to only load the metadata after the page is loaded) and `none` (to not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
> - The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback if the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
> - If the `x5-playsinline` attribute is set, the X5 UI player will be used in the TBS kernel.

#### Step 3. Get the video file object address
1. [Create a bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. [Upload a video file object](https://intl.cloud.tencent.com/document/product/436/13321).
3. Get the video file object address in the format of `https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.<video format>`.

>?
> - If cross-origin access is involved, you need to set CORS for the bucket as instructed in [Setting CORS](https://intl.cloud.tencent.com/document/product/436/13318).
> - If the bucket permission is private read/write, the object address needs to carry a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

#### Step 4. Initialize the player and pass in the COS video file object URL
```
var player = TCPlayer("player-container-id", {}); // `player-container-id` is the player container ID, which must be the same as that in HTML.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COS video object address
```

## Feature Guide
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
var player = TCPlayer("player-container-id", {}); // `player-container-id` is the player container ID, which must be the same as that in HTML.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4"); // COS video address
```

Get code samples:
- [Sample code for MP4 playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/mp4.html)
- [Sample code for FLV playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/flv.html)
- [Sample code for HLS playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/m3u8.html)
- [Sample code for DASH playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/dash.html)


[](id:2)
### Playing back PM3U8 video
PM3U8 refers to private M3U8 video file. COS provides a download authorization API for getting private M3U8 TS resources. For more information, see [Private M3U8 API](https://intl.cloud.tencent.com/document/product/436/47220).
```
var player = TCPlayer("player-container-id", {
	poster: "https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8?ci-process=pm3u8&expires=3600" // Relative validity period of the download credential for the private TS resource URL, which is 3,600 seconds.
});
```

Get code samples:
- [Sample code for PM3U8 playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/pm3u8.html)

[](id:3)
### Setting thumbnail
1. Get the object address of the thumbnail in the COS bucket.
>!CI's [intelligent thumbnail](https://intl.cloud.tencent.com/document/product/1045/47740) feature can extract optimal frames to generate thumbnails to make the video content more engaging.
2. Set the thumbnail.
```
var player = TCPlayer("player-container-id", {
	poster: "https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.png"
});
```

Get code samples:
- [Sample code for thumbnail configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/poster.html)

[](id:4)
### Playing back HLS encrypted video
To ensure the security of video content and prevent unauthorized download and distribution of videos, CI provides the feature of encrypting HLS video content, which is more secure than privately readable files. Encrypted videos cannot be distributed to users without access for playback. Even if they are downloaded, they are still encrypted and cannot be redistributed maliciously. This protects your video copyrights from being infringed upon.

The steps are as follows:
1. Generate an encrypted video as instructed in [Playing back HLS Encrypted Video](https://www.tencentcloud.com/document/product/436/48293).
2. Initialize the player and pass in the video object address.
```
var player = TCPlayer("player-container-id", {}); // `player-container-id` is the player container ID, which must be the same as that in HTML.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"); // HLS encrypted video address
```

Get code samples:
- [Sample code for HLS encrypted playback](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/m3u8.html)

[](id:5)
### Switching definition
CI's [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/1045/47745) feature can transcode a video and remux it into adaptive bitstreams for output, helping you quickly distribute video content in different network conditions. The player can dynamically select the most appropriate bitrate to play back the video based on the current bandwidth.
The steps are as follows:
1. Generate the multi-bitrate adaptive HLS or DASH target file with CI's [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/1045/47745) feature.
2. Initialize the player and pass in the video object address.
```
var player = TCPlayer("player-container-id", {}); // `player-container-id` is the player container ID, which must be the same as that in HTML.
player.src("https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.m3u8"); // Multi-bitrate video address
```

Get code samples:
- [Sample code for definition switching](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/multiDefinition.html)

[](id:6)
### Setting dynamic watermark
The player supports adding a dynamic watermark that changes its position and speed to a video. When using the dynamic watermark feature, the reference of the player object should not be exposed to the global environment; otherwise, the dynamic watermark can be easily removed. CI also allows you to add a dynamic watermark to a video in the cloud. For more information, see Watermark Template APIs.
```
var player = TCPlayer("player-container-id", {
    plugins:{
      DynamicWatermark: {
        speed: 0.2, // Speed
        content: "Tencent Cloud CI", // Text
        opacity: 0.7 // Opacity
      }
    }
  });
```

Get code samples:
- [Sample code for dynamic watermark configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/dynamicWatermark.html)

[](id:7)
### Setting roll image ad
The steps are as follows:
1. Prepare the ad thumbnail and link.
2. Initialize the player, set the ad thumbnail and link, and set the ad node.
```
var PosterImage = TCPlayer.getComponent('PosterImage');
PosterImage.prototype.handleClick = function () {
	window.open('https://www.tencentcloud.com/products/ci'); // Set the ad link
};

var player = TCPlayer('player-container-id', {
	poster: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx..png', // Ad thumbnail
});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');

var adTextNode = document.createElement('span');
adTextNode.className = 'ad-text-node';
adTextNode.innerHTML = 'Ad';

var adCloseIconNode = document.createElement('i');
adCloseIconNode.className = 'ad-close-icon-node';
adCloseIconNode.onclick = function (e) {
  e.stopPropagation();
  player.posterImage.hide();
};

player.posterImage.el_.appendChild(adTextNode);
player.posterImage.el_.appendChild(adCloseIconNode);
```

Get code samples:
- [Sample code for roll image ad configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/advertise.html)

[](id:8)
### Setting video progress thumbnail (image sprite)
The steps are as follows:
1. Generate an image sprite with CI's [video frame capturing](https://intl.cloud.tencent.com/document/product/1045/47736) feature.
2. Get the object addresses of the image sprite and VTT (image sprite location description file) generated in step 1.
3. Initialize the player and set the video and VTT file addresses.
```
var player = TCPlayer('player-container-id', {
  plugins: {
    VttThumbnail: {
      vttUrl: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.vtt' // VTT file
    },
  },
});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
```

Get code samples:
- [Sample code for image sprite configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/preview.html)

[](id:9)
### Setting video subtitles
The steps are as follows:
1. Generate a subtitle file with CI's speech recognition feature.
2. Get the object address of the SRT file generated in step 1.
3. Initialize the player and set the video and SRT file addresses.
```
var player = TCPlayer('player-container-id', {});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
player.on('ready', function () {
  // Add the subtitles file
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.srt', // Subtitles file
    kind: 'subtitles',
    srclang: 'zh-cn',
    label: 'Chinese',
    default: 'true',
  }, true);
});
```

Get code samples:
- [Sample code for video subtitles configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/subtitle.html)

[](id:10)
### Setting multilingual video subtitles
The steps are as follows:
1. Generate a subtitles file with CI's speech recognition feature and translate it into multiple languages.
2. Get the object address of the multilingual SRT file generated in step 1.
3. Initialize the player and set the video and multilingual SRT file addresses.
```]
var player = TCPlayer('player-container-id', {});
player.src('https://<BucketName-APPID>.cos.<Region>.myqcloud.com/xxx.mp4');
player.on('ready', function () {
  // Set Chinese subtitles
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/zh.srt', // Subtitles file
    kind: 'subtitles',
    srclang: 'zh-cn',
    label: 'Chinese',
    default: 'true',
  }, true);
  // Set English subtitles
  var subTrack = player.addRemoteTextTrack({
    src: 'https://<BucketName-APPID>.cos.<Region>.myqcloud.com/en.srt', // Subtitles file
    kind: 'subtitles',
    srclang: 'en',
    label: 'English',
    default: 'false',
  }, true);
});
```

Get code samples:
- [Sample code for multilingual subtitles configuration](https://github.com/tencentyun/cos-demo/blob/main/cos-video/examples/web/tcplayer/multiLanguage.html)

