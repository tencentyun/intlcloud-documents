This document describes how to use the MLVB SDK to implement live streaming.

## Sample Code
Regarding frequently asked questions among developers, Tencent Cloud offers an easy-to-understand API example project, which you can use to quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## Prerequisites
1. To ensure a better user experience, we recommend you activate [CSS](https://intl.cloud.tencent.com/product/css). If you don't need to use CSS, skip this step.
2. Download and install Xcode from App Store.
3. Download and install CocoaPods as instructed at the [CocoaPods website](https://cocoapods.org/).


## This Document Describes
* How to integrate the Player SDK for iOS.
* How to use the Player SDK for live playback.
* How to use the underlying capabilities of the Player SDK to implement more live streaming features.

## SDK Integration
### Step 1. Download the SDK ZIP file
Download the SDK ZIP file and integrate the SDK into your application as instructed in the SDK integration document.


### Step 2. Create a player object
The TXLivePlayer module in the Tencent Video Cloud SDK implements the livestream playback feature.
```objectivec
TXLivePlayer _txLivePlayer = [[TXLivePlayer alloc] init];
```

### Step 3. Create a rendering view
In iOS, a view is used as the basic UI rendering unit. Therefore, you need to configure a view, whose size and position you can adjust, for the player to display video images on.

```objectivec
// Use `setupVideoWidget` to bind the view determining the rendering area to the player. The first parameter `frame` has been disused since v1.5.2.
[_txLivePlayer setupVideoWidget:CGRectMake(0, 0, 0, 0) containView:_myView insertIndex:0];
```

Technically, the player does not render video images directly on the view (`_myView` in the sample code) you provide. Instead, it creates a subview for OpenGL rendering over the view.

You can adjust the size of video images by changing the size and position of the view. The SDK will make changes to the video images accordingly.

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)
 <dx-alert infotype="explain" title="How to make an animation?">
You are allowed great flexibility in view animation, but note that you need to modify the `transform` rather than `frame` attribute of the view.

```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // Shrink by 1/3
        }];
```
</dx-alert>

### Step 4. Start playback
```objectivec
NSString* flvUrl = @"http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
[_txLivePlayer startPlay:flvUrl type:PLAY_TYPE_LIVE_FLV];
```

| Option | Enumerated Value | Description |
|---------|---------|---------|
| PLAY_TYPE_LIVE_RTMP | 0 | The URL passed in is an RTMP live streaming URL |
| PLAY_TYPE_LIVE_FLV | 1 | The URL passed in is an FLV live streaming URL |
| PLAY_TYPE_LIVE_RTMP_ACC | 5 | The low-latency linkage URL (applicable to only mic connect scenarios) |
| PLAY_TYPE_VOD_HLS | 3 | The URL passed in is an HLS (M3U8) playback URL|


<dx-alert infotype="explain" title="About HLS (M3U8)">
We recommend you not use the HLS protocol to play back live streaming video sources in your app because the latency is too high (though HLS protocol is suitable for VOD). Instead, we recommend using LIVE_FLV and LIVE_RTMP playback protocols.
</dx-alert>

### Step 5. Stop playback
Remember to use **removeVideoWidget** to terminate the view control before exiting the current UI when stopping playback. This can prevent memory leak and screen flashing issues.

```objectivec
// Stop playback
[_txLivePlayer stopPlay];
[_txLivePlayer removeVideoWidget]; // Remember to terminate the view control
```

## How to Use
This document describes how to use common live streaming features.


### 1. Image adjustment
- **view: size and position**
You can modify the size and position of the view by adjusting the size and position of the parameter `view` of setupVideoWidget. The SDK will automatically adjust the size and position of the view based on your configuration.

- **setRenderMode: Aspect fill or aspect fit**
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>Images are scaled to fill the entire screen, and the excess parts are cropped. There are no black bars in this mode, but images may not be displayed in whole.</td>
</tr>
<tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>Images are scaled as large as the longer side can go. Neither side exceeds the screen after scaling. Images are centered, and there may be black bars.</td>
</tr>
</tbody></table>
- **setRenderRotation: Image rotation**
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_ROTATION_PORTRAIT</td>
<td>Normal playback (the Home button is below the video image)</td>
</tr>
<tr>
<td>RENDER_ROTATION_LANDSCAPE</td>
<td>Clockwise rotation of the image by 270 degrees (the Home button is on the left of the video image)</td>
</tr>
</tbody></table>



### 2. Playback pause
Technically speaking, live playback cannot be paused. In this document, pausing the playback means **freezing the video image** and **disabling audio**, while the video source continues to be streamed in the cloud. When you call `resume`, the playback will start from the time of resumption. This is different from VOD, where when you pause or resume the playback, the player will behave the same way as it does when you pause or resume a local video file.

```objectivec
// Pause playback
[_txLivePlayer pause];
// Resume playback
[_txLivePlayer resume];
```

### 3. Message reception
This feature is used to deliver certain custom messages from the publisher to the audience through the audio/video lines. It is applicable to the following scenarios:
(1) Online quiz: The publisher delivers <strong>questions</strong> to the viewers with perfectly synced audio, image, and questions.
(2) Live show: The publisher delivers <strong>lyrics</strong> to the viewers. The lyrics can be displayed in real time in the player without being affected by video encoding quality degradation.
(3) Online education: The publisher delivers <strong>laser pointer</strong> and <strong>doodle</strong> operations to the viewers to circle and underline content in the player in real time.

You can use this feature as follows:
- Set **enableMessage** in `TXLivePlayConfig` to **YES**.
- Make `TXLivePlayer` use **TXLivePlayListener** to listen for the message **PLAY_EVT_GET_MESSAGE (2012)**.

```objectiveC
 -(void) onPlayEvent:(int)EvtID withParam:(NSDictionary *)param {
    [self asyncRun:^{
        if (EvtID == PLAY_EVT_GET_MESSAGE) {
            dispatch_async(dispatch_get_main_queue(), ^{
                if ([_delegate respondsToSelector:@selector(onPlayerMessage:)]) {
                    [_delegate onPlayerMessage:param[@"EVT_GET_MSG"]];
                }
            });
        }
    }];
}
```

### 4. Screencapturing
You can capture the current image as a frame by calling **snapshot**. This feature can only capture frames from the current live streaming video. To capture the entire UI, you must call the API of the iOS system.



### 5. Live stream recording
Live stream recording is an extended feature in the live streaming scenario: When audience members are watching a live stream, they can click the "Record" button to record a live stream segment and publish it through a video distribution platform such as Tencent Cloud VOD. This allows them to distribute the video as a UGC message on social media platforms like WeChat Moments.



```objectivec
// The following sample code is used to show the recording feature in live streaming scenarios
//
// Specify a `TXVideoRecordListener` to sync the recording progress and result
_txLivePlayer.recordDelegate = recordListener;
// Start recording. This API can be placed in the response function of the "Record" button. Currently, only the video source can be recorded, while other data such as on-screen comments cannot.
[_txLivePlayer startRecord: RECORD_TYPE_STREAM_SOURCE]; 
// ...
// ...
// Stop recording. This API can be placed in the response function of the "Stop" button.
[_txLivePlayer stopRecord];                             
```
- The recording progress is measured by time and will be notified of through the `onRecordProgress` of `TXVideoRecordListener`.
- A recorded file will be notified of as an MP4 file through the `onRecordComplete` of `TXVideoRecordListener`.
- `TXUGCPublish` is used to implement video upload and publishing. For detailed directions, see [iOS](https://intl.cloud.tencent.com/document/product/1069/38016).


### 6. Seamless definition switch
During daily use, network conditions change constantly. When the network conditions are poor, switching to a lower image quality can reduce lag, and the higher quality video can be switched back when network conditions improve.
Traditionally, playback is interrupted when a stream is switched, which can cause problems such as video image discontinuity, black screen, and lag. With the seamless switch solution, you can switch to another stream without interrupting the live streaming.

The definition switch API can be called at any time after live streaming starts.
```objectivec
// The stream `http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e.flv` is being played back
// Switch to a new stream with a bitrate of 900 Kbps
[_txLivePlayer switchStream:@"http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e_900.flv"];
```

>?You need to configure PTS alignment on the backend to use the seamless definition switch feature. To do this, [submit a ticket](https://console.cloud.tencent.com/workorder).

### 7. Live stream replay
The time shifting feature allows you to return to any previous time point during a live stream and resume playback from that time point. It is highly suitable for scenarios in which there is no need for interaction but viewers may want to rewind and replay a video, such as sports and gaming events.

```objectivec
// Call `startPlay` first before setting time shifting
// Start playback
[TXLiveBase setAppID:@"1253131631"]; // Configure `appId`
[_txLivePlayer prepareLiveSeek];     // The backend requests the live streaming start time
```
After correct configuration, the current progress will not start from 0 in the `LAY_EVT_PLAY_PROGRESS` event, but will be calculated based on the actual playback start time.
Call the `seek` method to start live streaming again from a previous time point
```objectivec
[_txLivePlayer seek:600]; // Start playback from the 10th minute
```

Configure the following settings on the backend to connect to time shifting:

1. Recording: Configure the time shifting duration and time shifting storage period.
2. Playback: Enable metadata acquisition in time shifting.

>? The time shifting feature is currently in beta test. If you need to use it, [submit a ticket](https://console.cloud.tencent.com/workorder) for application.

### 8. Latency adjustment
The live playback feature of the SDK is not based on FFmpeg, but Tencent Cloud's proprietary playback engine, which is why the SDK offers better latency control than open-source players do. We provide three latency control modes, which can be used for showrooms, game streaming, and hybrid scenarios.

- **Comparison of control modes**
<table>
<thead>
<tr>
<th>Control Mode</th>
<th>Lag Rate</th>
<th>Average Latency</th>
<th>Application Scenarios</th>
<th>How It Works</th>
</tr>
</thead>
<tbody><tr>
<td>Expedited</td>
<td>More likely than the expedited mode</td>
<td>2-3s</td>
<td>Live showroom (online quiz)</td>
<td>The mode delivers low latency and is suitable for latency-sensitive scenarios.</td>
</tr>
<tr>
<td>Smooth</td>
<td>Least likely of the three</td>
<td>&gt;= 5s</td>
<td>Game streaming (Penguin Esports)</td>
<td>It is suitable for game live streaming scenarios with a high bitrate, such as battle royale games.</td>
</tr>
<tr>
<td>Auto</td>
<td>Self-adaptive to network conditions</td>
<td>2-8s</td>
<td>Hybrid</td>
<td>The better network conditions at the audience end, the lower the latency.</td>
</tr>
</tbody></table>

- **Code to integrate the three modes**
```objectivec
TXLivePlayConfig*  _config = [[TXLivePlayConfig alloc] init];
// Auto mode
_config.bAutoAdjustCacheTime   = YES;
_config.minAutoAdjustCacheTime = 1; 
_config.maxAutoAdjustCacheTime = 5;
// Expedited mode
_config.bAutoAdjustCacheTime   = YES;
_config.minAutoAdjustCacheTime = 1;
_config.maxAutoAdjustCacheTime = 1;
// Smooth mode
_config.bAutoAdjustCacheTime   = NO;
_config.cacheTime              = 5;

[_txLivePlayer setConfig:_config];

// Start the playback after configuration
```

>? For more information on stuttering and latency control, see [Video Stutter](https://intl.cloud.tencent.com/document/product/1071/39362).

### 9. Ultra low-latency playback
The live player supports live playback at a latency of about <strong>400 ms</strong>. It can be used in scenarios with very strict requirements for latency, such as <strong>remote claw machine</strong> and <strong>mic connect</strong>. You need to know the following information about this feature:

- **Enabling this feature is not required**
This feature doesn't need to be enabled in advance, but the live stream must be in Tencent Cloud, because there are technical and other difficulties in implementing an ultra low-latency linkage across cloud service providers.

- **The playback URL must be configured with hotlink protection**
The playback URL cannot be a general CDN URL and must carry a hotlink protection signature. For more information on how to calculate a signature, see [Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).

- **ACC must be specified as the playback type**
When calling the `startPlay` playback function, you need to set `type` to **PLAY_TYPE_LIVE_RTMP_ACC**, and the SDK will use the RTMP-UDP protocol to directly pull the live stream.

- **It has a limit on the number of streams played back concurrently**
Currently, a maximum of ten streams can be played back concurrently. Because the cost of low-latency lines is much greater than CDN lines, we encourage users to use this feature only in scenarios that actually require high interaction rather than using it for scenarios which do not require extremely low latency.

- **The latency of OBS doesn't meet the requirements**
If [TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/38157) is used, call [setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38157) to set `quality` to `MAIN_PUBLISHER` or `VIDEO_CHAT`. It's difficult to achieve low latency with OBS because data tends to build up at the streaming end.

- **It is billed by playback duration**
This feature is billed by playback duration, and the fees are subject to the number of pulled streams, but not the audio/video stream bitrate. For pricing details, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/1071/38114).

### 10. Video information acquisition
The Player SDK plays back a video through a URL string. The URL doesn't contain the video information, and you need to access the cloud server to load such information. Therefore, the SDK can only send the video information to your application as event notifications. For more information, see [Event Listening](#monitor).

For example, you can use the `NET_STATUS_VIDEO_WIDTH` and `NET_STATUS_VIDEO_HEIGHT` of `onNetStatus` to get the video width and height. For detailed directions, see [Status feedback (onNetStatus)](#onNetStatus).

[](id:monitor)
## Event Listening
You can bind a `TXLivePlayListener` to the `TXLivePlayer` object. Then, all internal SDK status messages will be notified to you through `onPlayEvent` ([event notification](#onPlayEvent)) and `onNetStatus` ([status callback](#onNetStatus)) messages.

[](id:onPlayEvent)
### Event notification (onPlayEvent)
#### 1. Playback events
| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CONNECT_SUCC     |  2001    | The server was connected.                |
| PLAY_EVT_RTMP_STREAM_BEGIN|  2002    | The server was connected and stream pull started (this is thrown only for an RTMP URL). |
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | The network received the first renderable video data packet (IDR).  |
|PLAY_EVT_PLAY_BEGIN    |  2004|  Video playback started, and the loading icon animation (if any) ends. |
|PLAY_EVT_PLAY_LOADING|  2007|  The video is being loaded. The `BEGIN` event will be reported if video playback resumes. |
|PLAY_EVT_GET_MESSAGE|  2012|  It is used to receive a message in an audio/video stream. For more information, see [Message reception](#Message). |

- **Don't hide the playback image after receiving `PLAY_LOADING`**
Because the length of time between `PLAY_LOADING` and `PLAY_BEGIN` is uncertain (it may be five seconds or five milliseconds), some customers hide the playback image upon `LOADING` and display the image upon `BEGIN`, which will cause serious image flashing (especially in live streaming). We recommend you place a translucent loading animation on top of the video playback image.

#### 2. Stop events
| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_END      |  2006|  Video playback ended.      |
|PLAY_ERR_NET_DISCONNECT |  -2301  | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |

- **How do I determine whether live streaming is over?**
Due to the varying implementation principles of different standards, no end events (error code 2006) are returned for many live streams. Instead, when a host pushing a stream, the SDK will soon find that data stream pull fails (`WARNING_RECONNECT`) and attempt to retry until the `PLAY_ERR_NET_DISCONNECT` event is thrown after three failed attempts.

 Therefore, both error codes 2006 and -2301 need to be listened for and used to determine the end of live streaming.


#### 3. Warning events
You can ignore the following events, which are provided only based on the white box SDK design philosophy to sync the event information.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | Failed to decode the current video frame.  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | Failed to decode the current audio frame.  |
| PLAY_WARNING_RECONNECT           |  2103  | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| PLAY_WARNING_RECV_DATA_LAG       |  2104  | Unstable transfer of packets from the network. This may be caused by insufficient downstream bandwidth or uneven outbound stream from the host. |
| PLAY_WARNING_VIDEO_PLAY_LAG      |  2105  | Video playback encountered lag.|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | Failed to start the hardware decoder, and the software decoder was used instead.   |
| PLAY_WARNING_VIDEO_DISCONTINUITY |  2107  | Current video frames are discontinuous. Certain frames may be dropped. |
| PLAY_WARNING_DNS_FAIL            |  3001  | RTMP-DNS failed (thrown only for RTMP playback URLs). |
| PLAY_WARNING_SEVER_CONN_FAIL     |  3002  | RTMP server connection failed (thrown only for RTMP playback URLs). |
| PLAY_WARNING_SHAKE_FAIL          |  3003  | RTMP server handshake failed (thrown only for RTMP playback URLs). |

[](id:onNetStatus)
### Status feedback (onNetStatus)
The notification is triggered once every second to provide real-time feedback on the current status of the pusher. It can act as a dashboard to inform you of what is happening inside the SDK so you can better understand the current network conditions and video information.

|   Parameter                   |  Description                   |
| :------------------------  |  :------------------------ |
| NET_STATUS_CPU_USAGE     | Current instantaneous CPU utilization |
| NET_STATUS_VIDEO_WIDTH | Video resolution - width |
| NET_STATUS_VIDEO_HEIGHT| Video resolution - height |
|	NET_STATUS_NET_SPEED     | Current network data reception speed |
|	NET_STATUS_NET_JITTER    | Network jitter. The greater the jitter, the more unstable the network |
|	NET_STATUS_VIDEO_FPS     | Current video frame rate of streaming media    |
|	NET_STATUS_VIDEO_BITRATE | Current video bitrate in Kbps of streaming media |
|	NET_STATUS_AUDIO_BITRATE | Current audio bitrate in Kbps of streaming media |
|NET_STATUS_CACHE_SIZE    | Buffer (`jitterbuffer`) size. If the current buffer length is 0, lag will occur soon |
| NET_STATUS_SERVER_IP | Connected server IP |


