Tencent Cloud RT-Cube Superplayer for Flutter is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait orientation switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it supports live stream (FLV + RTMP) playback, features instant broadcasting of the first frame and low latency, and offers advanced capabilities, including seamless definition switch and live time shifting.

This player is based on a Flutter plugin of SuperPlayer and supports both Android and iOS. It is open-source and free of charge and does not restrict the source of playback addresses, so you can use it as desired.

## SDK Download

The Tencent Cloud RT-Cube Superplayer SDK for Flutter can be downloaded [here](https://github.com/tencentyun/SuperPlayer/tree/main/Flutter). 

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://cloud.tencent.com) services before reading it. If you haven't registered an account, please [sign up for free trial](https://intl.cloud.tencent.com/login) first.

## Integration Guide[](id:Guide)

1. Add the following configuration to `pubspec.yaml`.
```yaml
  super_player:
    git:
      url: https://github.com/tencentyun/SuperPlayer
      path: Flutter
```

2. Update the dependency package.
```yaml
   flutter pub upgrade
```
4. Add the native configuration.

### Android configuration[](id:Android_config)

Add the following configuration to the `AndroidManifest.xml` file of Android.

```xml
<!--Network permission-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD player floating window permission -->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--Storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

On Android, Superplayer depends on the native player SDK. Copy the `example/android/superplayerkit` folder in the directory to your project directory and insert `include ':superplayerkit'` into `settings.gradle`. You can also download an appropriate version at the official website and import it.

### iOS configuration[](id:iOS_config)

Add the following configuration to the `Info.plist` file of iOS:
```xml
    <key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```

iOS natively uses `pod` for dependency. Edit the `podfile` file and specify your player version.
```xml
pod 'SuperPlayer/Player', '3.3.9'
```

If no version is specified, the latest version of `SuperPlayer` will be installed by default.

### Call in Flutter[](id:Flutter_call)

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'dart:async';
import 'package:super_player/super_player.dart';

class TestSuperPlayer extends StatefulWidget {
  @override
  _TestSuperPlayerState createState() => _TestSuperPlayerState();
}

class _TestSuperPlayerState extends State<TestSuperPlayer> {

  SuperPlayerViewConfig _playerConfig;
  SuperPlayerViewModel _playerModel;
  SuperPlayerPlatformViewController _playerController;
  String _url = "http://liteavapp.qcloud.com/live/liteavdemoplayerstreamid_demo1080p.flv";
  int _appId = 0;
  String _fileId = "";

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    _playerConfig = SuperPlayerViewConfig();
    _playerModel = SuperPlayerViewModel();
    _playerModel.videoURL = _url;
  }

 @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            ackgroundColor: Colors.blueGrey,
            title: const Text('SuperPlayer'),
        ),
        body: Builder(
        builder: (context) =>
        SafeArea(
            child: Container(
            color: Colors.blueGrey,
            child: Column(
                children: [
                AspectRatio(
                    aspectRatio: 16.0/9.0,
                    child:SuperPlayerVideo(
                        onCreated: (SuperPlayerPlatformViewController vc) {
                            _playerController = vc;
                            await _playerController.setPlayConfig(_playerConfig);
                            await _playerController.playWithModel(_playerModel);// Start playback
                        },
                    )
                ),
                ],
            ),
            ),
        )
        ),
    );
  }

```



## Using Player[](id:usePlayer)

The main class of the player is `SuperPlayerVideo`, and videos can be played back after it is created.

```dart
  void initState() {
    // TODO: implement initState
    super.initState();
    _playerConfig = SuperPlayerViewConfig();
    _playerModel = SuperPlayerViewModel();
    _playerModel.videoURL = _url;
  }
```

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            ackgroundColor: Colors.blueGrey,
            title: const Text('SuperPlayer'),
        ),
        body: Builder(
            builder: (context) =>
                SafeArea(
                    child: Container(
                        color: Colors.blueGrey,
                        child: Column(
                            children: [
                                AspectRatio(
                                    aspectRatio: 16.0/9.0,
                                    child:SuperPlayerVideo(
                                        onCreated: (SuperPlayerPlatformViewController vc) {
                                            _playerController = vc;
                                            await _playerController.setPlayConfig(_playerConfig);
                                            await _playerController.playWithModel(_playerModel);// Start playback
                                        },
                                    )
                                ),
                            ],
                        ),
                    ),
                )
        ),
    );
  }
