

## Overview

In **RTMP-based mic connect**, the MLVB SDK offers the `MLVBLiveRoom` component to help you quickly implement the mic connect feature. To better cater to your mic connect needs, Tencent Cloud has launched an RTC-based mic connect scheme and offered simpler and more flexible V2 APIs.

MLVB’s V2 APIs support publishing/mic connect via RTMP as well as RTC. You can choose whichever scheme fits your needs. Below is a comparison of the two schemes.

| Item   | RTMP                  | RTC                                           |
| -------- | -------------------------- | ------------------------------------------------------- |
| Protocol     | Based on TCP            | Based on UDP (more suitable for streaming)                 |
| QoS      | Poor adaptability to bad network connection              | Video streaming unaffected with 50% packets loss; audio mic connect unaffected with 70% packets loss |
| Region | Chinese mainland | Worldwide                                           |
| Tencent Cloud products used | MLVB, CSS | MLVB, CSS, TRTC             |
| Price     | 0.0028 USD/min               | Tiered pricing. For details, please see [Billing](#price).  |


## Demonstration

The MLVB SDK provides new V2 APIs via `V2TXLivePusher` (publishing) and `V2TXLivePlayer` (playback) to power larger-scale live streaming scenarios with greater flexibility and lower latency. Hosts can use capabilities provided by the APIs to publish streams via RTC. Audience, by default, play streams via CDNs, whose cost is relatively low. To connect mic with hosts, audience can switch to RTC-based playback, which has lower latency and guarantees better interactive experience. To enable RTC-based mic connect, you must activate TRTC. For detailed directions, please see **Enable mic connect and host competition**.
Below are the UI views of the [MLVB-API-Example](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) demo.

### UI demonstration

#### Before streaming

<table>
        <tr> 
                <th><div align=center>Host (Phone A)</div></th>
                <th><div align=center>Mic-connecting audience (Phone B)</div></th>
                <th><div align=center>Audience (Phone C)</div></th>
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
        </tr>
</table>



#### Mic connecting

<table>
        <tr> 
                <th><div align=center>Host (Phone A)</div></th>
                <th><div align=center>Mic-connecting audience (Phone B)</div></th>
                <th><div align=center>Audience (Phone C)</div></th>
        </tr>
        <tr>
                <td>
                  <div align=center>
                    <img src="https://main.qcloudimg.com/raw/12ab1388f6a7b398229e9734f2b39647.jpg" style="width: 250px;height: 510px">
                    </div>
                  </td>
                <td>
                  <div align=center>
                     <img src="https://main.qcloudimg.com/raw/6bcb8e3682404832ed8ac22242793301.jpg" style="width: 250px;height: 510px">
                    </div>
                </td>
                <td>
                  <div align=center>
                    <img src="https://main.qcloudimg.com/raw/079652c3b1bbcda92879882c0bcdc77c.jpg" style="width: 250px;height: 510px"> 
                    </div>
                </td>
        </tr>
</table>



## Implementation

As shown in the figure below, user A is the host, while user B and C are the audience. For user B to connect mic with user A, follow these steps:

- User B: Start publishing using the `trtc://` protocol and switch from CDN playback to the ultra-low-latency `trtc://` protocol.
- User A: Start playing user B’s stream and initiate a stream mixing task to mix his or her stream with user B’s.
- User C can continue to play streams via a CDN and will see the mic connecting images of user A and B after stream mixing.
  <img src="https://main.qcloudimg.com/raw/adf54d7d08abe642d948aa6fe8517bb3.png">

[](id:step_live1)
### 1. Publish streams via RTC (host)
User A calls `V2TXLivePusher` to publish streams. For how to splice a publishing URL, please see [Publish/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).
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

[](id:step_live2)
### 2. Play streams via CDNs (audience)
All audience call `V2TXLivePlayer` to play user A’s stream. For how to splice a playback URL, please see [Publish/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).
<dx-codeblock>
::: java java
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
/**

 * Streams are played via CDNs in the example. The protocols supported include FLV, HLS, and WebRTC. Standard protocols such as FLV and HLS are more cost-effective, but WebRTC delivers interactive experience with lower latency.
 * playURLA= "http://3891.liveplay.myqcloud.com/live/streamidA.flv";
 * playURLA= "http://3891.liveplay.myqcloud.com/live/streamidA.hls";
 * playURLA= "webrtc://3891.liveplay.myqcloud.com/live/streamidA"
   */
   player.startPlay(playURLA);
   :::
   ::: Objective-C ObjectiveC
   V2TXLivePlayer * player = [[V2TXLivePlayer alloc] init];
   /**
 * Streams are played via CDNs in the example. The protocols supported include FLV, HLS, and WebRTC. Standard protocols such as FLV and HLS are more cost-effective, but WebRTC delivers interactive experience with lower latency.
 * NSString *playURLA= @"http://3891.liveplay.myqcloud.com/live/streamidA.flv";
 * NSString *playURLA= @"http://3891.liveplay.myqcloud.com/live/streamidA.hls";
 * NSString *playURLA= @"webrtc://3891.liveplay.myqcloud.com/live/streamidA"
   */
   [player setRenderView:view];
   [player startPlay:playURLA];
   :::
   </dx-codeblock>

[](id:step_live3)

### 3. Initiate mic connect (audience)

User B (the mic-connecting user B) calls `V2TXLivePusher` to publish streams.
<dx-codeblock>
::: java java
V2TXLivePusher pusher = new V2TXLivePusherImpl(this,V2TXLiveMode.TXLiveMode_RTC);
pushURLB= "trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=B&usersig=xxx";
pusher.startPush(pushURLB);
:::
::: Objective-C ObjectiveC
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTC];
NSString *pushURLB = @"trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=B&usersig=xxx";
[pusher startPush:pushURLB];
:::
</dx-codeblock>

