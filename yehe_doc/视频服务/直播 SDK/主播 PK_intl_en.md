
## Overview
In **RTMP-based mic connect**, the MLVB SDK of Tencent Video Cloud Toolkit offers the `MLVBLiveRoom` component to help you quickly implement the host competition feature. To better cater to your needs, Tencent Cloud has launched an RTC-based host competition scheme and offered simpler and more flexible V2 APIs.

MLVB’s V2 APIs support publishing/host competition via RTMP as well as RTC. You can choose whichever scheme fits your needs. Below is a comparison of the two schemes.

| Item   | RTMP                  | WebRTC                                           |
| -------- | -------------------------- | -------------------------------------------------- |
| Protocol     | Based on TCP            | Based on UDP (more suitable for streaming)                 |
| QoS      | Poor adaptability to bad network connection              | Video streaming unaffected with 50% packets loss; audio mic connect unaffected with 70% packets loss |
| Region | Chinese mainland | Worldwide                                           |
| Tencent Cloud products used | MLVB, CSS | MLVB, CSS, TRTC             |
| Price     | 0.0028 USD/min           | Tiered pricing. For details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1071/38114). |


## Demonstration
The MLVB SDK provides new V2 APIs via `V2TXLivePusher` (publishing) and `V2TXLivePlayer` (playback) to power larger-scale live streaming scenarios with greater flexibility and lower latency. Hosts can use the capabilities provided by the APIs for RTC-based publishing. Audience, by default, play streams via CDNs, whose cost is relatively low. To compete, hosts only need to play each other’s stream. To enable RTC-based host competition, you must activate TRTC.
Below are the UI views of the MLVB-API-Example demo.

### UI demonstration

#### Before streaming
<table>
<tr> 
	<th><div align=center>Host A (Phone A)</div></th>
	<th><div align=center>Host B (Phone B)</div></th>
	<th><div align=center>Audience of Host A (Phone C)</div></th>
 </tr>
        <tr>
                <td>
                  <div align=center>
                    <img src="https://main.qcloudimg.com/raw/4bc948ab47ba1a5331f2f74331524d00.jpg" style="width: 250px;height: 510px">
                    </div>
                  </td>
                <td>
                  <div align=center>
                    <img src="https://main.qcloudimg.com/raw/e56ccd3afd789c8ea4f10b2992413205.jpg" style="width: 250px;height: 510px">
                    </div>
                </td>
                <td>
                  <div align=center>
                    <img src="https://main.qcloudimg.com/raw/5655b92e4407e5855a396493d6ce2495.jpg" style="width: 250px;height: 510px">
                    </div>
                </td>
        </tr></table>


#### Competing
<table>
<tr> 
	<th><div align=center>Host A (Phone A)</div></th>
	<th><div align=center>Host B (Phone B)</div></th>
	<th><div align=center>Audience of Host A (Phone C)</div></th>
</tr><tr>
<td>
	<div align=center><img src="https://main.qcloudimg.com/raw/a4b22306830a0cf7754df0668d0f7dfa.png"></div>
</td><td>
	<div align=center><img src="https://main.qcloudimg.com/raw/1c22fd4c4b7cbf8696050386ad3591ab.png"></div>
</td><td>
	<div align=center><img src="https://main.qcloudimg.com/raw/e85046243380bb1c505033c74e1f97a4.png"></div>
</td>
</tr></table>

## Implementation
As shown in the figure below, both host A and host B have their audience. To compete, they only need to do the following:
- Host A starts playing host B’s stream and initiates a stream mixing task to mix his or her stream with host B’s so that his or her audience can watch them compete.
- Host B starts playing host A’s stream and initiates a stream mixing task to mix his or her stream with host A’s so that his or her audience can watch them compete.
- Audience A and B can continue to play streams via CDNs and will see the competing videos of host A and host B after stream mixing.

<img src="https://main.qcloudimg.com/raw/638542d7e0bbb8fb3979ebfb00177f9d.png">

[](id:step1)
### 1. Host A starts publishing
Host A calls `V2TXLivePusher` to publish a stream. For how to splice a publishing URL, please see [Publish/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).
<dx-codeblock>
::: java java
V2TXLivePusher pusher = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
pushURLA= "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxx";
pusher.startPush(pushURLA);
:::
::: Objective-C ObjectiveC
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
NSString *pushURLA = @"trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxx";
[pusher startPush:pushURLA];
:::
</dx-codeblock>

[](id:step2)
### 2. Host B starts publishing
Host B calls `V2TXLivePusher` to publish a stream. For how to splice a publishing URL, please see [Publish/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).
<dx-codeblock>
::: java java
V2TXLivePusher pusher = new V2TXLivePusherImpl(this, V2TXLiveMode.TXLiveMode_RTC);
pushURLB "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=B&usersig=xxx";
pusher.startPush(pushURLB);
:::
::: Objective-C ObjectiveC
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
NSString *pushURLB = @"trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=B&;usersig=xxx";
[pusher startPush:pushURLB];
:::
</dx-codeblock>

