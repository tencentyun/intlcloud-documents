## Use Cases
CDN live streaming is also called CDN relayed live streaming. As TRTC uses the UDP protocol to transfer audio/video data, while LVB CDN uses protocols such as RTMP, HLS, and FLV to transfer data, the audio/video data in TRTC needs to be **relayed** to LVB CDN for viewers to watch.

Connecting TRTC to CDN for stream watching is generally used to solve the following two problems:
- **Problem 1: ultra-high-concurrence watching traffic**
TRTC supports low-latency watching for up to 100,000 viewers in a single room. Although watching through CDN has a relatively higher latency, it supports more concurrent viewers and is more cost-effective.
- **Problem 2: playback on webpages on mobile devices**
TRTC supports connection over the WebRTC protocol, but this protocol is mainly used in Chrome Desktop Edition and has very poor compatibility with mobile browsers, especially on Android. Therefore, if you want to share your live stream on a webpage through mobile browsers, you are recommended to use the HLS (m3u8) playback protocol, which means that you need to use the capabilities of LVB CDN to support HLS.


## How It Works
Tencent Cloud uses a relayed transcoding cluster to relay the audio/video data from TRTC to the LVB CDN system. The cluster converts the UDP protocol used in TRTC to the RTMP protocol used in LVB.
<span id="directCDN"></span>
**Relayed live streaming of a single channel of video image**
If there is only one anchor in a TRTC room, relayed push in TRTC is the same as standard direct push over RTMP, but UDP of TRTC has higher immunity to bad network condition than RTMP.
![](https://main.qcloudimg.com/raw/23ac68cb46b06cc4eb6000fa98500dc4.jpg)

<span id="mixCDN"></span>
**Relayed live streaming of mixed channels of video images**
TRTC works best in audio/video co-anchoring. If there are multiple anchors in the same room but a CDN viewer wants to pull only one channel of audio/video image, [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) is required to combine multiple channels of video images into one channel. It works as follows:
![](https://main.qcloudimg.com/raw/77eeed776e61c3a6bd0e1669e5747727.jpg)

> **Why not play back multiple channels of CDN video images directly?**
>If multiple channels of CDN video images are played back directly, their latency cannot be properly aligned, and the download traffic for pulling multiple channels is higher than that for one channel. Therefore, on-cloud mixtranscoding schemes are widely adopted in the industry.

## Prerequisites
You have activated Tencent Cloud [LVB](https://console.cloud.tencent.com/live). You need to configure a playback domain name for live stream playback according to the requirements of applicable authorities. For detailed directions, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).

## Directions

<span id="step1"></span>
### Step 1. Enable relayed push

1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** on the left sidebar and click **Feature Configuration** on the row of the target application.
3. In **Relayed Push Configuration**, click ![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png) on the right of **Auto-relay Push**, and click **OK** in the pop-up window.

<span id="step2"></span>
### Step 2. Configure the playback domain name and CNAME record
1. Log in to the [LVB Console](https://console.cloud.tencent.com/live/).
2. On the left sidebar, select **Domain Management** and you can see that a push domain name is added in the domain name list. Its format is `xxxxx.livepush.myqcloud.com`, where `xxxxx` is a number called `bizid`. You can find the `bizid` information in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC Console.
3. Click **Add Domain Name**, enter a playback domain name for which you have already obtained the ICP filing for service in Mainland China, select **Playback domain name** as its type, select an acceleration region (which is **Mainland China** by default), and click **OK**.
4. Once your domain name is added, the system will automatically assign it a CNAME domain name (suffixed with `.liveplay.myqcloud.com`), which cannot be accessed directly before you complete the CNAME configuration at your domain name service provider. After the configuration takes effect, LVB can be used properly. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/267/31057).

> **You do not need to add a push domain name.** After the relayed live streaming feature is enabled in [step 1](#step1), Tencent Cloud will add a push domain name in the format of `xxxxx.livepush.myqcloud.com` in the LVB Console by default. It is the default push domain name agreed on between LVB and TRTC and cannot be modified currently.

<span id="step3"></span>
### Step 3. Associate a TRTC audio/video stream with a LVB streamId
After enabling relayed push, each channel of video image in the TRTC room will be configured with a corresponding playback address in the following format:
```
http://playback domain name/live/[streamId].flv
```
`streamId` in the address can uniquely identify a live stream in LVB. You can customize it or use the default one generated by the system.

#### Method 1. Customize streamId
You can specify the live stream ID by setting the `streamId` parameter in the `TRTCParams` parameter when calling the `enterRoom` function in `TRTCCloud`.
This document uses Objective-C code for iOS as an example:

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // `SDKAppID` in TRTC, which can be obtained after an application is created
param.roomId   = 1001;           // Room ID
param.userId   = @"rexchang";    // Username
param.userSig  = @"xxxxxxxx";    // Login signature
param.role     = TRTCRoleAnchor; // Role: anchor
param.streamId = @"stream1001";  // Stream ID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // Please use the `LIVE` mode
```
For the calculation method of `userSig`, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

#### Method 2. Use the streamId generated by the system
After automatic relayed push is enabled, if you do not specify a custom `streamId`, the system will generate one for you by default according to the following rules:

- **Fields used to splice `streamId`**
  - SDKAppID: you can find it in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app).
  - bizid: you can find it in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app).
  - roomId: it is specified in the `TRTCParams` parameter in the `enterRoom` function.
  - userId: it is specified in the `TRTCParams` parameter in the `enterRoom` function.
  - streamType: it is `main` for the camera image and `aux` for the screen sharing image (as WebRTC supports only one upstream channel at the same time, the stream type of screen sharing over WebRTC is `main`).

- **Calculation rules for splicing `streamId`**
 <table>
<tr>
<th>Splicing</th>
<th>Applications created on or after January 9, 2020</th>
<th>Applications created and used before January 9, 2020</th>
</tr>
<tr>
<td>Splicing Rule</td>
<td>streamId = urlencode(sdkAppId_roomId_userId_streamType)</td>
<td>StreamId = bizid_MD5(roomId_userId_streamType)</td>
</tr>
<tr>
<td>Calculation Example</td>
<td>For example, if `sdkAppId` is `12345678`, `roomId` is `12345`, `userId` is `userA`, and the user is using a camera, <br>then, `streamId` will be `12345678_12345_userA_main`</td>
<td>For example, if `bizid` is `1234`, `roomId` is `12345`, `userId` is `userA`, and the user is using a camera, <br>then, `streamId` will be `1234_MD5(12345_userA_main)`, which is `1234_8D0261436C375BB0DEA901D86D7D70E8`</td>
</tr>
</table>


<span id="step4"></span>
### Step 4. Control the mix scheme for multi-channel video image

If you want to get the live stream video image after mixing, you need to call the `setMixTranscodingConfig` API of `TRTCCloud` to enable On-Cloud MixTranscoding. The `TRTCTranscodingConfig` parameter of this API can be used to configure:
 - Position and size of each subimage
 - Quality and encoding parameters of mixed video image.

For more information on how to configure the video image layout, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618). For more information on the relationship between modules involved in the whole process, please see [How It Works](#mixCDN).

> `setMixTranscodingConfig` does not perform stream mixing on devices; instead, it sends the stream mixing configuration to servers in the cloud, where stream mixing and transcoding are performed. As both stream mixing and transcoding require decoding and encoding of the original audio/video data, a longer time will be needed for processing. Therefore, the actual watching latency of a mixed video image is 1–2s longer than that of an independent video image.

<span id="step5"></span>
### Step 5. Get the playback address and start playback after connection
After you configure the playback domain name in [step 2](#step2) and map the `streamId` in [step 3](#step3), you can get a live stream playback address, which is in the following format:
```
http://playback domain name/live/[streamId].flv
```

For example, if your playback domain name is `live.myhost.com` and you use a room entry parameter to set the live stream ID (`streamId`) of userA in room 1001 to `streamd1001`:
Then, you can get three playback addresses:
```
 RTMP playback address: rtmp://live.myhost.com/live/streamd1001
 FLV playback address: http://live.myhost.com/live/streamd1001.flv
 HLS playback address: http://live.myhost.com/live/streamd1001.m3u8
```

You are recommended to use the **http - flv** address prefixed with `http` and suffixed with `.flv`, as it features high stability and reliability and low playback latency and delivers an excellent instant broadcasting experience.
You are recommended to select the player based on the following schemes:

| Platform | API Overview | Supported Format |
|:-------:|:-------:|-------|
| iOS application | TXLivePlayer(iOS) | FLV is recommended |
| Android application | TXLivePlayer(Android) | FLV is recommended |
| Web browser | - | Chrome Desktop Edition supports FLV <br> Safari on macOS and mobile browsers support only HLS |
| WeChat Mini Program |  [&lt;live-player&gt; tag](https://developers.weixin.qq.com/miniprogram/en/dev/component/live-player.html) | FLV is recommended |


<span id="step6"></span>
### Step 6. Optimize playback latency

After the `http - flv` address is enabled for relayed live streaming, as the traffic is distributed through LVB CDN, the watching latency will certainly be higher than the call latency in the TRTC live room.
The following latency values can be achieved through the current Tencent Cloud LVB CDN technology together with the TXLivePlayer player:

| Relayed Stream Type | TXLivePlayer Playback Mode | Average Latency | Test Result |
|:-------:|:-------:|:--------:|:---------:|
| Independent video image | Ultrafast mode (recommended) | **2–3s** | Please see the comparison (orange) in the left part of the figure below |
| Mixed video image | Ultrafast mode (recommended) | **4–5s** | Please see the comparison (blue) in the right part of the figure below |

The test in the figure below is conducted by using the same set of mobile phones. iPhone 6s on the left uses the TRTC SDK for live streaming, while Mi 6 on the right uses the TXLivePlayer player to play back a live stream over the FLV protocol.


If your actual latency is longer than that as listed in the table above, you can optimize it as follows:

- **Use the TXLivePlayer built in the TRTC SDK**
Common players packaged based on the FFmpeg kernel such as ijkplayer or FFmpeg lack latency control capabilities. If you use them to play back a stream at the live stream addresses above, the latency will generally be uncontrollable. TXLivePlayer has a proprietary playback engine, which can control the latency.

- **Set the ultrafast mode as the TXLivePlayer playback mode**
You can set three parameters in `TXLivePlayerConfig` to implement the ultrafast mode. Take iOS as an example:
This document uses Objective-C code for iOS as an example:
```
 // Set the ultrafast mode as the TXLivePlayer playback mode
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // The minimum cache time is 1s
    config.maxAutoAdjustCacheTime = 1; // The maximum cache time is 1s
    [player setConfig:config];
    // Start LVB playback
```

<span id="expense"></span>
## Applicable Fees

Fees of CDN relayed live streaming include **watching fees** and **transcoding fees**. The watching fees are the basic fees, while transcoding fees will be charged only if [On-Cloud MixTranscoding](#mixCDN) is enabled.

>The prices in this document are for reference only, and the prices listed in the billing description of [LVB](https://intl.cloud.tencent.com/document/product/267/2819) shall prevail.

### Watching fees: incurred during CDN relayed live streaming

For CDN relayed live streaming, **LVB** will charge you for downstream traffic/bandwidth incurred during watching. You can choose an appropriate billing mode based on your actual needs. The bill-by-traffic mode is used by default.


### Transcoding fees: incurred after On-Cloud MixTranscoding is enabled
If you enable [On-Cloud MixTranscoding](#mixCDN), as stream mixing needs decoding and encoding, additional On-Cloud MixTranscoding fees will be incurred. On-Cloud MixTranscoding is billed by resolution and transcoding duration. The higher the anchor's resolution or the longer the co-anchoring duration (generally, On-Cloud MixTranscoding is required only in co-anchoring), the higher the fees.

## FAQs
**There is only one user in the room, but the video image is lagging and blurry. Why?**
Please specify the `TRTCAppScene` parameter in `enterRoom` as **`TRTCAppSceneLIVE`**.
The `VideoCall` mode is optimized for video calls, so when there is only one user in the room, the video image will maintain a low bitrate and frame rate to reduce network traffic usage, which will look lagging and blurry.