[](id:step_live4)

### 4. Start mic connect

User A calls `V2TXLivePlayer` to play the stream of **the mic-connecting user B** via RTC.
<dx-codeblock>
::: java java
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
playURLB= "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=B&usersig=xxx&appscene=live";
player.startPlay(playURLB);
:::
::: Objective-C ObjectiveC
V2TXLivePlayer * player = [[V2TXLivePlayer alloc] init];
NSString* playURLB = @"trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=B&usersig=xxx&appscene=live";
[player setRenderView:view];
[player startPlay:playURLB];
:::
</dx-codeblock>

**The mic-connecting user B** calls `V2TXLivePlayer` to switch to RTC and play user A’s stream.
<dx-codeblock>
::: java java
V2TXLivePlayer player = new V2TXLivePlayerImpl(mContext);
playURLA= "trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxx&appscene=live";
player.startPlay(playURLA);
:::
::: Objective-C ObjectiveC
V2TXLivePlayer * player = [[V2TXLivePlayer alloc] init];
NSString* playURLA = @"trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxx&appscene=live";
[player setRenderView:view];
[player startPlay:playURLA];
:::
</dx-codeblock>

User A and the **mic-connecting user B** start ultra-low-latency interaction.


[](id:step_live5)

### 5. Mix streams

To make sure that other audience can see the host and the mic-connecting user interact with each other, user A needs to initiate a stream mixing task to mix his or her stream and user B’s into one stream. Specifically, user A needs to call the `setMixTranscodingConfig` API to start On-Cloud MixTranscoding, specifying audio-related parameters including `audioSampleRate`, `audioBitrate`, and `audioChannels`.
If your application involves the transfer of video data, you must also set video-related parameters such as `videoWidth`, `videoHeight`, `videoBitrate`, and `videoFramerate`.

**Sample code**:
<dx-codeblock>
::: java java
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

// Image position of the mic-connecting user
V2TXLiveDef.V2TXLiveMixStream remoteA = new V2TXLiveDef.V2TXLiveMixStream();
remoteA.userId   = "remoteUserIdA";
remoteA.streamId = "remoteStreamIdA"; // `streamID` is required for the remote user but not for the local user
remoteA.x        = 400; // For reference only
remoteA.y        = 800; // For reference only
remoteA.width    = 180; // For reference only
remoteA.height   = 240; // For reference only
remoteA.zOrder   = 1;
config.mixStreams.add(remoteA);

