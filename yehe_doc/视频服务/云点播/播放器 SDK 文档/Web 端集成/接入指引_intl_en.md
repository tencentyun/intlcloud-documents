This document introduces you to the Player SDK for web (TCPlayer), which you can quickly integrate into your web application to enable VOD and live playback. TCPlayer comes with UI elements.
## Overview
TCPlayer implements playback using the `<video>` element of HTML5 and Flash Player. It delivers a unified video playback experience across platforms. You can also use it together with Tencent Cloud VOD to enable hotlink protection and playback of encrypted HLS videos.


### Supported protocols

<table>
<tr><th style="text-align:center">Audio/Video Protocol</th><th>Scenario</th><th>URL Format</th><th>PC Browser</th><th>Mobile Browser</th>
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
<td rowspan=2 style="text-align:center">HLS<br> (M3U8)</td>
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
- Only H.264 encoding is supported.
- The player is compatible with mainstream browsers and can automatically select the optimal playback scheme depending on the browser.
- In some browser environments, HLS and FLV video playback depends on [Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions).
- If a browser does not support WebRTC, a WebRTC URL passed in will be converted automatically to better support playback.
</dx-alert>

## Supported Features

<Table>
  <tr>
    <th width="50px" style="text-align:center">Feature\Browser</th>
      <th width="50px" style="text-align:center">Chrome</th>
      <th width="50px" style="text-align:center">Firefox</th>
      <th width="50px" style="text-align:center">Edge</th>
      <th width="50px" style="text-align:center">QQ Browser</th>
      <th width="50px" style="text-align:center">Safari for macOS</th>
      <th width="50px" style="text-align:center">Safari for iOS</th>
      <th width="50px" style="text-align:center">WeChat</th>
      <th width="50px" style="text-align:center">Chrome for Android</th>
      <th width="50px" style="text-align:center">Internet Explorer 11</th>
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
         <td style="text-align:center">Resuming playback</td>
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
         <td style="text-align:center">Playback speed change</td>
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
         <td style="text-align:center">Preview thumbnails</td>
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
         <td style="text-align:center">Flipping videos</td>
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
         <td style="text-align:center">Definition change notifications</td>
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
         <td style="text-align:center">Playing HLS videos encrypted using standard schemes</td>
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
         <td style="text-align:center">Playing HLS videos encrypted using private protocols</td>
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
         <td style="text-align:center">Custom UI messages</td>
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
         <td style="text-align:center">On-screen comments</td>
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
         <td style="text-align:center">Playlist</td>
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
- Only H.264 encoding is supported.
- Chrome and Firefox for Windows and macOS are supported.
- Chrome, Firefox, Edge, and QQ Browser need to load `hls.js` in order to play HLS files.
- The referer hotlink protection feature is implemented based on the `Referer` field in the HTTP request header. HTTP requests initiated by some Android browsers do not carry the `Referer` field.
</dx-alert>

The player is compatible with mainstream browsers and can automatically select the optimal playback scheme depending on the browser used. For example, for modern browsers such as Chrome, the player uses the HTML5 technology for playback, and for mobile browsers, it uses the HTML5 technology or the browser’s built-in capabilities.


## Integration Guide

You can add a video player to your webpage in the following steps:

### Step 1. Import files into the page

