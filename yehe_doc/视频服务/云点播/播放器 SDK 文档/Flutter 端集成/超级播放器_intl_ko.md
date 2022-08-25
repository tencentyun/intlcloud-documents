Flutter용 Tencent Cloud RT-Cube Superplayer는 오픈 소스 Tencent Cloud 플레이어 컴포넌트입니다. 몇 줄의 코드로 Tencent Video와 유사한 강력한 재생 기능을 사용할 수 있습니다. 가로/세로 방향 전환, 화질 선택, 제스처 및 작은 창 재생과 같은 기본 기능과 비디오 버퍼링, 소프트웨어/하드웨어 디코딩 전환 및 재생 속도 조정 등 특수 기능이 있습니다. 시스템 기본 플레이어보다 더 많은 형식을 지원하고 더 나은 호환성과 기능을 제공합니다. 또한 라이브 스트림(FLV + RTMP) 재생을 지원하고 첫 번째 프레임 바로 재생과 저지연 성능을 제공하며 끊김 없는 해상도 전환 및 라이브 타임 시프팅을 포함한 고급 기능을 제공합니다.
이 플레이어는 SuperPlayer의 Flutter 플러그 인을 기반으로 하며 Android와 iOS를 모두 지원합니다. 무료 오픈소스이며 재생주소의 출처를 제한하지 않으므로 원하는 대로 사용할 수 있습니다.

## SDK 다운로드

