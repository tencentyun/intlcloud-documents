## Overview
Publishing from the camera refers to the process of collecting video and audio data from the mobile phone's camera and mic, encoding the data, and pushing it to cloud-based live streaming platforms. Tencent Cloud `live_flutter_plugin` provides the camera push capabilities via `V2TXLivePusher` APIs.

## Sample Code
Tencent Cloud offers an easy-to-understand API example project to help you quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/LiteAVSDK/Live_iOS/tree/main/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/LiteAVSDK/Live_Android/tree/main/MLVB-API-Example) |
| Flutter  | [GitHub](https://github.com/LiteAVSDK/Live_Flutter/blob/main/Live-API-Example/lib/page/push/live_screen_push.dart) |

## Environment Requirements

### Android

- Screen recording is supported in Android 5.0 and above.
- Floating windows need to be enabled manually on some mobile phones and systems.

### iOS

Screen recording is a new feature in iOS 10. In addition to using ReplayKit to record video from the screen, which is possible in iOS 9, with iOS 10, users can also stream live video from the screen. For details, see [Go Live with ReplayKit](https://developer.apple.com/videos/play/wwdc2016/601/). In iOS 11, Apple made ReplayKit more usable and more universally applicable and launched [ReplayKit2](https://developer.apple.com/videos/play/wwdc2017/606/), going from supporting ReplayKit alone to allowing the recording of the entire screen. Therefore, we recommend using ReplayKit2 in iOS 11 to enable the screen sharing feature. Screen sharing relies on extensions, which operate as independent processes. However, to ensure system smoothness, iOS allocates limited resources to extensions and may kill extensions with high memory usage. Given this, Tencent Cloud has further reduced the memory usage of LiteAVSDK while retaining its high streaming quality and low latency to ensure the stability of extensions.

>!This document describes how to use ReplayKit 2 on iOS 11 to push streams from the screen. The parts about the use of the SDK also apply to other custom stream push scenarios. For more information, see the code sample in the `Live Demo Screen` folder of the [demo](https://github.com/LiteAVSDK/Live_Flutter/tree/main/Live-API-Example).

1. **Create the live streaming extension**
Open your project with Xcode and select **New** > **Target...** > **Broadcast Upload Extension**, as shown below.
![](https://main.qcloudimg.com/raw/c4c0b0ee049c733640f813a318a25adb.png)
Enter a product name and click **Finish**. A new directory with the product name entered will appear in your project. Under the directory, there is an automatically generated `SampleHandler` class, which is responsible for screen recording operations.
>!Xcode 9 or later is required, and your iPhone must be updated to iOS 11 or later. Screen recording is not supported on emulators.
2. **Import `TXLiteAVSDK_ReplayKitExt.framework`**
Import `TXLiteAVSDK_ReplayKitExt.framework` into the live streaming extension the same way you import a framework into the host application. The system libraries the SDK depends on are also the same. For more information, see [iOS](https://www.tencentcloud.com/document/product/1071/38155).


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
### 3. Create a pusher object
Create a **V2TXLivePusher** object, which will be responsible for publishing operations.

```dart
V2TXLivePusher livePusher = V2TXLivePusher(V2TXLiveMode.v2TXLiveModeRTMP);
```

[](id:step4)
### 4. Start stream push
After completing [Step 1](#step1), you can use the code below to start publishing streams:
```dart
String rtmpUrl = "rtmp://2157.livepush.myqcloud.com/live/xxxxxx";
livePusher.startMicrophone();
livePusher.startScreenCapture();
livePusher.startPush(rtmpUrl);
```
-  **How can I obtain a valid publishing URL?**
Activate CSS. In the **CSS console**, go to **Auxiliary Tools** > [**Address Generator**](https://console.tencentcloud.com/live/addrgenerator/addrgenerator) to generate a stream push URL. For more information, see [Publishing/Playback URL](https://www.tencentcloud.com/document/product/1071/39359).
![](https://qcloudimg.tencent-cloud.cn/raw/6f43cae97630a6cef2dd62ef6b65f99c.png)
- **Why is `V2TXLIVE_ERROR_INVALID_LICENSE` returned?**    
If the `startPush` API returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means your license verification failed. Please check your configuration against [Step 2. Configure a license for the SDK](#step2).

[](id:step5)
### 5. Stop stream push
As there can be only one `V2TXLivePusher` object running at a time, make sure that you release all the resources when stopping publishing.
```dart
// Stop screen sharing and release the resources
void stopPush() {
    livePusher.stopMicrophone();
    livePusher.stopScreenCapture();
    livePusher.stopPush();
}
```

## Event Handling

### Listening for events
The SDK listens on push events and errors via the [V2TXLivePusherObserver](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_pusher_observer/v2_tx_live_pusher_observer-library.html) delegate. See [v2_tx_live_code library](https://pub.flutter-io.cn/documentation/live_flutter_plugin/latest/v2_tx_live_code/v2_tx_live_code-library.html) for a detailed list of events and error codes.

### Errors
An error indicates that the SDK encountered a serious problem that made it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :------------------------------------ | :---- | :------------------------------- |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common unclassified error occurred. |
| V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
|V2TXLIVE_ERROR_REFUSED                 | -3 | The API call was rejected.  |
|V2TXLIVE_ERROR_NOT_SUPPORTED           | -4 | The API cannot be called.  |
|V2TXLIVE_ERROR_INVALID_LICENSE         | -5 | Failed to call the API due to invalid license.  |
|V2TXLIVE_ERROR_REQUEST_TIMEOUT         | -6 | The server request timed out.  |
|V2TXLIVE_ERROR_SERVER_PROCESS_FAILED   | -7 | The server could not handle your request.  |

### Warnings
A warning indicates that the SDK encountered a problem whose severity level is warning. Warning events trigger tentative protection or recovery logic and can often be resolved.

| Event ID                                       | Code  | Description                                                     |
| :-------------------------------------------- | :---- | :----------------------------------------------------------- |
|V2TXLIVE_WARNING_NETWORK_BUSY                  |  1101|  Bad network connection: data upload blocked due to limited upstream bandwidth. |
|V2TXLIVE_WARNING_VIDEO_BLOCK                   |  2105|  Stuttering during video playback.  |
|V2TXLIVE_WARNING_CAMERA_START_FAILED           | -1301|  Failed to turn the camera on.  |
|V2TXLIVE_WARNING_CAMERA_OCCUPIED               | -1316| The camera is occupied. Try a different camera. |
|V2TXLIVE_WARNING_CAMERA_NO_PERMISSION          | -1314| No access to the camera. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_MICROPHONE_START_FAILED       | -1302| Failed to turn the mic on. |
|V2TXLIVE_WARNING_MICROPHONE_OCCUPIED           | -1319| The mic is occupied. This occurs when, for example, the user is having a call on the mobile device. |
|V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION      | -1317| No access to the mic. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED  | -1309|  The system does not support screen sharing.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED   | -1308|  Failed to start screen recording. If this occurs on a mobile device, it may be because the user denied the access.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED    | -7001|  Screen recording was stopped by the system.  |


## FAQs
ReplayKit2 is a new framework introduced by Apple in iOS 11, for which relatively few official documents have been released. The framework is still being improved, and problems have been found. See below for some common questions you may have when using ReplayKit2.

1. **When does screen recording stop automatically?**
Screen recording stops automatically when the screen locks or there is an incoming call. At such times, the `broadcastFinished` function in `SampleHandler` will be invoked, and you can send a notification to users about the interruption.

2. **Why does screen recording stop sometimes during screen sharing?**
The problem usually occurs after landscape/portrait mode switch if the resolution for stream publishing is set high. The broadcast upload extension is allocated a memory of only 50 MB and will be killed if its memory usage exceeds the limit. Given this, we recommend that you set the resolution to 720p or lower.

3. **Why are images streamed from the screen of iPhone X distorted?**
iPhone X has a notch at the top of the screen, so video captured from the screen is not in the aspect ratio of 16:9. If you set the output resolution for stream publishing to 16:9, for example, to HD (960 × 540), the images published will be slightly distorted because their original aspect ratio is not 16:9. We recommend that you set the resolution according to your screen size. Besides, if you play video streamed from the screen of iPhone X in aspect fit mode, the video may have black bars, and if you play it in aspect fill mode, the video may be cropped.