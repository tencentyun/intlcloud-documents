This document describes the Tencent Cloud RT-Cube Superplayer for web (TCPlayer), which can be quickly integrated with your own web applications through flexible APIs to implement video playback. This document is intended for developers with a basic knowledge of JavaScript.

## Capability Overview
The Tencent Cloud RT-Cube Superplayer for web implements video playback through the HTML5 `<Video>` tag and Flash. It enables a browser that does not support video playback natively to play back videos, delivering a unified video experience across platforms. In addition, it features hotlink protection and playback of encrypted general HLS videos with the aid of the VOD service.

[](id:function)
### Supported features

<Table>
  <tr>
    <th width="50px" style="text-align:center">Feature/Browser</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQ Browser</th>
      <th width="50px" style="text-align:center">Safari on macOS</th>
      <th width="50px" style="text-align:center">Safari on iOS</th>
      <th width="50px" style="text-align:center">WeChat/QQ on iOS</th>
      <th width="50px" style="text-align:center">Chrome on Android</th>
      <th width="50px" style="text-align:center">WeChat/QQ on Android</th>
      <th width="50px" style="text-align:center">Mobile QQ Browser</th>
      <th width="50px" style="text-align:center">Internet Explorer 8, 9, 10, and 11</th>
  </tr>
   <tr>
         <td style="text-align:center">MP4 format</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
      <tr>
         <td style="text-align:center">HLS format</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">Player dimensions configuration</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">Resumable playback</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">Adjustable-speed playback</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">Thumbnail preview</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">- <br>(Supported for 11)</td>
    </tr>
            <tr>
         <td style="text-align:center">Changing `fileID` for playback</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
            <tr>
         <td style="text-align:center">Mirroring</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
         <tr>
         <td style="text-align:center">Progress bar marking</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">HLS adaptive bitrate</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">Referer hotlink protection</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">Definition switch prompt</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
    </tr>
               <tr>
         <td style="text-align:center">Preview</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>
               <tr>
         <td style="text-align:center">Encrypted HLS playback</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
    </tr>
               <tr>
         <td style="text-align:center">Video statistics</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
    </tr>
               <tr>
         <td style="text-align:center">Prompt text customization</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
    </tr>

</Table>

>?
>- Only the H.264 video encoder is supported.
>- Chrome and Firefox on Windows and macOS are supported.
>- Chrome, Firefox, Edge, and QQ Browser need to load `hls.js` when playing back HLS files.
>- WeChat and QQ for Android, which have the TBS kernel, natively support MP4 and HLS.
>- The referer hotlink protection feature is implemented based on the `Referer` field in the HTTP request header. HTTP requests initiated by some Android browsers do not carry the `Referer` field.
>- Flash is needed to play back videos in Internet Explorer 8 and HLS files in Internet Explorer 9/10/11. Please make sure that the browser supports Flash.
>- Internet Explorer 8 is supported only on Windows 7.

The player is compatible with common browsers and can automatically identify the platform to use the optimal playback scheme. For example, it will use the Flash player in Internet Explorer 11/10/9/8 to enable the browser to play HLS videos through HTML5, preferably use the HTML5 technology for video playback in modern browsers such as Chrome, and directly use the HTML5 technology or the browser kernel capabilities in mobile browsers.

### Transcoding service on VOD platform
As MP4 and HLS (M3U8) are currently the most widely supported formats in desktop and mobile browsers, Tencent Cloud's VOD platform will eventually publish the uploaded videos in MP4 or HLS (M3U8) format.
[](id:preparation)
## Preparations

