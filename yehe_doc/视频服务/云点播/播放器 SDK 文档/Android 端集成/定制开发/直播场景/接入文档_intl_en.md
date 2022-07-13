This document describes how to use the MLVB SDK to implement live streaming.

## Sample Code
Tencent Cloud offers an easy-to-understand API example project to help you quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## Prerequisites
1. To ensure a better user experience, we recommend you activate [CSS](https://intl.cloud.tencent.com/product/css). If you don't need to use CSS, skip this step.
2. Download and install [Android Studio](https://developer.android.com/studio). If you have already done so, skip this step.


## This Document Describes
* How to integrate the Player SDK for Android.
* How to use the Player SDK for live playback.
* How to use the underlying capabilities of the Player SDK to implement more live streaming features.



## SDK Integration
### Step 1. Download the SDK ZIP file
Download the SDK ZIP file and integrate the SDK into your application as instructed in the SDK integration document.


### Step 2. Add a view
The SDK provides `TXCloudVideoView` for video rendering by default. First, add the following code to the layout XML file:
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="gone"/>
```

### Step 3. Create a player object
The **TXLivePlayer** module of the Player SDK is used to implement the live playback feature. Use the **setPlayerView** API to associate the module with the **video_view** control just added to the UI.
```java
// `mPlayerView` is the view added in step 1
TXCloudVideoView mView = (TXCloudVideoView) view.findViewById(R.id.video_view);

// Create a player object
TXLivePlayer mLivePlayer = new TXLivePlayer(getActivity());

// Associate the player object with the view
mLivePlayer.setPlayerView(mView);
```

### Step 4. Start playback
```java
String flvUrl = "http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
mLivePlayer.startPlay(flvUrl, TXLivePlayer.PLAY_TYPE_LIVE_FLV); // FLV is recommended
```

| Option | Enumerated Value | Description |
| ----------------------- | ------ | ---------------------------------- |
| PLAY_TYPE_LIVE_RTMP | 0 | The URL passed in is an RTMP live streaming URL |
| PLAY_TYPE_LIVE_FLV | 1 | The URL passed in is an FLV live streaming URL |
| PLAY_TYPE_LIVE_RTMP_ACC | 5 | The low-latency URL (applicable to only mic connect scenarios) |
| PLAY_TYPE_VOD_HLS | 3 | The URL passed in is an HLS (M3U8) playback URL|


>?We recommend you not use the HLS protocol to play back live streaming video sources in your app because the latency is too high (though HLS protocol is suitable for VOD). Instead, we recommend using LIVE_FLV and LIVE_RTMP playback protocols.

### Step 5. Stop playback
You **need to terminate the view control** when stopping the playback, especially before the next call of `startPlay`. **This can prevent memory leak and screen flashing issues.**

In addition, when exiting the playback UI, you **need to call the `onDestroy()` function for the rendering view**. **This can prevent memory leak and "Receiver not registered" alarms.**
```java
@Override
public void onDestroy() {
    super.onDestroy();
    mLivePlayer.stopPlay(true); // `true` indicates to clear the last-frame image
    mView.onDestroy(); 
}
```

The boolean parameter of `stopPlay` indicates whether to clear the last-frame image. Early versions of the live player of the RTMP SDK don't have a pause function; therefore, this boolean value is used to clear the last-frame image.

If you want to retain the last-frame image after VOD stops, simply do nothing after receiving the playback stop event; playback will stop at the last frame by default.


## How to Use
This document describes how to use common live streaming features.

### 1. Image adjustment
- **view: size and position**
You can modify the size and position of video images by adjusting the size and position of the `video_view` control added in **step 1**.

- **setRenderMode: Aspect fill or aspect fit**

| Value | Description |
| ----------------------------- | ------------------------------------------------------------ |
| RENDER_MODE_FULL_FILL_SCREEN  | Images are scaled to fill the entire screen, and the excess parts are cropped. There are no black bars in this mode, but images may not be displayed in whole. |
| RENDER_MODE_ADJUST_RESOLUTION | The longer side of the image is scaled to fit the screen. In this mode, neither side of the image will exceed the edge of the screen. Images are centered, and there may be black bars. |

- **setRenderRotation: Image rotation**

| Value | Description |
| ------------------------- | ------------------------------------------ |
| RENDER_ROTATION_PORTRAIT  | Normal playback (the Home button is below the video image)            |
| RENDER_ROTATION_LANDSCAPE | Clockwise rotation of the video image by 270 degrees (the Home button is on the left of the image) |

```Java
// Set the fill mode
mLivePlayer.setRenderMode(TXLiveConstants.RENDER_MODE_ADJUST_RESOLUTION);
// Set the rotation of video
mLivePlayer.setRenderRotation(TXLiveConstants.RENDER_ROTATION_LANDSCAPE);
```




### 2. Playback pause
Technically speaking, live playback cannot be paused. In this document, pausing the playback means **freezing the video image** and **disabling audio**, while the video source continues to be streamed in the cloud. When you call `resume`, the playback will start from the time of resumption. This is different from VOD, where when you pause or resume the playback, the player will behave the same way as it does when you pause or resume a local video file.

```java
// Pause playback
mLivePlayer.pause();
// Resume playback
mLivePlayer.resume();
```

### 3. Message reception
This feature is used to deliver custom messages from the publisher to the audience along with audio/video data. It is applicable to the following scenarios:

- Online quiz: The pusher delivers the **questions** to the audience. Seamless "sound-image-question" synchronization can be achieved.
- Live show: The pusher delivers **lyrics** to the audience. The lyrics can be displayed in real time on the player and will not be affected by video encoding quality degradation.
- Online education: The publisher delivers **laser pointer** and **doodle** operations to the viewers to circle and underline content in the player in real time.

You can use this feature as follows:
- Set **setEnableMessage** in `TXLivePlayConfig` to **true**.
- Make `TXLivePlayer` use **TXLivePlayListener** to listen for the message **PLAY_EVT_GET_MESSAGE (2012)**.

```java
//Sample code for Android
    mTXLivePlayer.setPlayListener(new ITXLivePlayListener() {
        @Override
        public void onPlayEvent(int event, Bundle param) {
            if (event == TXLiveConstants.PLAY_ERR_NET_DISCONNECT) {
                roomListenerCallback.onDebugLog("[AnswerRoom] Stream pull failed: The network is disconnected");
                roomListenerCallback.onError(-1, "The network is disconnected, and stream pull failed");
            }
            else if (event == TXLiveConstants.PLAY_EVT_GET_MESSAGE) {
                String msg = null;
                try {
                    msg = new String(param.getByteArray(TXLiveConstants.EVT_GET_MSG), "UTF-8");
                    roomListenerCallback.onRecvAnswerMsg(msg);
                } catch (UnsupportedEncodingException e) {
                    e.printStackTrace();
                }
            }
        }
        @Override
        public void onNetStatus(Bundle status) {
        }
        });
```

### 4. Screencapturing
Call **snapshot** to take a screenshot of the live streamed video. This method captures a frame of the video. To capture the UI, use the corresponding API of the Android system.



```java
mLivePlayer.snapshot(new ITXSnapshotListener() {
    @Override
    public void onSnapshot(Bitmap bmp) {
        if (null != bmp) {
           // Get the screenshot bitmap
        }
    }
});
```

### 5. Live stream recording
Live stream recording is an extended feature in the live streaming scenario: When audience members are watching a live stream, they can click the "Record" button to record a live stream segment and publish it through a video distribution platform such as Tencent Cloud VOD. This allows them to distribute the video as a UGC message on social media platforms like WeChat Moments.



```java
// Specify a `ITXVideoRecordListener` to sync the recording progress and result
mLivePlayer.setVideoRecordListener(recordListener);
// Start recording. This API can be placed in the response function of the "Record" button. Currently, only the video source can be recorded, while other data such as on-screen comments cannot.
mLivePlayer.startRecord(int recordType);
// ...
// ...
// Stop recording. This API can be placed in the response function of the "Stop" button.
mLivePlayer.stopRecord();
```

- The recording progress is measured by time and will be notified of through the `onRecordProgress` of `ITXVideoRecordListener`.
- A recorded file will be notified of as an MP4 file through the `onRecordComplete` of `ITXVideoRecordListener`.
- `TXUGCPublish` is used to implement video upload and publishing. For detailed directions, see [Android](https://intl.cloud.tencent.com/document/product/1069/38026).

### 6. Seamless definition switch
During daily use, network conditions change constantly. When the network conditions are poor, switching to a lower image quality can reduce lag, and the higher quality video can be switched back when network conditions improve.
Traditionally, playback is interrupted when a stream is switched, which can cause problems such as video image discontinuity, black screen, and lag. With the seamless switch solution, you can switch to another stream without interrupting the live streaming.

The definition switch API can be called at any time after live streaming starts.
```java
// The stream `http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e.flv` is being played back
// Switch to a new stream with a bitrate of 900 Kbps
mLivePlayer.switchStream("http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e_900.flv");
```

>?You need to configure PTS alignment on the backend to use the seamless definition switch feature. To do this, [submit a ticket](https://console.cloud.tencent.com/workorder).

### 7. Live stream replay
The time shifting feature allows you to return to any previous time point during a live stream and resume playback from that time point. It is highly suitable for scenarios in which there is no need for interaction but viewers may want to rewind and replay a video, such as sports and gaming events.

```java
// Call `startPlay` first before setting time shifting
// Start playback
TXLiveBase.setAppID("1253131631"); // Configure `appId`
mLivePlayer.prepareLiveSeek();     // The backend requests the live streaming start time
```
After correct configuration, the current progress will not start from 0 in the `LAY_EVT_PLAY_PROGRESS` event, but will be calculated based on the actual playback start time.
Call the `seek` method to start live streaming again from a previous time point
```java
mLivePlayer.seek(600); // Start playback from the 10th minute
```

Configure the following settings on the backend to connect to time shifting:

- Recording: Configure the time shifting duration and time shifting storage period.
- Playback: Enable metadata acquisition in time shifting.

The time shifting feature is currently in beta testing. To use it, [submit a ticket](https://console.cloud.tencent.com/workorder).

### 8. Latency adjustment
The live playback feature of the SDK is not based on FFmpeg, but Tencent Cloud's proprietary playback engine, which is why the SDK offers better latency control than open-source players do. We provide three latency control modes, which can be used for showrooms, game streaming, and hybrid scenarios.

- **Comparison of control modes**

| Control Mode | Lag Rate | Average Latency | Applicable Scenario | Description |
| -------- | ---------- | -------- | -------------------- | -------------------------------------------------------- |
| Expedited mode | Relatively high | 2s–3s| Live show (online quiz) | Has better latency control and is suitable for scenarios that require a low latency. |
| Smooth mode | Lowest | ≥ 5s | Game live streaming (Tencent Penguin eSports) | Suitable for game live streaming scenarios with a high bitrate, such as battle royale games. |
| Auto mode | Network adaption | 2s–8s | Hybrid scenario | The better the audience's network, the shorter the latency, and vice versa. |


- **Code to integrate the three modes**
```java
TXLivePlayConfig mPlayConfig = new TXLivePlayConfig();
//
// Auto mode
mPlayConfig.setAutoAdjustCacheTime(true);
mPlayConfig.setMinAutoAdjustCacheTime(1);
mPlayConfig.setMaxAutoAdjustCacheTime(5);
//
// Expedited mode
mPlayConfig.setAutoAdjustCacheTime(true);
mPlayConfig.setMinAutoAdjustCacheTime(1);
mPlayConfig.setMaxAutoAdjustCacheTime(1);
//
// Smooth mode
mPlayConfig.setAutoAdjustCacheTime(false);
mPlayConfig.setCacheTime(5);
//
mLivePlayer.setConfig(mPlayConfig);
// Start the playback after configuration
```

>?For more information on stutter and latency control, see [Video Stutter](https://intl.cloud.tencent.com/document/product/1071/39362).

### 9. Ultra low-latency playback
The live player supports live playback at a latency of about **400 ms**. It can be used in scenarios with very strict requirements for latency, such as **remote claw machine** and **mic connect**. You need to know the following information about this feature:

- **Enabling this feature is not required**
This feature doesn't need to be enabled in advance, but the live stream must be in Tencent Cloud, because there are technical and other difficulties in implementing an ultra low-latency linkage across cloud service providers.

- **The playback URL must be configured with hotlink protection**
The playback URL cannot be a general CDN URL and must carry a hotlink protection signature. For more information on how to calculate a signature, see [Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).

- **ACC must be specified as the playback type**
When calling the `startPlay` playback function, you need to set `type` to **PLAY_TYPE_LIVE_RTMP_ACC**, and the SDK will use the RTMP-UDP protocol to directly pull the live stream.

- **It has a limit on the number of streams played back concurrently**
Currently, a maximum of **ten** streams can be played back concurrently. Because the cost of low-latency lines is much greater than CDN lines, we encourage users to use this feature only in scenarios that actually require high interaction rather than using it for scenarios which do not require extremely low latency.

- **The latency of OBS doesn't meet the requirements**
If [TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/38158) is used, call [setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38158) to set `quality` to `MAIN_PUBLISHER` or `VIDEO_CHAT`. It's difficult to achieve low latency with OBS because data tends to build up at the streaming end.

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
| ---------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN       | 2004 | Video playback started.                                               |
| PLAY\_EVT\_PLAY\_PROGRESS    | 2005 | Video playback progress (including the current playback progress, loading progress, and total video duration).      |
| PLAY\_EVT\_PLAY\_LOADING     | 2007 | The video is being loaded. The `LOADING_END` event will be reported if video playback resumes. |
| PLAY\_EVT\_VOD\_LOADING\_END | 2014 | Video loading ended, and video playback resumed.                        |

**Do not hide the playback image after receiving `PLAY_LOADING`**: Because the length of time between `PLAY_LOADING` and `PLAY_BEGIN` is uncertain (it may be five seconds or five milliseconds), some customers hide the playback image upon `LOADING` and display the image upon `BEGIN`, which will cause serious image flashing (especially in live streaming). **We recommend you place a translucent loading animation on top of the video playback image.**

#### 2. Stop events
| Event ID | Code | Description |
| :---------------------- | :---- | :----------------------------------------------------- |
| PLAY_EVT_PLAY_END       | 2006  | Video playback ended.                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | The network was disconnected and could not be reconnected after multiple retries. You can restart the player to perform more connection retries. |
| PLAY_ERR_HLS_KEY        | -2305 | Failed to get the HLS decryption key.                                  |

**How do I determine whether live streaming is over?**
Due to the varying implementation principles of different standards, no end events (error code 2006) are returned for many live streams. Instead, when a host pushing a stream, the SDK will soon find that data stream pull fails (`WARNING_RECONNECT`) and attempt to retry until the `PLAY_ERR_NET_DISCONNECT` event is thrown after three failed attempts.

Therefore, both error codes 2006 and -2301 need to be listened for and used to determine the end of live streaming.

#### 3. Warning events
You can ignore the following events, which are only used to notify you of some internal events of the SDK.

| Event ID | Code | Description |
| :-------------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | Failed to decode the current video frame.  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | Failed to decode the current audio frame.  |
| PLAY_WARNING_RECONNECT           |  2103  | The network was disconnected, and automatic reconnection was performed (the `PLAY_ERR_NET_DISCONNECT` event will be thrown after three failed attempts). |
| PLAY_WARNING_HW_ACCELERATION_FAIL | 2106 | Failed to start the hardware decoder, and the software decoder was used instead.   |

[](id:onNetStatus)
### Status feedback (onNetStatus)
The notification is triggered once every second to provide real-time feedback on the current status of the pusher. It can act as a dashboard to inform you of what is happening inside the SDK so you can better understand the current network conditions and video information.
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>NET_STATUS_CPU_USAGE</td><td>Current instantaneous CPU utilization</td>
</tr><tr>
<td>NET_STATUS_VIDEO_WIDTH</td><td>Video resolution - width</td>
</tr><tr>
<td>NET_STATUS_VIDEO_HEIGHT</td><td>Video resolution - height</td>
</tr><tr>
<td>NET_STATUS_NET_SPEED</td><td>Current network data reception speed</td>
</tr><tr>
<td>NET_STATUS_VIDEO_FPS</td><td>Current video frame rate of streaming media</td>
</tr><tr>
<td>NET_STATUS_VIDEO_BITRATE</td><td>Current video bitrate in Kbps of streaming media</td>
</tr><tr>
<td>NET_STATUS_AUDIO_BITRATE</td><td>Current audio bitrate in Kbps of streaming media</td>
</tr><tr>
<td>NET_STATUS_CACHE_SIZE</td><td>Buffer (`jitterbuffer`) size. If the current buffer length is 0, lag will occur soon.</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>Connected server IP</td>
</tr></table>