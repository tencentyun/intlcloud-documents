
This document describes the web superplayer of VOD, which can be quickly integrated with your own web applications through flexible APIs to implement video playback. This document is intended for developers who have a basic knowledge of JavaScript.

## Overview of Capabilities
The VOD superplayer implements video playback through the HTML5 `<video>` tag and Flash. It enables a browser that does not support video playback natively to play back videos, delivering a unified video experience across platforms. In addition, it features hotlink protection and playback of encrypted general HLS videos with the aid of the VOD service.

### Supported video formats and platforms

| Browser/Format     | MP4 | HLS |
|:----------------|:---:|:---:|
| Chrome          |  ✔  |  ✔  |
| Firefox         |  ✔  |  ✔  |
| Edge            |  ✔  |  ✔  |
| QQ Browser       |  ✔  |  ✔  |
| Safari for macOS      |  ✔  |  ✔  |
| Safari for iOS      |  ✔  |  ✔  |
| WeChat/QQ for iOS     |  ✔  |  ✔  |
| Chrome for Android  |  ✔  |  ✔  |
| WeChat/QQ for Android |  ✔  |  ✔  |
| Mobile QQ Browser  |  ✔  |  ✔  |
| IE 8, 9, 10, 11     |  ✔  |  ✔  |

>?
>- Only the H.264 video encoder is supported.
>- Chrome and Firefox on Windows and macOS are supported.
>- Chrome, Firefox, Edge, and QQ Browser need to load `hls.js` when playing back HLS files.
>- WeChat and QQ for Android, which have the TBS kernel, natively support MP4 and HLS.
>- Flash is needed to play back videos in IE 8 and HLS files in IE 9/10/11. Please make sure that the browser supports Flash.
>- IE 8 is supported only on Windows 7.

The player is compatible with common browsers and can automatically identify the platform to use the optimal playback scheme. For example, it will use the Flash player in IE 11/10/9/8 to enable the browser to play HLS videos through HTML5, preferably use the HTML5 technology in modern browsers such as Chrome for video playback, and directly use the HTML5 technology or the browser kernel capabilities in mobile browsers.

### Transcoding service on VOD platform
As MP4 and HLS (M3U8) are currently the most widely supported formats in desktop and mobile browsers, Tencent Cloud's VOD platform will eventually publish the uploaded videos in MP4 or HLS (M3U8) format.

## Preparations

