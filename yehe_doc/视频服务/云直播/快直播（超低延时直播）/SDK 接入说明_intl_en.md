As a lower-latency version of LVB, LEB provides superb **live streaming** experience with millisecond playback latency, far lower than that of live stream playback using traditional protocols.
Before you use LEB, please read [LEB Billing Overview](https://intl.cloud.tencent.com/document/product/267/39969) to learn about its billable items and pricing.

>! LEB uses the WebRTC protocol to ensure low latency. It adopts the Opus codec and does not support B-frames. If the original stream contains B-frames or the codec is not Opus, the CSS backend will remove the B-frames and transcode the stream to Opus format, which will incur [standard transcoding fees](https://intl.cloud.tencent.com/document/product/267/39604).

[](id:app)
## Integration into Application
### Directions
You can integrate the MLVB SDK into your iOS or Android application to implement the live push and playback features.

- **Live push**: Capture from the camera or phone screen and push the stream to CSS using the RTMP protocol. For details, see [Publishing (Camera)](https://www.tencentcloud.com/document/product/1071/38157) and [Publishing (Screen Recording)](https://www.tencentcloud.com/document/product/1071/41878).
- **Live playback**: Play streams using WebRTC with ultra-low latency. For details, see [Playback > LEB](https://www.tencentcloud.com/document/product/1071/41875).

>? The MLVB SDK leverages the capabilities of CSS, IM, TRTC, and other services to implement low-latency audio/video communication for multiple parties, allowing participants to interact with each other while others watch. For details, see [Mic Connect](https://www.tencentcloud.com/document/product/1071/42210).

### Free demo
TCToolkit is an open-source and comprehensive audio/video solution developed by Tencent Cloud. You can use it to try out LEB’s capability to play live streams with millisecond latency.
<table>
  <tr>
    <th><div align="center">Platform</div></th>
    <th><div align="center">Demo</div></th>
    <th><div align="center">Push Demonstration (Android)</div></th>
    <th><div align="center">Playback Demonstration (Android)</div></th>
  </tr>
  <tr>
    <td>Android</td>
    <td style="text-align:center"><img width="150" src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png"> </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200" src="https://main.qcloudimg.com/raw/dca4b24bc363d25c9ea45e60859a2f6d.png"/>
      </div>
    </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200"  src="https://main.qcloudimg.com/raw/6dd7c02dc2381d84225c2f2f286e7358.png"/>
      </div>
    </td>
  </tr>
  <tr>
      <td>iOS</td>
    <td style="text-align:center">Under maintenance</td>
  </tr>
</table>



[](id:web)
## Integration into Webpage
### Directions
You can use the following ways to achieve live push and playback on your websites:

- **Live push on web**: The push component is designed and packaged according to the WebRTC standard, which is supported by most browsers. You can enable the live push feature simply by importing the code we provide. For details, see [WebRTC Push](https://intl.cloud.tencent.com/document/product/267/41620).
>! 
>- The Opus audio codec is used for the push of WebRTC streams. Therefore, if you use an LVB protocol (RTMP, HTTP-FLV, or HLS) for playback, the CSS backend will automatically convert the audio to AAC format to ensure successful playback, which will incur audio transcoding fees. For details, see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604). If you publish and play streams using the LEB protocol, CSS will not transcode the audio.
>- With WebRTC, each push domain can be used for up to **1,000 concurrent streams** by default. If you want to push more streams, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

- **Live playback on web**: We recommend you use our web player SDK [TCPlayerLite](https://www.tencentcloud.com/document/product/266/33977), which supports playing **WebRTC streams** on mobile and desktop browsers and delivers a superb streaming experience with millisecond latency, far lower than that of playback using traditional live streaming protocols.
>! If a browser does not support WebRTC, a WebRTC URL passed into the player will be converted to better support playback. By default, WebRTC is converted to HLS on mobile browsers and HTTP-FLV on desktop browsers.

### Free demo

- **Live push on web**: You can test the web push feature in [Web Push](https://console.cloud.tencent.com/live/tools/webpush) of the CSS console.
- **Live playback on web**: You can use the [TCPlayer demo](https://tcplayer.vcube.tencent.com/) to test playback on web.
>?
>- Both live push and playback on web use the standard WebRTC protocol. Web push does not generate B-frames, and audio is encoded in Opus format, so there will be no costs of audio transcoding or B-frame removal.
>- The demo supports changing video quality during playback. To test it, create a transcoding template to output HD and SD videos in **Feature Configuration** > [Live Transcoding](https://console.cloud.tencent.com/live/config/transcode), enter in the demo a WebRTC URL containing the transcoding template, and play it. If you don't need to test this feature, enter the original WebRTC URL.
>- For more information on live transcoding and its billing, see [Live Transcoding](https://intl.cloud.tencent.com/document/product/267/31071).


[](id:obs)
## Implementing WebRTC Push Using OBS
LEB (ultra-low-latency live streaming) uses WebRTC to push live audio/video or video files to the CSS server. The following describes how to use OBS to push WebRTC streams.

### Notes
- Your OBS version must be v26 or later.
- We only offer an OBS plugin for Windows currently. If you want to use OBS to implement the WebRTC push feature on macOS, see [Integration into Webpage](https://intl.cloud.tencent.com/document/product/267/42131).

[](id:set)
### Configuring the OBS plugin
1. **Configure the plugin**
	1. Download the [OBS plugin](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20220509.zip), replace the `services.json` and `package.json` files in the **data > obs-plugins > rtmp-services** directory (`obs-studio` is installed in `C:\Program Files\` by default and the path is `C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`) with the same files in the `data` directory of the downloaded package.
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
	2. Use the above two JSON files to replace the same files in `C:\Users\<Your computer name>\AppData\Roaming\obs-studio\plugin_config\rtmp-services`.
2. **Configure the plugin's dynamic library**
Move the DLL files in `obs-plugins\64bit` to **obs-studio** > **obs-plugins** > **64bit**. (`obs-studio` is installed in `C:\Program Files\` by default and the path is `C:\Program Files\obs-studio\obs-plugins\64bit`).<br>
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
### Configuring the push URL
[](id:push)
1. **Generate a WebRTC push address**.
  1. Log in to the CSS console and go to **CSS Toolkit** > [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to generate a push URL. For detailed directions, see [Address Generator](https://intl.cloud.tencent.com/document/product/267/31084).
  2. Change the `rtmp` prefix in the URL generated to `webrtc`. For details, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

  ![](https://qcloudimg.tencent-cloud.cn/raw/e4e8118922b8f4be309e33f740152006.png)    
2. **Configure push in OBS**[](id:set_obs)
  1. Open OBS and click **Controls** > **Settings** at the bottom to enter the settings page.
  2. Click **Stream**, select `Tencent webrtc` for **Service** and `Default` for **Server**, enter the generated [WebRTC push URL](#push) in **Stream Key**, and append to it `&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`.
**Sample stream key:**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
As shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8035e95d3f62e62dcb3c33db2e5560d6.png)     

[](id:play)
### LEB playback
For how to use the MLVB SDK for LEB playback, see [Playback > (LEB)](www.tencentcloud.com/document/product/1071/41875).
