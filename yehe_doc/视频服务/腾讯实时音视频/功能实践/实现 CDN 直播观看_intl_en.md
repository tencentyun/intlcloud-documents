## Use Cases
TRTC uses UDP to transfer audio/video data, but standard live streaming CDNs use protocols such as RTMP, HLS, and FLV. As a result, the audio/video data in TRTC needs to be **relayed** to live streaming CDNs for viewers to watch.

It is often necessary to relay from TRTC to live streaming CDNs in the following two scenarios.
- **Scenario 1: ultra-high-concurrency watching**
In each TRTC room, up to 100,000 viewers can watch live streams at low latency at the same time. CDN live streaming has a higher latency, but it allows more concurrent viewers and is more cost-effective.
- **Scenario 2: playback on mobile browsers**
TRTC can be accessed through WebRTC, but WebRTC works mainly for desktop Chrome and is poorly supported by mobile browsers, especially on Android. Therefore, if you want to stream on mobile browsers, we recommend that you use the HLS (m3u8) protocol, which requires the support of live streaming CDNs.


## How It Works
Tencent Cloud uses a relayed transcoding cluster to relay TRTC’s audio/video data to live streaming CDNs. The cluster converts the UDP streams of TRTC to the standard RTMP streams.
<span id="directCDN"></span>
**Relaying and streaming single-channel streams**
If there is only one anchor in a TRTC room, relayed push in TRTC is the same as direct push over the standard RTMP, but UDP, which TRTC uses for data transmission, adapts better to poor network conditions than RTMP does.
![](https://main.qcloudimg.com/raw/23ac68cb46b06cc4eb6000fa98500dc4.jpg)

<span id="mixCDN"></span>
**Relaying and streaming streams mixed from multiple channels**
The biggest strength of TRTC is audio/video co-anchoring. If there are multiple anchors in a room but a CDN viewer wants to pull only one channel of audio/video streams, TRTC can use the [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) feature to mix multiple channels of streams into one channel. Here is how it works:
![](https://main.qcloudimg.com/raw/77eeed776e61c3a6bd0e1669e5747727.jpg)

> **Why not play back multiple channels of video images via CDNs?**
> For one, it is difficult to synchronize multiple channels of streams played back via CDNs; for another, pulling multiple channels of streams consumes more traffic than downloading single-channel streams. Therefore, it is common in the industry to mix streams in the cloud before playback.

## Prerequisites
You have activated Tencent Cloud [LVB](https://console.cloud.tencent.com/live) and, according to the requirements of the regulator, you must have a playback domain name for live streaming. For details, see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970)

## Directions

<span id="step1"></span>
### Step 1. Enable relayed push.

1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** in the navigation pane to the left, find your application, and click **Function Configuration**.
3. In **Relayed Push Configuration**, click ![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png) next to **Enable Relayed Push**, and click **Enable Relayed Push** in the dialog box that pops up.


<span id="step2"></span>
### Step 2. Configure the playback domain name and CNAME record.
1. Log in to the [LVB console](https://console.cloud.tencent.com/live).
2. In the navigation pane to the left, select **Domain Management** and you will see that a push domain name in the format of `xxxxx.livepush.myqcloud.com` has been added to the list. `xxxxx` is `bizid`, which is a numeric string and can be found in TRTC console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info**.
3. Click **Add Domain**, enter a playback domain name for which you have obtained an ICP license. For **Type**, select **Playback Domain**, choose an acceleration region, and click **Confirm**.
4. Once your domain name is added, the system will automatically assign to it a CNAME, which ends with `.liveplay.myqcloud.com`. The CNAME can be accessed only after you configure it at your domain name service provider. You will be able to use LVB services once the configuration takes effect. For detailed directions, see [Configuring CNAME for Domain Name](https://intl.cloud.tencent.com/document/product/267/31057).

>! **You do not need to add a push domain name.** After you enable relayed push in [step 1](#step1), Tencent Cloud will add a push domain name in the format of `xxxxx.livepush.myqcloud.com` to the domain list of the LVB console, which is the default push domain name used by LVB and TRTC and cannot be modified.

<span id="step3"></span>
### Step 3. Associate TRTC streams with LVB `streamId`.
After relayed push is enabled, each stream in a TRTC room will be assigned a playback address in the following format:
```
http://playback domain name/live/[streamId].flv
```
`streamId` uniquely identifies a live stream. You can specify a `streamId` or use the default one.

#### Method 1: specifying a `streamId`
You can specify a live stream ID by setting `streamId` in `TRTCParams` when calling the `enterRoom` function in `TRTCCloud`.
Below is an example of the setting code using `Objective-C` on iOS.

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // `SDKAppID` in TRTC, which is generated after the creation of an application
param.roomId   = 1001;           // Room ID
param.userId   = @"rexchang";    // User ID
param.userSig  = @"xxxxxxxx";    // Login signature
params.role     = TRTCRoleAnchor; // Role: anchor
param.streamId = @"stream1001";  // Stream ID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // Please use the `LIVE` mode.
```
For how to calculate `userSig`, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)

#### Method 2: using the default `streamId`
After relayed push is enabled, if you do not specify a `streamId`, the system will automatically generate one according to the following rules.

- **Fields included**
  - SDKAppID, which can be found in [TRTC console] (https://console.cloud.tencent.com/trtc/app) > ** Application Management > **Application Info**.
  - bizid: which can be found in [TRTC console] (https://console.cloud.tencent.com/trtc/app) > ** Application Management > **Application Info**.
  - roomId, which is specified in `TRTCParams` when you call `enterRoom`.
  - userId, which is specified in `TRTCParams` when you call `enterRoom`.
  - streamType, which is `main` if the camera image is streamed and `aux` if the screen sharing image is streamed. WebRTC supports only one upstream channel, so in WebRTC, `streamType` is `main` too if the screen sharing image is streamed.

- **Format**
 <table>
<tr>
<th>`streamId` Generation</th>
<th>Applications created on or after January 9, 2020</th>
<th>Applications created and used before January 9, 2020</th>
</tr>
<tr>
<td>Format</td>
<td>streamId = urlencode(sdkAppId_roomId_userId_streamType)</td>
<td>StreamId = bizid_MD5(roomId_userId_streamType)</td>
</tr>
<tr>
<td>Example</td>
<td>If `sdkAppId` is `12345678`, `roomId` is `12345`, `userId` is `userA`, and the camera image is streamed, <br>the `streamId` will be `12345678_12345_userA_main`.</td>
<td>If `bizid` is `1234`, `roomId` is `12345`, `userId` is `userA`, and the camera image is streamed, <br>the `streamId` will be `1234_MD5(12345_userA_main)`, i.e. `1234_8D0261436C375BB0DEA901D86D7D70E8`.</td>
</tr>
</table>


<span id="step4"></span>
### Step 4. Select a stream mixing scheme.

To play mixed streams, enable On-Cloud MixTranscoding by calling the `setMixTranscodingConfig` API in `TRTCCloud`. The `TRTCTranscodingConfig` parameter of the API allows you to configure:
 - The position and size of each image
 - The image quality and encoding parameter of the mixed stream

For more information on how to configure the image layout, see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618). For the modules involved in the process and their relations, see [How It Works](#mixCDN).

>! `setMixTranscodingConfig` does not mix streams at the viewer end. Instead, it uploads configurations to the cloud, and mix and transcode streams in cloud servers. The process may take a while as both stream mixing and transcoding involve the decoding and re-encoding of the original audio/video data. Consequently, the latency of playing mixed streams is often 1 or 2 seconds longer than that of playing individual streams.

<span id="step5"></span>
### Step 5. Get the playback address and integrate the player.
After configuring the playback domain name in [step 2](#step2) and the `streamId` in [step 3](#step3), you will get a playback address for live streaming in the following format.
```
http://playback domain name/live/[streamId].flv
```

Suppose your playback domain name is `live.myhost.com`, and you set the live stream ID (`streamId`) of user A in room 1001 to `streamd1001` in the room entry parameter.
You will get three playback addresses:
```
 RTMP: rtmp://live.myhost.com/live/streamd1001
 FLV: http://live.myhost.com/live/streamd1001.flv
 HLS: http://live.myhost.com/live/streamd1001.m3u8
```

We recommend **http - flv** addresses that start with `http` and end with `.flv`, as they feature high stability and reliability, low playback latency, and good instant playback performance.
For players, we recommend the integration methods in the following documents.

| Platform | Integration Document | API Overview | Supported Format|
|:-------:|:-------:|:-------:|-------|
| iOS app| [Integration instructions](https://intl.cloud.tencent.com/document/product/1071/38159) | TXLivePlayer (iOS)  | FLV is recommended. |
| Android app | [Integration instructions](https://intl.cloud.tencent.com/document/product/1071/38160) | TXLivePlayer (Android) | FLV is recommended. |
| Web browser | Integration instructions | - |  Desktop Chrome supports FLV. <br> Safari on macOS and mobile browsers support only HLS. |


<span id="step6"></span>
### Step 6. Reduce playback latency.

When relayed push is enabled, because streams are distributed via live streaming CDNs, playback via `http - flv` addresses tends to have higher latency than direct playback in TRTC call rooms.
The table below lists the average latency of playback via TXLiveplayer using Tencent Cloud’s live streaming CDN technology.

| Stream Type | TXLivePlayer Playback Mode | Average Latency |   Test Result |
|:-------:|:-------:|:--------:|:---------:|
| Individual streams | Ultrafast mode (recommended) | **2-3s** | See the left figure (orange) below. |
| Mixed streams | Ultrafast mode (recommended) | **4-5s** | See the right figure (blue) below. |

If you experience higher latency than the above test results, try reducing the latency by following the steps below.

- **Use the built-in TXLivePlayer of the TRTC SDK**
Average players such as ijkplayer or players based on FFmpeg are incapable of controlling latency, but TXLivePlyer comes with a player engine developed in-house by Tencent Cloud, which gives it the ability to control latency.

- **Set TXLivePlayer to the ultrafast mode**
You can switch to the ultrafast mode by configuring three parameters of `TXLivePlayerConfig`. Below is an example of configuration on [iOS](https://intl.cloud.tencent.com/document/product/1071/38159#Delay).
Example of the configuration code using `Objective-C` on iOS:
```
 // Set TXLivePlayer to the ultrafast mode.
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // Min. buffer time: 1s
    config.maxAutoAdjustCacheTime = 1; // Max. buffer time: 1s
    [player setConfig:config];
    // Start playback.
```

<span id="expense"></span>
## Billing

The costs of CDN relayed live streaming include **playback fees** and **transcoding fees**. Playback fees are basic service fees, and transcoding fees are charged only if [On-Cloud MixTranscoding](#mixCDN) is enabled.

>!The prices used in this document are for reference only. In case of any inconsistencies, the prices specified in [LVB > Purchase Guide > LVB Pricing Overview](https://intl.cloud.tencent.com/document/product/267/2819) shall prevail.

### Playback fees: cost of playing live streams via CDNs

**LVB** charges you for playing streams via CDNs based on the downstream traffic generated or bandwidth used. You can choose whichever billing mode fits your need. By default, the bill-by-traffic mode is used. For details, see [LVB > Purchase Guide > Basic Services > Billing Details > Traffic and Bandwidth](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#traffic-and-bandwidth).


### Transcoding fees: cost of mixing multiple channels of streams
Stream mixing involves data decoding and encoding, so if you enable [stream mixing](#mixCDN), an additional stream mixing and transcoding fee will be incurred, which is charged based on the resolution and duration of the streams transcoded. The higher resolution an anchor uses, and the longer co-anchoring (the most common application scenario for stream mixing) lasts, the higher the cost. For details, see [LVB > Purchase Guide > Basic Services > Billing Details > LVB Transcoding](https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#lvb-transcoding).

>Suppose you use [`setVideoEncodrParam()`](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) to set the bitrate (`videoBitrate`) for anchors to 1,500 Kbps and resolution to 720p, and an anchor co-anchored with a viewer for 1 hour, during which [stream mixing](#mixCDN) was enabled. The transcoding fee incurred will be `0.0057 USD/min × 60 min=0.342 USD`.

## FAQ
**Why is the video choppy and blurry when there is only one user in the room?**
Please set the `TRTCAppScene` parameter in `enterRoom` to **`TRTCAppSceneLIVE`**.
The `VideoCall` mode is optimized for video calls, so when there is only one user in a room, TRTC tends to maintain a low bitrate and frame rate to reduce traffic usage, which makes the video choppy and blurry.