[](id:step3)
### 3. Start competition 
Host A and host B call `V2TXLivePlayer` to play each other’s stream and start RTC-based competition. For how to splice a playback URL, please see [Publish/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).
<dx-codeblock>
::: java java
// Host A
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
playURLB = "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=B&usersig=xxx&appscene=live"
player.startPlay(playURLB);
...

// Host B
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
playURLA= "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxx&appscene=live"
player.startPlay(playURLA);
:::
::: Objective-C ObjectiveC
// Host A
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];
NSString *playURLB = "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=B&usersig=xxx&appscene=live"
[player setRenderView:view];
[player startPlay:playURLB];
...

// Host B
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];
 NSString *playURLA = "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxx&appscene=live"
[player setRenderView:view];
[player startPlay:playURLA];
:::
</dx-codeblock>

[](id:step4)
### 4. Audience watch the hosts compete
After host competition starts, audience can watch via one of two methods.
1. Host A’s audience calls `V2TXLivePlayer` to play host B’s stream, and host B’s audience calls `V2TXLivePlayer` to play host A’s stream.
2. Host A and host B mix their streams, and audience use the original URL to play the mixed stream.
Host A and host B each initiate a stream mixing task to mix their streams so that their audience can watch them complete. To achieve this, the hosts need to call `setMixTranscodingConfig` to start On-Cloud MixTranscoding, specifying audio-related parameters including `audioSampleRate`, `audioBitrate`, and `audioChannels`.

**Sample code**:
<dx-codeblock>
::: java java
// Host A 
V2TXLiveDef.V2TXLiveTranscodingConfig config = new V2TXLiveDef.V2TXLiveTranscodingConfig();

// Set the resolution to 720 × 1280 px, bitrate 1500 Kbps, and frame rate 20 fps
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
config.mixStreams      = new ArrayList<>();

// Position of the camera image of host A
V2TXLiveDef.V2TXLiveMixStream local = new V2TXLiveDef.V2TXLiveMixStream();
local.userId   = "localUserId";
local.streamId = null; // `streamID` is required for the remote user but not for the local user
local.x        = 0;
local.y        = 0;
local.width    = videoWidth;
local.height   = videoHeight;
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the host’s image is displayed at the bottom
config.mixStreams.add(local);

// Position of the camera image of host B
V2TXLiveDef.V2TXLiveMixStream remoteB = new V2TXLiveDef.V2TXLiveMixStream();
remoteB.userId   = "remoteUserIdB";
remoteB.streamId = "remoteStreamIdB"; // `streamID` is required for the remote user but not for the local user
remoteB.x        = 400; // For reference only
remoteB.y        = 800; // For reference only
remoteB.width    = 180; // For reference only
remoteB.height   = 240; // For reference only
remoteB.zOrder   = 1;
config.mixStreams.add(remoteB);

// Start On-Cloud MixTranscoding
pusher.setMixTranscodingConfig(config);

//Host B
V2TXLiveDef.V2TXLiveTranscodingConfig config = new V2TXLiveDef.V2TXLiveTranscodingConfig();

// Set the resolution to 720 × 1280 px, bitrate 1500 Kbps, and frame rate 20 fps
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;
config.mixStreams      = new ArrayList<>();

// Position of the camera image of host B
V2TXLiveDef.V2TXLiveMixStream local = new V2TXLiveDef.V2TXLiveMixStream();
local.userId   = "localUserId";
local.streamId = null; // `streamID` is required for the remote user but not for the local user
local.x        = 0;
local.y        = 0;
local.width    = videoWidth;
local.height   = videoHeight;
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the host’s image is displayed at the bottom
config.mixStreams.add(local);

// Position of the camera image of host A
V2TXLiveDef.V2TXLiveMixStream remoteA = new V2TXLiveDef.V2TXLiveMixStream();
remoteA.userId   = "remoteUserIdA";
remoteA.streamId = "remoteStreamIdA"; // `streamID` is required for the remote user but not for the local user
remoteA.x        = 400; // For reference only
remoteA.y        = 800; // For reference only
remoteA.width    = 180; // For reference only
remoteA.height   = 240; // For reference only
remoteA.zOrder   = 1;
config.mixStreams.add(remoteA);

// Start On-Cloud MixTranscoding
pusher.setMixTranscodingConfig(config);
:::
::: Objective-C ObjectiveC
// Host A 
V2TXLiveTranscodingConfig *config = [[V2TXLiveTranscodingConfig alloc] init];

// Set the resolution to 720 × 1280 px, bitrate 1500 Kbps, and frame rate 20 fps
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// Position of the camera image of host A
V2TXLiveMixStream *local = [[V2TXLiveMixStream alloc] init];
local.userId   = @"localUserId";
local.streamId = nil; // `streamID` is required for the remote user but not for the local user
local.x        = 0;
local.y        = 0;
local.width    = videoWidth;
local.height   = videoHeight;
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the host’s image is displayed at the bottom

