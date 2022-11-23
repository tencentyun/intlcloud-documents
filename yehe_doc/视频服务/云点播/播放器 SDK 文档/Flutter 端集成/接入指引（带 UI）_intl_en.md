## SDK Download

The Tencent Cloud RT-Cube Player SDK for Flutter can be downloaded [here](https://github.com/LiteAVSDK/Player_Flutter/tree/main/Flutter).

## Intended Audience

This document describes some of the proprietary capabilities of Tencent Cloud. Make sure that you have activated the relevant [Tencent Cloud](https://intl.cloud.tencent.com) services before reading this document. If you don't have an account yet, [sign up for free trial](https://intl.cloud.tencent.com/login) first.

## This Document Describes

* How to integrate the Tencent Cloud RT-Cube Player SDK for Flutter.
* How to use the Player component for VOD playback.

## Player Component Overview

The Player component for Flutter is an extension of the Player SDK for Flutter. Compared with the VOD player, the Player component is easier to use and integrates more features, including full screen playback, definition selection, progress bar, playback control, and thumbnails. To integrate Flutter video playback capabilities more easily, you can use the Player component for Flutter.

Supported features:

- Full screen playback

- Adaptive screen rotation during playback

- Custom video thumbnail

- Definition selection

- Audio and brightness adjustment

- Playback speed change

- Hardware acceleration

- Picture-in-picture (PiP) on Android and iOS

- Image sprite and keyframe timestamp information

  More features to come soon.

## Integration Guide[](id:Guide)

1. Copy the `superplayer` directory in `example` in the project to your Flutter project.
2. On the page where you need the player, import the dependency package of `superplayer` as follows:
```dart
import 'superplayer/demo_superplayer_lib.dart';
```

## SDK Integration[](id:stepone)

### Step 1. Apply for and integrate a video playback license[](id:step1)

To integrate a player, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/login), apply for the video playback license, and then integrate the license as follows. We recommend you integrate it during application start.

If no license is integrated, exceptions may occur during playback.

```dart
String licenceURL = ""; // The license URL obtained
String licenceKey = ""; // The license key obtained
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

### Step 2. Create a controller[](id:step2)

```dart
SuperPlayerController _controller = SuperPlayerController(context);
```

### Step 3. Configure the player[](id:step3)

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// If `preferredResolution` is not configured, the 720x1280 resolution stream will be played back preferably during multi-bitrate video playback
config.preferredResolution = 720 * 1280;
_controller.setPlayConfig(config);
```

For detailed configuration in `FTXVodPlayConfig`, see the player configuration API of the VOD player SDK for Flutter.

### Step 4. Configure event listening[](id:step4)

```dart
_controller.onSimplePlayerEventBroadcast.listen((event) {
  String evtName = event["event"];
  if (evtName == SuperPlayerViewEvent.onStartFullScreenPlay) {
    setState(() {
      _isFullScreen = true;
    });
  } else if (evtName == SuperPlayerViewEvent.onStopFullScreenPlay) {
    setState(() {
      _isFullScreen = false;
    });
  } else {
    print(evtName);
  }
});
```

### Step 5. Add a layout[](id:step5)

```dart
Widget _getPlayArea() {
    return Container(
    height: 220,
    child: SuperPlayerView(_controller),
  );
}
```

### Step 6. Listen on the Back button clicking event[](id:step6)

Add listening for the return event to ensure that the full screen mode is exited first if the player is in full screen mode when the return event is triggered, and the page will be exited only when the return event is triggered again.
**If you want to directly exit the page in full screen playback mode, you don't need to implement the listening.**

```dart
  @override
Widget build(BuildContext context) {
  return WillPopScope(
      child: Container(
        decoration: BoxDecoration(
            image: DecorationImage(
              image: AssetImage("images/ic_new_vod_bg.png"),
              fit: BoxFit.cover,
            )),
        child: Scaffold(
          backgroundColor: Colors.transparent,
          appBar: _isFullScreen
              ? null
              : AppBar(
            backgroundColor: Colors.transparent,
            title: const Text('SuperPlayer'),
          ),
          body: SafeArea(
            child: Builder(
              builder: (context) => getBody(),
            ),
          ),
        ),
      ),
      onWillPop: onWillPop);
}

Future<bool> onWillPop() async {
  return !_controller.onBackPress();
}
```

### Step 7. Start the playback[](id:step7)
<dx-tabs>
::: Through the URL
```dart
SuperPlayerModel model = SuperPlayerModel();
model.videoURL = "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";
_controller.playWithModelNeedLicence(model);
```
:::

::: Through `fileId`
```dart
SuperPlayerModel model = SuperPlayerModel();
model.appId = 1500005830;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "8602268011437356984";
// `psign` is a player signature. For more information on the signature and how to generate it, visit: https://intl.cloud.tencent.com/document/product/266/38099
model.videoId.pSign = "psignXXX"
_controller.playWithModelNeedLicence(model);
```

Find the target video file in [Media Assets](https://console.cloud.tencent.com/vod/media), and you can view the `FileId` below the filename.

Play back the video through the `FileId`, and the player will request the backend for the real playback URL. If the network is abnormal or the `FileId` doesn't exist, the `SuperPlayerViewEvent.onSuperPlayerError` event will be received.

:::
</dx-tabs>


### Step 8. Stop the playback[](id:step8)

**Remember to call the controller termination method** when stopping the playback, especially before the next call of `startVodPlay`. This can prevent memory leak and screen flashing issues, as well as ensure that playback is stopped when the page is exited.
```dart
  @override
void dispose() {
  // must invoke when page exit.
  _controller.releasePlayer();
  super.dispose();
}
```

## Player Component APIs[](id:sdkList)

### 1. Playing back a video

**Note**

Starting from v10.7, `startPlay` is replaced by `startVodPlay`, and playback will succeed only after you use `{@link SuperPlayerPlugin#setGlobalLicense}` to set the license; otherwise, playback will fail (black screen occurs). The license needs to be set only once globally. You can use the license for CSS, UGSV, or video playback. If you have no such licenses, you can [quickly apply for a trial license](https://www.tencentcloud.com/document/product/266/51098) or [purchase an official license](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license).

**Description**

This API is used to start video playback.

**API**

```dart
_controller.playWithModelNeedLicence(model);
```

**Parameter description**

1. SuperPlayerModel

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| appId | int | The application's `appId`, which is required for playback via `fileId`. |
| videoURL | String | The video URL, which is required for playback via URL. |
| multiVideoURLs | List<String> | Multi-bitrate playback URLs, which are required for playback via multi-bitrate URLs. |
| defaultPlayIndex | int | The default playback bitrate number, which is used together with `multiVideoURLs`. |
| videoId | SuperPlayerVideoId | The `fileId` storage object, which is further described below. |
| title | String | The video title. You can use this to customize the title and overwrite the title internally requested by the player from the server. |
| coverUrl | String | The thumbnail image pulled from the Tencent server, whose value will be assigned automatically in `SuperVodDataLoader`. |
| customeCoverUrl | String | A custom video thumbnail. This parameter is used preferentially and is used to customize the video thumbnail. |
| duration | int | The video duration in seconds. |
| videoDescription | String | The video description. |
| videoMoreDescription | String | The detailed video description. |
| playAction | int | Valid values: PLAY_ACTION_AUTO_PLAY, PLAY_ACTION_MANUAL_PLAY, PLAY_ACTION_PRELOAD, as described below. |

2. SuperPlayerVideoId

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| fileId | String | The file ID, which is required. |
| psign | String | The player signature. For more information on the signature and how to generate it, see [Player Signature](https://intl.cloud.tencent.com/document/product/266/38099). |

3. playAction

 -  PLAY_ACTION_AUTO_PLAY: The video will be automatically played back after `playWithModel` is called.
 -  PLAY_ACTION_MANUAL_PLAY: The video needs to be played back manually after `playWithModel` is called. The player doesn't load the video and only displays the thumbnail image, which consumes no video playback resources compared with `PLAY_ACTION_PRELOAD`.
 -  PLAY_ACTION_PRELOAD: The player will display the thumbnail image and won't start the video playback after `playWithModel` is called, but the video will be loaded. This can start the playback faster than `PLAY_ACTION_MANUAL_PLAY`.

### 2. Pausing playback

**Description**

This API is used to pause video playback.

**API**

```dart
_controller.pause();
```

### 3. Resuming playback

**Description**

This API is used to resume the playback.

**API**

```dart
_controller.resume();
```
### 4. Restarting playback

**Description**

This API is used to restart the video playback.

**API**

```dart
_controller.reStart();
```

### 5. Resetting the player

**Description**

This API is used to reset the player status and stop the video playback.

**API**

```dart
_controller.resetPlayer();
```

### 6. Releasing the player

**Description**

This API is used to release the player resources and stop the video playback. After it is called, the controller can no longer be reused.

**API**

```dart
_controller.releasePlayer();
```

### 7. Processing the player Back button event

**Description**

This API is used to determine the action to perform when the Back button is clicked in full screen playback mode. If `true` is returned, the full screen mode is exited, and the Back button clicking event is consumed; if `false` is returned, the event is unconsumed.

**API**

```dart
_controller.onBackPress();
```

### 8. Switching the definition

**Description**

This API is used to switch the definition of the video being played back in real time.

**API**

```dart
_controller.switchStream(videoQuality);
```

**Parameter description**

After playback starts, you can get the valid values of `videoQuality` through `_controller.currentQualiyList` (definition options) and `_controller.currentQuality` (default definition). **The definition switch feature has been integrated into the Player component. In full screen mode, you can click the button in the bottom-right corner to switch the definition.**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| index | int | The definition number. |
| bitrate | int | Bitrate for the definition. |
| width | int | The video width for the definition. |
| height | int | The video height for the definition. |
| name | String | The definition abbreviation. |
| title | String | Displayed definition name. |
| url | String | The multi-bitrate URL, which is optional. |

### 9. Adjusting the playback progress (seek)

**Description**

This API is used to adjust the current video playback progress.

**API**

```dart
_controller.seek(progress);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| progress | double | Target time in seconds. |

### 10. Configuring the Player component

**Description**

This API is used to configure the Player component.

**API**

```dart
_controller.setPlayConfig(config);
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| connectRetryCount | int | The number of player reconnections. If the SDK is disconnected from the server due to an exception, the SDK will attempt to reconnect to the server. |
| connectRetryInterval | int | The interval between two player reconnections. If the SDK is disconnected from the server due to an exception, the SDK will attempt to reconnect to the server. |
| timeout | int | Player connection timeout period |
| playerType | int | Player type. Valid values: 0: VOD; 1: Live streaming; 2: Live stream replay. |
| headers | Map | Custom HTTP headers |
| enableAccurateSeek | bool | Whether to enable accurate seek. Default value: true. |
| autoRotate | bool | If it is set to `true`, the MP4 file will be automatically rotated according to the rotation angle set in the file, which can be obtained from the `PLAY_EVT_CHANGE_ROTATION` event. Default value: `true`. |
| smoothSwitchBitrate | bool | Whether to enable smooth multi-bitrate HLS stream switch. If it is set to `false` (default), multi-bitrate URLs are opened faster. If it is set to `true`, the bitrate can be switched smoothly when IDR frames are aligned. |
| cacheMp4ExtName | String | The cached MP4 filename extension. Default value: `mp4`. |
| progressInterval | int | Progress callback interval in ms. If it is not set, the SDK will call back the progress once every 0.5 seconds. |
| maxBufferSize | int | The maximum size of playback buffer in MB. The setting will affect `playableDuration`. The greater the value, the more the data that is buffered in advance. |
| maxPreloadSize | int | Maximum preload buffer size in MB |
| firstStartPlayBufferTime | int | Duration of the video data that needs to be loaded during the first buffering in ms. Default value: 100 ms |
| nextStartPlayBufferTime | int | The minimum buffered data size to stop buffering (secondary buffering for insufficient buffered data or progress bar drag buffering caused by `seek`) in milliseconds. Default value: 250 ms |
| overlayKey | String | The HLS security enhancement encryption and decryption key. |
| overlayIv | String | The HLS security enhancement encryption and decryption IV. |
| extInfoMap | Map | Some special configuration items. |
| enableRenderProcess | bool | Whether to allow the postrendering and postproduction feature, which is enabled by default. If the super-resolution plugin exists after it is enabled, the plugin will be loaded by default. |
| preferredResolution | int | Resolution of the video used for playback preferably. `preferredResolution` = `width` * `height` |

### 11. Enabling/Disabling hardware decoding

**Description**

This API is used to enable/disable playback based on hardware decoding.

**API**

```dart
_controller.enableHardwareDecode(enable);
```

### 12. Getting the playback status

**Description**

This API is used to get the playback status.

**API**

```dart
SuperPlayerState superPlayerState = _controller.getPlayerState();
```

**Parameter description**

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| INIT | SuperPlayerState | Initial status |
| PLAYING | SuperPlayerState | Playing back |
| PAUSE | SuperPlayerState | Paused |
| LOADING | SuperPlayerState | Loading |
| END | SuperPlayerState | Ended |

### 13. Entering the PiP mode

**Description**

This API is used to display the current video in PiP mode. The PiP mode can be enabled only on supported device models on Android 7.0 or later.

**API**

```dart
_controller.enterPictureInPictureMode(
backIcon: "images/ic_pip_play_replay.png",
playIcon: "images/ic_pip_play_normal.png",
pauseIcon: "images/ic_pip_play_pause.png",
forwardIcon: "images/ic_pip_play_forward.png");
```

**Parameter description**

The parameters are applicable only to Android.

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| backIcon | String | The seek backward icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| playIcon | String | The playback icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| pauseIcon | String | The pause icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |
| forwardIcon | String | The fast forward icon, which can be up to 1 MB in size as limited by Android. It is optional, and if it is not set, the system icon will be used. |

## Event Notifications

### 1. Listening on the playback status

**Description**

This callback is used to listen for the video playback status and status change after encapsulation.

**Code**

```dart
_playController.onPlayStateBroadcast.listen((event) {
  SuperPlayerState state = event['event'];
});
```

**Event description**

The enumeration class `SuperPlayerState` is used to transfer the event.

| Status | Description |
| ------ |------------------ |
| INIT | Initial status |
| PLAYING | Playing back |
| PAUSE | Paused |
| LOADING  | Loading |
| END | Ended |

### 2. Listening on playback events

**Description**

This callback is used to listen for player operation events.

**Code**

```dart
_controller.onSimplePlayerEventBroadcast.listen((event) {
    String evtName = event["event"];
    if (evtName == SuperPlayerViewEvent.onStartFullScreenPlay) {
        setState(() {
        _ isFullScreen = true;
        });
    } else if (evtName == SuperPlayerViewEvent.onStopFullScreenPlay) {
        setState(() {
          _isFullScreen = false;
        });
    } else {
        print(evtName);
    }
});
```

**Event description**


| Status | Description |
| ------ |------------------ |
| onStartFullScreenPlay | Entered the full screen playback mode |
| onStopFullScreenPlay | Exited the full screen playback mode |
| onSuperPlayerDidStart | Playback started |
| onSuperPlayerDidEnd  | Playback ended |
| onSuperPlayerError | Playback error |
| onSuperPlayerBackAction | Return event |

## Advanced Features

### 1. Requesting video data in advance through `fileId`

The `SuperVodDataLoader` API can be used to request the video data in advance to accelerate the playback start process.

**Sample code**

```dart
SuperPlayerModel model = SuperPlayerModel();
model.appId = 1500005830;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "8602268011437356984";
model.title = "VOD";
SuperVodDataLoader loader = SuperVodDataLoader();
// Values of the required parameters in `model` are directly assigned in `SuperVodDataLoader`
loader.getVideoData(model, (resultModel) {
  _controller.playWithModelNeedLicence(resultModel);
})
```


### 2. Using the PiP mode

#### 1. Configuration for Android

1.1 In the `android` package of your project, open `AndroidManifest.xml` and add the following configuration under the `activity` node at the project entry:

```xml
android:supportsPictureInPicture="true"
android:resizeableActivity="true"
android:configChanges="screenSize|smallestScreenSize|screenLayout|orientation"

// In the `android` package of your project, open `build.gralde` and make sure that the versions of `compileSdkVersion` and `targetSdkVersion` are both 31 or later.
```

1.2 Inheriting the PiP Activity

In `example/android` in the GitHub project, copy `FTXFlutterPipActivity.java` to the same directory as the entry Activity and change the parent class of your Activity to this class.

#### 2. Configuration for iOS
   2.1 Under your project target, select **Signing & Capabilities**, click **+ Capability** to add **Background Modes**, and select **Audio, AirPlay, and Picture in Picture**.

#### 3. Copy the sample code of `SuperPlayer`

In `example/lib` in the GitHub project, copy the `SuperPlayer` package to the `lib` directory in your project and integrate the Player component as instructed in `demo_superplayer.dart` in the sample code.
Then, you can see the PiP mode button at the center on the right of the playback UI of the Player component and click the button to enter the PiP mode.

#### 4. Listening on the lifecycle of the PiP mode

You can use `onExtraEventBroadcast` in `SuperPlayerPlugin` to listen on the lifecycle of the PiP mode as follows:

```dart
SuperPlayerPlugin.instance.onExtraEventBroadcast.listen((event) {
  int eventCode = event["event"];
  if (eventCode == TXVodPlayEvent.EVENT_PIP_MODE_ALREADY_EXIT) {
    // exit pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_PIP_MODE_REQUEST_START) {
    // enter pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_PIP_MODE_ALREADY_ENTER) {
    // already enter pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_IOS_PIP_MODE_WILL_EXIT) {
    // will exit pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_IOS_PIP_MODE_RESTORE_UI) {
    // restore UI only support iOS
  } 
});
```

#### 5. Error codes for entering the PiP mode

If the user fails to enter the PiP mode, the failure will not only be logged but also be prompted through a toast. You can modify the error handling operations in the `_onEnterPipMode` method in `superplayer_widget.dart`. The error codes are as detailed below:

| Parameter | Code | Description |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | Started successfully with no errors. |
| ERROR_PIP_LOWER_VERSION | -101 | The Android version is too early and doesn't support the PiP mode. |
| ERROR_PIP_DENIED_PERMISSION | -102 | The PiP mode permission wasn't enabled, or the current device doesn't support PiP. |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | The current UI was terminated. |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | The device model or system version doesn't support PiP (only supported on iPadOS 9+ and iOS 14+). | Supported only for iOS|
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | The player doesn't support PiP. | Supported only for iOS|
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | The video doesn't support PiP. | Supported only for iOS|
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | The PiP controller was unavailable. | Supported only for iOS|
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | The PiP controller reported an error. | Supported only for iOS|
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | The player object didn't exist. | Supported only for iOS|
| ERROR_IOS_PIP_IS_RUNNING | -110 | The PiP feature was running. | Supported only for iOS|
| ERROR_IOS_PIP_NOT_RUNNING | -111 | The PiP feature didn't start. | Supported only for iOS|

#### 6. Checking whether the current device supports PiP

You can use `isDeviceSupportPip` in `SuperPlayerPlugin` to check whether the PiP mode can be enabled as follows:

```dart
int result = await SuperPlayerPlugin.isDeviceSupportPip();
if(result == TXVodPlayEvent.NO_ERROR) {
  // pip support
}
```

The returned result in `result` means the same as the error code of the PiP mode.