```

Run the code and you can see that the video is played back on the phone and most of the features in the UI are available.



## Multiple Definitions[](id:resolution)

Only one definition is specified in the sample code above. It is easy to add multiple definitions. For example, open the [CSS console](https://console.cloud.tencent.com/live/livemanage), find the live stream to be played back, and enter the details page.


Here, different playback addresses for different definitions and formats are provided. We recommend you use the FLV address for playback. The code is as follows:

```dart
  void initState() {
    // TODO: implement initState
    super.initState();
    _playerConfig = SuperPlayerViewConfig();
    _playerModel = SuperPlayerViewModel();
    SuperPlayerUrl url1 = SuperPlayerUrl();
    url1.title = "FHD";
    url1.url = "http://5815.liveplay.myqcloud.com/live/5815_89aad37e06ff11e892905cb9018cf0d4.flv";

    SuperPlayerUrl url2 = SuperPlayerUrl();
    url2.title = "FHD";
    url2.url = "http://5815.liveplay.myqcloud.com/live/5815_89aad37e06ff11e892905cb9018cf0d4.flv";

    SuperPlayerUrl url3 = SuperPlayerUrl();
    url3.title = "FHD";
    url3.url = "http://5815.liveplay.myqcloud.com/live/5815_89aad37e06ff11e892905cb9018cf0d4.flv";

    _playerModel.multiVideoURLs = [url1, url2, url3];
    _playerModel.videoURL = url1.url;// Set the default definition for playback
  }
```

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.blueGrey,
        title: const Text('SuperPlayer'),
      ),
      body: Builder(
        builder: (context) =>
        SafeArea(
          child: Container(
            color: Colors.blueGrey,
            child: Column(
              children: [
                AspectRatio(
                    aspectRatio: 16.0/9.0,
                    child:SuperPlayerVideo(
                      onCreated: (SuperPlayerPlatformViewController vc) async {
                        _playerController = vc;
                        await _playerController.setPlayConfig(_playerConfig);
                        await _playerController.playWithModel(_playerModel);// Start playback
                      },
                    )
                ),
              ],
            ),
          ),
        )
      ),
    );
  }

```

You can see these definitions in the player and click them to switch.



## Time Shifting Playback[](id:timeShift)

It is easy to enable time shifting for the player, and you only need to configure the `appId` before playback.

```dart
SuperPlayerViewModel playModel = SuperPlayerViewModel();
playModel.appId = 1252463788;// Replace it with your `appID` here
```

>?`appId` can be viewed in the **Tencent Cloud console** > **[Account Info](https://console.cloud.tencent.com/developer)**.

You can see the progress bar below the live stream being played back and seek to a desired point. You can also click **Return to Live Stream** to watch the latest live stream.



>?The time shifting feature is currently in beta test. If you need to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder) for application.

## Playback Through FileId
In addition to setting the definition by entering the URL, an easier way is playback through `fileId`, which is usually returned by the server after the video is uploaded:
1. After the video is published on the client, the server will return a `fileId` to the client.
2. When the video is uploaded to the server, the corresponding `fileId` will be included in the notification of upload confirmation.


If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media) and find it. After clicking it, you can view the `appId` and `fileId` parameters in the video details on the right.


The code for playback through `fileId` is as follows:

```dart
SuperPlayerViewModel playModel = SuperPlayerViewModel();
playModel.appId = 1252463788;// Replace it with your `appID` here
SuperPlayerVideoId videoId = SuperPlayerVideoId();
videoId.fileId = "4564972819219071679";
playModel.videoId = videoId;

_playerController.playWithModel(playModel);
```

After the video is uploaded, it will be automatically transcoded on the backend (for all transcoding formats, please see [Transcoding Template](https://console.cloud.tencent.com/vod/video-process/template)). After the transcoding is completed, the player will automatically display multiple definitions.

## More Features[](id:moreFeature)

To try out the complete features, scan the QR code below to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
