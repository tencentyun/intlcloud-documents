## Feature Overview
Publishing from the camera refers to the process of collecting video and audio data from the mobile phone's camera and mic, encoding the data, and pushing it to cloud-based live streaming platforms. [Tencent Cloud live_flutter_plugin](https://pub.dev/packages/live_flutter_plugin) provides the camera push capabilities via the `v2_tx_live_pusher` APIs.

## Notes
**About running projects on x86 emulators:** The SDK uses many  audio and video APIs of the iOS system, most of which cannot be used on the x86 emulator built into macOS. Therefore, we recommend that you test your project on a real device.

## Sample Code
| Platform |                         GitHub Address                          |           Key Class            |
| :------: | :----------------------------------------------------------: | :-------------------------: |
|   iOS    | [GitHub](https://github.com/tencentyun/LiteAVProfessional_iOS/blob/master/Demo/TXLiteAVDemo/LivePusherDemo/CameraPushDemo/CameraPushViewController.m) | CameraPushViewController.m  |
| Android  | [GitHub](https://github.com/tencentyun/LiteAVProfessional_Android/blob/master/Demo/livepusherdemo/src/main/java/com/tencent/liteav/demo/livepusher/camerapush/ui/CameraPushMainActivity.java) | CameraPushMainActivity.java |
| Flutter | [GitHub](https://github.com/LiteAVSDK/Live_Flutter) | live_camera_push.dart |
>? In addition to the above sample code, regarding frequently asked questions among developers, Tencent Cloud offers an easy-to-understand API example project, which you can use to quickly learn how to use different APIs.
>- iOS: [MLVB-API-Example](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC)
>- Android: [MLVB-API-Example](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example)
>- Flutter: [Live-API-Example](https://github.com/LiteAVSDK/Live_Flutter/tree/main/Live-API-Example)

## Getting Started
[](id:step1)
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
>! **The `packageName/BundleId` configured in the license must be the same as that of the application; otherwise, stream push will fail.**

[](id:step3)
### 3. Initialize the `V2TXLivePusher` component
Create a `V2TXLivePusher` object and specify `V2TXLiveMode`.

```dart
import 'package:live_flutter_plugin/v2_tx_live_pusher.dart';

/// Initialize `V2TXLivePusher`
initPusher() {
  _livePusher = V2TXLivePusher(V2TXLiveMode.v2TXLiveModeRTC);
}
```

[](id:step4)
### 4. Set the video rendering view
```dart
import 'package:live_flutter_plugin/widget/v2_tx_live_video_widget.dart';

/// The video rendering view widget
Widget renderView() {
  return V2TXLiveVideoWidget(
    onViewCreated: (viewId) async {
      /// Set the video rendering view
      _livePusher.setRenderViewID(_renderViewId);
      /// Enable camera preview
      _livePusher.startCamera(true);
    },
  );
}

```

[](id:step5)
### 5. Start and stop publishing
After calling `startCamera` to enable camera preview, you can call the [startPush](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/startPush.html) API in `V2TXLivePusher` to start publishing. You can use [TRTC's URL](https://www.tencentcloud.com/document/product/1071/39359) or an [RTMP URL](https://www.tencentcloud.com/document/product/1071/39359#.E8.87.AA.E4.B8.BB.E6.8B.BC.E8.A3.85.E6.8E.A8.E6.B5.81-url) for publishing. The former uses UDP. It offers better streaming quality and supports co-anchoring.
```dart
/// Start stream push
startPush() async {
  // Generate a stream push address of RTMP/TRTC
  var url = "";
  // Start stream push
  await _livePusher.startPush(url);
    // Turn the mic on
  await _livePusher.startMicrophone();
}
```

After stream push ends, you can call the [stopPush](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/stopPush.html) API in `V2TXLivePusher` to stop stream push.
```dart
/// Stop stream push
stopPush() async {
  // Turn the camera off
  await _livePusher.stopCamera();
  // Turn the mic off
  await _livePusher.stopMicrophone();
  // Stop stream push
  await _livePusher.stopPush();
}
```
>! If you have enabled camera preview, please disable it when you stop publishing streams. 

-  **How do I get a valid stream push URL?**
Activate CSS. In the **CSS console**, go to **Auxiliary Tools** > [**Address Generator**](https://console.tencentcloud.com/live/addrgenerator/addrgenerator) to generate a stream push URL. For more information, see [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359).
![](https://qcloudimg.tencent-cloud.cn/raw/6f43cae97630a6cef2dd62ef6b65f99c.png)
- **Why is `V2TXLIVE_ERROR_INVALID_LICENSE` returned?**    
If the `startPush` API returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means your license verification failed. Please check your configuration against [Step 2. Configure a license for the SDK](#step2).

[](id:step6)
### 6. Publish audio-only streams
If your live streaming scenarios involve audio only, you can skip [Step 4](#step4) or do not call `startCamera` before `startPush`.
```dart
/// Start stream push
startPush() async {
  // Initialize `V2TXLivePusher`
  _livePusher = V2TXLivePusher(V2TXLiveMode.v2TXLiveModeRTC);
  // Generate a stream push address of RTMP/TRTC
  var url = "";
  // Start stream push
  await _livePusher.startPush(url);
    // Turn the mic on
  await _livePusher.startMicrophone();
}
```
>? If you publish audio-only streams but no streams can be pulled from an RTMP, FLV, or HLS playback URL, there is a problem with your line configuration. Please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for help.

[](id:step7)
### 7. Set video quality
You can call the [setVideoQuality](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setVideoQuality.html) API in `V2TXLivePusher` to set image definition on the viewer end. The video image watched by the host is the source video without encoding or compression and is not subject to settings. However, viewers can perceive the encoding quality of the video encoder set in `setVideoQuality`. For more information, see [Setting Video Quality](https://www.tencentcloud.com/document/product/1071/41861).

[](id:step8)
### 8. Set the beauty filter style and skin brightening and rosy skin effects

You can call the [getBeautyManager](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/getBeautyManager.html) API in `V2TXLivePusher` to get the `TXBeautyManager` instance so as to further set the beauty filter effect.

#### Beauty filter style
The SDK has three built-in skin smoothing algorithms, each of which corresponds to a beauty filter style. You can select the one most suitable for your product needs. For more information, see the [TXBeautyManager.h](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/manager_tx_beauty_manager/TXBeautyManager-class.html) file.

| Beauty Filter Style | Description |
|---------|---------|
| TXBeautyStyleSmooth | The smooth style, which features more obvious skin smoothing effects and is suitable for live showrooms.  |
| TXBeautyStyleNature | The natural style, which retains more facial details and is more natural.  |
| TXBeautyStylePitu | The Pitu style, which uses the beauty filter algorithm developed by YouTu Lab. Its effect combines the smooth style and the natural style, that is, it retains more skin details than the smooth style and delivers more obvious skin smoothing effects than the natural style.  |

You can call the [setBeautyStyle](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/manager_tx_beauty_manager/TXBeautyManager/setBeautyStyle.html) API in `TXBeautyManager` to set the beauty filter style.

<table>
<tr><th>Item</th><th width=51%>Configuration</th><th>Description</th></tr>
<tr>
<td>Beauty filter strength</td>
<td>Via the <code>setBeautyLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the more obvious the effect.</td>
</tr><tr>
<td>Skin brightening filter strength</td>
<td>Via the <code>setWhitenessLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the more obvious the effect.</td>
</tr><tr>
<td>Rosy skin filter strength</td>
<td>Via the <code>setRuddyLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the more obvious the effect.</td>
</tr></table>

[](id:step9)
### 9. Manage devices
`V2TXLivePusher` offers a set of APIs for device control. You can use `getDeviceManager` to get the `TXDeviceManager` instance for device management. For detailed directions, see [TXDeviceManager API](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/getDeviceManager.html).


[](id:step10)
### 10. Set the mirror effect on the audience side
You can call [setRenderMirror](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setRenderMirror.html) of `V2TXLivePusher` to change the camera mirroring mode, so as to change the mirroring effect of the video image seen by viewers. If the host uses the front camera for live streaming, the image will be reversed by the SDK by default.
![](https://main.qcloudimg.com/raw/520d16280962523809e5695d2483d9ef.png)

[](id:step11)
### 11. Publish streams in landscape mode
In most cases, hosts stream while holding their phones vertically, and audience watch videos in portrait resolutions (e.g., 540 × 960). However, there are also cases where hosts hold phones horizontally, and ideally, audience should watch videos in landscape resolutions (960 × 540).

![](https://qcloudimg.tencent-cloud.cn/raw/63c38391680f75081a7aeec8aa3e4707.png)

`V2TXLivePusher` pushes video images in portrait mode by default. To push video images in landscape mode, you can modify the parameters in the [setVideoQuality](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/setVideoQuality.html) API to set the image orientation on viewers' devices.
```dart
// Video encoding parameters
var param = V2TXLiveVideoEncoderParam();
param.videoResolutionMode = isLandscape ? V2TXLiveVideoResolutionMode.v2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionMode.v2TXLiveVideoResolutionModePortrait;
_livePusher.setVideoQuality(param);
```

[](id:step12)
### 12. Set audio effects
Call [getAudioEffectManager](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher/V2TXLivePusher/getAudioEffectManager.html) in `V2TXLivePusher` to get a `TXAudioEffectManager` instance, which can be used to mix background music and set in-ear monitoring, reverb, and other audio effects. Background music mixing means mixing into the published stream the music played by the host's phone so that the audience can also hear the music.


- Call the `enableVoiceEarMonitor` API in `TXAudioEffectManager` to enable in-ear monitoring, which allows hosts to hear their vocals in earphones when they sing.
- Call the `setVoiceReverbType` API in `TXAudioEffectManager` to add reverb effects such as karaoke, hall, husky, and metal. The effects are applied to the videos watched by the audience.
- Call the `setVoiceChangerType` API in `TXAudioEffectManager` to add voice changing effects such as little girl and middle-aged man to enrich host-audience interaction. The effects are applied to the videos watched by the audience.
![](https://main.qcloudimg.com/raw/f8282bd6e1ba20e1e902bad52fa3131f.png)

>? For detailed directions, see [TXAudioEffectManager API](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/manager_tx_audio_effect_manager/TXAudioEffectManager-class.html).



## Event Handling
### Listening for events
The SDK listens on push events and errors via the [V2TXLivePusherObserver](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) delegate. See [v2_tx_live_code library](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_code/v2_tx_live_code-library.html) for a detailed list of events and error codes.

### Errors 
An error indicates that the SDK encountered a serious problem that made it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common unclassified error occurred. |
|V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
|V2TXLIVE_ERROR_REFUSED                 | -3 | The API call was rejected.  |
|V2TXLIVE_ERROR_NOT_SUPPORTED           | -4 | The API cannot be called.  |
|V2TXLIVE_ERROR_INVALID_LICENSE         | -5 | Failed to call the API due to invalid license.  |
|V2TXLIVE_ERROR_REQUEST_TIMEOUT         | -6 | The server request timed out.  |
|V2TXLIVE_ERROR_SERVER_PROCESS_FAILED   | -7 | The server could not handle your request.  |

### Warnings 
A warning indicates that the SDK encountered a problem whose severity level is warning. Warning events trigger tentative protection or recovery logic and can often be resolved.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_WARNING_NETWORK_BUSY                  |  1101|  Bad network connection: data upload blocked due to limited upstream bandwidth. |
|V2TXLIVE_WARNING_VIDEO_BLOCK                   |  2105|  Latency during video playback.  |
|V2TXLIVE_WARNING_CAMERA_START_FAILED           | -1301|  Failed to turn the camera on.  |
|V2TXLIVE_WARNING_CAMERA_OCCUPIED               | -1316| The camera is occupied. Try a different camera. |
|V2TXLIVE_WARNING_CAMERA_NO_PERMISSION          | -1314| No access to the camera. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_MICROPHONE_START_FAILED       | -1302| Failed to turn the mic on. |
|V2TXLIVE_WARNING_MICROPHONE_OCCUPIED           | -1319| The mic is occupied. This occurs when, for example, the user is having a call on the mobile device. |
|V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION      | -1317| No access to the mic. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED  | -1309|  The system does not support screen sharing.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED   | -1308|  Failed to start screen recording. If this occurs on a mobile device, it may be because the user denied the access.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED    | -7001|  Screen recording was stopped by the system.  |
