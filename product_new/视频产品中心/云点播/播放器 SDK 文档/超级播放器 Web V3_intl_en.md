
This document describes the we superplayer of VOD, which can be quickly integrated with your own web applications through flexible APIs to implement video playback. This document is intended for developers who have a basic knowledge of JavaScript.

## Overview of Capabilities
The VOD superplayer implements video playback via the HTML5 `<video>` tag and Flash. It enables a browser that does not support video playback natively to play back videos, delivering a unified video experience across platforms. In addition, it features hotlink protection and DRM-encrypted playback with the aid of the VOD service.

### Supported video formats and platforms

| Browser/Format   | MP4 | HLS | DASH |
|:----------------|:---:|:---:|:----:|
| Chrome          |  ✔  |  ✔  |  ✔   |
| Firefox         |  ✔  |  ✔  |  ✔   |
| Edge            |  ✔  |  ✔  |  ✔   |
| QQ Browser   |  ✔  |  ✔  |  ✔   |
| Mac Safari      |  ✔  |  ✔  |  ✔   |
| iOS Safari      |  ✔  |  ✔  |  ✖   |
| iOS WeChat/QQ     |  ✔  |  ✔  |  ✖   |
| Android Chrome  |  ✔  |  ✔  |  ✔   |
| Android WeChat/QQ |  ✔  |  ✔  |  ✖   |
| Mobile QQ Browser  |  ✔  |  ✔  |  ✖   |
| IE 11/10/9/8     |  ✔  |  ✔  |  ✖   |

>
>- Only the H.264 video encoder is supported.
>- Chrome and Firefox on Windows and macOS are supported.
>- Chrome, Firefox, Edge, and QQ Browser need to load hls.js when playing back HLS files.
>- Chrome, Firefox, Edge, Android Chrome, and macOS Safari need to load dash.js when playing back DASH files.
>- Android WeChat and QQ, which have the TBS kernel, natively support MP4 and HLS.
>- Flash is needed to play back videos in IE 8 and HLS files in IE 9/10/11. Please make sure that the browser supports Flash.
>- IE 8 is supported only on Windows 7.

The player is compatible with common browsers and can automatically identify the platform to use the optimal playback scheme. For example, it will use the Flash player in IE 11/10/9/8 to enable the browser to play HLS videos through HTML5, preferably use the HTML5 technology in modern browsers such as Chrome for video playback, and directly use the HTML5 technology or the browser kernel capabilities in mobile browsers.

