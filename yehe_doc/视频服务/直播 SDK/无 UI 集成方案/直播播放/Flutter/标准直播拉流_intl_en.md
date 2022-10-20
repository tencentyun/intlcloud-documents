## Basics
This document describes the live playback feature of Live Flutter Plugin.

### Live streaming overview
In **live streaming**, the video source is pushed by the host in real time. When the host stops pushing the source, the player will also stop playing the video. Because the live stream is played back in real time, no progress bar will be displayed in the player during the playback.

### Supported protocols
Common live streaming protocols are as listed below. We recommend you use an FLV-based live streaming URL that starts with `http` and ends with `.flv` for LVB. For LEB, we recommend you use the WebRTC protocol. For more information, see [LEB](https://www.tencentcloud.com/document/product/1071/41875).

|Protocol |Advantage |Disadvantage |Playback Latency |
|---------|---------|---------|---------|
|HLS | Mature, well adapted to high-concurrency scenarios | SDK integration is required | 3–5 seconds |
| FLV | Mature, well adapted to high-concurrency scenarios | SDK integration is required. | 2-3 seconds |
|RTMP |Relatively low latency |Poor performance in high-concurrency scenarios |1-3 seconds |
|WebRTC |Lowest latency |SDK integration is required |< 1 second |


>? LVB and LEB are priced differently. For details, see [LVB Billing Overview](https://intl.cloud.tencent.com/document/product/267/2818) and [LEB Billing Overview](https://intl.cloud.tencent.com/document/product/267/39969).


## Notes
The SDK **does not impose any restrictions on the sources of playback URLs**, which means you can use it to play both Tencent Cloud and non-Tencent Cloud URLs. However, the player of the SDK supports only live streaming URLs in FLV, RTMP, HLS (M3U8), and WebRTC formats and VOD URLs in MP4, HLS (M3U8), and FLV formats.

## Sample Code
Tencent Cloud offers an easy-to-understand API example project to help you quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example) |
| Flutter  | [live_flutter_plugin](https://github.com/LiteAVSDK/Live_Flutter) |

## Getting Started

### 1. Set dependencies
Integrate `live_flutter_plugin` into your application as instructed in [SDK Integration Guide](https://www.tencentcloud.com/document/product/1071/50582).
```dart
dependencies:
  live_flutter_plugin: latest version number
```

[](id:step2)
### 2. Configure a license for the SDK
1. Get the license:
  - If you have the required license, get the license URL and key in the [CSS console](https://console.tencentcloud.com/live/license).
    ![](https://qcloudimg.tencent-cloud.cn/raw/a6b24e8677c514ee1721d38893fd9ca2.png)
  - If you don't have the required license, apply for a license as instructed in [New License and Renewal](https://www.tencentcloud.com/document/product/1071/38546).
2. Before your application calls features of `live_flutter_plugin`, complete the following configuration:
```dart
import 'package:live_flutter_plugin/v2_tx_live_premier.dart';

 /// Tencent Cloud license management page (https://console.tencentcloud.com/live/license)
setupLicense() {
  // The license URL of the current application
  var LICENSEURL = "";
  // The license key of the current application
  var LICENSEURLKEY = "";
  V2TXLivePremier.setLicence(LICENSEURL, LICENSEURLKEY);
}
```

>! **The `packageName/BundleId` configured in the license must be the same as that of the application; otherwise, playback will fail.**

[](id:step3)
### 3. Create the player
The `V2TXLivePlayer` module in the SDK offers live playback capabilities.
```dart
import 'package:live_flutter_plugin/v2_tx_live_player.dart';
/// Initialize `V2TXLivePlayer`
initPlayer() {
  _livePlayer = V2TXLivePlayer();
  _livePlayer.addListener(onPlayerObserver);
}
```

[](id:step4)
### 4. Render the view
In Flutter, you need to depend on `v2_tx_live_video_widget` to create a video rendering view for the player to display video images on.

```dart
import 'package:live_flutter_plugin/widget/v2_tx_live_video_widget.dart';

/// The video rendering view widget
Widget renderView() {
  return V2TXLiveVideoWidget(
    onViewCreated: (viewId) async {
      // Set the video rendering view
      _livePlayer.setRenderViewID(_renderViewId);
    },
  );
}

```

[](id:step5)
### 5. Start playback
```dart
/// Start pulling the stream
startPlay() async {
  // Generate the `url` (RTMP/TRTC/LEB)
  var url = ""
  // Start pulling the stream
  await _livePlayer?.startPlay(url);
}
```
-  **How do I get a valid stream push URL?**
Activate CSS. In the **CSS console**, go to **Auxiliary Tools** > [**Address Generator**](https://console.tencentcloud.com/live/addrgenerator/addrgenerator) to generate a stream push URL. For more information, see [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359).
![](https://qcloudimg.tencent-cloud.cn/raw/f273d68fa4334983e0ac0a7a126d3505.png)
- **Why is `V2TXLIVE_ERROR_INVALID_LICENSE` returned?**    
If the `startPush` API returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means your license verification failed. Please check your configuration against [Step 2. Configure a license for the SDK](#step2).

[](id:step6)
### 6. Adjust the image

- **setRenderFillMode: Fill or fit**
<table>
<tr><th>Value</th><th>Description</th>
</tr><tr>
<td>V2TXLiveFillModeFill</td>
<td>Images are scaled to fill the entire screen, and the excess parts are cropped. There are no black bars in this mode, but images may not be displayed entirely.</td>
</tr><tr>
<td>V2TXLiveFillModeFit</td>
<td>Images are scaled so that the long side of the video fits the screen. Neither side exceeds the screen after scaling. Images are centered, and there may be black bars visible.</td>
</tr></table>

- **setRenderRotation: Clockwise rotation of video**
<table>
<tr><th>Value</th><th>Description</th>
</tr><tr>
<td>V2TXLiveRotation0</td>
<td>No rotation</td>
</tr><tr>
<td>V2TXLiveRotation90</td>
<td>Rotate 90 degrees clockwise</td>
</tr><tr>
<td>V2TXLiveRotation180</td>
<td>Rotate 180 degrees </td>
</tr><tr>
<td>V2TXLiveRotation270</td>
<td>Rotate 270 degrees clockwise</td>
</tr></table>

![](https://qcloudimg.tencent-cloud.cn/raw/38c966d878867204f7fa05eb337dec06.png)

[](id:step7)
### 7. Pause playback
Technically speaking, you cannot pause a live playback. In this document, pausing live playback refers to **freezing the video** and **disabling the audio**. While the video is frozen, new video streams continue to be sent to the cloud. When you resume playback, it resumes playing the current latest stream. This is different from pausing and resuming playback in VOD, in which the player behaves the same way as it does when you pause and resume a local video file.

```dart
// Pause playback
_livePlayer.pauseAudio();
_livePlayer.pauseVideo();
// Resume playback
_livePlayer.resumeAudio();
_livePlayer.resumeVideo();
```

[](id:step8)
### 8. Stop playback

```dart
// Stop playback
_livePlayer.stopPlay();
```

## Latency Control
The live playback feature of the SDK is not based on FFmpeg, but Tencent Cloud's proprietary playback engine, which is why the SDK offers better latency control than open-source players do. We provide three latency control modes, which can be used for live showrooms, game streaming, and hybrid scenarios.

- **Comparison of control modes**
<table>
<tr><th>Mode</th><th>Stutter</th><th>Average Latency</th><th>Scenario</th><th>Remarks</th>
</tr><tr>
<td>Speedy</td>
<td>Relatively high</td>
<td>2-3s</td>
<td>Live showroom</td>
<td>Has better latency control and is suitable for scenarios that require a low latency.</td>
</tr><tr>
<td>Smooth</td>
<td>Low</td>
<td>&gt;= 5s</td>
<td>Game streaming</td>
<td>Suitable for game live streaming scenarios with a high bitrate.</td>
</tr><tr>
<td>Auto</td>
<td>Adapts to network conditions</td>
<td>2-8s</td>
<td>Hybrid</td>
<td>The better the network conditions at the audience end, the lower the latency.</td>
</tr></table>

- **Code to integrate the three modes**
```objectivec
// Auto mode
_txLivePlayer.setCacheParams(1, 5);
// Speedy mode
_txLivePlayer.setCacheParams(1, 1);
// Smooth mode
_txLivePlayer.setCacheParams(5, 5);

// Start playback after configuration
```

>? For more information on stutter and latency control, see [Video Stutter](https://www.tencentcloud.com/document/product/1071/41876).

[](id:sdklisten)
## Listening for SDK Events
You can bind a [V2TXLivePlayerObserver](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/v2_tx_live_player_observer-library.html) to `V2TXLivePlayer`. Then, all internal SDK status information, such as player status, playback volume level, reception of the first audio/video frame, statistical data, warnings, and errors, will be notified to you through corresponding callbacks.

### Periodically triggered notification
- The [onStatisticsUpdate](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/v2_tx_live_player_observer-library.html) notification is triggered once every 2 seconds to provide real-time feedback on the current player status. It can act as a dashboard to inform you of what is happening inside the SDK so you can better understand the current network conditions and video information.
<table>
<tr><th>Parameter</th><th>Description</th>
</tr><tr>
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

- [onPlayoutVolumeUpdate](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/v2_tx_live_player_observer-library.html) is the callback for the player volume level. It will be returned only when you call [enableVolumeEvaluation](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_player_observer/v2_tx_live_player_observer-library.html) to enable the prompt for the player volume level. The callback interval is the same as that specified by the `intervalMs` parameter in `enableVolumeEvaluation`.

### Event-triggered notifications
Other callbacks are triggered when specific events occur.