Create the `index.html` file in your project and import the player style file and script file to the HTML page:
```html
 <link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.min.css" rel="stylesheet"/>
 <!--If you want to play back WebRTC videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `TXLivePlayer-x.x.x.min.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <!--Some browser environments don't support WebRTC. In such cases, the player will automatically convert a WebRTC URL to an HLS URL. Therefore, you also need to import `hls.min.x.xx.xm.js` in WebRTC live streaming scenarios.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/TXLivePlayer-1.2.3.min.js"></script>
 <!--If you want to play back HLS videos through HTML5 in a browser such as Chrome and Firefox, you need to import `hls.min.x.xx.xm.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/hls.min.1.1.5.js"></script>
 <!--If you want to play back FLV videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `flv.min.x.x.x.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/flv.min.1.6.3.js"></script>
  <!--If you want to play back DASH videos through HTML5 in a modern browser such as Chrome and Firefox, you need to import `dash.min.x.x.x.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/libs/dash.all.min.4.4.1.js"></script>
 <!--Player script file-->
 <script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/tcplayer.v4.5.4.min.js"></script>
```
We recommend you deploy the resources on your own when using the Player SDK. You can download the player resources [here](https://web.sdk.qcloud.com/player/tcplayer/release/v4.5.4/release.zip).
To avoid reference errors, do not rearrange the directories in the folder after decompression.
Suppose the address of your deployment is `aaa.xxx.ccc`. Follow the steps below to import the style and script files:
```html
 <link href="aaa.xxx.ccc/tcplayer.min.css" rel="stylesheet"/>
 <!--If you want to play back HLS videos through HTML5 in a browser such as Chrome and Firefox, you need to import `hls.min.x.xx.m.js` before importing `tcplayer.vx.x.x.min.js`.-->
 <script src="aaa.xxx.ccc/libs/hls.min.x.xx.m.js"></script>
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
>- The player container must be a `<video>` element.
>- In the example, `player-container-id` is the ID of the player container. You can set your own container ID.
>- We recommend you use CSS to size the player, which allows greater flexibility than attribute settings and can achieve effects such as full screen and container adaption.
>- The `preload` attribute in the sample specifies whether to load the video after the page is loaded, which is usually set to `auto` for faster start of the playback. Other options include `meta` (only loads the metadata after the page is loaded) and `none` (does not load the video after the page is loaded). Due to system restrictions, videos will not be automatically loaded on mobile devices.
>- The `playsinline` and `webkit-playsinline` attributes are used to implement inline playback in a standard mobile browser without the browser hijacking the playback. You can use these two attributes based on your actual conditions.
>- If  `x5-playsinline`  is set, the X5 UI player will be used in the TBS kernel.

### Step 3. Initialize the player
After page initialization, the video resources can be played back. The player supports both VOD playback and live playback.
- VOD playback: The player can play back a VOD media resource through `FileID`. For the specific process, see [Stage 1. Play back a video with Player](https://intl.cloud.tencent.com/document/product/266/38098).
- Live playback: The player can pull a live audio/video stream for playback through the URL passed in. For more information on how to generate a Tencent Cloud live streaming URL, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

<dx-tabs>
::: URL playback (VOD and live)
After page initialization, call the method in the player instance to pass in the URL to the method.
<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', {}); // player-container-id is the player container ID, which must be the same as that in HTML
player.src(url); // Playback URL
:::
</dx-codeblock>

:::
::: File ID playback (VOD)
Add the following initialization script to the `index.html` page initialization code and pass in the `fileID` (which can be viewed in [Media Assets](https://console.cloud.tencent.com/vod/media)) and `appID` (which can be viewed in **Account Information** > [Basic Information](https://console.cloud.tencent.com/developer)).

<dx-codeblock>
:::  javascript
var player = TCPlayer('player-container-id', { // player-container-id is the player container ID, which must be the same as that in HTML
    fileID: '3701925921299637010', // Pass in the file ID of the video to be played, which is required
    appID: '1500005696' // Pass in the appID of your VOD account, which is required
  // If you enable hotlink protection, you need to enter a `psign` (player signature) for playback. For more information on the signature and how to generate it, see https://www.tencentcloud.com/document/product/266/38099
  //psign:'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAwNTY5NiwiZmlsZUlkIjoiMzcwMTkyNTkyMTI5OTYzNzAxMCIsImN1cnJlbnRUaW1lU3RhbXAiOjE2MjY4NjAxNzYsImV4cGlyZVRpbWVTdGFtcCI6MjYyNjg1OTE3OSwicGNmZyI6InByaXZhdGUiLCJ1cmxBY2Nlc3NJbmZvIjp7InQiOiI5YzkyYjBhYiJ9LCJkcm1MaWNlbnNlSW5mbyI6eyJleHBpcmVUaW1lU3RhbXAiOjI2MjY4NTkxNzksInN0cmljdE1vZGUiOjJ9fQ.Bo5K5ThInc4n8AlzIZQ-CP9a49M2mEr9-zQLH9ocQgI',
});
:::
</dx-codeblock>

>! Not all videos can be played successfully in a browser. We recommend you use Tencent Cloud’s services to transcode a video before playing it.
:::
</dx-tabs>

### Step 4. Implement more features
You can use VOD’s capabilities to implement more features in the player, such as adaptive bitrate, preview thumbnails, and timestamping. For detailed directions, see [Stage 5. Play back a long video](https://intl.cloud.tencent.com/document/product/266/44191).

For a full list of the player’s features, see [TCPlayer Demo](https://tcplayer.vcube.tencent.com/).