Flutter용 Tencent Cloud RT-Cube Superplayer SDK는 [SuperPlayer Flutter](https://github.com/LiteAVSDK/Player_Flutter/tree/main/Flutter)에서 다운로드할 수 있습니다.

## 프로젝트 개요

RT-Cube·Player SDK는 Tencent Cloud의 강력한 백엔드 기능과 AI 기술을 기반으로 우수한 VOD 및 라이브 플레이어를 제공하는 RT-Cube의 하위 제품 SDK입니다. VOD 또는 CSS와 함께 사용하여 다양한 사용 사례에 대해 부드럽고 안정적인 재생을 빠르게 구현할 수 있습니다. 초고속 HD 재생 경험을 제공하면서 비즈니스에 집중할 수 있도록 지원합니다.

이 프로젝트는 자신의 재생 서비스를 설정하는 데 사용할 수 있는 VOD 및 라이브 플레이어 SDK를 제공합니다:

- [VOD 플레이어 SDK](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E7%82%B9%E6%92%AD%E6%92%AD%E6%94%BE-EN.md): `TXVodPlayerController`는 Android 및 iOS용 VOD 플레이어 SDK의 API를 캡슐화합니다. `TXVodPlayerController`를 통합하여 VOD 서비스를 개발할 수 있습니다. 자세한 코드 샘플은 `DemoTXVodPlayer`를 참고하십시오.

- [라이브 플레이어 SDK](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E7%9B%B4%E6%92%AD%E6%92%AD%E6%94%BE-EN.md): `TXLivePlayerController`는 Android 및 iOS용 라이브 플레이어 SDK의 API를 캡슐화합니다. `TXLivePlayerController`를 통합하여 라이브 재생 서비스를 개발할 수 있습니다. 자세한 코드 샘플은 `DemoTXLivePlayer`를 참고하십시오.

연결 비용을 줄이기 위해 example로 Superplayer 컴포넌트(UI가 있는 플레이어)가 제공됩니다. 몇 줄의 간단한 코드를 기반으로 자신의 비디오 재생 서비스를 설정할 수 있습니다. Superplayer 코드를 프로젝트에 적용하고 프로젝트 요구 사항에 따라 UI 및 인터랙션 세부 정보를 조정할 수 있습니다.

- [Superplayer 컴포넌트](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/%E6%92%AD%E6%94%BE%E5%99%A8%E7%BB%84%E4%BB%B6-EN.md): `SuperPlayerController`는 VOD와 라이브 플레이어 SDK를 결합한 Superplayer 컴포넌트입니다. 현재 베타 테스트 중이며 기능이 최적화되고 있습니다. 자세한 코드 샘플은 DemoSuperplayer를 참고하십시오.

## 빠른 통합

### pubspec.yaml 구성
LiteAVSDK_Player(기본적으로 통합됨)를 통합하고 `pubspec.yaml`에 다음 구성을 추가합니다:
```yaml
super_player:
  git:
    url: https://github.com/tencentyun/SuperPlayer
    path: Flutter
```
2. LiteAVSDK_Professional을 통합하려면 `pubspec.yaml`의 구성을 다음과 같이 변경하십시오:
```yaml
super_player:
  git:
    url: https://github.com/tencentyun/SuperPlayer
    path: Flutter
    ref: Professional
```
3. 종속성 패키지를 업데이트합니다:
```yaml
flutter packages get
```

### 기본 구성 추가

#### Android 구성
Android의 `AndroidManifest.xml` 파일에 다음 구성을 추가합니다:
```xml
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD 플레이어 플로팅 창 권한-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--스토리지-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

#### iOS 구성
1. iOS의 `Info.plist` 파일에 다음 구성을 추가합니다.
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```
2. iOS는 기본적으로 종속성을 위해 `pod`를 사용합니다. `podfile` 파일을 편집하고 플레이어 SDK 버전을 지정하십시오. TXLiteAVSDK_Player는 기본적으로 통합되어 있습니다.
```xml
pod 'TXLiteAVSDK_Player'        //Player 에디션
```
3. SDK Professional Edition을 통합합니다:
```
pod 'TXLiteAVSDK_Professional' //Professional 에디션
```

에디션을 지정하지 않으면 기본적으로 최신 버전의 `TXLiteAVSDK_Player`가 설치됩니다.

### 통합에 대한 FAQ
- `flutter doctor` 명령을 실행하여, “No issues found!”가 표시될 때까지 런타임 환경을 확인하십시오.
- `flutter pub get`을 실행하여 모든 종속 컴포넌트가 성공적으로 업데이트되었는지 확인하십시오.


## VOD 플레이어 사용
VOD 플레이어의 핵심 클래스는 `TXVodPlayerController`입니다. 자세한 Demo는 `DemoTXVodPlayer`를 참고하십시오.
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
    String licenceUrl = ""; // 획득한 licence url
    String licenseKey = ""; // 획득한 licence key
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
## Superplayer 사용
Superplayer의 핵심 클래스는 `SuperPlayerVideo`이며, 비디오를 생성한 후 재생할 수 있습니다.
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
    String licenceUrl = "구매한 license의 url 입력";
    String licenseKey = "구매한 license의 key 입력";
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
    model.title = "Tencent Cloud 오디오/비디오";
    _controller.playWithModel(model);
  }
}
```

## 사용자 정의 개발 가이드 

Flutter 플러그 인용 Player SDK는 기본 플레이어 기능을 캡슐화합니다. 심층 사용자 정의 개발을 위해 다음 방법을 사용하는 것이 좋습니다.

- VOD 플레이어 SDK(API 클래스는 `TXVodPlayerController`) 또는 라이브 플레이어 SDK(API 클래스는 `TXLivePlayerController`)를 기반으로 사용자 정의 개발을 수행합니다. 이 프로젝트는 example 프로젝트의 `DemoTXVodPlayer` 및 `DemoTXLivePlayer`에서 사용자 정의 개발 Demo를 제공합니다.

- Superplayer 컴포넌트 `SuperPlayerController`는 플레이어 SDK를 캡슐화하고 간단한 UI 인터랙션을 제공합니다. 코드는 example 디렉터리에 있습니다. 다음과 같이 Superplayer 컴포넌트를 사용자 정의할 수 있습니다.

  `exmple/lib/superplayer`의 Superplayer 컴포넌트 코드를 사용자 지정 개발을 위해 프로젝트에 복사합니다.

## 추가 기능

전체 기능을 사용하려면 비디오 클라우드 툴 킷을 다운로드하거나 프로젝트 Demo를 직접 실행하십시오.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
