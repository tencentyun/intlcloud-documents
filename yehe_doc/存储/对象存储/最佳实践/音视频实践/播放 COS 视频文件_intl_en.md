## Overview

This document describes how to play back video files stored in a COS bucket with a web browser and implement some advanced video playback scenarios. The steps take [Tencent Cloud VOD superplayer (TCPlayer)](https://intl.cloud.tencent.com/document/product/266/33977) as an example.

## Directions

1. To prepare a COS video file link, you need to:
   - [Create a bucket](https://intl.cloud.tencent.com/document/product/436/13309)
   - [Upload an object](https://intl.cloud.tencent.com/document/product/436/13321)
   - Copy the object address in the [object information](https://intl.cloud.tencent.com/document/product/436/13326)
2. Import the player style and script files into the page:
```
<!--Player style file-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.min.css" rel="stylesheet"/>
<!--If you want to play back HLS videos through HTML5 in a browser such as Chrome and Firefox, you need to import `hls.min.0.13.2m.js` before importing `tcplayer.v4.2.2.min.js`.-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/libs/hls.min.0.13.2m.js"></script>
<!--Player script file-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.v4.2.2.min.js"></script>
```
>?We recommend you deploy the above static resources on your own when using the player SDK. [Click here to download the player resources](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip). Deploy the folder generated after decompression. Do not adjust the directories in the folder; otherwise, resource import exceptions may occur.
>
3. Set the player container node.
Add a player container where you want to play back videos. For example, you can add the following code to `index.html` (the container ID, width, and height are customizable).
```
   <video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
   </video>
```
>?
> - The player container must be a `<video>` tag.
> - The `player-container-id` in the sample is the ID of the player container, which can be customized.
> - We recommend you set the size of the player container zone through CSS, which is more flexible than the attribute and can achieve effects such as fit to full screen and container adaption.
> - The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include `meta` (only loads the metadata after the page is loaded) and `none` (does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
> - The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback when the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
> - If the `x5-playsinline` attribute is set, the X5 UI player will be used in the TBS kernel.
> 
4. Initialize the player and pass in the COS video file object URL.
```
   var player = TCPlayer('player-container-id', {}); // `player-container-id` is the player container ID, which must be the same as that in HTML
   player.src(url); // Playback URL
```

## Advanced Use Cases

### Use case 1. Playing publicly readable video files

There are two types of public read permissions of buckets: public read/private write and public read/write. Under the public read/private write permission, anyone (including anonymous visitors) has read permission for the objects in the bucket, but only the bucket creator and authorized accounts have write permission for them. Under the public read/write permission, anyone (including anonymous visitors) has read/write permissions for objects in the bucket, which is not recommended.

The steps to playing back a publicly readable video file are as follows:
1. Set the bucket as publicly readable as instructed in [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
2. Upload the video file and copy its object address from [object information](https://intl.cloud.tencent.com/document/product/436/13326).
3. Use TCPlayer to play back the publicly readable video file at its address based on the previous steps. The code is as follows:
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.mp4')
   </script>
```
4. View the effect.


### Use case 2. Playing back privately readable video files

To ensure the security of bucket data, we generally recommend you set the private read/write permission for your bucket. In this case, only the bucket creator and authorized accounts can read/write the objects in the bucket, while others cannot.

The steps to playing back a privately readable video file are as follows:
1. Set the bucket as privately readable as instructed in [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
2. As the bucket is privately readable, the address of the accessed object needs to carry a signature. There are three ways:
 - Option 1. **Copy the temporary link** in the [object information](https://intl.cloud.tencent.com/document/product/436/13326), which carries a signature parameter valid for one hour.

 - Options 2 and 3. Use an API or SDK to calculate the signature of your object. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
The SDK option is recommended, which can calculate your object signature more conveniently and securely.
3. Use TCPlayer to play back the privately readable video file at its address **with a signature** based on the previous steps. The code is as follows:
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.mp4?<Authorization>')
   </script>
```
4. View the effect.


### Use case 3. Playing back publicly readable HLS video file

>? **HTTP Live Streaming (HLS)** is an HTTP-based video streaming protocol released by Apple, which is part of Apple's QuickTime X and iPhone software systems. It works by dividing an entire stream into small HTTP-based files for multipart download. While a media stream is playing, the client can choose to download the same resource at different speeds from different sources, allowing the streaming session to adapt to different data rates. When starting a streaming session, the client downloads an extended M3U (m3u8 playlist) file containing metadata to find available media streams.
>

COS data processing provides the [HLS video transcoding](https://intl.cloud.tencent.com/document/product/436/46409) feature. You can play back HLS video files based on a transcoding job in the COS data workflow.

1. Select an HLS transcoding job in the system template and configure the job to generate an HLS video file as instructed in [Configuring Job](https://intl.cloud.tencent.com/document/product/436/46409).

2. Copy the generated m3u8 file object address.

3. Use TCPlayer to play back the **publicly readable HLS** video file at its address based on the previous steps. The code is as follows:
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.m3u8')
   </script>
```
4. View the effect.


### Use case 4. Playing back privately readable HLS video files

On the basis of use case 3, to ensure the security of bucket data, you can set the bucket as privately readable/writable, and then play back private HLS video files by using the PM3U8 API. The steps are as follows:
1. Set the bucket as privately readable as instructed in [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
2. Since the bucket is private, you need to set a request signature for each TS segment. COS provides a **PM3U8** API to allow carrying the `?ci-process=pm3u8&expires=3600` parameter when requesting m3u8 files. In this way, the request paths for the TS segments in the returned file can carry the corresponding request signature.
  - The request result of an ordinary m3u8 file is as follows, where the TS segment don't carry a signature:
     ![image-20211105162546606](https://qcloudimg.tencent-cloud.cn/raw/6209b43447acb028380ecc9a630b0fa7.png)
  - After the **PM3U8 API** is used, the request result is as follows, where the TS segments carry a signature: ![image-20211105163202007](https://qcloudimg.tencent-cloud.cn/raw/d6eff5820f5aad79876c0cd65147ae64.png)
3. Use TCPlayer to play back the **privately readable HLS** video file at its address based on the previous steps. The code is as follows:
```
   <script>
     var tcplayer = TCPlayer("player-container-id", {})
     tcplayer.src('https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/test.m3u8?ci-process=pm3u8&expires=3600&sign')
   </script>
```


