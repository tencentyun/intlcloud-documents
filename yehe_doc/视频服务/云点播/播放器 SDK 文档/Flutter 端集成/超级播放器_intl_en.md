Tencent Cloud RT-Cube Player for Flutter is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait orientation switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it supports live stream (FLV + RTMP) playback, features instant broadcasting of the first frame and low latency, and offers advanced capabilities, including seamless definition switch and live time shifting.
This player is based on a Flutter plugin of VOD and live playback and supports both Android and iOS. It is open-source, free of charge, and does not restrict the source of playback addresses, so you can use it as desired.

## SDK Download

The Tencent Cloud RT-Cube Player SDK for Flutter can be downloaded [here](https://github.com/LiteAVSDK/Player_Flutter).

## Project Overview

The RT-Cube Player SDK is a subproduct SDK of RT-Cube, which provides excellent VOD and live players based on Tencent Cloud's powerful backend capabilities and AI technologies. It can be used with VOD or CSS to quickly implement smooth and stable playback for various use cases. It allows you to focus on your business while delivering an ultra fast HD playback experience.

This project provides the VOD and live playback which you can use to set up your own playback services.

- [VOD player SDK](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E7%82%B9%E6%92%AD%E6%92%AD%E6%94%BE-EN.md): `TXVodPlayerController` encapsulates the APIs of the VOD player SDKs for Android and iOS. You can integrate it to develop your VOD service. For the detailed code sample, see `DemoTXVodPlayer`.

- [Live player SDK](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E7%9B%B4%E6%92%AD%E6%92%AD%E6%94%BE-EN.md): `TXLivePlayerController` encapsulates the APIs of the live player SDKs for Android and iOS. You can integrate it to develop your live playback service. For the detailed code sample, see `DemoTXLivePlayer`.

To reduce the connection costs, the Player component (player with UIs) is provided in `example`. You can set up your own video playback service based on a few lines of simple code. You can apply the Player component's code to your project and adjust UI and interaction details based on your project requirements.

- [Player component](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E6%92%AD%E6%94%BE%E5%99%A8%E7%BB%84%E4%BB%B6-EN.md): `SuperPlayerController` is the Superplayer component, which is a secondary encapsulation of the VOD and live player SDKs for quick and easy integration. It is currently in beta testing, and its features are being optimized. For the detailed code sample, see `DemoSuperplayer`.

## Quick Integration

### `pubspec.yaml` configuration
1. Integrate `LiteAVSDK_Player` (which is integrated by default) and add the following configuration to `pubspec.yaml`:
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
```
2. To integrate `LiteAVSDK_Professional`, change the configuration in `pubspec.yaml` as follows:
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: Professional
```
3. Update the dependency packages:
```yaml
flutter packages get
```

### Adding native configuration

#### Android configuration
Add the following configuration to the `AndroidManifest.xml` file of Android:
```xml
<!--network permission-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD player floating window permission -->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

#### iOS configuration
1. Add the following configuration to the `Info.plist` file of iOS:
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```
2. iOS natively uses `pod` for dependency. Edit the `podfile` file and specify your player SDK edition. `TXLiteAVSDK_Player` is integrated by default.
```xml
pod 'TXLiteAVSDK_Player'          // Player Edition
```
3. Integrate SDK Professional Edition.
```
pod 'TXLiteAVSDK_Professional'  // Professional Edition
```

If no edition is specified, the latest version of `TXLiteAVSDK_Player` will be installed by default.

### FAQs about integration
- Run the `flutter doctor` command to check the runtime environment until "No issues found!" is displayed.
- Run `flutter pub get` to ensure that all dependent components have been updated successfully.

## Applying for and Integrating Video Playback License
If you have the required license, you need to get the license URL and key in the [RT-Cube console](https://console.cloud.tencent.com/vcube).

If you don't have the required license, you need to get it as instructed in Video Playback License.

To integrate a player, you need to [sign up for a Tencent Cloud account](https://www.tencentcloud.com/en/account/register), apply for the video playback license, and then integrate the license as follows. We recommend you integrate it during application start.

If no license is integrated, exceptions may occur during playback.
```dart
String licenceURL = ""; // The license URL obtained
String licenceKey = ""; // The license key obtained
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

## Setting the SDK Connection Environment

In order to help you conduct business with higher quality and security in compliance with applicable laws and regulations in different countries and regions, Tencent Cloud provides two SDK connection environments. If you serve global users, we recommend you use the following API to configure the global connection environment.

```dart
// If you serve global users, configure the global SDK connection environment.
SuperPlayerPlugin.setGlobalEnv("GDPR");
```

## Using the VOD Player

The core class of the VOD player is `TXVodPlayerController`. For the detailed demo, see `DemoTXVodPlayer`.
```dart
import 'package:flutter/material.dart';
import 'package:super_player/super_player.dart';

class Test extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _TestState();
}

class _TestState extends State<Test> {
  late TXVodPlayerController _controller;

  double _aspectRatio = 16.0 / 9.0;
  String _url =
          "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";

  @override
  void initState() {
    super.initState();
    String licenceUrl = ""; // The obtained license URL
    String licenseKey = ""; // The obtained license key
    SuperPlayerPlugin.setGlobalLicense(licenceUrl, licenseKey);
    _controller = TXVodPlayerController();
    initPlayer();
  }

  Future<void> initPlayer() async {
    await _controller.initialize();
    await _controller.startPlay(_url);
  }

  @override
  Widget build(BuildContext context) {
    return Container(
            height: 220,
            color: Colors.black,
            child: AspectRatio(aspectRatio: _aspectRatio, child: TXPlayerVideo(controller: _controller)));
  }
}
```
## How to Use the Player Component

The core class of the Player component is `SuperPlayerVideo`, and videos can be played back after it is created.
```dart
import 'package:flutter/material.dart';
import 'package:super_player/super_player.dart';

/// flutter superplayer demo
class DemoSuperplayer extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _DemoSuperplayerState();
}

class _DemoSuperplayerState extends State<DemoSuperplayer> {
  List<SuperPlayerModel> videoModels = [];
  bool _isFullScreen = false;
  SuperPlayerController _controller;

  @override
  void initState() {
    super.initState();
    String licenceUrl = "Enter the URL of the purchased license";
    String licenseKey = "Enter the license key";
    SuperPlayerPlugin.setGlobalLicense(licenceUrl, licenseKey);
    _controller = SuperPlayerController(context);
    FTXVodPlayConfig config = FTXVodPlayConfig();
    config.preferredResolution = 720 * 1280;
    _controller.setPlayConfig(config);
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
    initData();
  }

  @override
  Widget build(BuildContext context) {
    return WillPopScope(
        child: Container(
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

  Widget getBody() {
    return Column(
      children: [_getPlayArea()],
    );
  }

  Widget _getPlayArea() {
    return SuperPlayerView(_controller);
  }

  Widget _getListArea() {
    return Container(
      margin: EdgeInsets.only(top: 10),
      child: ListView.builder(
        itemCount: videoModels.length,
        itemBuilder: (context, i) => _buildVideoItem(videoModels[i]),
      ),
    );
  }

  Widget _buildVideoItem(SuperPlayerModel playModel) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        ListTile(
            leading: Image.network(playModel.coverUrl),
            title: new Text(
              playModel.title,
              style: TextStyle(color: Colors.white),
            ),
            onTap: () => playCurrentModel(playModel)),
        Divider()
      ],
    );
  }

  void playCurrentModel(SuperPlayerModel model) {
    _controller.playWithModel(model);
  }

  void initData() async {
    SuperPlayerModel model = SuperPlayerModel();
    model.videoURL = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/48d0f1f9387702299774251236/gZyqjgaZmnwA.m4v";
    model.playAction = SuperPlayerModel.PLAY_ACTION_AUTO_PLAY;
    model.title = "Tencent Cloud Audio/Video";
    _controller.playWithModel(model);
  }
  
  @override
  void dispose() {
    // must invoke when page exit.
    _controller.releasePlayer();
    super.dispose();
  }
}
```

## Custom Development Guide 

The Player SDK for Flutter plugin encapsulates native player capabilities. We recommend you use the following methods for deep custom development:

- Perform custom development based on VOD playback (the API class is `TXVodPlayerController`) or live playback (the API class is `TXLivePlayerController`). The project provides custom development demos in `DemoTXVodPlayer` and `DemoTXLivePlayer` in the `example` project.

- The Player component `SuperPlayerController` encapsulates VOD and live playback and provides simple UI interaction. The code is in the `example` directory. You can customize the Player component as follows:

  Copy the Player component code in `exmple/lib/superplayer` to your project for custom development.

## More features

To experience all features, scan the QR code to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
