As a lower-latency version of CSS, LEB provides superb **live streaming** experience with millisecond playback latency, far lower than that of live stream playback using traditional protocols.

> ! LEB uses the WebRTC protocol to ensure low latency. It adopts the Opus codec and does not support B-frames. If the original stream contains B-frames or the codec is not Opus, the CSS backend will remove the B-frames and transcode the stream to Opus format, which will incur [standard transcoding fees](https://intl.cloud.tencent.com/document/product/267/39604).

[](id:app)
## App Access
### Access instructions
You can integrate the MLVB SDK with apps on iOS and Android clients for live push and playback.

- **Live push on apps**: supports capturing camera or mobile phone screens and then pushing the content to the CSS platform using the RTMP protocol. For details, see [Publishing (Camera)](https://intl.cloud.tencent.com/document/product/1071/38157) and [Publishing (Screen Recording)](https://intl.cloud.tencent.com/document/product/1071/41878).
- **Live playback on apps**: supports WebRTC playback protocol. You can integrate the MLVB SDK with LEB to quickly achieve live streaming with low latency. For details, see [Playback](https://intl.cloud.tencent.com/document/product/1071/41875).

>? The MLVB SDK uses CSS, IM, TRTC and other services for low-latency audiovisual communication for multiple parties. It offers co-anchoring for interaction between viewers, and other viewers who don’t join co-anchoring can also watch the live streaming. For details, see [Co-anchoring](https://intl.cloud.tencent.com/document/product/1071/42210).

### Free Demos
Video Cloud Toolkit is an open-source and comprehensive audio/video solution developed by Tencent Cloud. You can use it to try out LEB’s capability to play live streams with millisecond latency.
<table>
  <tr>
    <th><div align="center">Platform</div></th>
    <th><div align="center">Demo</div></th>
    <th><div align="center">Publishing Demonstration (Android)</div></th>
    <th><div align="center">Playback Demonstration (Android)</div></th>
  </tr>
  <tr>
    <td >Android</td>
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
      <td >iOS</td>
    <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150"></td>
  </tr>
</table>




[](id:web)
## Web Access
### Access instructions
You can use the following ways to achieve live push and playback on your websites:

- **Live push on web**: you can use the standard WebRTC protocol to design and mux streams, and insert code snippets to websites to enable live push. For details, see [WebRTC Push](https://intl.cloud.tencent.com/document/product/267/41620).
> ! WebRTC push uses the Opus audio codec. If you use a standard live streaming protocol (RTMP, HTTP-FLV, or HLS) for playback, the CSS backend will automatically convert the audio streams to AAC format to ensure normal playback, which will incur audio transcoding fees. For details, see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604#a_trans). Audio transcoding will not be initiated when only the LEB service is used.
- **Live playback on web**: we recommend you use the player SDK "TCPlayerLite" which supports playing back **LEB streams using the WebRTC protocol** on mobile and desktop browsers. Such playback delivers a superb streaming experience with millisecond latency, far lower than that of playback using traditional live streaming protocols.
> ! On a browser which does not support WebRTC, a WebRTC URL passed into the player will be converted to ensure normal playback. By default, WebRTC URLs are converted to HLS URLs on mobile browsers and HTTP-FLV URLs on desktop browsers.

### Free Demos

- **Live push on web**: you can test the web push feature in **CSS console** > [Web Push Tool](https://console.cloud.tencent.com/live/tools/webpush).
- **Live playback on web**: you can use [WebRTC Live Demo](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) to test playback.
>?
>- Both live push and live playback on web use the standard WebRTC protocol. Push on web does not include B-frames, and the audio is encoded in Opus format, so there will be no costs of audio transcoding and B-frame removal transcoding.
>- WebRTC Live Demo supports the multi-definition feature. You can configure transcoding templates for HD and SD in **Feature Configuration** > [**Live Transcoding**](https://console.cloud.tencent.com/live/config/transcode) in the CSS console, enter a WebRTC stream address containing a transcoding template, test it, and the play it back. (If you don't need to test this feature, simply enter a WebRTC original stream in the demo.)
>- For more information on live transcoding operations and billing, see [CSS Transcoding](https://intl.cloud.tencent.com/document/product/267/31071).

[](id:obs)
## OBS WebRTC Push Access
Push over the WebRTC protocol is mainly used for LEB (ultra low-latency live streaming). It is responsible for pushing the collected audio/video or video file to the CSS server through the WebRTC protocol. The following describes how to use the OBS tool to implement push over WebRTC.

### Notes
Currently, OBS must be on v26 or above.

[](id:set)
### Configuring OBS plugin
1. **Configure the plugin data**.
Download the [OBS plugin](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20210628.zip), copy the `services.json` and `package.json` files in the `data` directory to the corresponding **obs-studio** > **rtmp-service** > **data** folder in an overwriting manner. (`obs-studio` is installed on the C drive by default, and the directory is `C:\Program Files\obs-studio\data\obs-plugins\rtmp-services`, subject to the actual situation.)
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
2. **Configure the plugin's dynamic library**.
Move the dll and pdb files in `obs-plugins\64bit` to the corresponding **obs-studio** > **obs-plugins** > **64bit** directory. (`obs-studio` is installed on the C drive by default, and the corresponding directory is `C:\Program Files\obs-studio\obs-plugins\64bit`, subject to the actual situation.)
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
### Configuring push URL
[](id:push)
1. **Generate a WebRTC push URL**.
	1. Log in to the CSS console and generate a push URL in **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) as instructed in [Live Remuxing and Transcoding](https://intl.cloud.tencent.com/document/product/267/31084).
	2. Change the generated `rtmp` prefix to `webrtc` as instructed in [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).    
2. **Configure the OBS push service**.[](id:set_obs)
	1. Open OBS and click **Controls** > **Settings** at the bottom to enter the settings page.
	2. Click **Push** to enter the stream settings tab, select the service type as `Tencent webrtc` and the server as `Default`, enter the previously generated [WebRTC push URL](#push) as the stream key, and add `&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream` at the end.
	**Sample stream key:**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx &stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```

[](id:play)
### LEB pull and playback
For how to integrate the LEB SDK for pull and playback, see [iOS & Android](https://intl.cloud.tencent.com/document/product/1071/41875).
