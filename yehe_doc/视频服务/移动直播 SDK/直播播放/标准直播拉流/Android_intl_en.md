## Basics
This document introduces the live playback feature of the Video Cloud SDK.

### Live streaming and video on demand
- In **live streaming**, the video streams published by hosts in real time are the source of streaming. When hosts stop publishing streams, the video played stops. Since video is streamed in real time, players do not have progress bars when they play live streaming URLs.
- In **video on demand (VOD)**, video files in the cloud are the source of streaming. Videos can be played at any time as long as they are not deleted from the cloud, and the playback progress can be adjusted using the progress bar. Video streaming websites such as Tencent Video and Youku Tudou are typical applications of VOD.

### Supported protocols
The table below lists the common protocols used for live streaming. We recommend FLV URLs (which start with `http` and end with `flv`) for LVB and WebRTC for LEB. For more information, please see [LEB](https://intl.cloud.tencent.com/document/product/1071/41875).

|Protocol |Pro |Con |Playback Latency |
|---------|---------|---------|---------|
| FLV | Mature, well adapted to high-concurrency scenarios | SDK integration is required. | 2-3s |
|RTMP |Relatively low latency |Poor performance in high-concurrency scenarios |1-3s |
| HLS (M3U8) | Well supported on mobile browsers | High latency |10-30s|
|WebRTC |Lowest latency |SDK integration is required. |< 1s |

>? LVB and LEB are priced differently. For details, please see [LVB Billing Overview](https://intl.cloud.tencent.com/document/product/267/2818) and [LEB Billing Overview](https://intl.cloud.tencent.com/document/product/267/39969).


## Notes
The Video Cloud SDK **does not impose any limit on the sources of playback URLs**, which means you can use it to play both Tencent Cloud and non-Tencent Cloud URLs. However, the player of the SDK supports only live streaming URLs in FLV, RTMP, HLS (M3U8), and WebRTC formats and VOD URLs in MP4, HLS (M3U8), and FLV formats.

## Sample Code
Regarding frequently asked questions among developers, Tencent Cloud offers a straightforward API example project, which you can use to quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## Integration
[](id:step1)
### Step 1. Create a rendering view
For the player to display video images, you need to add a rendering view in the layout XML file:
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="visible"/>
```

[](id:step2)
### Step 2. Create a player object
The **V2TXLivePlayer** module in the Video Cloud SDK offers live playback capabilities. Use the **setRenderView** API to associate the module with the **video_view** control added to the UI in Step 1.
```java
// mPlayerView is the view added in step 1
TXCloudVideoView mView = (TXCloudVideoView) view.findViewById(R.id.video_view);
// Create a player object
V2TXLivePlayer mLivePlayer = new V2TXLivePlayerImpl(mContext);
// Associate the player object with the view
mLivePlayer.setRenderView(mView);
```

[](id:step3)
### Step 3. Start playback
```java
String flvUrl = "http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
mLivePlayer.startPlay(flvUrl); 
```

[](id:step4)
### Step 4. Change the fill mode
- **view: size and position**
You can modify the size and position of video images by adjusting the size and position of the `video_view` control added in [Step1](#step1).
- **setRenderFillMode: aspect fill or aspect fit**
<table><tr><th>Value</th><th>Description</th>
</tr><tr>
<td>V2TXLiveFillModeFill</td>
<td>Images are scaled to fill the entire screen, and the excess parts are cropped. There are no black bars in this mode, but images may not be displayed in whole.</td>
</tr><tr>
<td>V2TXLiveFillModeFit</td>
<td>Images are scaled as large as the longer side can go. Neither side exceeds the screen after scaling. Images are centered, and there may be black bars.</td>
</tr></table>
- **setRenderRotation: clockwise rotation of video**
<table>
<tr><th>Value</th><th>Description</th></tr>
<td>V2TXLiveRotation0</td><td>Original</td>
</tr><tr>
<td>V2TXLiveRotation90</td><td>Rotate 90 degrees clockwise</td>
</tr><tr>
<td>V2TXLiveRotation180</td><td>Rotate 180 degrees clockwise</td>
</tr><tr>
<td>V2TXLiveRotation270</td><td>Rotate 270 degrees clockwise</td>
</tr></table>

<dx-codeblock>
::: Java Java
// Set the fill mode
mLivePlayer.setRenderFillMode(V2TXLiveFillModeFit);
// Set the rotation of video
mLivePlayer.setRenderRotation(V2TXLiveRotation0);
:::
</dx-codeblock>

![](https://main.qcloudimg.com/raw/6cddb671d6e5bc6e87d48e9ca3eed42a.png)

[](id:step5)

### Step 5. Pause playback
Technically speaking, you cannot pause a live playback. In this document, by pausing playback, we mean **freezing video** and **disabling audio**. In the meantime, new video streams continue to be sent to the cloud. When you resume playback, it starts from the time of resumption. This is in contrast to VOD. With VOD, when you pause and resume playback, the player behaves the same way as it does when you pause and resume a local video file.

```java
// Pause playback
mLivePlayer.pauseAudio();
mLivePlayer.pauseVideo();
// Resume playback
mLivePlayer.resumeAudio();
mLivePlayer.resumeVideo();
```

[](id:step6)
### Step 6. Stop playback
Call `stopPlay` to stop playback.
```java
mLivePlayer.stopPlay();  
```

[](id:step7)
### Step 7. Take a screenshot
Call **snapshot** to take a screenshot of the live video streamed. This method captures a frame of the streamed video. To capture the UI, use the corresponding API of the Android system.
![](https://main.qcloudimg.com/raw/06c0df9f2efb56c0f917dea24b658c59.png)

```java
mLivePlayer.setObserver(new MyPlayerObserver());
mLivePlayer.snapshot();
// Get the screenshot taken in the onSnapshotComplete callback of MyPlayerObserver
private class MyPlayerObserver extends V2TXLivePlayerObserver  {
    ...
    @Override
    public void onSnapshotComplete(V2TXLivePlayer v2TXLivePlayer, Bitmap bitmap) {
    }
    ...
}
```

[](id:Delay)
## Latency Control
The live playback feature of the SDK is not based on FFmpeg, but Tencent Cloud’s proprietary playback engine, which is why the SDK offers better latency control than open-source players do. We provide three latency control modes, which can be used for showrooms, game streaming, and hybrid scenarios.

- **Comparison of the three modes**
<table>
<tr><th>Mode</th><th>Stutter</th><th>Average Latency</th><th>Scenario</th><th>Remarks</th>
<tr>
<td>Speedy</td>
<td>More likely than the speedy mode</td>
<td>2-3s</td>
<td>Live showroom (Chongding Dahui)</td>
<td>The mode delivers low latency and is suitable for latency-sensitive scenarios.</td>
</tr><tr>
<td>Smooth</td>
<td>Least likely of the three</td>
<td>&gt;= 5s</td>
<td>Game streaming (Penguin Esports)</td>
<td>Playback is least likely to stutter in this mode, which makes it suitable for ultra-high-bitrate streaming of games such as PUBG.</td>
</tr><tr>
<td>Auto</td>
<td>Self-adaptive to network conditions</td>
<td>2-8s</td>
<td>Hybrid</td>
<td>The better network conditions at the audience end, the lower the latency.</td>
</tr></table>
- **Code to integrate the three modes**
```java
// Auto mode
mLivePlayer.setCacheParams(1.0f, 5.0f);
// Speedy mode
mLivePlayer.setCacheParams(1.0f, 1.0f);
// Smooth mode
mLivePlayer.setCacheParams(5.0f, 5.0f);
// Start playback after configuration
```

>? For more information on stuttering and latency control, see [Video Stutter](https://intl.cloud.tencent.com/document/product/1071/41876).

[](id:sdklisten)

## Listening for SDK Events
You can bind a [V2TXLivePlayerObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html) to your `V2TXLivePlayer` object to receive callback notifications about the player status, playback volume, first audio/video frame, statistics, warning and error messages, etc.

### Periodically triggered notification

- The [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#ab10e1f4e22e9bb73e3cea4ae15c36465) callback notification is triggered every 2 seconds to update you on the player’s status in real time. Like a car’s dashboard, the callback gives you information about the SDK, such as network conditions and video information.
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>appCpu</td>
<td>CPU usage (%) of the application</td>
</tr><tr>
<td>systemCpu</td>
<td>CPU usage (%) of the system</td>
</tr><tr>
<td>width</td>
<td>Video width</td>
</tr><tr>
<td>height</td>
<td>Video height</td>
</tr><tr>
<td>fps</td>
<td>Frame rate (fps)</td>
</tr><tr>
<td>audioBitrate</td>
<td>Audio bitrate (Kbps)</td>
</tr><tr>
<td>videoBitrate</td>
<td>Video bitrate (Kbps)</td>
</tr></table>
- The [onPlayoutVolumeUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a57fc000bf5e935f7253fa94e1750359e) callback, which notifies you of the player’s volume, works only after you call [enableVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#aaa893a96eff34a7ba660441f7597d6d8) to enable the volume reminder. You can set the interval of the callback by specifying the `intervalMs` parameter of `enableVolumeEvaluation`.

### Event-triggered notifications
Other callbacks are triggered when specific events occur.
