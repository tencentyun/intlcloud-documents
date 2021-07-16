## RTC-based Co-anchoring
In RTMP-based co-anchoring, the MLVB SDK offers the co-anchoring component `MLVBLiveRoom` to help you quickly implement the co-anchoring feature. To better cater to your co-anchoring needs, Tencent Cloud has launched an RTC-based co-anchoring scheme and offered simpler and more flexible V2 APIs.

MLVB’s V2 APIs support publishing/co-anchoring via RTMP as well as RTC. You can choose whichever scheme fits your needs. Below is a comparison of the two schemes.

| Item   | RTMP                  | RTC                                           |
| -------- | -------------------------- | -------------------------------------------------- |
| Protocol     | Based on TCP            | Based on UDP (more suitable for streaming)                 |
| QoS      | Low adaptability to poor network connection              | Streaming unaffected with 50% of packets loss; co-anchoring unaffected with 70% of packets loss |
| Region | Chinese mainland | Worldwide                                           |
| Tencent Cloud products used | MLVB, CSS | MLVB, CSS, TRTC             |
| Price     | [Contact sales](https://intl.cloud.tencent.com/contact-sales)                | Tiered pricing. See [Billing](#price).  |


## Trying out RTC-based Co-anchoring
Video Cloud Toolkit is a comprehensive audio-video service solution developed by Tencent Cloud. It allows you to try out the features of the TRTC, MLVB and UGC SDKs, including RTC-based co-anchoring: **Co-anchoring (New)**.

### GitHub address
| Platform    | Demo                                                    | Source code                                                     | Folder                                                   |
| ------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Android | <img width="150" src="https://liteav.sdk.qcloud.com/doc/res/mlvb/picture/video_cloud_tools_app_qr_code_android.png"> | [GitHub](https://github.com/tencentyun/LiteAVProfessional_Android) | [Demo/livelinkmicdemonew](https://github.com/tencentyun/LiteAVProfessional_Android/tree/master/Demo/livelinkmicdemonew) |
| iOS     | <img width="150" src="https://liteav.sdk.qcloud.com/doc/res/mlvb/picture/video_cloud_tools_app_qr_code_ios.png"> | [GitHub](https://github.com/tencentyun/LiteAVProfessional_iOS) | [Demo/TXLiteAVDemo/LiveLinkMicDemoNew](https://github.com/tencentyun/LiteAVProfessional_iOS/tree/master/Demo/TXLiteAVDemo/LiveLinkMicDemoNew) |

### Directions
![](https://main.qcloudimg.com/raw/c3494c2741ea0e816ae6a74fe7077bb0.png)
>!When you try out the demo, please note that due to the use of the ultra-low-latency streaming protocol, in RTC-based co-anchoring, you cannot **use the same `streamid` for ultra-low-latency publishing and playback on the same device**.

## Integration

The latest MLVB SDK offers new V2 APIs `V2TXLivePusher` (publishing) and `V2TXLivePlayer` (playback) to power live streaming scenarios with **greater flexibility, lower latency, and larger scale**. See below for how to quickly implement interactive features such as co-anchoring and anchor competition using `V2TXLivePusher` and `V2TXLivePlayer`.

[](id:RegistrationService)
### Step 1: Activate TRTC. 
Before you start ultra-low-latency playback, follow the steps bellow to activate [**TRTC**](https://intl.cloud.tencent.com/document/product/647).

1. [Sign up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and complete [Identity Verification](https://intl.cloud.tencent.com/document/product/378/3629).
2. Log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)**.
3. Click Create Application, enter an application name, e.g., `V2Demo`, and click confirm.
![](https://main.qcloudimg.com/raw/91895a5aa85529b0de3ad6d36ca8874a.png)
4. Find the application you created, and click **Application Info** on the right to view its `SDKAppID`.
5. Click **Quick Start**, wait for the information to load, and note the **key needed to issue UserSig**.

> !
>- The method for generating `UserSig` described in this document involves configuring `UserSig` in client code. In this method, `UserSig` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

> ? After activating TRTC, you are advised to compile the SimpleCode (a simplified demo) we provide to try out the service and learn to use the demo’s APIs with the help of the following documents.
> - [Android](https://github.com/tencentyun/LiteAVProfessional_Android)
> - [iOS](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/SimpleDemo)

### Step 2. Learn about publishing and playback protocols.
In live streaming scenarios, URLs are required for both publishing and playback. Below are examples of the URLs used for ultra-low-latency streaming.

- **Publish**
```http
trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxxxx
```
-**Playback**
```http
trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxx
```

The table below lists the key fields in the URLs and their meanings.

| Field              | Description                                                     |
| --------------------- | ------------------------------------------------------------ |
| **trtc://**           | Prefix of the URL for low-latency publishing                                       |
| **cloud.tencent.com** | Dedicated domain name for low-latency streaming, which **must not be modified**                              |
| **push**              | Identifier, which indicates publishing                                             |
| **play**              | Identifier, which indicates playback                                             |
| **sdkappid**          | The SDKAppID generated in [**Activate TRTC**](#RegistrationService) |
| **userId**            | Anchor’s ID, which is set by you                                  |
| **usersig**           | The UserSig key obtained in [Activate TRTC](#RegistrationService) |


### Step 3. Learn about V2TXLivePusher publishing.

#### Splicing URLs
You need to splice your own URLs in the project code according to the rules described above.

#### Sample code
<dx-codeblock>
::: Java
// Create a V2TXLivePusher object and set the mode to TXLiveMode_RTC.
V2TXLivePusher pusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTC);
pusher.setObserver(new MyPusherObserver());
pusher.setRenderView(mSurfaceView);
pusher.startCamera(true);
pusher.startMicrophone();
// Pass in the low-latency publishing URL to start publishing.
pusher.startPush("trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=finnguan&usersig=xxxxx");
:::
::: Objective-C
// Create a V2TXLivePusher object and set the mode to TXLiveMode_RTC.
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
[pusher setObserver:self];
[pusher setRenderView:videoView];
[pusher startCamera:true];
[pusher startMicrophone];
// Pass in the low-latency publishing URL to start publishing.
[pusher startPush:@"trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=finnguan&usersig=xxxxx"];
:::
</dx-codeblock>


#### Step 4. Learn about V2TXLivePlayer playback.

### Splicing URLs
You need to splice your own URLs in the project code according to the publishing URL and the rules described above.

#### Sample code
<dx-codeblock>
::: Java
// Create a V2TXLivePlayer object.
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
player.setObserver(new MyPlayerObserver(playerView));
player.setRenderView(mSurfaceView);
// Pass in the low-latency playback URL to start playback.
player.startPlay("trtc://cloud.tencent.com/play/streamid?sdkappid=1400188366&userId=A&usersig=xxx");
:::
::: Objective-C
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];
[player setObserver:self];
[player setRenderView:videoView];
[player startPlay:@"trtc://cloud.tencent.com/play/streamid?sdkappid=1400188366&userId=A&usersig=xxx"];
:::
</dx-codeblock>


### Step 5. Start co-anchoring.
![](https://main.qcloudimg.com/raw/51732906260d33b3ba67a3e1bda6dbea.png)
1. Anchor A starts streaming by calling `V2TXLivePusher`.
<dx-codeblock>
::: Java
V2TXLivePusher pusherA = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
pusherA.startPush(pushURLA);
:::
::: Objective-C
V2TXLivePusher *pusherA = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
...
[pusherA startPush:pushURLA];
:::
</dx-codeblock>
2. All viewers play back anchor A’s stream by calling `V2TXLivePlayer`.
<dx-codeblock>
::: Java
V2TXLivePlayer playerA = new V2TXLivePlayerImpl(mContext);
...
playerA.startPlay(playURLA);
:::
::: Objective-C
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];
...
[player startPlay:playURLA];
:::
</dx-codeblock>
3. **Start co-anchoring**: viewer B (referred to as co-anchoring viewer B below) calls `V2TXLivePusher` to start publishing.
<dx-codeblock>
::: Java
V2TXLivePusher pusherB = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
pusherB.startPush(pushURLB);
:::
::: Objective-C
V2TXLivePusher *pusherB = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
...
[pusherB startPush:pushURLB];
:::
</dx-codeblock>
4. **After receiving the co-anchoring notification**, anchor A calls `V2TXLivePlayer` to play back **co-anchoring viewer B**’s stream and start ultra-low-latency interaction with **co-anchoring viewer B**.
<dx-codeblock>
::: Java
V2TXLivePlayer playerB = new V2TXLivePlayerImpl(mContext);
...
playerB.startPlay(playURLB);
:::
::: Objective-C
V2TXLivePlayer *playerB = [[V2TXLivePlayer alloc] init];
...
[playerB startPlay:playURLB];
:::
</dx-codeblock>
5. **After the co-anchoring starts**, other viewers call `V2TXLivePlayer` to play back **co-anchoring viewer B**’s stream.

### Step 6. Start anchor competition.
1. Anchor A starts streaming by calling `V2TXLivePusher`.
<dx-codeblock>
::: Java
V2TXLivePusher pusherA = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
pusherA.startPush(pushURLA);
:::
::: Objective-C
V2TXLivePusher *pusherA = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
...
[pusherA startPush:pushURLA];
:::
</dx-codeblock>
2. Anchor B starts streaming by calling `V2TXLivePusher`.
<dx-codeblock>
::: Java
V2TXLivePusher pusherB = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
...
pusherB.startPush(pushURLB);
:::
::: Objective-C
V2TXLivePusher *pusherB = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
...
[pusherB startPush:pushURLB];
:::
</dx-codeblock>

3. **Start anchor competition**: anchor A and B call `V2TXLivePlayer` to play back each other’s stream and interact with ultra low latency.

<dx-codeblock>
::: Java  Java 
V2TXLivePlayer playerA = new V2TXLivePlayerImpl(mContext);
...
playerA.startPlay(playURLA);
      
V2TXLivePlayer playerB = new V2TXLivePlayerImpl(mContext);
...
playerB.startPlay(playURLB);
:::
::: Objective-C  Objective-C
V2TXLivePlayer *playerA = [[V2TXLivePlayer alloc] init];
...
[playerA startPlay:playURLA];
      
V2TXLivePlayer *playerB = [[V2TXLivePlayer alloc] init];
...
[playerB startPlay:playURLB];
:::
</dx-codeblock>

4. **After the anchor competition starts**, anchor A’s viewers call `V2TXLivePlayer` to play back anchor B’s stream, and anchor B’s viewers call `V2TXLivePlayer` to play back anchor A’s stream.

>? Since you need to maintain a room and users yourself, you may think that the new RTC-based co-anchoring scheme is more complicated that the old one. In fact, **there isn’t an absolutely better scheme, only one that better suits your needs**.
> - You can stick to the old co-anchoring scheme if your application scenarios are not demanding on latency or concurrency.
> - If you want to use V2 APIs without having to manage a room and users, try using [Tencent Cloud’s IM SDK](https://intl.cloud.tencent.com/document/product/1047) to implement the necessary logic.

[](id:price)
## Billing

The RTC-based co-anchoring scheme is enabled by TRTC, which charges you based on **mic-on duration**. The table below lists the types of durations and their list prices.

| Duration Type | Playback Resolution                   | Unit Price (USD/1,000 Min) |
| ------------ | ---------------------------- | ------------------- |
| Audio       | -                            | 0.99                |
| SD      | ≤ 640 × 480        | 1.99                |
| HD      | 640 × 480 - 1280 × 720 | 3.99                |
| UHD     | > 1280 × 720               | 14.99               |

>?
>- Mic-on duration is the duration of playback by the anchor and co-anchoring viewers. The type of a duration depends on the playback resolution.
>- If a user plays an audio-video stream, the duration will be charged only once as a video duration rather than twice as a video and audio duration.
>- If a mic-on user publishes streams but does not play back streams, the user’s duration will be billed as an audio duration, whose length is the same as the duration of publishing.

## FAQs

### 1. Why is publishing and playback using the same `streamid` on the same device possible with `TXLivePusher` and `TXLivePlayer` but not with `V2TXLivePusher` and `V2TXLivePlayer`?
`V2TXLivePusher` and `V2TXLivePlayer` are based on Tencent Cloud’s TRTC protocol. The UDP-based ultra-low latency private protocol does not support communication using the same `streamid` on the same device. Given the current use case, we have not worked to support the feature, but may consider enabling it in the future.

#### 2. What do the parameters generated in [**Activate TRTC**](#RegistrationService) mean?
`SDKAppID` is used to identify your application, and `UserID` your user. `UserSig` is a security signature calculated based on the two parameters using the **HMAC SHA256** encryption algorithm. Attackers cannot use your Tencent Cloud traffic without authorization as long as they cannot forge a `UserSig`. UserSig calculation involves hashing crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`, as shown below.
```Cpp
// `UserSig` calculation formula, in which `secretkey` is the key used to calculate `UserSig`.

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```

### 3. How can I set the audio or video quality using `V2TXLivePusher` and `V2TXLivePlayer`?
We provide APIs for the setting of audio and video quality. For details, please see [setAudioQuality()](http://doc.qcloudtrtc.com/group__V2TXLivePusher__ios.html#a88956a3ad5e030af7b2f7f46899e5f13) and [setVideoQuality:resolutionMode()](http://doc.qcloudtrtc.com/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84).

#### 4. What does the error code `-5` mean?
The error code `-5` means failure to call an API due to invalid license. The enumerated value is [V2TXLIVE_ERROR_INVALID_LICENSE](http://doc.qcloudtrtc.com/group__V2TXLiveCode__ios.html). For other error codes, please see [V2TXLiveCode](http://doc.qcloudtrtc.com/group__V2TXLiveCode__ios.html).

#### 5. What is the typical latency of RTC-based co-anchoring?
In the new RTC-based co-anchoring scheme, the co-anchoring latency is lower than 200 ms, and the latency for anchors and viewers is 100-1,000 ms.