// Position of the camera image of host B
V2TXLiveMixStream *remoteB = [[V2TXLiveMixStream alloc] init];
remoteB.userId   = @"remoteUserIdB";
remoteB.streamId = @"remoteStreamIdB"; // `streamID` is required for the remote user but not for the local user
remoteB.x        = 400; // For reference only
remoteB.y        = 800; // For reference only
remoteB.width    = 180; // For reference only
remoteB.height   = 240; // For reference only
remoteB.zOrder   = 1;

// Specify the streams to mix
config.mixStreams = @[local,remoteB];

// Start On-Cloud MixTranscoding
pusher.setMixTranscodingConfig(config);

//Host B
V2TXLiveTranscodingConfig *config = [[V2TXLiveTranscodingConfig alloc] init];

// Set the resolution to 720 × 1280 px, bitrate 1500 Kbps, and frame rate 20 fps
config.videoWidth      = 720;
config.videoHeight     = 1280;
config.videoBitrate    = 1500;
config.videoFramerate  = 20;
config.videoGOP        = 2;
config.audioSampleRate = 48000;
config.audioBitrate    = 64;
config.audioChannels   = 2;

// Position of the camera image of host A
V2TXLiveMixStream *local = [[V2TXLiveMixStream alloc] init];
local.userId   = @"localUserId";
local.streamId = nil; // `streamID` is required for the remote user but not for the local user
local.x        = 0;
local.y        = 0;
local.width    = videoWidth;
local.height   = videoHeight;
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the host’s image is displayed at the bottom

// Position of the camera image of host A
V2TXLiveMixStream *remoteA = [[V2TXLiveMixStream alloc] init];
remoteA.userId   = @"remoteUserIdA";
remoteA.streamId = @"remoteStreamIdA"; // `streamID` is required for the remote user but not for the local user
remoteA.x        = 400; // For reference only
remoteA.y        = 800; // For reference only
remoteA.width    = 180; // For reference only
remoteA.height   = 240; // For reference only
remoteA.zOrder   = 1;

// Specify the streams to mix
config.mixStreams = @[local,remoteA];

// Start On-Cloud MixTranscoding
pusher.setMixTranscodingConfig(config);
:::
</dx-codeblock>

>? Since you need to maintain room and user status by yourself, the new RTC-based scheme may seem more complicated than the old one. In fact, **there isn’t an always better scheme, only one that better suits your needs**.
- You can stick to the old scheme if your application scenarios do not require low latency or high concurrency.
- If you want to use V2 APIs without having to manage a room and users, try using [Tencent Cloud’s IM SDK](https://intl.cloud.tencent.com/document/product/1047) to implement the necessary logic.

[](id:price)
## Billing
For billing details, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1071/38114).

[](id:que)
## FAQs
[](id:que1)
#### 1. Why is publishing and playback using the same `streamid` on the same device possible with `TXLivePusher` and `TXLivePlayer` but not with `V2TXLivePusher` and `V2TXLivePlayer`?

`V2TXLivePusher` and `V2TXLivePlayer` are based on Tencent Cloud’s [TRTC](https://intl.cloud.tencent.com/document/product/647/39958) protocol. This is a UDP-based private protocol that features ultra-low latency and does not support **using the same `streamid` for ultra-low-latency publishing and playback on the same device**. We have determined that it’s not necessary to support this given the current use cases, but may consider optimizing the protocol in the future.

[](id:que2)
#### 2. What are the parameters mentioned in [**Activate TRTC**](#step1)?

`SDKAppID` identifies your application, and `UserID` your user. `UserSig` is a security signature calculated based on the two parameters using the **HMAC SHA256** encryption algorithm. Attackers cannot use your Tencent Cloud traffic without authorization as long as they cannot forge a `UserSig`. `UserSig` calculation involves hashing crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`, as shown below.

```Cpp
// UserSig formula, in which `secretkey` is the key used to calculate UserSig

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```

[](id:que3)
#### 3. How can I set audio or video quality using `V2TXLivePusher` and `V2TXLivePlayer`?
We provide APIs for the setting of audio and video quality. For details, please see [setAudioQuality()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a88956a3ad5e030af7b2f7f46899e5f13) and [setVideoQuality:resolutionMode:()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84).

[](id:que4)
#### 4. What does the error code `-5` mean?
The error code `-5` means failure to call an API due to invalid license. The enumerated value is [V2TXLIVE_ERROR_INVALID_LICENSE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html). For other error codes, please see [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html).

[](id:que5)
#### 5. What is the typical latency of RTC-based mic connect?
In the new RTC-based mic connect scheme, the mic connect latency is lower than 200 ms, and the latency for hosts and audience is 100-1,000 ms.

[](id:que6)
#### 6. What should I do if the `404` error occurs when I try to play streams via CDNs after successfully publishing streams over RTC?
Check if you have enabled TRTC’s relayed push feature. The feature is needed because, after publishing streams via RTC, to enable CDN playback, you need to relay the streams to CDNs.


