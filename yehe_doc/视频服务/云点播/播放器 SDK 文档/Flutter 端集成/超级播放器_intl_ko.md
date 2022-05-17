Flutter용 Tencent Cloud RT-Cube Superplayer는 오픈 소스 Tencent Cloud 플레이어 컴포넌트입니다. 몇 줄의 코드로 Tencent Video와 유사한 강력한 재생 기능을 사용할 수 있습니다. 가로/세로 방향 전환, 화질 선택, 제스처 및 작은 창 재생과 같은 기본 기능과 비디오 버퍼링, 소프트웨어/하드웨어 디코딩 전환 및 재생 속도 조정 등 특수 기능이 있습니다. 시스템 기본 플레이어보다 더 많은 형식을 지원하고 더 나은 호환성과 기능을 제공합니다. 또한 라이브 스트림(flv + rtmp) 재생을 지원하고 첫 번째 프레임 바로 재생과 저지연 성능을 제공하며 끊김 없는 해상도 전환 및 라이브 타임 시프팅을 포함한 고급 기능을 제공합니다.

이 플레이어는 SuperPlayer의 Flutter 플러그 인을 기반으로 하며 Android와 iOS를 모두 지원합니다. 무료 오픈소스이며 재생주소의 출처를 제한하지 않으므로 원하는 대로 사용할 수 있습니다.

## SDK 다운로드

Flutter용 Tencent Cloud RT-Cube Superplayer SDK는 [SuperPlayer Flutter](https://github.com/tencentyun/SuperPlayer/tree/main/Flutter)에서 다운로드할 수 있습니다. 

## 타겟 오디언스

이 문서는 Tencent Cloud의 독점 기능에 대해 설명합니다. 읽기 전에 관련 [Tencent Cloud](https://cloud.tencent.com) 서비스를 활성화했는지 확인하십시오. 계정을 등록하지 않은 경우 먼저 [무료 평가판](https://intl.cloud.tencent.com/login)에 등록하십시오.

## 통합 가이드[](id:Guide)

1. `pubspec.yaml`에 다음 구성을 추가합니다.
```yaml
  super_player:
    git:
      url: https://github.com/tencentyun/SuperPlayer
      path: Flutter
```

2. 종속성 패키지를 업데이트합니다.
```yaml
   flutter pub upgrade
```
4. 네이티브 구성을 추가합니다.

### Android 구성[](id:Android_config)

Android의 `AndroidManifest.xml` 파일에 다음 구성을 추가합니다.

```xml
<!--네트워크 권한-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VOD 플레이어 플로팅 창 권한-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--저장-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

Android에서 Superplayer는 기본 플레이어 SDK에 따라 다릅니다. 디렉터리의 `example/android/superplayerkit` 폴더를 프로젝트 디렉터리에 복사하고 `include ':superplayerkit'`을 `setings.gradle`에 삽입합니다. 공식 웹 사이트에서 적절한 버전을 다운로드하여 가져올 수도 있습니다.

### iOS 구성[](id:iOS_config)

iOS의 `Info.plist` 파일에 다음 구성을 추가합니다.
```xml
    <key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```

iOS는 기본적으로 종속성을 위해 `pod`를 사용합니다. `podfile` 파일을 편집하고 플레이어 버전을 지정하십시오.
```xml
pod 'SuperPlayer/Player', '3.3.9'
```

버전을 지정하지 않으면 기본적으로 최신 버전의 `SuperPlayer`가 설치됩니다.

### Flutter 호출[](id:Flutter_call)

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
                            await _playerController.playWithModel(_playerModel);// 재생 시작
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



## 플레이어 사용[](id:usePlayer)

플레이어의 메인 클래스는 `SuperPlayerVideo`이며, 비디오를 생성한 후 재생할 수 있습니다.

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
                                            await _playerController.playWithModel(_playerModel);// 재생 시작
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

코드를 실행하면 비디오가 휴대폰에서 재생되며, 인터페이스 대부분의 기능을 사용할 수 있음을 확인할 수 있습니다.

## 다중 해상도[](id:resolution)

상기 샘플 코드에는 하나의 해상도만 지정되어 있습니다. 여러 해상도를 추가하는 것은 쉽습니다. 예를 들어 [CSS 콘솔](https://console.cloud.tencent.com/live/livemanage)을 열고 재생할 라이브 스트림을 찾은 다음 세부 정보 페이지로 들어갑니다.


여기에서 서로 다른 해상도와 형식에 대해 서로 다른 재생 주소가 제공됩니다. 재생에는 FLV 주소를 사용하는 것이 좋습니다. 코드는 다음과 같습니다.

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
    _playerModel.videoURL = url1.url;// 재생을 위한 기본 해상도 설정
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
                        await _playerController.playWithModel(_playerModel);// 재생 시작
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

플레이어에서 이러한 해상도를 보고 클릭하여 전환할 수 있습니다.

## 타임 시프트 재생[](id:timeShift)

플레이어에 대한 시간 이동을 활성화하는 것은 쉽고 재생하기 전에 appId를 구성하기만 하면 됩니다.

```dart
SuperPlayerViewModel playModel = SuperPlayerViewModel();
playModel.appId = 1252463788;// 사용자의 appID로 변경
```

>?appId는 [Tencent Cloud 콘솔]>[[계정 정보](https://console.cloud.tencent.com/developer)]에서 볼 수 있습니다.

재생 중인 라이브 스트림 아래에 진행률 표시줄이 표시되고 원하는 지점으로 탐색할 수 있습니다. [라이브 스트림으로 돌아가기]를 클릭하여 최신 라이브 스트림을 볼 수도 있습니다.

>?타임 시프트 기능은 현재 베타 테스트 중입니다. 사용이 필요한 경우에는 [티켓 제출](https://console.cloud.tencent.com/workorder)하여 신청하십시오.

## FileId를 통한 재생
url을 입력하여 해상도를 설정하는 것 외에도 더 쉬운 방법은 fileId를 통해 재생하는 것입니다. 이 fileId는 일반적으로 비디오가 업로드된 후 서버에서 반환됩니다.
1. 비디오가 클라이언트에 게시된 후 서버는 클라이언트에 fileId를 반환합니다.
2. 동영상이 서버에 업로드되면 업로드 확인 알림에 해당 fileId가 포함됩니다.


파일이 이미 Tencent Cloud에 있는 경우 [미디어 자산](https://console.cloud.tencent.com/vod/media)으로 이동하여 찾을 수 있습니다. 클릭 후 오른쪽의 동영상 세부정보에서 appId 및 fileId 매개변수를 볼 수 있습니다.


fileId를 통한 재생 코드는 다음과 같습니다.

```dart
SuperPlayerViewModel playModel = SuperPlayerViewModel();
playModel.appId = 1252463788;// 사용자의 appID로 변경
SuperPlayerVideoId videoId = SuperPlayerVideoId();
videoId.fileId = "4564972819219071679";
playModel.videoId = videoId;

_playerController.playWithModel(playModel);
```

비디오가 업로드되면 백엔드에서 자동으로 트랜스 코딩됩니다(모든 트랜스 코딩 형식은 [트랜스 코딩 템플릿](https://console.cloud.tencent.com/vod/video-process/template) 참고). 트랜스 코딩이 완료되면 플레이어는 자동으로 여러 해상도를 표시합니다.

## 더 많은 기능[](id:moreFeature)

모든 기능을 경험하려면 QR 코드를 스캔하여 Tencent Video Cloud 툴킷을 다운로드하거나 프로젝트 Demo를 직접 실행하십시오.
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