For the specific process, please see [Using Superplayer for Playback - Integration Guide](https://intl.cloud.tencent.com/document/product/266/38098).

## Initializing Web Player
After the preparations are completed, you can add a video player to your webpage in the following steps:
### Step 1. Import files into the page
Import the player style and script files into the right places:
```
 <link href="https://imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.css" rel="stylesheet">
 <!--If you want to play back HLS videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `hls.min.0.13.2m.js` before importing `tcplayer.v4.1.min.js`.-->
 <script src="https://imgcache.qq.com/open/qcloud/video/tcplayer/libs/hls.min.0.13.2m.js"></script>
 <!--Player script file-->
 <script src="https://imgcache.qq.com/open/qcloud/video/tcplayer/tcplayer.v4.1.min.js"></script>
```

If your business is in a domain-limited region, you can import the following link:
```
 <link href="https://cloudcache.tencent-cloud.com/open/qcloud/video/tcplayer/tcplayer.css" rel="stylesheet">
 <!--If you want to play back HLS videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `hls.min.0.13.2m.js` before importing `tcplayer.v4.1.min.js`.-->
 <script src="https://cloudcache.tencent-cloud.com/open/qcloud/video/tcplayer/libs/hls.min.0.13.2m.js"></script>
 <!--Player script file-->
 <script src="https://cloudcache.tencent-cloud.com/open/qcloud/video/tcplayer/tcplayer.v4.1.min.js"></script>
```


>?Currently, the module load method for frameworks such as VUE and React is not supported. You can use the player by importing the relevant scripts globally.

### Step 2. Place the player container
Place the player container at the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>- The player container must be a `<video>` tag.
>- The `player-container-id` in the sample is the ID of the player container, which can be customized.
>- We recommend you set the size of the player container zone through CSS, which is more flexible than the attribute and can achieve effects such as fit to full screen and container adaption.
>- The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include `meta` (which only loads the metadata after the page is loaded) and `none` (which does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
>- The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback in case where the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
>- If the `x5-playsinline` attribute is set, the X5 UI player will be used in the TBS kernel.

### Step 3. Initialize the code
Add the following initialization script to the page initialization code to pass in the `fileID` (video ID in **[Media Assets](https://console.cloud.tencent.com/vod/media)**) and `appID` (which can be viewed in **Account Info** > **[Basic Info](https://console.cloud.tencent.com/developer)**) obtained in the preparations.
```
var player = TCPlayer('player-container-id', { // `player-container-id` is the player container ID, which must be the same as that in HTML
    fileID: '5285890799710670616', // Pass in the `fileID` of the video to be played back, which is required
    appID: '1400329073' // Pass in the `appID` of the VOD account, which is required
  });
```

>!The video to be played back needs to be transcoded by Tencent Cloud as it cannot be guaranteed that the source video can be played back normally in the browser.

## Complete Sample Page
Click [Sample Code](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html) to enter the sample code page, right-click the page, and select the option to **view the webpage source code** to view the sample source code.
## How to Use
Some of the features of the player are described in detail below, including best practices and precautions.
### Setting the player size
Here are a few ways to set the size of the player:

* The width and height attributes can be set for the `<video>` tag. They should be in px (for example, `width = "100px"` or `width = 100`) but not percentage.
*	The size can be set through CSS which supports values in px and percentage (such as `width:"100px"` or `width:"100%"`).

>?
>- If you do not set the width and height, the player will set its display size to the obtained resolution of the video. If the viewable zone size of the browser is smaller than the video resolution, the player will overflow the browser's viewable zone; therefore, this is generally not recommended. The best practice is to set the player size through CSS.
>- Skilled use of CSS can achieve effects such as fit to full screen and container adaption.

#### Sample
- [Set size through CSS](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size.html)
- [Fit to the viewable zone of the webpage](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-full-viewport.html)
- [Implement proportional adaption](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-adaptive.html)

Enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.

### Resumable playback feature
The prerequisite for enabling resumable playback is that the video is played back through `fileID`. Only with a unique `fileID` can the player record the playback time point of the video. If the page is closed before playback is completed, playback can be resumed from where it left off when the page is opened again in the same browser. Resumable playback can be enabled with the following parameters:

```
var player = TCPlayer('player-container-id', {
    fileID: '', // Pass in the `fileID` of the video to be played back, which is required
    appID: '', // Pass in the `appID` of the VOD account, which is required
    plugins:{
        ContinuePlay: { // Enable resumable playback
          // auto: true, // Whether to resume automatically after the video is played back, which is optional
          // text: 'You left off at', // Prompt text, which is optional
          // btnText: 'Resume' // Button text, which is optional
        },
      }
  });
```
The effect after this feature is successfully enabled is as shown below:
![](https://main.qcloudimg.com/raw/90bffb38a6658744b3012196676fef8a.png)

#### Sample
Click [Resumable Playback](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-continue-play.html) to enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.
>!
> - This feature is available only for videos that are transcoded by Tencent Cloud and played back through `fileID` and `appID`.
> - This feature stores the playback time point in `localStorage`, which should be supported by the browser.
> - This feature is unavailable for browser-hijacking playback.
> - This feature is not interoperable across platforms/browsers. For example, if the user left off in a PC browser, they cannot resume the playback in a mobile browser or another PC browser. If you want to implement this, you need to develop additional APIs on your own.

### Adjustable-Speed playback
If it is supported by the browser, adjustable-speed playback is enabled by default for the player.

```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  playbackRates: [0.5, 1, 1.25, 1.5, 2] // Set the adjustable-speed playback option, which is available only for HTML5
});
```

>!
> - If the browser does not support adjustable-speed playback, the button will not be displayed on the player.


### Thumbnail preview
The VOD superplayer supports thumbnail preview. There are two ways to enable this feature:
1. Generate the thumbnail and VTT files of the video by using the server API. For more information, please see [Screencapturing - Image sprite generating template](https://intl.cloud.tencent.com/document/product/266/33940).
2. Generate the thumbnail and VTT files on your own and pass in the URLs of the two files to the player. For more information, please see the sample "Thumbnail preview - Pass in thumbnail and VTT files".

#### Sample
- [Thumbnail preview - Generation on server](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail.html)
- [Thumbnail preview - Pass in thumbnail and VTT files](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail-src.html)

Enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.
>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.
>- The more the generated thumbnails, the more accurate the progress bar preview, but the slower the loading. You need to find the desired balance.

### Changing fileID for playback
The video can be changed for playback by instantiating the object's `loadVideoByID(args)` method. The supported parameters are as follows:
```
player.loadVideoByID({
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  t: '', // Please see the description of key hotlink protection
  us: '', // Please see the description of key hotlink protection
  sign:'', // Please see the description of key hotlink protection
  exper:'' // Please see the description of the preview feature
});
```

#### Sample
Click [Changing fileID for Playback](http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file.html) to enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.

### Mirroring feature
You can enable the mirroring feature to flip over the video screen as shown below:
![](https://main.qcloudimg.com/raw/500ef27aa1f88712a76e1fe58b256556.png)
Display the mirroring option in the right-click menu:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  plugins: {
    ContextMenu: {
      mirror: true
    }
  }
});
```

#### Sample
Click [Mirroring Feature](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-mirror.html) to enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.

>!This feature is unavailable for browser-hijacking playback.

### Progress bar marking
You can enable progress bar marking in the player by adding timestamps through the server API as shown below:

How to enable in the player:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  plugins: {
    ProgressMarker: true
  }
});
```

#### Sample
Click [Progress Bar Marking](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-progress-marker.html) to enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.

>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.

### HLS adaptive bitrate playback
- The Master Playlist of the HLS specification can be played back at an adaptive bitrate according to the network speed. During video download, if the network speed is high enough to download TS segments with a high bitrate, the player will play back the TS segments; otherwise, it will play back TS segments with a low bitrate. This feature is supported by most mobile and desktop browsers.
- When the HLS Master Playlist is played back, the player's definition selection feature will become selection of a specified bitrate or automatic selection based on the network speed.

>!
>- The automatic switch logic is used by default for adaptive bitrate playback on all devices. 
>- As certain browsers do not have the corresponding APIs or support MSE, manual selection of a specified definition is unavailable for such browsers, and the option for switching definitions is also unavailable.
>- Manual selection of a specified bitrate is not supported in Flash playback mode.

#### Sample
Click [HLS Master Playlist](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-hls-masterplaylist.html) to enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.

### Referer hotlink protection
For detailed directions on how to enable this feature, please see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985). The following parameters should be added during player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the `fileID` of the video to be played back, which is required
     appID: '', // Pass in the `appID` of the VOD account, which is required
     flash:{
         swf: '//[Tencent Cloud's isolated domain name]/vod-player/[appID]/[fileID]/tcplayer/player.swf' // .swf file address, which is required
     }
   });
```
The SWF URL needs to be passed in. If the browser uses Flash for playback, the Flash player will be obtained from this address. When the Flash player initiates a video request, the request's referer will bring this URL or the URL of the page.

>?
>- The referer of the video request initiated by the player in Flash mode will bring the SWF URL in IE and Firefox or the page URL in Chrome.
>- You can also download the `player.swf` file to your CDN server and pass in the SWF parameter pointing to the path to your CDN server.
>- The isolated domain name provided by Tencent Cloud is a domain name exclusive to each user. One appID corresponds to one domain name, which is usually in the format of `[appID].vod2.myqcloud.com`.
>- You need to add the domain name of the player SWF URL to the allowlist before videos for which referer hotlink protection is enabled can be played back in Flash mode.
>- The Flash SWF file of the player is stored under the `imgcache.qq.com` domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- If your business is in a domain-limited region, the Flash SWF file needs to be stored under the `cloudcache.tencent-cloud.com` domain name by default.
>- If iframe is embedded in the player page, the referer of the video request will bring `iframe src`.

### Key hotlink protection
For detailed directions on how to enable this feature, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986). The following parameters should be added during player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the `fileID` of the video to be played back, which is required
     appID: '', // Pass in the `appID` of the VOD account, which is required
     psign:''
   });
```
The `psign` parameter is the superplayer signature. For its specific description, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

>!If referer hotlink protection is also enabled, simply add the parameters to the sample code of the referer hotlink protection configuration.

### Preview
You can use the preview feature only after enabling key hotlink configuration. For detailed directions on how to enable it, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986). The following parameters should be added during player initialization:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  psign:''
});
```
The `psign` parameter is the superplayer signature. For its specific description, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

>!
>- The duration of video playback in the player is the length specified by the `exper` parameter. Unlike other preview features that control the playback duration on the player side, the player does not get the complete video.
>- Preview works by clipping the video according to the video keyframes, and the actually clipped preview video may be shorter than the pre-configured preview duration value.
>- The player will still display the original video duration after the preview feature is enabled (the preview duration will be displayed for HLS videos in Chrome and Firefox).

### Encrypted HLS playback
The playback page must load `hls.js`, and the playback sample code is as follows:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the `fileID` of the video to be played back, which is required
     appID: '' // Pass in the `appID` of the VOD account, which is required
     psign:''
   });
```
The `psign` parameter is the superplayer signature. For its specific description, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

