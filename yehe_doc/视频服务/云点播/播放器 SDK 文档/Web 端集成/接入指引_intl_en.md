This document describes the Player SDK for web (TCPlayer) suitable for VOD and live playback, which can be quickly integrated with your own web applications to implement video playback. TCPlayer contains some UIs by default for you to use as needed.
## Overview
TCPlayer implements video playback through the HTML5 `<Video>` tag and Flash. It enables a browser that does not support video playback natively to play back videos, delivering a unified video experience across platforms. In addition, it features hotlink protection and playback of encrypted general HLS videos with the aid of the VOD service.


### Supported protocols

<table>
<tr><th style="text-align:center">Audio/Video Protocol</th><th>Purpose</th><th>URL Format</th><th>PC Browser</th><th>Mobile Browser</th>
</tr>
<tr>
<td style="text-align:center">MP3</td>
<td>Audio</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.mp3</code></td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td style="text-align:center">MP4</td>
<td>VOD playback</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.mp4</code></td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td rowspan=2 style="text-align:center">HLS<br>(M3U8)</td>
<td>Live playback</td>
<td><code>http://xxx.liveplay.myqcloud.com/xxx.m3u8</code></td>
<td>Supported</td>
<td>Supported</td>
</tr><tr>
<td>VOD playback</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.m3u8</code></td>
<td>Supported</td>
<td>Supported</td>
</tr><tr>
<td rowspan=2 style="text-align:center">FLV</td>
<td>Live playback</td>
<td><code>http://xxx.liveplay.myqcloud.com/xxx.flv</code></td>
<td>Supported</td>
<td>Partially supported</td>
</tr><tr>
<td>VOD playback</td>
<td><code>http://xxx.vod.myqcloud.com/xxx.flv</code></td>
<td>Supported</td>
<td>Partially supported</td>
</tr>
<tr>
<td style="text-align:center">WebRTC</td>
<td>Live playback</td>
<td><code>webrtc://xxx.liveplay.myqcloud.com/live/xxx</code></td>
<td>Supported</td>
<td>Supported</td>
</tr>
</table>


<dx-alert infotype="explain" title="">
- Only the H.264 video encoder is supported.
- The player is compatible with common browsers and can automatically identify the platform to use the optimal playback scheme.
- In some browser environments, HLS and FLV video playback depends on [Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions).
- Currently, the WebRTC browser environment is not supported. If a WebRTC URL of the player is passed in, the protocol will be converted automatically to better support the media playback.
</dx-alert>

## Supported Features

<Table>
  <tr>
    <th width="50px" style="text-align:center">Feature/Browser</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQ Browser</th>
      <th width="50px" style="text-align:center">Mac Safari</th>
      <th width="50px" style="text-align:center">iOS Safari</th>
      <th width="50px" style="text-align:center">WeChat</th>
      <th width="50px" style="text-align:center">Chrome on Android</th>
      <th width="50px" style="text-align:center">IE 11</th>
  </tr>
     <tr>
         <td style="text-align:center">Player dimension configuration</td>
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
         <td style="text-align:center">&#10003;</td>
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
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
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
    </tr>
    <tr>
         <td style="text-align:center">General encrypted HLS playback</td>
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
         <td style="text-align:center">Private encrypted HLS playback</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">-</td>
         <td style="text-align:center">
      		<ul>
            <li nowrap="nowrap">Android: &#10003;</li><br>
            <li nowrap="nowrap">iOS: -</li>
           </ul>	
      	</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
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
    </tr>
    <tr>
         <td style="text-align:center">Video data monitoring</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
         <td style="text-align:center">&#10003;</td>
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
    </tr>
    <tr>
         <td style="text-align:center">Custom UI</td>
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
         <td style="text-align:center">On-screen comment</td>
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
         <td style="text-align:center">Watermark</td>
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
         <td style="text-align:center">Video list</td>
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
         <td style="text-align:center">Frame sync under poor network conditions</td>
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
<dx-alert infotype="explain" title="">
- Only the H.264 video encoder is supported.
- Chrome and Firefox on Windows and macOS are supported.
- Chrome, Firefox, Edge, and QQ Browser need to load `hls.js` when playing back HLS files.
- The referer hotlink protection feature is implemented based on the `Referer` field in the HTTP request header. HTTP requests initiated by some Android browsers do not carry the `Referer` field.
</dx-alert>

The player is compatible with common browsers and can automatically identify the platform to use the optimal playback scheme. For example, it will preferably use the HTML5 technology for video playback in modern browsers such as Chrome and directly use the HTML5 technology or the browser kernel capabilities in mobile browsers.


## Integration Guide

You can add a video player to your webpage in the following steps:

### Step 1. Import files into the page