// Image position of the mic-connecting user
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
:::
::: Objective-C ObjectiveC
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

// Position of the camera image of the host
V2TXLiveMixStream *local = [[V2TXLiveMixStream alloc] init];
local.userId   = @"localUserId";
local.streamId = nil; // `streamID` is required for the remote user but not for the local user
local.x        = 0;
local.y        = 0;
local.width    = videoWidth;
local.height   = videoHeight;
local.zOrder = 0;   // When `zOrder` is set to `0`, it indicates that the host’s image is displayed at the bottom

// Image position of the mic-connecting user
V2TXLiveMixStream *remoteA = [[V2TXLiveMixStream alloc] init];
remoteA.userId   = @"remoteUserIdA";
remoteA.streamId = @"remoteStreamIdA"; // `streamID` is required for the remote user but not for the local user
remoteA.x        = 400; // For reference only
remoteA.y        = 800; // For reference only
remoteA.width    = 180; // For reference only
remoteA.height   = 240; // For reference only
remoteA.zOrder   = 1;

// Image position of the mic-connecting user
V2TXLiveMixStream *remoteB = [[V2TXLiveMixStream alloc] init];
remoteB.userId   = @"remoteUserIdB";
remoteB.streamId = @"remoteStreamIdB"; // `streamID` is required for the remote user but not for the local user
remoteB.x        = 400; // For reference only
remoteB.y        = 800; // For reference only
remoteB.width    = 180; // For reference only
remoteB.height   = 240; // For reference only
remoteB.zOrder   = 1;

// Specify the streams to mix
config.mixStreams = @[local,remoteA,remoteB];

// Start On-Cloud MixTranscoding
pusher.setMixTranscodingConfig(config);
:::
</dx-codeblock>

>! In On-Cloud MixTranscoding, the default ID for the post-mixing stream is the stream ID of the user who initiates the stream mixing task. To specify an ID for the post-mixing stream, pass in the ID when calling the API.

After the above steps are performed, other audience will be able to see user A and B interact with each other.
    

