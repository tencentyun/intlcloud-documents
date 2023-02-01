## SDK 다운로드

Flutter용 Tencent Cloud RT-Cube Player SDK는 [Player Flutter](https://github.com/LiteAVSDK/Player_Flutter/tree/main/Flutter)에서 다운로드할 수 있습니다.

## 대상

분문의 일부 내용은 Tencent Cloud의 독점적 기능을 설명하고 있습니다. 본문을 읽기 전에 관련 [Tencent Cloud](https://intl.cloud.tencent.com) 서비스를 활성화했는지 확인하십시오. 아직 계정이 없다면 먼저 [가입](https://intl.cloud.tencent.com/login)하고 무료 평가판을 사용해 볼 수 있습니다.

## 내용 요약

* Tencent Cloud RT-Cube Player SDK for Flutter 통합 방법
* Player 컴포넌트를 사용하여 VOD를 재생하는 방법

## Player 컴포넌트 개요

Flutter용 Player 컴포넌트는 Flutter용 Player SDK의 확장입니다. VOD 플레이어와 비교할 때 Player 컴포넌트는 사용하기 쉽고 전체 화면 재생, 해상도 선택, 
진행률 표시줄, 재생 컨트롤, 썸네일 등 더 많은 기능이 통합되어 있습니다. Flutter 비디오 재생 기능을 보다 쉽게 통합하기 위해 Flutter용 Player 컴포넌트를 사용할 수 있습니다.

지원되는 기능:

- 전체 화면 재생

- 재생 중 어댑티브 화면 회전

- 사용자 지정 비디오 썸네일

- 해상도 선택

- 오디오 및 밝기 조정

- 재생 속도 변경

- 하드웨어 가속 활성화/비활성화

- Android 및 iOS의 PiP(Picture-in-picture)

- 이미지 스프라이트 및 키프레임 타임스탬프 정보

  더 많은 기능이 곧 제공될 예정입니다.

## 통합 가이드[](id:Guide)

1. 프로젝트의 example에 있는 `superplayer` 디렉터리를 Flutter 프로젝트에 복사
2. 플레이어가 필요한 페이지에서 다음과 같이 `superplayer`의 종속성 패키지 가져오기
```dart
import 'superplayer/demo_superplayer_lib.dart';
```

## SDK 통합[](id:stepone)

### 1단계: 비디오 재생 License 신청 및 통합[](id:step1)

플레이어를 통합하기 전에 [Tencent Cloud 계정을 등록](https://intl.cloud.tencent.com/login)한 후, 비디오 재생 License를 신청하고, 다음과 같이 License를 구성해야 합니다. 애플리케이션이 시작될 때 이 작업을 수행하는 것이 좋습니다.

통합 License가 없을 경우 재생 중 예외가 발생할 수 있습니다.

```dart
String licenceURL = ""; // 획득한 licence url
String licenceKey = ""; // 획득한 licence key
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

### 2단계: SDK 액세스 환경 설정

고객 비즈니스의 더 높은 보안성과 품질을 보장하고, 고객이 다양한 국가 및 지역의 법률 및 규정을 준수할 수 있도록 Tencent Cloud는 두 가지 세트의 SDK 액세스 환경을 제공합니다. 글로벌 사용자에게 서비스를 제공하는 경우 다음 인터페이스를 사용하여 글로벌 액세스 환경을 구성하는 것이 좋습니다.

```dart
SuperPlayerPlugin.setGlobalEnv("GDPR");
```

### 3단계: controller 생성[](id:step2)

```dart
SuperPlayerController _controller = SuperPlayerController(context);
```

### 4단계: 플레이어 구성[](id:step3)

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// preferredResolution이 구성되지 않은 경우 멀티 비트레이트 비디오 재생 중에 720 * 1280 해상도 스트림이 우선적으로 재생됨
config.preferredResolution = 720 * 1280;
_controller.setPlayConfig(config);
```

FTXVodPlayConfig의 자세한 구성은 Flutter용 VOD 플레이어 SDK의 플레이어 구성 API를 참고하십시오.

### 5단계: 이벤트 수신 구성[](id:step4)

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

### 6단계: 레이아웃 추가[](id:step5)

```dart
Widget _getPlayArea() {
    return Container(
    height: 220,
    child: SuperPlayerView(_controller),
  );
}
```

### 7단계: 뒤로 가기 버튼 클릭 이벤트 수신[](id:step6)

반환 이벤트가 트리거될 때 플레이어가 전체 화면 모드인 경우 전체 화면 모드가 먼저 종료되고 반환 이벤트가 다시 트리거될 때만 페이지가 종료되도록 반환 이벤트에 대한 수신 대기를 추가합니다.
**전체 화면 재생 모드에서 페이지를 바로 종료하려면 수신을 구현할 필요가 없습니다.**

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

### 8단계: 재생 시작[](id:step7)
<dx-tabs>
::: url 방식
```dart
SuperPlayerModel model = SuperPlayerModel();
model.videoURL = "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";
_controller.playWithModelNeedLicence(model);
```
:::

::: fileId 방식
```dart
SuperPlayerModel model = SuperPlayerModel();
model.appId = 1500005830;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "8602268011437356984";
// psign은 Player 서명입니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://www.tencentcloud.com/document/product/266/38099
model.videoId.pSign = "psignXXX"
_controller.playWithModelNeedLicence(model);
```

[미디어 자산](https://console.cloud.tencent.com/vod/media)에서 타깃 비디오 파일을 찾아 파일 이름 하단의 FileId를 볼 수 있습니다.

FileId를 통해 비디오를 재생하면 플레이어는 실제 재생 URL에 대한 백엔드를 요청합니다. 네트워크가 비정상적이거나 FileId가 존재하지 않는 경우 SuperPlayerViewEvent.onSuperPlayerError 이벤트가 수신됩니다.

:::
</dx-tabs>


### 9단계: 재생 중지[](id:step8)

재생 중지 시(특히 다음 startVodPlay 호출 전에), **controller 종료 메소드를 호출하는 것을 기억하십시오.** 이렇게 하면 메모리 누수 및 화면 깜박임 문제를 방지할 수 있을 뿐만 아니라 페이지를 종료할 때 재생이 중지되도록 할 수 있습니다.
```dart
  @override
void dispose() {
  // must invoke when page exit.
  _controller.releasePlayer();
  super.dispose();
}
```

## Player 컴포넌트 API[](id:sdkList)

### 1. 비디오 재생하기

**참고**

10.7 버전부터 startPlay는 startVodPlay로 대체되며 {@link SuperPlayerPlugin#setGlobalLicense}를 사용하여 Licence를 설정한 후에만 재생이 성공합니다. 그렇지 않으면 재생에 실패합니다(검은 화면이 나타남). Licence는 전역적으로 한 번만 설정하면 됩니다. CSS, UGSV 또는 비디오 재생에 Licence를 사용할 수 있습니다. 그러한 Licence가 없다면 [빠르게 무료 평가판 Licence 신청](https://www.tencentcloud.com/document/product/266/51098) 또는 공식 Licence를 [구매](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)할 수 있습니다.

**설명**

이 API는 비디오 재생을 시작하는 데 사용됩니다.

**API**

```dart
_controller.playWithModelNeedLicence(model);
```

**매개변수 설명**

1. SuperPlayerModel

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| appId | int | fileId를 통한 재생에 필요한 애플리케이션의 appId |
| videoURL | String | url을 통한 재생에 필요한 비디오 url |
| multiVideoURLs | List<String> | 멀티 비트레이트 url을 통한 재생에 필요한 멀티 비트레이트 재생 url |
| defaultPlayIndex | int | multiVideoURLs와 함께 사용되는 기본 재생 비트레이트 넘버 |
| videoId | SuperPlayerVideoId | fileId 스토리지 객체, 하기 상세 설명 참고 |
| title | String | 비디오 제목, 이를 사용하여 제목을 사용자 지정하고 플레이어가 서버에서 내부적으로 요청한 제목을 덮어쓸 수 있음 |
| coverUrl | String | Tencent 서버에서 가져온 썸네일 이미지로 SuperVodDataLoader에서 값이 자동으로 할당됨 |
| customeCoverUrl | String | 사용자 지정 비디오 썸네일, 이 매개변수는 우선적으로 사용되며 비디오 썸네일을 사용자 지정하는 데 사용됨 |
| duration | int | 비디오 재생 지속 시간(초) |
| videoDescription | String | 비디오 설명 |
| videoMoreDescription | String | 자세한 비디오 설명 |
| playAction | int | action에는 PLAY_ACTION_AUTO_PLAY, PLAY_ACTION_MANUAL_PLAY 및 PLAY_ACTION_PRELOAD가 포함되며 매개변수의 의미는 아래 설명 참고 |

2. SuperPlayerVideoId

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| fileId | String | 파일 id. 필수 입력 |
| psign | String | 플레이어 서명. 서명 소개 및 생성 방법. |

3. playAction

 -  PLAY_ACTION_AUTO_PLAY : playWithModel이 호출되면 비디오가 자동으로 재생됩니다.
 -  PLAY_ACTION_MANUAL_PLAY : playWithModel 호출 후 비디오를 수동으로 재생해야 합니다. 플레이어는 비디오를 로딩하지 않고 썸네일 이미지만 표시하므로 PLAY_ACTION_PRELOAD에 비해 비디오 재생 리소스를 전혀 소모하지 않습니다.
 -  PLAY_ACTION_PRELOAD : 플레이어는 썸네일 이미지를 표시하고 playWithModel이 호출된 후 비디오 재생을 시작하지 않지만 비디오는 로딩됩니다. PLAY_ACTION_MANUAL_PLAY보다 빠르게 재생을 시작할 수 있습니다.

### 2. 재생 일시 중지

**설명**

이 API는 비디오 재생을 일시 중지하는 데 사용됩니다

**API**

```dart
_controller.pause();
```

### 3. 재생 재개

**설명**

이 API는 재생을 재개하는 데 사용됩니다

**API**

```dart
_controller.resume();
```
### 4. 재생 다시 시작하기

**설명**

이 API는 비디오 재생을 다시 시작하는 데 사용됩니다

**API**

```dart
_controller.reStart();
```

### 5. 플레이어 재설정

**설명**

이 API는 플레이어 상태를 재설정하고 비디오 재생을 중지하는 데 사용됩니다

**API**

```dart
_controller.resetPlayer();
```

### 6. 플레이어 릴리스

**설명**

이 API는 플레이어 리소스를 릴리스하고 비디오 재생을 중지하는 데 사용됩니다. 호출된 후에는 controller를 더 이상 재사용할 수 없습니다.

**API**

```dart
_controller.releasePlayer();
```

### 7. 플레이어 뒤로 가기 이벤트

**설명**

이 API는 전체 화면 재생 모드에서 뒤로 가기 버튼을 클릭했을 때 수행할 작업을 결정하는 데 사용됩니다. true가 반환되면 전체 화면 모드가 종료되고 뒤로 가기 버튼 클릭 이벤트가 소비됩니다. false가 반환되면 이벤트가 사용되지 않습니다.

**API**

```dart
_controller.onBackPress();
```

### 8. 해상도 전환

**설명**

이 API는 실시간으로 재생되는 비디오의 해상도를 전환하는 데 사용됩니다

**API**

```dart
_controller.switchStream(videoQuality);
```

**매개변수 설명**

재생이 시작된 후 _controller.currentQualiyList(해상도 옵션) 및 _controller.currentQuality(기본 해상도)를 통해 videoQuality의 유효한 값을 가져올 수 있습니다. **해상도 전환 기능이 Player 컴포넌트에 통합되었습니다. 전체 화면 모드에서 오른쪽 하단에 있는 버튼을 클릭하여 해상도를 전환할 수 있습니다.**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| index | int | 해상도 넘버 |
| bitrate | int | 해상도 비트레이트 |
| width | int | 해상도 비디오 너비 |
| height | int | 해상도 비디오 높이 |
| name | String | 해상도 약칭 |
| title | String | 표시된 해상도 이름 |
| url | String | 해상도 url, 멀티 비트레이트의 해상도 url, 선택 사항 |

### 9. 재생 진행률 조정(seek)

**설명**

이 API는 현재 비디오 재생 진행률을 조정하는 데 사용됩니다

**API**

```dart
_controller.seek(progress);
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| progress | double | 목표 시간(초) |

### 10. SuperPlayer 컴포넌트 구성

**설명**

이 API는 Superplayer 컴포넌트를 구성하는 데 사용됩니다

**API**

```dart
_controller.setPlayConfig(config);
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| connectRetryCount | int | 플레이어 재접속 횟수, SDK가 예외로 인해 서버에서 연결이 끊어지면 SDK는 서버에 다시 연결을 시도함 |
| connectRetryInterval | int | 두 플레이어 재접속 사이의 간격, SDK가 예외로 인해 서버에서 연결이 끊어지면 SDK는 서버에 다시 연결을 시도함 |
| timeout | int | 플레이어 연결 제한 시간 |
| playerType | int | 플레이어 유형. 0 VOD, 1 라이브 스트리밍, 2 라이브 스트림 리플레이 |
| headers | Map | 사용자 지정 http headers |
| enableAccurateSeek | bool | 정확한 seek 활성화 여부, 기본값: true |
| autoRotate | bool | true로 설정하면 PLAY_EVT_CHANGE_ROTATION 이벤트에서 얻을 수 있는 파일에 설정된 회전 각도에 따라 mp4 파일이 자동으로 회전됨, 기본값: true |
| smoothSwitchBitrate | bool | 원활한 멀티 비트레이트 HLS 스트림 전환 활성화 여부, false(기본값)로 설정하면 멀티 비트레이트 URL이 더 빨리 열리고, true로 설정하면 IDR 프레임이 정렬되었을 때 비트레이트를 부드럽게 전환할 수 있음 |
| cacheMp4ExtName | String | 캐시된 mp4 파일 이름 확장자, 기본값: mp4 |
| progressInterval | int | 진행률 콜백 간격(ms), 설정되지 않은 경우 SDK는 0.5초마다 한 번씩 진행 상황을 콜백함 |
| maxBufferSize | int | 재생 버퍼의 최대 크기(MB), 이 설정은 playableDuration에 영향을 미치며, 값이 클수록 미리 버퍼링된 데이터가 많음 |
| maxPreloadSize | int | 최대 사전 로딩 버퍼 크기(MB) |
| firstStartPlayBufferTime | int | 첫 번째 버퍼링 중에 로딩해야 하는 동영상 데이터 지속 시간(ms), 기본값: 100ms |
| nextStartPlayBufferTime | int | 버퍼링을 중지하기 위한 최소 버퍼링 데이터 크기(버퍼링된 데이터 부족에 대한 보조 버퍼링 또는 seek로 인한 진행률 표시줄 드래그 버퍼링)(ms), 기본값: 250ms |
| overlayKey | String | HLS 보안 강화 암호화 및 암호 해독 key|
| overlayIv | String | HLS 보안 강화 암호화 및 복호화 Iv|
| extInfoMap | Map | 일부 특수 구성 항목 |
| enableRenderProcess | bool | 포스트 렌더링 및 포스트 프로덕션 기능 허용 여부, 기본값: 활성화, 초고해상도 플러그인이 활성화된 후 존재하는 경우 해당 플러그인은 기본적으로 로딩됨 |
| preferredResolution | int | 우선적으로 재생에 사용되는 동영상의 해상도, preferredResolution = width * height |

### 11. 하드웨어 디코딩 활성화/비활성화

**설명**

이 API는 하드웨어 디코딩을 기반으로 재생을 활성화/비활성화하는 데 사용됩니다

**API**

```dart
_controller.enableHardwareDecode(enable);
```

### 12. 재생 상태 가져오기

**설명**

이 API는 재생 상태를 가져오는 데 사용됩니다

**API**

```dart
SuperPlayerState superPlayerState = _controller.getPlayerState();
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| INIT | SuperPlayerState | 초기 상태 |
| PLAYING | SuperPlayerState | 재생 중 |
| PAUSE | SuperPlayerState | 일시중지됨 |
| LOADING | SuperPlayerState | 로딩 중 |
| END | SuperPlayerState | 재생 종료 |

### 13. PiP 모드로 들어가기

**설명**

이 API는 PiP 모드에서 현재 비디오를 표시하는 데 사용됩니다. PiP 모드는 android 7.0 이상에서 지원되는 장치 모델에서만 활성화할 수 있습니다.

**API**

```dart
_controller.enterPictureInPictureMode(
backIcon: "images/ic_pip_play_replay.png",
playIcon: "images/ic_pip_play_normal.png",
pauseIcon: "images/ic_pip_play_pause.png",
forwardIcon: "images/ic_pip_play_forward.png");
```

**매개변수 설명**

매개변수는 android에만 적용됩니다.

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| backIcon | String | 뒤로 가기 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| playIcon | String | 재생 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| pauseIcon | String | 일시 중지 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| forwardIcon | String | 앞으로 가기 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |

## 이벤트 알림

### 1. 재생 상태 수신

**설명**

이 콜백은 캡슐화 후 비디오 재생 상태 및 상태 변경을 수신하는 데 사용됩니다

**코드**

```dart
_playController.onPlayStateBroadcast.listen((event) {
  SuperPlayerState state = event['event'];
});
```

**이벤트 설명**

열거 클래스 SuperPlayerState는 이벤트를 전송하는 데 사용됩니다

| 상태 | 의미               |
| ------ |------------------ |
| INIT | 초기 상태 |
| PLAYING | 재생 중 |
| PAUSE | 일시중지됨 |
| LOADING  |로딩 중 |
| END | 재생 종료 |

### 2. 재생 이벤트 수신

**설명**

이 콜백은 플레이어 작업 이벤트를 수신하는 데 사용됩니다

**코드**

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

**이벤트 설명**


| 상태 | 의미               |
| ------ |------------------ |
| onStartFullScreenPlay | 전체 화면 재생 모드 시작 |
| onStopFullScreenPlay | 전체 화면 재생 모드 종료 |
| onSuperPlayerDidStart | 재생 시작됨 |
| onSuperPlayerDidEnd  | 재생 종료됨 |
| onSuperPlayerError | 재생 오류 |
| onSuperPlayerBackAction | 반환 이벤트 |

## 고급 기능

### 1. fileId를 통해 비디오 데이터를 미리 요청하기

SuperVodDataLoader API를 사용하여 비디오 데이터를 사전에 요청하여 재생 시작 프로세스를 가속화할 수 있습니다

**예시 코드**

```dart
SuperPlayerModel model = SuperPlayerModel();
model.appId = 1500005830;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "8602268011437356984";
model.title = "VOD";
SuperVodDataLoader loader = SuperVodDataLoader();
// model의 필수 매개변수 값은 SuperVodDataLoader에서 직접 할당됨
loader.getVideoData(model, (resultModel) {
  _controller.playWithModelNeedLicence(resultModel);
})
```


### 2. PiP 모드 사용하기

#### 1. Android 플랫폼 구성

1.1 프로젝트의 android 패키지에서 AndroidManifest.xml을 열고 프로젝트 항목의 activity 노드 아래에 다음 구성을 추가합니다

```xml
android:supportsPictureInPicture="true"
android:resizeableActivity="true"
android:configChanges="screenSize|smallestScreenSize|screenLayout|orientation"

// 프로젝트의 android 패키지에서 build.gralde를 열고 compileSdkVersion 및 targetSdkVersion의 버전이 모두 31 이상인지 확인
```

1.2 pip activity 상속

github 프로젝트의 example/android에서 FTXFlutterPipActivity.java를 Activity 항목과 동일한 디렉터리에 복사하고 Activity의 상위 클래스를 이 클래스로 변경합니다.

#### 2. iOS 플랫폼 구성
   2.1 프로젝트 target에서 Signing & Capabilities를 선택하고 + Capability를 클릭하여 Background Modes를 추가하고 Audio,AirPlay,and Picture in Picture를 선택합니다.

#### 3. superPlayer 샘플 코드 복사

github 프로젝트의 example/lib에서 superplayer 패키지를 프로젝트의 lib 디렉터리에 복사하고 샘플 코드의 demo_superplayer.dart에 지시된 대로 Player 컴포넌트를 통합합니다.
그 다음 SuperPlayer 컴포넌트의 재생 UI 오른쪽 중앙에 PiP 모드 버튼이 보이고 버튼을 클릭하면 PiP 모드로 들어갈 수 있습니다.

#### 4. PiP 모드의 라이프사이클에서 수신

다음과 같이 SuperPlayerPlugin에서 onExtraEventBroadcast를 사용하여 PiP 모드의 라이프사이클을 수신할 수 있습니다.

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

#### 5. PiP 모드 진입 오류 코드

사용자가 PiP 모드에 들어가지 못하면 실패가 log될 뿐만 아니라 toast를 통해 메시지가 표시됩니다. superplayer_widget.dart의 _onEnterPipMode 메소드에서 오류 처리 작업을 수정할 수 있습니다. 오류 코드는 아래와 같습니다.

| 매개변수 | 코드   | 설명               |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | 시작 성공, 오류 없음 |
| ERROR_PIP_LOWER_VERSION | -101 | android 버전이 너무 낮음, PiP 모드 미지원 |
| ERROR_PIP_DENIED_PERMISSION | -102 | PiP 모드 권한이 활성화되지 않았거나 현재 장치가 PiP 미지원 |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | 현재 UI가 폐기됨 |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | PiP 미지원(iPad iOS9+에서만 지원됨) | only support iOS|
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | 플레이어가 PiP를 지원하지 않음 | only support iOS|
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | 비디오가 PiP를 지원하지 않음 | only support iOS|
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | PIP 컨트롤러를 사용할 수 없음 | only support iOS|
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | PIP 컨트롤러에서 오류를 보고함 | only support iOS|
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | 플레이어 객체가 존재하지 않음 | only support iOS|
| ERROR_IOS_PIP_IS_RUNNING | -110 | PIP 기능이 이미 실행 중임 | only support iOS|
| ERROR_IOS_PIP_NOT_RUNNING | -111 | PIP 기능이 시작되지 않았음 | only support iOS|

#### 6. 현재 장치가 PiP를 지원하는지 확인

다음과 같이 SuperPlayerPlugin에서 isDeviceSupportPip를 사용하여 PiP 모드를 활성화할 수 있는지 확인할 수 있습니다

```dart
int result = await SuperPlayerPlugin.isDeviceSupportPip();
if(result == TXVodPlayEvent.NO_ERROR) {
  // pip support
}
```

result에 반환된 결과는 PiP 모드의 오류 코드와 동일함을 의미합니다.