>!
>- If the URL of the playback page or Flash SWF has a different domain name from the decryption key server, the key server needs to deploy `crossdomain.xml` and cross-origin resource sharing (CORS) to allow Flash and JavaScript to obtain the decryption key across origins.
>- The domain name of SWF URL is configured in `crossdomain.xml`, which must be placed in the root directory of the key server.
>- The Flash SWF file of the player is stored under the `imgcache.qq.com` domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- If your business is in a domain-limited region, the Flash SWF file needs to be stored under the `cloudcache.tencent-cloud.com` domain name by default.
>- Videos can be encrypted only once. Please strictly follow the steps in the video encryption document.
>- The correct length of a decryption key is 16 bytes, and there cannot be blank characters at the beginning and the end.

### Video statistics
Right-click to open the video statistics panel and view the real-time video information.
Display the video statistics option in the right-click menu:
```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  plugins: {
    ContextMenu: {
      statistic: true
    }
  }
});
```

#### Sample
Click [Video Statistics](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file-statistic.html) to enter the sample code page, right-click on the page, and select the option to **view the webpage source code** to view the sample source code.

>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.


## Changelog
TCPlayer is continuously updated and optimized. The following are the published major versions of TCPlayer:

| Date | Version | Update
|-----------------|--------- |-------------------------------------------- |
| July 10, 2020 | 4.1 | 1. Changed the default `hls.js` version to 0.13.2. <br> 2. Added the support for key hotlink protection. <br>3. Fixed other known issues. |
| June 17, 2020 | 4.0 |   1. Fixed the problem where the original video duration was displayed as the video preview duration. <br>2. Added the backend definition configuration. <br>3. Fixed other known issues. |
