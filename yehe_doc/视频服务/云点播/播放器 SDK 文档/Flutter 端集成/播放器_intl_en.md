Tencent Cloud RT-Cube Player (Flutter) is an open-source component. You can use it to equip your project with powerful playback capabilities similar to those in Tencent Video with just a few lines of code changes. It offers basic playback features such as landscape/portrait orientation, definition selection, gesture control, and small window playback, as well as special features such as caching, switch between software and hardware decoding, and playback speed change. Compared with built-in players, RT-Cube Player supports more formats, has better compatibility, and offers more features. It also supports live playback (FLV + RTMP), features instant streaming, and low latency, and provides advanced capabilities including seamless definition switch and time shifting.
This player is based on a Flutter plugin for on-demand and live playback and can be used for both Android and iOS. It is open-source, with no restrictions on playback URLs, and free of charge.

## SDK Download

You can download the Player SDK for Flutter [here](https://github.com/LiteAVSDK/Player_Flutter).

## Project Overview

The Player SDK is one of Tencent Cloud’s media SDKs (RT-Cube). It leverages Tencent Cloud’s powerful backend capabilities and AI technologies to offer on-demand and live playback capabilities. You can use it together with VOD or CSS to quickly implement smooth, stable, ultra-fast, and HD playback for various use cases, allowing you to focus more on business development.

The project offers VOD and live playback capabilities that help you set up your own playback services.

- [VOD player](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E7%82%B9%E6%92%AD%E6%92%AD%E6%94%BE-EN.md): `TXVodPlayerController` encapsulates the APIs of the VOD player SDK for Android and iOS. You can use it to set up a VOD service. For code samples, see `DemoTXVodPlayer`.
- [Live player](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E7%9B%B4%E6%92%AD%E6%92%AD%E6%94%BE.md): `TXLivePlayerController` encapsulates the APIs of the live player SDK for Android and iOS. You can use it to set up a live playback service. For code samples, see `DemoTXLivePlayer`.

To simplify the integration process, in `example`, we offer a player component that includes customizable UI elements. With it, you can easily set up your own video playback service with just a few lines of code changes.

- [Player component](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E6%92%AD%E6%94%BE%E5%99%A8%E7%BB%84%E4%BB%B6.md): The player component `SuperPlayerController` encapsulates the VOD player and live player and allows you to integrate playback capabilities more easily and quickly. The component is currently in beta testing. We are still working to improve its features. For code samples, see `DemoSuperplayer`.

## Quick Integration

### Configuring `pubspec.yaml`

1. Integrate `LiteAVSDK_Player` (the default edition). In

   ```
   pubspec.yaml
   ```

   add the following code:

   ```yaml
   super_player:
     git:
       url: https://github.com/LiteAVSDK/Player_Flutter
       path: Flutter
   ```

2. If you want to integrate `LiteAVSDK_Professional`, replace the content in

   ```
   pubspec.yaml
   ```

   with the following:

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

#### Android

Add the following configuration to `AndroidManifest.xml`.

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



#### iOS

1. For iOS, in

   ```
   Info.plist
   ```

   add the following configuration:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
       <key>NSAllowsArbitraryLoads</key>
       <true/>
   </dict>
   ```

2. iOS uses

   ```
   pod
   ```

   to manage dependencies. In

   ```
   podfile
   ```

   specify the SDK to integrate (`LiteAVSDK_Player` by default):

   ```xml
   pod 'TXLiteAVSDK_Player'            //LiteAVSDK_Player
   ```

3. Integrate `LiteAVSDK_Professional`:

   ```
   pod 'TXLiteAVSDK_Professional' // LiteAVSDK_Professional
   ```

If you do not specify the edition, the latest version of `TXLiteAVSDK_Player` will be installed.

### Troubleshooting

- Run the `flutter doctor` command to check the runtime environment until "No issues found!" is displayed.
- Run `flutter pub get` to ensure that all dependent components have been updated successfully.

## Obtaining and Configuring the Video Playback License

If you have obtained a license, you can view the license URL and key in the [RT-Cube console](https://console.cloud.tencent.com/vcube).
If you don’t have a license yet, please [contact us](https://intl.cloud.tencent.com/contact-us) to get a license.

Before you integrate the player, you need to [sign up for a Tencent Cloud account](https://cloud.tencent.com/login), apply for the video playback license, and configure the license as follows (we recommend you do this when the application is launched):

If you don’t configure a license, errors may occur during playback.

```dart
String licenceURL = ""; // The license URL obtained
String licenceKey = ""; // The license key obtained
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```



## Using the VOD Player

The core class of the VOD player is `TXVodPlayerController`. For the demo, see `DemoTXVodPlayer`.
Since v10.7.0, you need to call {@link SuperPlayerPlugin#setGlobalLicense} to set the license in order to use the playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the playback feature. If you don’t have any of the licenses, you can apply for a trial license for free or buy an official license.



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
    String licenceUrl = ""; // The license URL obtained
    String licenseKey = ""; // The license key obtained
    SuperPlayerPlugin.setGlobalLicense(licenceUrl, licenseKey);
    _controller = TXVodPlayerController();
    initPlayer();
  }

  Future<void> initPlayer() async {
    await _controller.initialize();
    await _controller.startVodPlay(_url);
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



## Using the Player Component

The core class of the player component is `SuperPlayerVideo`. You can create a `SuperPlayerView` object to play videos.
Since v10.7.0, you need to call {@link SuperPlayerPlugin#setGlobalLicense} to set the license in order to use the playback feature (you only need to set the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the playback feature. If you don’t have any of the licenses, you can apply for a trial license for free or buy an official license.



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
    String licenceUrl = "Enter the license URL";
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
    _controller.playWithModelNeedLicence(model);
  }

  void initData() async {
    SuperPlayerModel model = SuperPlayerModel();
    model.videoURL = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/48d0f1f9387702299774251236/gZyqjgaZmnwA.m4v";
    model.playAction = SuperPlayerModel.PLAY_ACTION_AUTO_PLAY;
    model.title = "Tencent Cloud Audio/Video";
    _controller.playWithModelNeedLicence(model);
  }

  @override
  void dispose() {
    // must invoke when page exit.
    _controller.releasePlayer();
    super.dispose();
  }
}
```

## Custom Development

The Flutter plugin of the Player SDK is based on the system’s native player capabilities. You can use either of the following methods for custom development:

- Use the VOD playback API class `TXVodPlayerController` or live playback API class `TXLivePlayerController` for custom development. You can refer to the demos we provide (`DemoTXVodPlayer` and `DemoTXLivePlayer` in `example`).

- The player component `SuperPlayerController` encapsulates VOD playback and live playback capabilities and includes basic UI elements.

  You can copy the code of the player component (in `example/lib/superplayer`) to your project for custom development.

## More

You can scan the QR code below to download the TCToolkit app or run the demo project to try out all features of the Player SDK.
![img](https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png)