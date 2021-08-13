## WebRTC-based Co-anchoring
In [**RTMP-based co-anchoring**](https://intl.cloud.tencent.com/zh/document/product/1071), the MLVB SDK offers the component `MLVBLiveRoom` to help you quickly implement the co-anchoring feature. To better cater to the needs for co-anchoring, Tencent Cloud has launched a WebRTC-based co-anchoring scheme and offered the simpler and more flexible V2 APIs.

MLVB’s V2 APIs support publishing/co-anchoring via RTMP as well as WebRTC. You can choose whichever scheme fits your needs. Below is a comparison of the two schemes.

| Item   | RTMP                  | WebRTC                                           |
| -------- | -------------------------- | -------------------------------------------------- |
| Protocol     | Based on TCP            | Based on UDP (more suitable for streaming)                 |
| QoS      | Poor adaptability to bad network connection              | Video streaming unaffected with 50% of packets loss; audio co-anchoring unaffected with 70% of packets loss |
| Region | Chinese mainland | Worldwide                                           |
| Tencent Cloud products used | MLVB, CSS | MLVB, CSS, TRTC             |
| Price     | 0.016 CNY/min               | Tiered pricing. For details, please see [Billing](#price).  |


## Trying out WebRTC-based Co-anchoring
Video Cloud Toolkit is a comprehensive audio-video service solution developed by Tencent Cloud that allows you to try out the features of the TRTC, MLVB and UGC SDKs, including WebRTC-based co-anchoring: **Co-anchoring (New)**.

### Address
| Platform    | Demo                                                    | Source code                                                     | Folder                                                   |
| ------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Android | <img width="150" src="https://main.qcloudimg.com/raw/bff0cfca4585c448f308b339a6c17c1c.png"> | [GitHub](https://github.com/tencentyun/LiteAVProfessional_Android) | [Demo/livelinkmicdemonew](https://github.com/tencentyun/LiteAVProfessional_Android/tree/master/Demo/livelinkmicdemonew) |
| iOS     | <img width="150" src="https://main.qcloudimg.com/raw/83973196cc1fc9972320182eb283d406.png"> | [GitHub](https://github.com/tencentyun/LiteAVProfessional_iOS) | [Demo/TXLiteAVDemo/LiveLinkMicDemoNew](https://github.com/tencentyun/LiteAVProfessional_iOS/tree/master/Demo/TXLiteAVDemo/LiveLinkMicDemoNew) |



### Demonstration
<table>
        <tr> 
                <th><div align=center>Host A</div></th>
                <th><div align=center>Host B</div></th>
                <th><div align=center>Audience</div></th>
        </tr>
        <tr>
                </td>
                  <div align=center>
                    <img src="https://liteav.sdk.qcloud.com/doc/res/mlvb/picture/anchor.gif">
                    </div>
                  </td>
                </td>
                  <div align=center>
                    <img src="https://liteav.sdk.qcloud.com/doc/res/mlvb/picture/link_audience.gif">
                    </div>
                </td>
                </td>
                  <div align=center>
                    <img src="https://liteav.sdk.qcloud.com/doc/res/mlvb/picture/others_audience.gif">
                    </div>
                </td>
        </tr>
</table>

### Directions
![](https://liteav.sdk.qcloud.com/doc/res/mlvb/picture/v2_demo_use_step.png)
> =Please note that due to the use of the ultra-low-latency streaming protocol, you cannot **use the same `streamid` for ultra-low-latency publishing and playback on the same device** with WebRTC-based co-anchoring.

## Integration
The MLVB SDK provides new V2 APIs via `V2TXLivePusher` (publishing) and `V2TXLivePlayer` (playback) to power larger-scale live streaming scenarios with greater flexibility and lower latency. Hosts can use WebRTC capabilities provided by the APIs to publish streams. Audience, by default, play streams via CDNs, whose cost is relatively low. To co-anchor with hosts, audience can switch to WebRTC-based streaming, which has lower latency and delivers better interaction experience. See below for how to integrate the feature.

[](id:step1)
### Step 1. Activate TRTC 
Before you integrate the WebRTC-based co-anchoring feature, follow the steps bellow to activate [**TRTC**](https://intl.cloud.tencent.com/document/product/647) first.

1. [Sign up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Log in to the TRTC console and click **[Application Management](https://intl.cloud.tencent.com/register)**.
3. Click **Create Application**, enter an application name, e.g., `V2Demo`, and click **Confirm**.
![](https://min-cos-1300507594.cos.ap-beijing.myqcloud.com/blog/min.helloworld/21ef2f952c428c08cedfbef88ba16407.png)
4. Find the application you created, and click **Application Info** on the right to view its `SDKAppID`.
5. Click **Quick Start**, wait for the information to load, and note the **key needed to generate UserSig**.
> !
>- The method for generating `UserSig` described in this document involves configuring `UserSig` in client code. In this method, `UserSig` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

> ? After activating TRTC, you are advised to compile the `SimpleCode` project (a simplified demo) we provide to try out the feature and learn to use the APIs with the help of the following documents.
> - [Android](https://github.com/tencentyun/MLVBSDK/tree/master/Android/SimpleDemo)
> - [iOS](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/SimpleDemo)

[](id:step2)

### Step 2. Use `V2TXLivePusher` to publish streams via WebRTC
#### Splice URLs
You need to splice publishing URLs by yourself in the project code, as shown below. Here is an example:

**Publishing URL**
```http
trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxxxx
```

The table below lists the key fields in a publishing URL and their meanings.

| Field              | Description                                                     |
| --------------------- | ------------------------------------------------------------ |
| **trtc://**           | Prefix of publishing URLs for interactive live streaming                                  |
| **cloud.tencent.com** | Dedicated domain name for interactive live streaming, which **must not be modified**                              |
| **push**              | Identifier, which indicates publishing                                             |
| **sdkappid**          | The `SDKAppID` generated in [**Activate TRTC**](#RegistrationService) |
| **userId**            | Host’s ID, which is set by you                                  |
| **usersig**           | The `UserSig` key obtained in [**Activate TRTC**](#RegistrationService) |


#### Sample code

```java
// Create a V2TXLivePusher object and set the mode to TXLiveMode_RTC
V2TXLivePusher pusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTC);
pusher.setObserver(new MyPusherObserver());
pusher.setRenderView(mSurfaceView);
pusher.startCamera(true);
pusher.startMicrophone();
// Pass in the URL to start WebRTC-based stream publishing
pusher.startPush("trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=finnguan&usersig=xxxxx");
```


### Step 3. Use `V2TXLivePlayer` to play streams via CDNs

#### Splice URLs
You need to splice playback URLs in the format of `domain name + streamID` by yourself in the project code.

#### Sample code
```java
// Create a V2TXLivePlayer object
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
player.setObserver(new MyPlayerObserver(playerView));
player.setRenderView(mSurfaceView);
// Pass in the URL to start playback
player.startPlay("https://3891.liveplay.myqcloud.com/live/streamid.flv");
```


### Step 4. Co-anchor
![](https://min-cos-1300507594.cos.ap-beijing.myqcloud.com/blog/min.helloworld/24e495dd1a910f53069237ecdf28491e.jpg)
#### 1. Publish streams via WebRTC

User A, the host, calls `V2TXLivePusher` to publish streams.

```java
V2TXLivePusher pusherA = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
/**
 * pushURLA= "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxx";
 */
pusherA.startPush(pushURLA);
```

#### 2. Play streams via CDNs

All audience call `V2TXLivePlayer` to play the host’s stream.

```java
V2TXLivePlayer playerA = new V2TXLivePlayerImpl(mContext);
...
/**
 * Streams are played back via CDNs in the example. The protocols supported include FLV, HLS, and WebRTC. Standard protocols such as FLV and HLS are more cost-effective, but WebRTC delivers interaction experience with lower latency.
 * playURLA= "http://3891.liveplay.myqcloud.com/live/streamidA.flv";
 * playURLA= "http://3891.liveplay.myqcloud.com/live/streamidA.hls";
 * playURLA= "webrtc://3891.liveplay.myqcloud.com/live/streamidA"
 */
playerA.startPlay(playURLA);
```


#### 3. Initiate co-anchoring

User B from the audience (the co-anchoring user B) calls `V2TXLivePusher` to publish streams.

```java
V2TXLivePusher pusherB = new V2TXLivePusherImpl(this,V2TXLiveMode.TXLiveMode_RTC);
...
/*
 * pushURLB= "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=B&usersig=xxx";
 */
pusherB.startPush(pushURLB);
```

#### 4. Start co-anchoring

User A the host calls `V2TXLivePlayer` to play the stream of **the co-anchoring user B** via WebRTC.

```java
V2TXLivePlayer playerB = new V2TXLivePlayerImpl(mContext);
...
/**
 * playURLB= "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=B&usersig=xxx";
 */
playerB.startPlay(playURLB);
```
**The co-anchoring user B** calls `V2TXLivePlayer` to switch to WebRTC and play the stream of user A the host.

```java
V2TXLivePlayer playerA = new V2TXLivePlayerImpl(mContext);
...
/**
 *playURLA= "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxx";
 */
playerA.startPlay(playURLA);
```
User A the host and the **co-anchoring user B** start ultra-low-latency interaction.


#### 5. Mix streams

For other audience to see user A the host and user B interact with each other in one channel of stream, user A needs to initiate a stream mixing task to mix his or her stream with that of user B. To do this, user A needs to call `setMixTranscodingConfig` to enable On-Cloud MixTranscoding, passing in audio parameters including `audioSampleRate`, `audioBitrate`, and `audioChannels`. If your application scenarios involve video, video parameters such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate` are also required.

Sample code:
```java
V2TXLiveDef.V2TXLiveTranscodingConfig config = new V2TXLiveDef.V2TXLiveTranscodingConfig();
// Set the resolution to 720 x 1280 px, bitrate 1500 Kbps, and frame rate 20 FPS
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
config.mixStreams      = new ArrayList<>();

// Position of the camera image of the host
V2TXLiveDef.V2TXLiveMixStream local = new V2TXLiveDef.V2TXLiveMixStream();
local.userId   = "localUserId";
local.streamId = null; // `streamID` is required for the remote user but not for the local user
local.x        = 0;
local.y        = 0;
local.width    = videoWidth;
local.height   = videoHeight;
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the host’s image is displayed at the bottom
config.mixStreams.add(local);

// Image position of the co-anchoring user
V2TXLiveDef.V2TXLiveMixStream remoteA = new V2TXLiveDef.V2TXLiveMixStream();
remoteA.userId   = "remoteUserIdA";
remoteA.streamId = "remoteStreamIdA"; // `streamID` is required for the remote user but not for the local user
remoteA.x        = 400; // For reference only
remoteA.y        = 800; // For reference only
remoteA.width    = 180; // For reference only
remoteA.height   = 240; // For reference only
remoteA.zOrder   = 1;
config.mixStreams.add(remoteA);

// Image position of the co-anchoring user
V2TXLiveDef.V2TXLiveMixStream remoteB = new V2TXLiveDef.V2TXLiveMixStream();
remoteB.userId   = "remoteUserIdB";
remoteB.streamId = "remoteStreamIdB"; // `streamID` is required for the remote user but not for the local user
remoteB.x        = 400; // For reference only
remoteB.y        = 800; // For reference only
remoteB.width    = 180; // For reference only
remoteB.height   = 240; // For reference only
remoteB.zOrder   = 1;
config.mixStreams.add(remoteB);

// Enable On-Cloud MixTranscoding
pusher.setMixTranscodingConfig(config);
```

> ! After On-Cloud MixTranscoding is enabled, the default ID for the post-mixing stream is the stream ID of the user who initiates the task. To specify an ID for the stream after mixing, pass in the ID when calling the API.

After the above steps are performed, other audience will be able to see user A and user B interact with each other.

### Step 5. Compete across rooms
1. Host A starts streaming by calling `V2TXLivePusher`.
<dx-codeblock>
::: java java
V2TXLivePusher pusherA = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
/**
 * pushURLA= "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxx";
 */
pusherA.startPush(pushURLA);
:::
</dx-codeblock>
2. Host B starts streaming by calling `V2TXLivePusher`.
<dx-codeblock>
::: java java
V2TXLivePusher pusherB = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
/**
 * pushURLB "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=B&usersig=xxx";
 */
pusherB.startPush(pushURLB);
:::
</dx-codeblock>
3. **Start competition**: host A and B call `V2TXLivePlayer` to play each other’s stream and start WebRTC-based co-anchoring.
<dx-codeblock>
::: java java
V2TXLivePlayer playerA = new V2TXLivePlayerImpl(mContext);
...
/**
 * Streams are played back via CDNs in the example. The protocols supported include FLV, HLS, and WebRTC. Standard protocols such as FLV and HLS are more cost-effective, but WebRTC delivers interaction experience with lower latency.
 * playURLA= "http://3891.liveplay.myqcloud.com/live/streamidB.flv";
 * playURLA= "http://3891.liveplay.myqcloud.com/live/streamidB.hls";
 * playURLA= "webrtc://3891.liveplay.myqcloud.com/live/streamidB"
 */
playerA.startPlay(playURLA);

V2TXLivePlayer playerB = new V2TXLivePlayerImpl(mContext);
...
/**
 * Streams are played back via CDNs in the example. The protocols supported include FLV, HLS, and WebRTC. Standard protocols such as FLV and HLS are more cost-effective, but WebRTC delivers interaction experience with lower latency.
 * playURLB= "http://3891.liveplay.myqcloud.com/live/streamidA.flv";
 * playURLB= "http://3891.liveplay.myqcloud.com/live/streamidA.hls";
 * playURLB= "webrtc://3891.liveplay.myqcloud.com/live/streamidA"
 */
playerB.startPlay(playURLB);
:::
</dx-codeblock>
4. **After the competition starts**, host A’s audience call `V2TXLivePlayer` to play host B’s stream, and host B’s audience call `V2TXLivePlayer` to play host A’s stream.

> ? Since you need to maintain a room and users by yourself, the new WebRTC-based co-anchoring scheme may seem more complicated that the old one. Indeed, **there isn’t an always better scheme, only one that better suits your needs**.
> - You can stick to the old co-anchoring scheme if your application scenarios do not require low latency or high concurrency.
> - If you want to use V2 APIs without having to manage a room and users, try using [Tencent Cloud’s IM SDK](https://intl.cloud.tencent.com/document/product/1047) to implement the necessary logic.


[](id:price)
## Billing

The WebRTC-based co-anchoring scheme is enabled by TRTC, which charges you based on **the durations of anchoring users**. The table below lists the types of durations and their list prices.

| Duration Type | Playback Resolution                   | Unit Price (USD/1,000 Min) |
| ------------ | ---------------------------- | ----------------- |
| Audio       | -                            | 0.99                |
| SD      | ≤ 640 x 480        | 1.99                |
| HD      | 640 x 480 - 1280 × 720 | 3.99                |
| FHD     | > 1280 x 720               | 14.99               |

>?
- Both the host and co-anchoring audience are anchoring users. Their durations are the length of periods when they play streams. The resolution of the streams played determines the duration type.
- If an anchoring user plays an audio-video stream, his or her duration will be charged only once as a video duration.
- If an anchoring user publishes streams but does not play streams, the user’s duration will be the length of period when he or she publishes streams and will be billed as an audio duration.

Accounts [creating applications](https://intl.cloud.tencent.com/document/product/647/39077) in the TRTC console for the first time will get a 10,000-min [free trial package](https://intl.cloud.tencent.com/document/product/647/39784). The service will be suspended for your account once you use up the trial package. You can [purchase a new package](https://cloud.tencent.com/product/trtc) to activate the service again.

## FAQs

#### 1. Why is publishing and playback using the same `streamid` on the same device possible with `TXLivePusher` and `TXLivePlayer` but not with `V2TXLivePusher` and `V2TXLivePlayer`?
`V2TXLivePusher` and `V2TXLivePlayer` are based on Tencent Cloud’s [TRTC](https://intl.cloud.tencent.com/document/product/647/39958) protocol. This UDP-based ultra-low latency private protocol does not support communication using the same `streamid` on the same device at the moment. We have not supported the feature for now given the current use cases, but may consider supporting it in the future.

#### 2. What do the parameters generated in [**Activate TRTC**](#RegistrationService) mean?
`SDKAppID` identifies your application, and `UserID` your user. `UserSig` is a security signature calculated based on the two parameters using the **HMAC SHA256** encryption algorithm. Attackers cannot use your Tencent Cloud traffic without authorization as long as they cannot forge a `UserSig`. `UserSig` calculation involves hashing crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`, as shown below.
```Cpp
// UserSig formula, in which `secretkey` is the key used to calculate UserSig

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```

#### 3. How can I set audio or video quality using `V2TXLivePusher` and `V2TXLivePlayer`?
We provide APIs for the setting of audio and video quality. For details, please see [setAudioQuality()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a88956a3ad5e030af7b2f7f46899e5f13) and [setVideoQuality:resolutionMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84).

#### 4. What does the error code `-5` mean?
The error code `-5` means failure to call an API due to invalid license. The enumerated value is [V2TXLIVE_ERROR_INVALID_LICENSE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html). For other error codes, please see [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html).

#### 5. What is the typical latency of WebRTC-based co-anchoring?
In the new WebRTC-based co-anchoring scheme, the co-anchoring latency is lower than 200 ms, and the latency for hosts and audience is 100-1,000 ms.
