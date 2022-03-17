As a lower-latency version of LVB, LEB provides superb **live streaming** experience with millisecond playback latency, far lower than that of live stream playback using traditional protocols.
Before you use LEB, please read [LEB Billing Overview](https://intl.cloud.tencent.com/document/product/267/39969) to learn about its billable items and pricing.

> ! LEB uses the WebRTC protocol to ensure low latency. It adopts the Opus codec and does not support B-frames. If the original stream contains B-frames or the codec is not Opus, the CSS backend will remove the B-frames and transcode the stream to Opus format, which will incur [standard transcoding fees](https://intl.cloud.tencent.com/document/product/267/39604).

[](id:app)
## Integration into App
### Directions
You can integrate the MLVB SDK into your iOS or Android app to implement the live push and playback features.

- **Live push on apps**: Supports capturing camera video or mobile phone screens and then pushing the content to the CSS platform using the RTMP protocol. For details, see [Publishing from Camera](https://intl.cloud.tencent.com/document/product/1071/38157) and [Publishing from Screen](https://intl.cloud.tencent.com/document/product/1071/41878).
- **Live playback on apps**: Supports the WebRTC playback protocol. You can use the MLVB SDK, which integrates LEB, to quickly enable playback with ultra-low latency on mobile apps. For details, see [Playback > LEB](https://intl.cloud.tencent.com/document/product/1071/41875).

>? The MLVB SDK uses CSS, IM, TRTC, and other services for low-latency audiovisual communication for multiple parties. Participants can interact with each other through mic connect while others watch. For details, see [Mic Connect](https://intl.cloud.tencent.com/document/product/1071/42210).

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
    <td style="text-align:center"><img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150"></td>
  </tr>
</table>




[](id:web)
## Integration into Webpage
### Directions
You can use the following ways to achieve live push and playback on your websites:

- **Live push on web**: The push component is designed and packaged according to the WebRTC standard, which is supported by most browsers. You can enable the live push feature simply by importing the code we provide. For details, see [WebRTC Push](https://intl.cloud.tencent.com/document/product/267/41620).
> ! 
> - WebRTC push uses the Opus audio codec. If you use an LVB protocol (RTMP, HTTP-FLV, or HLS) for playback, the CSS backend will automatically convert audio to AAC format to ensure normal playback, which will incur audio transcoding fees. For details, see [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604). If only LEB is used, the CSS backend will not transcode the audio.
> - With WebRTC, each push domain name can be used for up to **100 concurrent streams** by default. If you want to push more streams, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


### Free demo

- **Live push on web**: You can test the web push feature in **CSS console** > **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)**.

- **Live playback on web**: You can use [WebRTC Live Demo](https://tcplayer.vcube.tencent.com/webrtc-demo/index.html) to test playback.
>?
>- Both live push and playback on web use the standard WebRTC protocol. Web push does not generate B-frames, and audio is encoded in Opus format, so there will be no costs of audio transcoding or B-frame removal.
>- WebRTC Live Demo supports multi-definition playback. You can create a transcoding template for HD and SD output in **Feature Configuration** > [**Live Transcoding**](https://console.cloud.tencent.com/live/config/transcode) in the CSS console, enter in the demo a WebRTC stream URL containing the transcoding template, and test its playback. If you don't need to test transcoding, enter the original URL of the WebRTC stream.
>- For more information on live transcoding and its billing, see [Live Transcoding](https://intl.cloud.tencent.com/document/product/267/31071).

[](id:obs)
## WebRTC Push Integration via OBS
Push over the WebRTC protocol is mainly used for LEB (ultra-low-latency live streaming). It pushes live audio/video or video files to the CSS server through the WebRTC protocol. The following describes how to use OBS to implement WebRTC push.

### Notes
- Your OBS version must be v26 or above.
- We only offer an OBS plugin for Windows currently. If you want to use OBS to implement the WebRTC push feature on macOS, see [Integration into Webpage](https://intl.cloud.tencent.com/document/product/267/42131).

[](id:set)
### Configuring OBS plugin
1. **Configure the plugin data**
Download the [OBS plugin](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TOBSWebRTC/Release/tencent_webrtc_plugin_20210628.zip), copy the `services.json` and `package.json` files in the `data` directory and use them to replace the corresponding files in **obs-studio** > **rtmp-service** > **data**. (`obs-studio` is installed in `C:\Program Files\` by default.)
![](https://main.qcloudimg.com/raw/967335d17284d931e3a01505d45b884a.png)  
2. **Configure the plugin's dynamic library**
Move the DLL and PDB files in `obs-plugins\64bit` to **obs-studio** > **obs-plugins** > **64bit**. (`obs-studio` is installed in `C:\Program Files\` by default.)
![](https://main.qcloudimg.com/raw/ca9cc7d84071526009624978dc38e2c8.png)   

[](id:push)
### Configuring push URL
[](id:push)
1. **Generate a WebRTC push address**.
  1. Log in to the CSS console and go to **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to generate a push URL. For detailed directions, see [Address Generator](https://intl.cloud.tencent.com/document/product/267/31084).
  2. Change the `rtmp` prefix in the URL generated to `webrtc`. For details, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

    ![](https://qcloudimg.tencent-cloud.cn/raw/e4e8118922b8f4be309e33f740152006.png)    
2. **Configure push in OBS**[](id:set_obs)
  1. Open OBS and click **Controls** > **Settings** at the bottom to enter the settings page.
  2. Click **Stream**, select `Tencent webrtc` for **Service** and `Default` for **Server**, enter the generated [WebRTC push URL](#push) in **Stream Key**, and append to it `&stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream`.

    **Sample stream key:**
```
webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx &stopstream_api=https://webrtcpush.myqcloud.com/webrtc/v1/stopstream 
```
As shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8035e95d3f62e62dcb3c33db2e5560d6.png)     

[](id:play)
### LEB playback
For how to use the MLVB SDK for LEB playback, see [Playback > LEB](https://intl.cloud.tencent.com/document/product/1071/41875).