For the specific process, please see [Using Superplayer for Playback - Integration Guide](https://intl.cloud.tencent.com/document/product/266/38098).

## Initializing Web Player
After the preparations are completed, you can add a video player to your webpage in the following steps:
[](id:step1)
### Step 1. Import files into the page
Import the player style and script files into the right places:
```
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.min.css" rel="stylesheet">
 <!--If you want to play back HLS videos through HTML5 in a browser such as Chrome and Firefox, you need to import `hls.min.0.13.2m.js` before importing `tcplayer.v4.2.min.js`.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/libs/hls.min.0.13.2m.js"></script>
 <!--Player script file-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/tcplayer.v4.2.1.min.js"></script>
```

We recommend you deploy the resources on your own when using the player SDK. [Click here to download the player resources](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.1/release.zip).

Deploy the folder generated after decompression. Do not adjust the directories in the folder; otherwise, resource import exceptions may occur.

If the address of your deployment is `aaa.xxx.ccc`, then import the player style and script files into the right places:
```
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet">
 <!--If you want to play back HLS videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `hls.min.0.13.2m.js` before importing `tcplayer.v4.2.1.min.js`.-->
 <script src="aaa.xxx.ccc/libs/hls.min.0.13.2m.js"></script>
 <!--Player script file-->
 <script src="aaa.xxx.ccc/tcplayer.v4.2.1.min.js"></script>
```

>?Currently, the module load method for frameworks such as VUE and React is not supported. You can use the player by importing the relevant scripts globally.
[](id:step2)
### Step 2. Place the player container
Place the player container in the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>- The player container must be a `<Video>` tag.
>- The `player-container-id` in the sample is the ID of the player container, which can be customized.
>- We recommend you set the size of the player container zone through CSS, which is more flexible than the attribute and can achieve effects such as fit to full screen and container adaption.
>- The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include `meta` (only loads the metadata after the page is loaded) and `none` (does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
>- The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback when the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
>- If the `x5-playsinline` attribute is set, the X5 UI player will be used in the TBS kernel.
[](id:step3)
### Step 3. Initialize the code
Add the following initialization script to the page initialization code to pass in the `fileID` (video ID in **[Media Assets](https://console.cloud.tencent.com/vod/media)**) and `appID` (which can be viewed in **Account Info** > **[Basic Info](https://console.cloud.tencent.com/developer)**) obtained in the preparations.
```
var player = TCPlayer('player-container-id', { // `player-container-id` is the player container ID, which must be the same as that in HTML
    fileID: '5285890799710670616', // Pass in the `fileID` of the video to be played back, which is required
    appID: '1400329073' // Pass in the `appID` of the VOD account, which is required
  });
```

>!The video to be played back needs to be transcoded by Tencent Cloud as it cannot be guaranteed that the source video can be played back normally in the browser.
[](id:fullExample)
## Complete Sample Page
Click [Sample Code](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-base.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.
## How to Use
Some of the features of the player are described in detail below, including best practices and precautions.
### Setting the player size
Here are a few ways to set the size of the player:

* The width and height attributes can be set for the ![](https://main.qcloudimg.com/raw/9576adc95470eee7ec036688e6cae8c7.png) tag. They should be in px (for example, `width = "100px"` or `width = 100`) but not percentage.
*  The size can be set through CSS which supports values in px and percentage (such as `width:"100px"` or `width:"100%"`).

>?
>- If you do not set the width and height, the player will set its display size to the obtained resolution of the video. If the size of the browser’s visible area is smaller than the video resolution, the player will overflow the browser's visible area; therefore, this is generally not recommended. The best practice is to set the player size through CSS.
>- Skilled use of CSS can achieve effects such as fit to full screen and container adaption.

#### Samples
- [Set size through CSS](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size.html)
- [Fit to the visible area of the webpage](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-full-viewport.html)
- [Implement proportional adaption](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-size-adaptive.html)

Enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.

### Resumable playback
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
![](https://mc.qcloudimg.com/static/img/e155be329a6fec959e1ad6b361add390/image.png)

#### Samples
Click [Resumable Playback](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-continue-play.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.
>!
> - This feature is available only for videos that are transcoded by Tencent Cloud and played back through `fileID` and `appID`.
> - This feature stores the playback time point in `localStorage`, which should be supported by the browser.
> - This feature is unavailable for playback in a hijacked browser.
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
>- If the browser does not support adjustable-speed playback, the button will not be displayed on the player.
>- If you need to disable this feature, please see [Developer Guide](https://intl.cloud.tencent.com/document/product/266/42095).


### Thumbnail preview
The VOD superplayer supports thumbnail preview. There are two ways to enable this feature:
- Generate the thumbnail and VTT files of the video by using the server API. For more information, please see [Screencapturing - Image sprite generating template](https://intl.cloud.tencent.com/document/product/266/33940).
- Generate the thumbnail and VTT files on your own and pass in the URLs of the two files to the player. For more information, please see the sample "Thumbnail preview - Pass in thumbnail and VTT files".

The effect after this feature is successfully enabled is as shown in the figure below:
![](https://main.qcloudimg.com/raw/cf668bbf1a991c347fbeacb6555831c1.png)

#### Samples
- [Thumbnail preview - Generate on server](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail.html)
- [Thumbnail preview - Pass in thumbnail and VTT files](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-vtt-thumbnail-src.html)

Enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.
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
  psign:'' // Please see the description of key hotlink protection
});
```

#### Samples
Click [Changing fileID for Playback](http://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.

### Mirroring
You can activate the mirroring feature to flip over the video screen as shown below:
![](https://main.qcloudimg.com/raw/d5886d7d550be72b608077f341299610.png)
Display the mirroring option in the right click menu:
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

#### Samples
Click [Mirroring](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-mirror.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.

>!This feature is unavailable for playback in a hijacked browser.

### Progress bar marking
You can enable progress bar marking in the player by adding timestamps through the server API as shown below:
![](https://main.qcloudimg.com/raw/70d880065adce22cb64270f4999558f8.png)

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

#### Samples
Click [Progress Bar Marking](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-progress-marker.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.

>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.

### HLS adaptive bitrate playback
- The Master Playlist of the HLS specification can be played back at an adaptive bitrate according to the network speed. During video download, if the network speed is high enough to download TS segments with a high bitrate, the player will play back the TS segments; otherwise, it will play back TS segments with a low bitrate. This feature is supported by most mobile and desktop browsers.
- When the HLS Master Playlist is played back, the player's definition selection feature will become selection of a specified bitrate or automatic selection based on the network speed as shown below:
![](https://main.qcloudimg.com/raw/339d7dfb3a4d247deb70460edac35a0e.png)

>!
>- The automatic switch logic is used by default for adaptive bitrate playback on all devices. 
>- As certain browsers do not have the corresponding APIs or support MSE, manual definition selection is unavailable for such browsers, and the option for switching definitions is also unavailable.
>- Manual bitrate selection is not supported in Flash playback mode.

#### Samples
Click [HLS Master Playlist](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-hls-masterplaylist.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.

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
The SWF URL needs to be passed in. If the browser uses Flash for playback, the Flash player will be obtained from this address. When the Flash player initiates a video request, the referer in the request will carry this URL or the URL of the page.

>?
>- The referer in the video request initiated by the player in Flash mode will carry the SWF URL in Internet Explorer and Firefox or the page URL in Chrome.
>- You can also download the `player.swf` file to your CDN server and pass in the SWF parameter pointing to the path to your CDN server.
>- The isolated domain name provided by Tencent Cloud is a domain name exclusive to each user. One `appID` corresponds to one domain name, which is usually in the format of `[appID].vod2.myqcloud.com`.
>- You need to add the domain name of the player SWF URL to the allowlist before videos for which referer hotlink protection is enabled can be played back in Flash mode.
>- The Flash SWF file of the player is stored under the `imgcache.qq.com` domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- If your business is in a domain-limited region, the Flash SWF file needs to be stored under the `cloudcache.tencent-cloud.com` domain name by default.
>- If iframe is embedded in the player page, the referer of the video request will bring `iframe src`.

### Definition switch prompt
You can add the following prompt after enabling definition switch prompt:
![](https://main.qcloudimg.com/raw/0d5559bd07681929fd45ce0b8a2353e9.png)

The following parameters should be added during player initialization:
```
var tcplayer = TCPlayer('player-container-id', { // `player-container-id` is the player container ID, which must be the same as that in HTML
    fileID: '', // Pass in the `fileID` of the video to be played back, which is required
    appID: '', // Pass in the `appID` of the VOD account, which is required
    plugins: {
      ContextMenu: {
        levelSwitch: {
          open: true, // Enable switch prompt
          // switchingText: 'Switching to', // Text for switch start
          // switchedText: 'Switched successfully', // Text for switch success
          // switchErrorText: 'Switch failed', // Text for switch failure
        }
      }
    }
  });

```


### Key hotlink protection
For detailed directions on how to enable this feature, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986). The following parameters should be added during player initialization:
```
var player = TCPlayer('player-container-id', {
     fileID: '', // Pass in the `fileID` of the video to be played back, which is required
     appID: '', // Pass in the `appID` of the VOD account, which is required
     psign:''
   });
```
The `psign` parameter is the superplayer signature. For its description, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

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
The `psign` parameter is the superplayer signature. For its description, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

>!
>- The duration of video playback in the player is the length specified by the `exper` parameter. Unlike other preview features that control the playback duration on the player side, the player does not get the complete video.
>- Preview works by clipping the video according to the video keyframes, and the actually clipped preview video may be shorter than the pre-configured preview duration.
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
The `psign` parameter is the superplayer signature. For its description, please see [Superplayer Signature](https://intl.cloud.tencent.com/document/product/266/38099).

>!
>- If the URL of the playback page or Flash SWF has a different domain name from the decryption key server, the key server needs to deploy `crossdomain.xml` and cross-origin resource sharing (CORS) to allow Flash and JavaScript to obtain the decryption key across origins.
>- The domain name of the SWF URL is configured in `crossdomain.xml`, which must be placed in the root directory of the key server.
>- The Flash SWF file of the player is stored under the `imgcache.qq.com` domain name by default. If you need to deploy it to your own server, you can download it [here](https://imgcache.qq.com/open/qcloud/video/tcplayer/player.swf) and deploy it by yourself.
>- If your business is in a domain-limited region, the Flash SWF file needs to be stored under the `cloudcache.tencent-cloud.com` domain name by default.
>- Videos can be encrypted only once. Please strictly follow the steps in the video encryption document.
>- A decryption key should contain 16 characters, and cannot start or end with a whitespace character.

### Video statistics
Right-click to open the video statistics panel and view the real-time video information as shown below:
![](https://main.qcloudimg.com/raw/77d6e949cb3a5cfb28bed86a7dea980e.png)
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

#### Samples
Click [Video Statistics](https://imgcache.qq.com/open/qcloud/video/tcplayer/examples/vod/tcplayer-vod-change-file-statistic.html) to enter the sample code page, right-click on the page, and select **View page source** to view the sample source code.

>!
>- This feature is only available for desktop browsers.
>- This feature is unavailable for browser-hijacking playback.

### Prompt text customization
If you want to customize the prompt text, you can set it through the initialization parameter `languages`. Below is the sample code:

```
var player = TCPlayer('player-container-id', {
  fileID: '', // Pass in the `fileID` of the video to be played back, which is required
  appID: '', // Pass in the `appID` of the VOD account, which is required
  languages:{
    'zh-cn':{
      'AppID is not exist, Please check if the AppID is correct.': 'Please check whether the `appID` is entered correctly'
    }
  }
});
```

The corresponding text prompts of error codes are as listed below:

| Name | Description                                           ||
|------|----------------------------------------------|-------------------------|
| -1   | No video has been loaded.                    | The player didn't detect an available video address. |
| -2   | Could not download the video.                | Video data acquisition timed out. |
| 1    | You aborted the media playback.              | Video data loading was aborted. |
| 2    | A network error caused the media download to fail part-way. | Failed to load the video due to network issues. |
| 3    | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | An error occurred while decoding the video. |
| 4    | The media could not be loaded, either because the server or network failed or because the format is not supported. | The video couldn't be loaded due to unsupported format or server/network issues. |
| 5    | The media is encrypted and we do not have the keys to decrypt it.   | An error occurred while decrypting the video. |
| 10   | Request timed out.                          | The VOD media data API request timed out. |
| 11   | Server is not respond.                      | The VOD media data API didn't return any data. |
| 12   | Server respond error data.                  | The VOD media data API returned exceptional data. |
| 13   | No video transcoding information found.     | The player didn't detect any video data that could be played back in the current player. Please transcode the video. |
| 14   | A network error caused the media download to fail part-way.   | Failed to download the video due to network issues. |
| 15   | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | The playback was aborted because the video file was corrupted or the video used features that your browser does not support.  |
| 16   | The media playback was aborted due to a corruption problem or because the media used features your browser did not support. | The playback was aborted because the video file was corrupted or the video used features that your browser does not support.  |
| 17   | Rise an internal exception when playing HLS.| An internal exception occurred while playing back the HLS video. |
| 500  | Server failed.                              | A media server error occurred. |
| 1001 | The media file does not exist. Please check if the fileID is correct. | The media file does not exist. Please check whether the `fileID` is correct. |
| 1002 | The trial duration is illegal. The trial duration must be within the video duration. | Invalid preview duration. The preview duration must be within the video duration. |
| 1003 | Param pcfg is not unique.                   | The `pcfg` is not unique. |
| 1004 | The license has expired. Please check whether the expiration time setting is reasonable. | The license has expired. Please check whether the expiration time setting is reasonable. |
| 1005 | Did not find an adaptive stream that can be played. | An adaptive bitstream that could be played back was not found. |
| 1006 | Invalid request format, please check the request format. | Invalid request format. Please check the request format. |
| 1007 | AppID is not exist, Please check if the AppID is correct. | The `AppID` does not exist. Please check whether the `AppID` is correct. |
| 1008 | Without anti-leech information.             | No hotlink protection detection. |
| 1009 | psign check failed.                         | Failed to verify the playback parameter `psign`. |
| 1010 | Other errors.                               | Other errors occurred. |
| 2001 | Internal error.                             | An internal error occurred. |
| 10008 | The media file does not exist. Please check if the fileID is correct. | The media file does not exist. Please check whether the `fileID` is correct. |

## Changelog
TCPlayer is continuously updated and optimized. The following are the published major versions of TCPlayer:

| Date | Version | Update|
|-----------------|--------- |-------------------------------------------- |
| July 10, 2020 | 4.1 | 1. Changed the default `hls.js` version to 0.13.2. <br> 2. Added the support for key hotlink protection. <br>3. Fixed other known issues. |
| June 17, 2020 | 4.0 |   1. Fixed the problem where the original video duration was displayed as the video preview duration. <br>2. Added the backend definition configuration. <br>3. Fixed other known issues. |