[](id:price)
## Billing
Your usage of the RTC-based mic connect feature is calculated based on the total played [video duration](#v_duration) and [audio duration](#s_duration) of mic-connecting users.

>! A duration is calculated in seconds and monthly cumulative seconds are converted to minutes for billing. A duration of less than one minute is calculated as one minute.

[](id:v_duration)

### Video duration

Video duration is the cumulative time when audience play mic-connecting users’ videos. A video duration is categorized according to the **actual resolution of video received**. Video durations of different categories are charged differently.

**The table below shows how video durations are categorized by resolution.**

| Category | Resolution of Received Video               |
| -------- | ---------------------------- |
| SD  | ≤ 640 × 480        |
| HD  |640 × 480 - 1280 × 720|
| FHD | > 1280 × 720               |

- If a user plays video, you will only pay for the video duration, regardless of whether the video contains audio.
- If a user plays multiple video streams, TRTC will add up the video duration of each stream.


[](id:s_duration)

### Audio duration

Audio duration is the cumulative time when audience play mic-connecting users’ audio.

- Audio duration is billed only if a user does not play video.
- If a user plays the audio of multiple mic-connecting users, the overlapping segments will be billed only once.

[](id:Fixed_price)

### Pricing

The RTC-based mic connect feature is priced as follows.

|Billable Item|Unit Price (USD/1,000 Min)|
| -------- | ------------------- |
| Audio     | 0.99                |
| SD  | 1.99                |
| HD  | 3.99                |
| FHD | 14.99               |

[](id:Billing_method)

### Billing Mode

RTC-based mic connect supports two billing modes: **prepaid packages** (default) and **pay-as-you-go**. You will be switched to the pay-as-you-go mode automatically after your prepaid package is exhausted or expires. You cannot switch to the pay-as-you-go mode by yourself.

[](id:pre-payment)

#### Prepaid packages

You can purchase general packages for RTC-based mic connect, from which audio, SD video, HD video, and FHD video durations are deducted in the proportion of *1:1, 2:1, 4:1, and 15:1** respectively. For example, for 1 minute of HD video duration used, 4 minutes are deducted from a general package.
Below are the prices of general packages.

<table>
     <tr>
         <th style="text-align:center">Package Type</th>  
         <th style="text-align:center">Package Duration (1,000 Min)</th> 
         <th style="text-align:center">List Unit Price (USD/1,000 Min)</th> 
         <th style="text-align:center">Package Unit Price (USD/1,000 Min)</th> 
         <th style="text-align:center">Package Price (USD)</th> 
          <th style="text-align:center">Package Price/List Price</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">Fixed-time package</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center"><96%</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center"><91%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center"><85%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center">80%</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">Custom package</td>   
         <td style="text-align:center">0 ＜ X ＜ 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">Package unit price × Package duration (X)</td>   
         <td style="text-align:center">100%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ X ＜ 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center"><96%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ X ＜ 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center"><91%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ X ＜ 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center"><85%</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">X ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">80%</td>   
     </tr> 
</table>



>? The package unit prices in the table are rounded up to 3 decimal places. However, in actual billing, unit prices are rounded off to 8 decimal places.

About general packages:

- A general package is valid from the day of purchase to the last day of the same month next year.
  For example, if you purchased a package on May 1, 2020, it would be valid from May 1, 2020 to May 31, 2021.
- You can purchase multiple packages. Durations are deducted in real time from the package that expires the fastest.
- A new package takes effect in about 5 minutes after payment. **If your account has a duration that is generated after 00:00 of the day of purchase and hasn’t been deducted, it will be deducted immediately from the newly purchased package.**
- To avoid interrupting your businesses, **TRTC will not suspend services for your account when your package is exhausted or expires**. The minutes not deducted from any package will be billed under the [pay-as-you-go](#post-payment) mode.
- Once a general package expires, the remaining minutes in the package will become invalid and cannot be retrieved.

[](id:post-payment)
#### Pay-as-you-go
If you overuse your package, the duration not deducted will be billed at [pay-as-you-go rates](#Fixed_price).
You can choose to pay [daily](#daily) or [monthly](#monthly).

- **Daily pay-as-you-go:**[](id:daily)
For accounts that create their first [application](https://intl.cloud.tencent.com/document/product/647/37714) in the TRTC console on or after September 1, 2020, **daily** pay-as-you-go applies by default. Fees for a day are deducted at 10:00 AM the next day.

- **Monthly pay-as-you-go:**[](id:monthly)
For accounts that created their first [application](https://intl.cloud.tencent.com/document/product/647/37714) in the TRTC console on or before August 31, 2020, **monthly** pay-as-you-go applies by default. Fees for a month are deducted within the first five days of the next month. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555/7432).

>!
>- You will be switched to the pay-as-you-go mode automatically after your prepaid package is exhausted or expires. You cannot switch to the mode by yourself.
>- You cannot change the billing cycle by yourself. If you wish to change the billing cycle from monthly to daily, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- If your account balance is insufficient for the deduction of the incurred fees, the overdue payment may cause other Tencent Cloud services to be suspended for your account too. For example, because on-cloud recording relies on **CSS** and **VOD**, your on-cloud recording task may fail due to the overdue payment.

[](id:Billing_examples)
### Billing examples
>! The examples below use list prices. You can [purchase a package](https://buy.cloud.tencent.com/trtc) to reduce your expenses.

#### Audio-only scenario

Assume that user A, B, and C used the RTC-based mic connect feature to interact with each other for 30 minutes, during which none of them received video.
The **total cost** would be `Unit price of audio duration × The sum of all three users’ audio durations = 0.99 USD/1,000 min × (30 min + 30 min + 30 min) ÷ 1,000 = 0.0891 USD`.

#### Video-only scenario

Assume that user A and B used the RTC-based mic connect feature to interact with each other for 45 minutes, during which they played each other’s video at the following resolutions.

<table>
     <tr>
         <th style="text-align:center">Segment</th>  
         <th style="text-align:center"> Resolution of Video A Received</th> 
         <th style="text-align:center"> Resolution of Video B Received</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="1">First 30 min</td>   
         <td style="text-align:center">1280 × 720 (HD)</td>
         <td style="text-align:center">1920 × 1080 (FHD)</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="1">Last 15 min</td>   
         <td style="text-align:center">640 × 360 (SD)</td> 
         <td style="text-align:center">640 × 360 (SD)</td>
     </tr> 
</table>


**Analysis:**

- A’s duration and expense
  - A received HD video from B in the first 30 minutes and SD video in the last 15 minutes.
  - A’s expense would be `Unit price of HD video × The duration of HD video A received + Unit price of SD video × The duration of SD video A received = 3.99 USD/1,000 min × (30 min ÷ 1,000) + 1.99 USD/1,000 min × (15 min ÷ 1,000) = 0.14955 USD`.
- B’s duration and expense
  - B received FHD video from A in the first 30 minutes and SD video in the last 15 minutes.
  - B’s expense would be `Unit price of FHD video × The duration of FHD video B received + Unit price of SD video × The duration of SD video B received = 14.99 USD/1,000 min × (30 min ÷ 1,000) + 1.99 USD/1,000 min × (15 min ÷ 1,000) = 0.47955 USD`.

The **total cost** would be `A’s expense + B’s expense = 0.6291 USD`.

#### Audio-video scenario

Assume that user A and B used the RTC-based mic connect feature to interact with each other for 45 minutes. A played B’s video throughout the process, and B played A’s video in the first 30 minutes and audio only in the last 15 minutes. The resolutions of the videos played are as follows:

<table>
     <tr>
         <th style="text-align:center">Segment</th>  
         <th style="text-align:center">Resolution of Video A Received</th> 
         <th style="text-align:center">Resolution of Video B Received</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="1">First 30 min</td>   
         <td style="text-align:center">1280 × 720 (HD)</td>
         <td style="text-align:center">1920 × 1080 (FHD)</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="1">Last 15 min</td>   
         <td style="text-align:center">640 × 360 (SD)</td> 
         <td style="text-align:center">Audio only</td>
     </tr> 
</table>


**Analysis:**

- A’s duration and expense
  - A received HD video from B in the first 30 minutes and SD video in the last 15 minutes.
  - A’s expense would be `Unit price of HD video × The duration of HD video A received + Unit price of SD video × The duration of SD video A received = 3.99 USD/1,000 min × (30 min ÷ 1,000) + 1.99 USD/1,000 min × (15 min ÷ 1,000) = 0.14955 USD`.
- B’s duration and expense
  - B received FHD video from A in the first 30 minutes and did not receive video in the last 15 minutes.
  - B’s expense would be `Unit price of FHD video × The duration of FHD video B received + Unit price of audio × The audio duration B received = 14.99 USD/1.000 min × (30 min ÷ 1,000) + 0.99 USD/1,000 min × (15 min ÷ 1,000) = 0.46455 USD`.

The **total cost** would be `A’s expense + B’s expense = 0.6141 USD`.

[](id:que)
## FAQs
[](id:que1)
#### 1. Why is publishing and playback using the same `streamid` on the same device possible with `TXLivePusher` and `TXLivePlayer` but not with `V2TXLivePusher` and `V2TXLivePlayer`?

`V2TXLivePusher` and `V2TXLivePlayer` are based on Tencent Cloud’s [TRTC](https://intl.cloud.tencent.com/document/product/647/39958) protocol. This is a UDP-based private protocol that features ultra-low latency and does not support **using the same `streamid` for ultra-low-latency publishing and playback on the same device**. We have determined that it’s not necessary to support this given the current use cases, but may consider optimizing the protocol in the future.

[](id:que2)
#### 2. What are the parameters mentioned in [**Activate TRTC**](#step1) above?

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

