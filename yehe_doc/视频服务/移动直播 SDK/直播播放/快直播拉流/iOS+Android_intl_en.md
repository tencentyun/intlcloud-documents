## LEB Overview
Live Event Broadcasting (LEB) is the ultra-low-latency version of LVB. It features lower latency than traditional streaming protocols and delivers superior playback experience with millisecond latency. It is suitable for scenarios with high requirements on latency, such as online education, sports streaming, and online quizzes. 

>?
> - The figure above (made using [scrcpy](https://github.com/Genymobile/scrcpy)) is a comparison of LEB and standard CDN live streaming. The images on the left and in the middle show the playback end of standard CDN live streaming and **LEB**, and the image on the right shows the publishing end.
> - LVB and LEB are priced differently. For details, please see [LVB Billing Overview](https://intl.cloud.tencent.com/document/product/267/2818) and [LEB Billing Overview](https://intl.cloud.tencent.com/document/product/267/39969).


### Strengths
<table>
<thead><tr><th width="20%">Strength</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Playback with millisecond latency</td>
<td>The latency is kept within 1s thanks to the use of UDP, as opposed to 3-5s in traditional live streaming. This, along with excellent instant streaming performance and low stuttering rate, guarantees a superior streaming experience.</td>
</tr><tr>
<td>Diverse features and smooth migration</td>
<td>LEB integrates a wide range of features including stream publishing, transcoding, recording, screenshot, porn detection, and playback. It allows smooth migration from standard live streaming.</td>
</tr><tr>
<td>Easy-to-use, secure, and reliable</td>
<td>The use of a standard protocol makes integration easy. You can play live video on Chrome and Safari without installing any plugins. In addition, the playback protocol encrypts video by default for improved security and reliability.</td>
</tr>
</tbody></table>


### Use cases

<table>
<thead><tr><th width="15%">Scenario</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Sports event</td>
<td>LEB offers ultra-low-latency streaming for sports events. It brings sports content to audience at low latency, allowing audience to learn what’s happening in real time.</td>
</tr><tr>
<td>E-commerce streaming</td>
<td>Some e-commerce streaming scenarios, for example, online auctions and sales promotion, require extremely low latency. LEB’s ability to stream at ultra-low latency ensures that hosts and audience get real-time feedback from each other, improving online shopping experience.</td>
</tr><tr>
<td>Online classes</td>
<td>LEB can be used for online classes. Its ability to stream at ultra-low latency allows teachers and students to interact with each other as they do in offline classes.</td>
</tr><tr>
<td>Online quizzes</td>
<td>Due to latency, some online quizzes have to insert extra frames at the audience end to ensure that the host and audience are in sync with each other. This is not necessary if you use LEB, whose ultra-low-latency streaming capability makes sure that the two sides are in sync. It helps you implement online quizzes more easily and deliver smoother experience.</td>
</tr>
<tr>
<td>Showrooms</td>
<td>LEB can significantly improve the experience of latency-sensitive interactions such as gift giving in live showrooms.</td>
</tr>
</tbody></table>

## Tryout
Video Cloud Toolkit is a comprehensive audio-video solution developed by Tencent Cloud that allows you to try out the features of the TRTC, MLVB and UGC SDKs, including the **LEB Player**.

>? The demonstration and directions in this document use the demo app for Android as an example. The UI of the app for iOS is slightly different.

[](id:code)
### Source code and demonstration
<table>
  <tr>
    <th><div align="center">Source Code</div></th>
    <th><div align="center">Demo</div></th>
    <th><div align="center">Publishing Demonstration (Android)</div></th>
    <th><div align="center">Playback Demonstration (Android)</div></th>
  </tr>
  <tr>
    <td ><a href='https://github.com/tencentyun/LiteAVProfessional_Android' > Android </a></td>
    <td><img width="150" src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png"> </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200" src="https://main.qcloudimg.com/raw/75573ec26ca0b75279cdff60daadfcf9.png"/>
      </div>
    </td>
    <td rowspan="2">
      <div align="center">
        <img  width="200"  src="https://main.qcloudimg.com/raw/a32537c628d4d40e918e0cc20e929357.png"/>
      </div>
    </td>
  </tr>
  <tr>
      <td ><a href='https://github.com/tencentyun/LiteAVProfessional_iOS'> iOS </a></td>
    <td style="text-align:center;"><img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150"></td>
  </tr>
</table>


>?In addition to the above sample code, regarding frequently asked questions among developers, Tencent Cloud offers a straightforward API example project, which you can use to quickly learn how to use different APIs.
>- iOS: [MLVB-API-Example](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) 
>- Android: [MLVB-API-Example](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example)


### Publishing
LEB is compatible with LVB, which means you can publish streams using an ordinary publisher and play the streams using LEB.
1. Download and install [Video Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1071/38147), log in, and go to **MLVB > Push (Camera)**.
2. Allow the permissions asked, and tap **Auto-generate** to start publishing streams.
3. If publishing is successful, tap the QR code icon in the top right and select **LEB** to get the playback URL for LEB.
4. During publishing, you can tap the menu icon in the bottom right to apply filters, add background music, switch cameras, etc. 



### Playback
1. Download and install [Video Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1071/38147), log in, and go to **Live Broadcast > LEB Player**.
2. Allow the permissions asked, tap the scan button, and scan the LEB playback URL obtained earlier.
3. Playback starts automatically once the QR code is read. During playback, you can tap the menu icon in the bottom right to mute playback or change other settings.


## Integration
In the new version of the MLVB SDK, you can use [V2TXLivePlayer](https://intl.cloud.tencent.com/document/product/1071/41273) for LEB and `V2TXLivePusher` for publishing. LEB supports WebRTC protocols and uses the standard extension method. All URLs in LEB start with `webrtc://`.

[](id:RegistrationService)[](id:step1)
### Step 1. Download the SDK

Download LiteAV_All or Professional at [SDK Download](https://intl.cloud.tencent.com/document/product/1071/38150).

[](id:step2)
### Step 2. Get a playback URL
In live streaming, URLs are needed for both publishing and playback. For instructions on how to get URLs for LEB, please see [Live Event Broadcasting (LEB) > Get Playback URL](https://intl.cloud.tencent.com/document/product/267/41030#step4).
All LEB URLs start with `webrtc://`, as in:

```http
webrtc://{Domain}/{AppName}/{StreamName}
```


The table below lists the key fields in an LEB URL and their meanings.

| Field | Description |
| ------ | ------ |
| webrtc:// | Prefix |
| Domain | Domain name |
| AppName | Application name, which is `live` by default. It specifies the storage path of a live streaming file. |
| StreamName | Stream name, which is the unique identifier of a stream |

>? To publish streams, please see [Publishing from Camera](https://intl.cloud.tencent.com/document/product/1071/38157) or [Publishing from Screen](https://intl.cloud.tencent.com/document/product/1071/41878).

[](id:step3)

### Step 3. Start LEB
You can use a `V2TXLivePlayer` object for LEB. For details, see the code below (make sure that you pass in the correct URL).

#### Sample code
<dx-codeblock>
::: Android
// Create a V2TXLivePlayer object
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
player.setObserver(new MyPlayerObserver(playerView));
player.setRenderView(mSurfaceView);
// Pass in the low-latency playback URL to start playback
player.startPlay("webrtc://{Domain}/{AppName}/{StreamName}");
:::
::: iOS
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];
[player setObserver:self];
[player setRenderView:videoView];
[player startPlay:@"webrtc://{Domain}/{AppName}/{StreamName}"];
:::
</dx-codeblock>