### Adaptive bitrate streaming service on the VOD Platform
Currently, the most widely used adaptive bitstream formats are HLS and Dash. Adaptive bitrate streaming supports dynamic selection of the appropriate bitrate based on bandwidth and commercial-grade DRM, while the player only plays back the adaptive streams of videos. Therefore, videos to be played back via this player need to be [transcoded to adaptive bitstream](https://intl.cloud.tencent.com/document/product/266/33942) through VOD.

## Preparations
### Step 1. Activate the service
Sign up for a Tencent Cloud account at [Tencent Cloud's official website](https://intl.cloud.tencent.com/) and activate the VOD service.
### Step 2. Upload a video and transcode it
After the VOD service is activated, you need to [upload a video](https://intl.cloud.tencent.com/document/product/266/33890) and [transcode](https://intl.cloud.tencent.com/document/product/266/33890) it.
### Step 3. Get the ID and APPID
1. Get ID (`fileid`): after a video is uploaded, you can [view the video ID](https://intl.cloud.tencent.com/document/product/266/33890) in "Media Assets".

2. Get APPID: it can be viewed in **Tencent Cloud Console** > **[Account Info](https://console.cloud.tencent.com/developer)**.

### Step 4. Transcode to adaptive bitstream and get `playDefinition`
You can initiate an [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) task for the uploaded video through ProcessMedia <!-- (https://intl.cloud.tencent.com/document/product/266/34125) -->:
You are recommended to enter 10 for `MediaProcessTask.AdaptiveDynamicStreamingTaskSet.Definition` in the API parameter, indicating transcoding to adaptive bitstream in HLS format. For common parameter combinations, VOD provides a [preset adaptive bitrate streaming template](https://intl.cloud.tencent.com/document/product/266/33932#preset-adaptive-bitrate-streaming-templates).


## Initializing Web Player
After the preparations are completed, you can add a video player to your webpage in the following steps.

### Step 1. Import files into the page
Import the player style and script files into the right places:
```
 <link href="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.css" rel="stylesheet">
 <!--If you want to play back HLS and Dash videos via HTML5 in a modern browser such as Chrome and Firefox, you need to import hls.js and dash.js before importing tcplayer.min.js.-->
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/hls.min.0.12.4.js"></script>
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/libs/dash.all.min.2.9.3.js"></script>
 <!--Player script file-->
 <script src="//imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.min.js"></script>
```

### Step 2. Place the player container
Place the player container at the desired place on the page. For example, add the following code to index.html (the container ID, width, and height can be customized).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

Here:
- The player container must be a `<video>` tag.
- The `player-container-id` is the ID of the player container, which can be customized.
- You are recommended to set the size of the player container zone through CSS which is more flexible than the attribute and can achieve effects such as fit to full screen and container adaption.
- The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include:
	- `meta`: it only loads the metadata after the page is loaded.
	- `none`: it does not load the video after the page is loaded. Due to system restrictions, videos will not be automatically loaded on mobile devices.
- The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback in case where the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
- If the `x5-playsinline` attribute is set, the X5 UI player will be used in the TBS kernel.

### Step 3. Initialize the code
Add the following initialization script to the page initialization code to pass in the `fileID` and `APPID` obtained in the preparations.
```
var player = TCPlayer('player-container-id', { // player-container-id is the player container ID, which must be the same as that in HTML
    fileID: '7447398157015849771', // Pass in the `fileID` of the video to be played back, which is required
    appID: '1256993030', // Pass in the `appID` of the VOD account, which is required
    playDefinition: '10', // Pass in the playback template, which is required
  });
```

>The video to be played back needs to be transcoded by Tencent Cloud as it cannot be guaranteed that the source video can be played back normally in the browser.

## Samples
[Sample code](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-base.html)
## How to Use
Some of the features of the player are described in detail below, including best practices and precautions.
### Setting the player size
Here are a few ways to set the size of the player:

* The width and height attributes can be set for the `<video>` tag. They should be in px (for example, width = "100px" or width = 100) but not percentage.
*	The size can be set through CSS which supports values in px and percentage (e.g., width:"100px" or width:"100%").

>
>- If you do not set the width and height, the player will set its display size to the obtained resolution of the video. If the viewable zone size of the browser is smaller than the video resolution, the player will overflow the browser's viewable zone; therefore, this is generally not recommended. The best practice is to set the player size through CSS.
>- Skilled use of CSS can achieve effects such as fit to full screen and container adaption.

Examples:
- [Set size through CSS](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-size.html)
- [Fit to the viewable zone of the webpage](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-size-full-viewport.html)
- [Proportional adaption](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-size-adaptive.html)

### Resumable playback feature
The prerequisite for enabling resumable playback is that the video is played back through `fileID`. Only with a unique `fileID` can the player record the playback time point of the video. If the page is closed before playback is completed, playback can be resumed from where it left off when the page is opened again in the same browser. Resumable playback can be enabled with the following parameters:

```
var player = TCPlayer('player-container-id', {
    fileID: '', // Pass in the `fileID` of the video to be played back, which is required
    appID: '', // Pass in the `appID` of the VOD account, which is required
    playDefinition: '', // Pass in the playback template, which is required
    plugins:{
        ContinuePlay: { // Turn on resumable playback
          // auto: true, // [Optional] whether to resume automatically after the video is played back
          // text: 'You left off at', // [Optional] prompt text
          // btnText: 'Resume' // [Optional] button text
        },
      }
  });
```
The effect after this feature is successfully enabled is as shown below:
![](https://mc.qcloudimg.com/static/img/e155be329a6fec959e1ad6b361add390/image.png)

Example: [Resumable playback](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-continue-play.html)

>
> - This feature is available only for videos that are transcoded by Tencent Cloud and played back through `fileID` and `appID`.
> - This feature stores the playback time point in `localStorage`, which should be supported by the browser.
> - This feature is unavailable for browser-hijacking playback.
> - This feature is not interoperable across platforms/browsers. For example, if the user left off in a PC browser, they cannot resume the playback in a mobile browser or another PC browser. If you want to implement this, you need to develop additional APIs on your own.

### Adjustable-speed playback
If it is supported by the browser, **adjustable-speed playback is enabled by default** for the player.

```
var player = TCPlayer('player-container-id', {
    fileID: '', // Pass in the `fileID` of the video to be played back, which is required
    appID: '', // Pass in the `appID` of the VOD account, which is required
    playbackRates: [0.5, 1, 1.25, 1.5, 2] // Set the adjustable-speed playback option, which is available only for HTML5
  });
```

>
> - If the browser does not support adjustable-speed playback, the button will not be displayed on the player.

### Setting player logo
The VOD superplayer supports configuring the player logo. You can select a player configuration in **[Web Player Management](https://console.cloud.tencent.com/vod/distribute-play/web-player)** and set the logo information in **Appearance**. After the logo information is set, when a video is played back with this player configuration, the logo will be displayed at the specified position.

Example: [Displaying logo](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-logo.html)

>
> - After the player is configured in the console, it may take about 10 minutes for the configuration to take effect on all CDN nodes.
> - The set logo cannot be displayed for browser-hijacking playback.

### Roll image feature
The VOD superplayer supports configuring pre-, mid-, and post-roll images where hyperlinks can be added. You can select a player configuration in **[Web Player Management](https://console.cloud.tencent.com/vod/distribute-play/web-player)** and set the roll image information in **Roll Image**.

- The default roll image display style is horizontally and vertically centered. If the image is larger than the player's display zone, it will be scaled down proportionally according to the width of the player and then horizontally centered. The excessive part of the image will not be displayed.
- You can customize the display style of the roll image through CSS.
```
.tcp-image-patch-start{} /* Pre-roll image style class */
.tcp-image-patch-pause{} /* Mid-roll image style class */
.tcp-image-patch-ended{} /* Post-roll image style class */
```

Example: [Roll image](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-image-patch.html)

>
>- To prevent the video initialization speed from being affected by a large roll image, you are recommended to use an image with a size of up to 50 KB and dimensions that do not exceed the display zone of the player.
>- After the player is configured in the console, it may take about 10 minutes for the configuration to take effect on all CDN nodes.
>- The set roll image cannot be displayed for browser-hijacking playback.

### Thumbnail preview
The VOD superplayer supports thumbnail preview. The thumbnail and VTT file of the video can be generated by using server APIs. For more information, please see [Screencapturing - Image Sprite Generating](https://intl.cloud.tencent.com/document/product/266/33940#.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.A8.A1.E6.9D.BF).


The effect after this feature is successfully enabled is as shown in the figure below:
![](https://main.qcloudimg.com/raw/cf668bbf1a991c347fbeacb6555831c1.png)

Example: [Thumbnail preview](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-vtt-thumbnail.html)

>
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.
>- The more the generated thumbnails, the more accurate the progress bar preview, but the slower the loading. You need to find the desired balance.

### Changing `fileID` for playback
The video can be changed for playback by instantiating the object's `loadVideoByID(args)` method. The supported parameters are as follows:
```
player.loadVideoByID({
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  playDefinition: '', // Pass in the playback template, which is required
  t: '', // Please see the description of key hotlink protection
  us: '', // Please see the description of key hotlink protection
  sign:'', // Please see the description of key hotlink protection
  exper:'' // Please see the description of the preview feature
});
```

Example: [Changing `fileID` for playback](http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-change-file.html)

### Mirroring feature
You can activate the mirroring feature to flip over the video screen as shown below:
![](https://main.qcloudimg.com/raw/d5886d7d550be72b608077f341299610.png)

Display the mirroring option in the right click menu:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  playDefinition: '', // Pass in the playback template, which is required
  plugins: {
    ContextMenu: {
      mirror: true
    }
  }
});
```

Example: [Mirroring feature](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-mirror.html)

>This feature is unavailable for browser-hijacking playback.

### Progress bar marking
You can enable progress bar marking in the player by adding timestamps <!--API (https://intl.cloud.tencent.com/document/product/266/14190)--> through the server API as shown below:
![](https://main.qcloudimg.com/raw/70d880065adce22cb64270f4999558f8.png)

How to enable in the player:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  playDefinition: '', // Pass in the playback template, which is required
  plugins: {
    ProgressMarker: true
  }
});
```

Example: [Progress bar marking](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-progress-marker.html)

>
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.

### Referer hotlink protection
For detailed direction to enable this feature, please see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985).

The following parameters should be added during player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the `fileID` of the video to be played back, which is required
     appID: '', // Pass in the `appID` of the VOD account, which is required
     playDefinition: '', // Pass in the playback template, which is required
     flash:{
         swf: '//[Tencent Cloud's isolated domain name]/vod-player/[appID]/[fileID]/tcplayer/player.swf' // Address of the .swf file, which is required
     }
   });
```
The swf URL needs to be passed in. If the browser uses Flash for playback, the Flash player will be obtained from this address. When the Flash player initiates a video request, the request's referer will bring this URL or the URL of the page.

>
>- The referer of the video request initiated by the player in Flash mode will bring the swf URL in IE and Firefox.
>- You can also download the player.swf file to your CDN server and pass in the swf parameter pointing to the path to your CDN server.
>- The isolated domain name provided by Tencent Cloud is a domain name exclusive to each user. One appID corresponds to one domain name, which is usually in the format of:
>`[appID].vod2.myqcloud.com`.
>- You need to add the domain name of the player swf URL to the whitelist before videos for which referer hotlink protection is enabled can be played in Flash mode.
>- The Flash swf file of the player is stored under the `imgcache.qq.com` domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- If iframe is embedded in the player page, the referer of the video request will bring `iframe src`.

#### Support conditions by browser
The support for DRM by each browser is as follows.

| Browser        | Widevine | FairPlay | SimpleAES |
|-----------------|----------|----------|-----------|
| Chrome (PC/Mac)  | ✔        | ✖        | ✔         |
| Firefox (PC/Mac) | ✔        | ✖        | ✔         |
| Edge            | ✖        | ✖        | ✔         |
| Mac Safari      | ✖        | ✔        | ✔         |
| iOS Safari      | ✖        | ✔        | ✔         |
| iOS Chrome      | ✖        | ✖        | ✔         |
| iOS WeChat/QQ     | ✖        | ✖        | ✔         |
| Android Chrome  | ✔        | ✖        | ✔         |
| Android WeChat/QQ | ✖        | ✖        | ✔         |
| IE 8, 9, 10, 11     | ✖        | ✖        | ✔         |

> Flash is used for playback in IE.

#### How to use

First, the application needs to get the token from your **business backend**. 
Then, play back the video through `FileId` and `Token` with the following playback code:

```
var player = TCPlayer('player-container-id', {
  appID:  '', // Pass in the `appID` of the VOD account, which is required
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  playDefinition: '' // Pass in the playback template, which is required for playing back DRM content
  plugins: {
    DRM: {
      token: '', // Pass in the token distributed by your backend service, which is required for playing back DRM content
      certificateUri: '', // Pass in the download address of the FairPlay certificate, which is required for playing back FairPlay-encrypted content
    }
  }``
});
```
The player will select an appropriate playback scheme based on the priority according to the playback template ID passed in and the support condition of the current browser. The priority order for DRM scheme selection is **Widevine** > **FairPlay** > **SimpleAES**; for example:
- If the `playDefinition` passed in is 20, the player will select the encrypted outputs of Widevine, FairPlay, or SimpleAES for playback.
- If the `playDefinition` passed in is 12, the player will select the encrypted outputs of Widevine or FairPlay for playback.
- If the `playDefinition` passed in is 10, the player will select unencrypted outputs of HLS or DASH for playback.

Example: [DRM automatic recognition playback](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod-v3/tcplayer-vod-drm-token-auto.html)

>
>- Commercial-grade DRM content can only be played back on pages using HTTPS.
>- Currently, DRM content only supports adaptive bitrate.