Create the `index.html` file in your project and import the player style file and script file to the HTML page:
```html
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/tcplayer.min.css" rel="stylesheet"/>
 <!--If you want to play back WebRTC videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `TXLivePlayer-x.x.x.min.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <!--Some browser environments don't support WebRTC. In this case, the player will automatically convert the address of the WebRTC stream to an HLS address. Therefore, you also need to import `hls.min.x.xx.xm.js` in WebRTC-based live streaming scenarios.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.1/libs/TXLivePlayer-1.2.0.min.js"></script>
 <!--If you want to play back HLS videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `hls.min.x.xx.xm.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/libs/hls.min.0.13.2m.js"></script>
 <!--If you want to play back FLV videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `flv.min.x.x.x.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/libs/flv.min.1.6.2.js"></script>
 <!--Player script file-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/tcplayer.v4.5.2.min.js"></script>
```
We recommend you deploy the resources on your own when using the Player SDK. [Click here to download the player resources](https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.2/release.zip).
Deploy the folder generated after decompression. Do not adjust the directories in the folder; otherwise, resource import exceptions may occur.
If the address of your deployment is `aaa.xxx.ccc`, then import the player style and script files into the correct places:
```html
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet"/>
 <!--If you want to play back HLS videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `hls.min.x.xx.m.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="aaa.xxx.ccc/libs/hls.min.0.13.2m.js"></script>
 <!--Player script file-->
 <script src="aaa.xxx.ccc/tcplayer.vx.x.x.min.js"></script>
```

### Step 2. Place the player container

Place the player container in the desired place on the page. For example, add the following code to `index.html` (the container ID, width, and height can be customized).
```html
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

>?
>
>- The player container must be a `<video>` tag.
>- The `player-container-id` in the sample is the ID of the player container, which can be customized.
>- It is more flexible to set the size of the player container zone through CSS  than through the attribute to have better display effects such as full-screen mode and container adaption.
>- The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include `meta` (only loads the metadata after the page is loaded) and `none` (does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
>- The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback when the standard mobile browser does not hijack the video playback. They are just for reference here and can be used as needed.
>- If  `x5-playsinline`  is set, the X5 UI player will be used in the TBS kernel.

### Step 3. Initialize the player
After page initialization, the video resources can be played back. The player supports both VOD playback and live playback as detailed below:
- VOD playback: The player can play back a VOD media resource through `FileID`. For the specific process, see [Stage 1. Play back a video with Player](https://intl.cloud.tencent.com/document/product/266/38098).
- Live playback: The player can pull a live audio/video stream for playback through the URL passed in. For more information on how to generate a Tencent Cloud live streaming URL, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

<dx-tabs>
::: Through the URL (VOD and live playback)
After page initialization, call the method in the player instance to pass in the URL to the method.
<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', {}); // `player-container-id` is the player container ID, which must be the same as that in HTML.
player.src(url); // Playback URL
:::
</dx-codeblock>

:::
::: Through `FileID` (VOD playback)
Add the following initialization script to the `index.html` page initialization code to pass in the `fileID` (video ID in [**Video/Audio Management**](https://console.cloud.tencent.com/vod/media)) and `appID` (which can be viewed in **Account Info** > [**Basic Info**](https://console.cloud.tencent.com/developer)) obtained in the preparations.

<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', { // `player-container-id` is the player container ID, which must be the same as that in HTML.
    fileID: '3701925921299637010', // Pass in the `fileID` of the video to be played back, which is required.
    appID: '1500005696' // Pass in the `appID` of the VOD account, which is required.
  // If you enable hotlink protection, you need to enter a `psign` (player signature) for playback. For more information on the signature and how to generate it, visit https://www.tencentcloud.com/document/product/266/38099.
  //psign:'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAwNTY5NiwiZmlsZUlkIjoiMzcwMTkyNTkyMTI5OTYzNzAxMCIsImN1cnJlbnRUaW1lU3RhbXAiOjE2MjY4NjAxNzYsImV4cGlyZVRpbWVTdGFtcCI6MjYyNjg1OTE3OSwicGNmZyI6InByaXZhdGUiLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI5YzkyYjBhYiJ9LCJkcm1MaWNlbnNlSW5mbyI6eyJleHBpcmVUaW1lU3RhbXAiOjI2MjY4NTkxNzksInN0cmljdE1vZGUiOjJ9fQ.Bo5K5ThInc4n8AlzIZQ-CP9a49M2mEr9-zQLH9ocQgI',
});
:::
</dx-codeblock>

>!We recommend you transcode the video to be played back in Tencent Cloud as it cannot be guaranteed that the source video can be played back normally in the browser.
:::
</dx-tabs>

### Step 4. Implement more features
The player can use the VOD server capabilities to implement advanced features, such as adaptive bitstream streaming, video preview thumbnail, and video timestamping. For more information on the features and how to implement them, see [Stage 5. Play back a long video](https://intl.cloud.tencent.com/document/product/266/44191).

For a full list of all the features of the player, see [Player for Web Demo](https://tcplayer.vcube.tencent.com/).
