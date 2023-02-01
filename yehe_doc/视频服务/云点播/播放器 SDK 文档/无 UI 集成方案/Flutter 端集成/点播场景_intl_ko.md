## 대상

분문의 일부 내용은 Tencent Cloud의 독점적 기능을 설명하고 있습니다. 본문을 읽기 전에 관련 [Tencent Cloud](https://intl.cloud.tencent.com) 서비스를 활성화했는지 확인하십시오. 아직 계정이 없다면 먼저 [가입](https://intl.cloud.tencent.com/login)하고 무료 평가판을 사용해 볼 수 있습니다.

## 내용 요약
* Tencent Cloud RT-Cube Player SDK for Flutter 통합 방법
* Player SDK를 사용하여 VOD를 재생하는 방법
* Player SDK의 기본 기능을 사용하여 더 많은 기능을 구현하는 방법

## 기본 내용
본 문서는 Player SDK의 VOD 재생 기능에 대해 설명합니다. 먼저 다음 기본 내용을 이해한 후 시작하는 것이 좋습니다.

- **라이브 스트리밍 및 주문형 비디오**
  라이브 스트리밍(LIVE)에서 비디오 소스는 실시간으로 호스트에 의해 푸시됩니다. 호스트가 스트림 푸시를 중지하면 플레이어도 비디오 재생을 중지합니다. 라이브 스트림은 실시간으로 재생되기 때문에 재생 중에는 플레이어에 진행률 표시줄이 표시되지 않습니다.

주문형 비디오(VOD)에서 비디오 소스는 클라우드에 있는 비디오 파일이며 클라우드에서 삭제되지 않는 한 언제든지 재생할 수 있습니다. 재생 진행률을 제어하기 위한 진행률 표시줄이 표시됩니다. Tencent Video 및 Youku Tudou와 같은 비디오 웹사이트에서의 비디오 시청이 전형적인 VOD 시나리오입니다.

- **지원되는 프로토콜**
  일반적인 VOD 프로토콜은 다음과 같습니다. 현재 HLS 형식의 VOD URL(‘http’로 시작하여 ‘.m3u8’로 끝남)이 널리 사용됩니다.
  ![](https://qcloudimg.tencent-cloud.cn/raw/5143d2e31ddbdcb77294fa72b045abb2.jpeg)

## 참고 사항
Player SDK는 **재생 URL 소스를 제한하지 않습니다**. 즉, 이를 사용하여 Tencent Cloud 및 비 Tencent Cloud URL에서 비디오를 재생할 수 있습니다. 그러나 SDK의 플레이어는 FLV, RTMP 및 HLS(m3u8) 형식의 라이브 스트리밍 URL과 MP4, HLS(m3u8) 및 FLV 형식의 VOD URL만 지원합니다.

## SDK 통합[](id:stepone)

### 1단계: SDK[](id:step1) 다운로드 및 통합

SDK 개발 패키지 다운로드 및 통합은 [통합 가이드](https://www.tencentcloud.com/document/product/266/51192)를 참고하십시오.

### 2단계: SDK 액세스 환경 설정

고객 비즈니스의 더 높은 보안성과 품질을 보장하고, 고객이 다양한 국가 및 지역의 법률 및 규정을 준수할 수 있도록 Tencent Cloud는 두 가지 세트의 SDK 액세스 환경을 제공합니다. 글로벌 사용자에게 서비스를 제공하는 경우 다음 인터페이스를 사용하여 글로벌 액세스 환경을 구성하는 것이 좋습니다.

```dart
SuperPlayerPlugin.setGlobalEnv("GDPR");
```

### 3단계: controller 생성[](id:step2)

```dart
TXVodPlayerController _controller = TXVodPlayerController();
```

### 4단계: 이벤트 수신 구성[](id:step3)

```dart
// 비디오 너비 및 높이 변경을 수신하고 적절한 종횡비를 설정합니다. 종횡비를 사용자 정의할 수도 있으며 비디오 텍스처가 비례적으로 늘어납니다.
_controller.onPlayerNetStatusBroadcast.listen((event) async {
  double w = (event["VIDEO_WIDTH"]).toDouble();
  double h = (event["VIDEO_HEIGHT"]).toDouble();

  if (w > 0 && h > 0) {
    setState(() {
      _aspectRatio = 1.0 * w / h;
    });
  }
});
```

### 5단계: 레이아웃 추가[](id:step4)
```dart
@override
Widget build(BuildContext context) {
return Container(
  decoration: BoxDecoration(
      image: DecorationImage(
        image: AssetImage("images/ic_new_vod_bg.png"),
        fit: BoxFit.cover,
      )),
  child: Scaffold(
      backgroundColor: Colors.transparent,
      appBar: AppBar(
        backgroundColor: Colors.transparent,
        title: const Text('VOD'),
      ),
      body: SafeArea(
          child: Container(
            height: 150,
            color: Colors.black,
            child: Center(
              child: _aspectRatio > 0
                  ? AspectRatio(
                aspectRatio: _aspectRatio,
                child: TXPlayerVideo(controller: _controller),
              ) : Container(),
            ),
          ))));
}
```

### 6단계: 플레이어 초기화[](id:step5)

```dart
// 플레이어 초기화 및 공유 텍스처 할당
await _controller.initialize();
```

### 7단계: 재생 시작[](id:step6)
<dx-tabs>
::: url 방식
TXVodPlayerController는 내부적으로 재생 프로토콜을 자동으로 인식합니다. 재생 URL을 startPlay 함수에 전달하기만 하면 됩니다.
```dart
// 비디오 리소스 재생
String _url =
    "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";
await _controller.startVodPlay(_url);
```
:::
::: field 방식
```dart
// psign은 Player 서명입니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://www.tencentcloud.com/document/product/266/38099
TXPlayInfoParams params = TXPlayInfoParams(appId: 1252463788,
        fileId: "4564972819220421305", psign: "psignxxxxxxx");
await _controller.startVodPlayWithParams(params);
```
[미디어 자산](https://console.cloud.tencent.com/vod/media)에서 타깃 비디오 파일을 찾아 파일 이름 하단의 FileId를 볼 수 있습니다.

FileId를 통해 비디오를 재생하면 플레이어가 실제 재생 URL에 대한 백엔드를 요청합니다. 네트워크가 비정상적이거나 FileId가 존재하지 않으면 `TXLiveConstants.PLAY_ERR_GET_PLAYINFO_FAIL` 이벤트가 수신됩니다. 그렇지 않으면 `TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`가 수신되어 요청이 성공했음을 나타냅니다.
:::
</dx-tabs>


### 8단계: 재생 중지[](id:step7)
재생 중지 시(특히 다음 startVodPlay 호출 전에), **controller 종료 메소드를 호출하는 것을 기억하십시오**. 이렇게 하면 메모리 누수 및 화면 깜박임 문제를 방지할 수 있습니다.
```dart
@override
void dispose() {
  _controller.dispose();
  super.dispose();
}
```

## 기본 기능 사용

### 1. 재생 제어

#### 재생 시작

```dart
// 재생 시작
_controller.startVodPlay(url)
```

#### 재생 일시 중지

```dart
// 비디오 일시 중지
_controller.pause();
```

#### 재생 재개

```dart
// 비디오 재개
_controller.resume();
```

#### 재생 중지

```dart
// 비디오 중지
_controller.stopPlay(true);
```

#### 플레이어 중지

```dart
// controller 릴리스
_controller.dispose();
```

#### 재생 진행률 조정(Seek)

사용자가 진행 표시줄을 드래그하면 seek를 호출하여 지정된 위치에서 재생을 시작할 수 있습니다. Player SDK는 정확한 seek를 지원합니다.

```dart
double time = 600; // double, 단위: 초
// 재생 진행률 조정
_controller.seek(time);
```

#### 재생 시작 시간 지정

startVodPlay를 처음 호출하기 전에 재생 시작 시간을 지정할 수 있습니다.

```dart
double startTimeInSecond = 60; // 단위: 초
_controller.setStartTime(startTimeInSecond);   // 재생 시작 시간 설정
_controller.startVodPlay(url);
```

### 2. 조정 가능한 속도 재생

VOD 플레이어는 조정 가능한 속도 재생을 지원합니다. 'setRate' API를 사용하여 VOD 재생 속도를 0.5X, 1.0X, 1.2X, 2X 등으로 설정할 수 있습니다.

```dart
// 1.2 배속으로 재생 설정
_controller.setRate(1.2); 
```

### 3. 재생 루프

```dart
// 재생 루프 설정
_controller.setLoop(true);
// 현재 재생 루프 상태 가져오기
_controller.isLoop(); 
```

### 4. 음소거/음소거 해제

```dart
// 플레이어를 음소거하거나 음소거 해제합니다. true: 음소거, false: 음소거 해제
_controller.setMute(true);
```

### 5. 롤 이미지 광고

Player SDK를 사용하면 다음과 같이 광고용 UI에 롤 이미지를 추가할 수 있습니다.

* 'autoPlay'가 NO로 설정된 경우 플레이어는 비디오를 정상적으로 로딩하지만 즉시 재생을 시작하지는 않습니다.
* 사용자는 플레이어가 로딩된 후 비디오 재생이 시작되기 전에 플레이어 UI에서 롤 이미지 광고를 볼 수 있습니다.
* 광고 표시 중지 조건이 충족되면 resume API가 호출되어 비디오 재생이 시작됩니다.
```dart
_controller.setAutoPlay(false);  // 수동 재생 설정
_controller.startVodPlay(url);    // 비디오는 startPlay가 호출된 후 로딩되며 성공적으로 로딩된 후 자동으로 재생되지 않음
// ......
// 플레이어 UI에 광고 표시
// ......  
_controller.resume();  // 광고가 표시된 후 resume을 호출하여 비디오 재생 시작
```

### 8. HTTP-REF

TXVodPlayConfig의 headers는 URL이 임의로 복사되는 것을 방지하기 위해 일반적으로 사용되는 Referer 필드(Tencent Cloud는 보다 안전한 서명 기반 링크 도용 방지 솔루션 제공) 및 클라이언트 인증을 위한 Cookie 필드와 같이 HTTP 요청 헤더를 설정하는 데 사용할 수 있습니다.

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
Map<String, String> httpHeaders = {'Referer': 'Referer Content'};
playConfig.headers = httpHeaders;
_controller.setConfig(playConfig);
```

### 9. 하드웨어 가속

소프트웨어 디코딩만 사용하면 Blu-ray(1080p) 이상 화질의 비디오를 원활하게 재생하기가 매우 어렵습니다. 따라서 주요 시나리오가 게임 라이브 스트리밍인 경우 하드웨어 가속을 사용하는 것이 좋습니다.

소프트웨어와 하드웨어 디코딩 간에 전환하기 전에 먼저 **stopPlay**를 호출해야 하고, 전환 후 **startVodPlay**를 호출해야 합니다. 그렇지 않으면 심한 흐림 현상이 발생합니다.

```dart
 _controller.stopPlay(true);
 _controller.enableHardwareDecode(true); 
 _controller.startVodPlay(url);
```

### 10. 해상도 설정

SDK는 HLS의 다중 비트 레이트 형식을 지원하므로 사용자는 다른 비트 레이트의 스트림 간에 전환하여 비디오 정의를 전환할 수 있습니다. PLAY_EVT_PLAY_BEGIN 이벤트를 수신한 후 다음과 같이 정의를 설정할 수 있습니다.

```dart
List _supportedBitrates = (await _controller.getSupportedBitrates())!;; //여러 비트레이트의 배열 가져오기
int index = _supportedBitrates[i];  // 재생할 스트림의 비트레이트 첨자 지정
_controller.setBitrateIndex(index);  // 대상 비트 레이트 및 해상도에서 스트림으로 전환
```

재생 중에 언제든지 `_controller.setBitrateIndex(int)`를 호출하여 비트 레이트를 전환할 수 있습니다. 전환하는 동안 다른 스트림의 데이터를 가져옵니다. SDK는 부드러운 전환을 구현하기 위해 Tencent Cloud 다중 비트 레이트 파일에 최적화되어 있습니다.

### 11. 어댑티브 비트 레이트 스트리밍

SDK는 HLS의 어댑티브 비트 레이트 스트리밍을 지원합니다. 이 기능이 활성화되면 플레이어는 현재 대역폭을 기반으로 재생에 가장 적합한 비트 레이트를 동적으로 선택할 수 있습니다. PLAY_EVT_PLAY_BEGIN 이벤트를 수신한 후 다음과 같이 어댑티브 비트 레이트 스트리밍을 활성화할 수 있습니다.

```dart
_controller.setBitrateIndex(-1); //index 매개변수에 -1 전달
```

재생 중에 언제든지 `_controller.setBitrateIndex(int)`를 호출하여 다른 비트 레이트로 전환할 수 있습니다. 전환 후에는 어댑티브 비트 레이트 스트리밍이 비활성화됩니다.

### 12. 매끄러운 비트레이트 전환

비트레이트 전환은 시간이 많이 걸릴 수 있습니다. 사용자 경험을 개선하기 위해 매끄러운 비트레이트 전환을 활성화하여 재생 중에 비트레이트를 부드럽고 매끄럽게 변경할 수 있습니다.

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
/// true로 설정하면 비트레이트를 부드럽게 전환할 수 있으며, false로 설정하면 멀티 비트레이트 URL이 더 빨리 열림
playConfig.smoothSwitchBitrate = true;
_controller.setConfig(playConfig);
```

### 13. 재생 진행 리스닝

VOD 진행률에는 두 가지 지표가 있습니다. **로딩 진행률** 및 **재생 진행률**. 현재 SDK는 이벤트 알림을 통해 실시간으로 두 가지 진행률 지표를 알려줍니다.

`onPlayerEventBroadcast` API를 사용하여 플레이어 이벤트를 수신할 수 있으며 진행률 알림은 **PLAY_EVT_PLAY_PROGRESS** 이벤트를 통해 애플리케이션으로 다시 호출됩니다.

```dart
_controller.onPlayerEventBroadcast.listen((event) async {
  if(event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_PROGRESS) {// 자세한 내용은 iOS 또는 Android의 네이티브 SDK 상태 코드 참고
    // 재생 가능한 시간, 즉 밀리초 단위의 로딩 진행
    double playableDuration = event[TXVodPlayEvent.EVT_PLAYABLE_DURATION_MS].toDouble();
    // 재생 진행률, 단위: 초
    int progress = event[TXVodPlayEvent.EVT_PLAY_PROGRESS].toInt();
    // 총 비디오 지속 시간, 단위: 초
    int duration = event[TXVodPlayEvent.EVT_PLAY_DURATION].toInt();
  }
});
```

### 14. 재생 네트워크 속도 리스닝

`onPlayerNetStatusBroadcast` API를 사용하여 `NET_STATUS_NET_SPEED`와 같은 플레이어 네트워크 상태를 수신할 수 있습니다.

```dart
_controller.onPlayerNetStatusBroadcast.listen((event) {
	(event[TXVodNetEvent.NET_STATUS_NET_SPEED]).toDouble();
});
```

### 15. 비디오 해상도 획득

Player SDK는 URL 문자열을 통해 비디오를 재생합니다. URL에는 비디오 정보가 포함되어 있지 않으며 이러한 정보를 로딩하려면 클라우드 서버에 액세스해야 합니다. 따라서 SDK는 비디오 정보를 이벤트 알림으로만 애플리케이션에 보낼 수 있습니다.

**해상도 정보는 다음 두 가지 방법으로 얻을 수 있습니다**

방법1: `onPlayerNetStatusBroadcast`의 `NET_STATUS_VIDEO_WIDTH` 및 `NET_STATUS_VIDEO_HEIGHT`를 사용하여 비디오 너비 및 높이 가져오기

방법2: 플레이어로부터 PLAY_EVT_VOD_PLAY_PREPARED 이벤트 콜백을 받은 후 `getWidth()` 및 `getHeight()`를 직접 호출하여 현재 비디오 너비와 높이를 가져옵니다.

```dart
 _controller.onPlayerNetStatusBroadcast.listen((event) {
  double w = (event[TXVodNetEvent.NET_STATUS_VIDEO_WIDTH]).toDouble();
  double h = (event[TXVodNetEvent.NET_STATUS_VIDEO_HEIGHT]).toDouble();
});

// 비디오 너비와 높이 가져오기, 값은 플레이어로부터 PLAY_EVT_VOD_PLAY_PREPARED 이벤트 콜백을 수신한 후에만 반환
_controller.getWidth();
_controller.getHeight();
```

### 16. 플레이어 버퍼 크기

일반 비디오 재생 시 네트워크에서 버퍼링되는 데이터의 최대 크기를 미리 조절할 수 있습니다. 최대 버퍼 크기가 구성되지 않은 경우 플레이어는 기본 버퍼 정책을 사용하여 원활한 재생 환경을 보장합니다.

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
playConfig.maxBufferSize = 10;  ///  재생 중 최대 버퍼 크기. 단위: MB
_controller.setConfig(playConfig);
```

### 17. 로컬 비디오 캐시[](id:cache)

짧은 비디오 재생 시나리오에서는 일반 사용자가 이미 시청한 비디오를 다시 로딩하기 위해 트래픽을 다시 소비할 필요가 없도록 로컬 비디오 파일 캐시가 필요합니다.

- **지원되는 형식:** SDK는 HLS(m3u8) 및 MP4의 두 가지 일반적인 VOD 형식으로 비디오 캐시를 지원합니다.
- **활성화 시간:** SDK는 기본적으로 캐시 기능을 활성화하지 않습니다. 대부분의 비디오를 한 번만 시청하는 시나리오에서는 활성화하지 않는 것이 좋습니다.
- **활성화 방법:** 이 기능은 플레이어에서 활성화할 수 있으며 전역으로 적용됩니다. 활성화하려면 로컬 캐시 디렉터리와 캐시 크기라는 두 가지 매개변수를 구성해야 합니다.

```dart
//재생 엔진의 전역 캐시 디렉터리 및 캐시 크기 설정, //단위 MB
SuperPlayerPlugin.setGlobalMaxCacheSize(200);
//재생 엔진의 전역 캐시 디렉터리 설정
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");
```

##  고급 기능 사용

### 1. 비디오 사전 로딩

#### 1단계: 비디오 사전 로딩 사용

UGSV 재생 시나리오에서 사전 로딩 기능은 원활한 시청 환경에 기여합니다. 비디오가 재생 중일 때 백엔드에서 재생할 다음 비디오를 로딩할 수 있습니다. 사용자가 다음 비디오로 전환하면 로딩되어 즉시 재생할 수 있습니다.

비디오 사전 로딩은 즉각적인 재생 효과를 제공할 수 있지만 특정 성능 오버헤드가 있습니다. 회사에서 많은 비디오를 사전 로딩해야 하는 경우 [비디오 사전 다운로드](#download)와 함께 이 기능을 사용하는 것이 좋습니다.

이것이 비디오 재생에서 매끄럽게 전환이 작동하는 방식입니다. TXVodPlayerController에서 setAutoPlay를 사용하여 다음과 같이 기능을 구현할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg)

```dart
// 재생 비디오 A: autoPlay가 true로 설정되어 있으면 startVodPlay가 호출될 때 비디오가 즉시 로딩되어 재생
String urlA = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
controller.setAutoPlay(isAutoPlay: true);
controller.startVodPlay(urlA);

// 비디오 A를 재생할 때 비디오 B를 미리 로딩하려면 setAutoPlay를 false로 설정
String urlB = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
controller.setAutoPlay(isAutoPlay: false);
controller.startVodPlay(urlB); // 비디오는 즉시 재생되지 않지만 로딩되기 시작함
```

비디오 A가 종료되고 비디오 B가 자동 또는 수동으로 전환된 후 resume 기능을 호출하여 비디오 B를 즉시 재생할 수 있습니다.

>! autoPlay를 false로 설정한 후 resume을 호출하기 전에 비디오 B가 준비되었는지 확인하십시오. 즉, 비디오 B의 PLAY_EVT_VOD_PLAY_PREPARED (2013, 플레이어가 준비되었으며 비디오를 재생할 수 있음) 이벤트가 감지된 후에만 호출해야 합니다.


```dart
controller.onPlayerEventBroadcast.listen((event) async {//상태 변경 구독
  if(event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_END) {
    await _controller_A.stop();
    await _controller_B.resume();
  }
});
```

#### 2단계: 비디오 사전 로딩 버퍼 구성

- 불안정한 네트워크 환경에서 보다 원활하게 비디오를 재생하기 위해 큰 버퍼를 설정할 수 있습니다.
- 트래픽 소모를 줄이기 위해 더 작은 버퍼를 설정할 수 있습니다. 

##### 버퍼 크기 사전 로딩

이 API는 사전 로딩 시나리오에서 재생이 시작되기 전에 최대 버퍼 크기를 제어하는 데 사용됩니다(즉, 비디오 재생이 시작되기 전에 player의 AutoPlay가 false로 설정됨).

```dart
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxPreloadSize(2);  // 최대 사전 로딩 버퍼 크기. 단위: MB, 트래픽 소비를 줄이기 위해 비즈니스 상황에 따라 설정
mVodPlayer.setConfig(config);  // config를 mVodPlayer에 전달
```

##### 재생 버퍼 크기 

일반 비디오 재생 시 네트워크에서 버퍼링되는 데이터의 최대 크기를 미리 조절할 수 있습니다. 최대 버퍼 크기가 구성되지 않은 경우 플레이어는 기본 버퍼 정책을 사용하여 원활한 재생 환경을 보장합니다.

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
config.maxBufferSize = 10; // 재생 중 최대 버퍼 크기. 단위: MB
_controller.setPlayConfig(config); // config를 controller에 전달
```

[](id:download)

### 2. 비디오 사전 다운로드

플레이어 인스턴스를 생성하지 않고 미리 비디오 콘텐츠의 일부를 다운로드하여 플레이어를 사용할 때 비디오 재생을 더 빠르게 시작할 수 있습니다. 이는 더 나은 재생 경험을 제공하는 데 도움이 됩니다.

재생 서비스를 이용하시기 전에 [비디오 캐시](#cache)가 설정되어 있는지 확인하십시오.

사용 예시:

```dart
//재생 엔진의 전역 캐시 디렉터리 및 캐시 크기 설정
SuperPlayerPlugin.setGlobalMaxCacheSize(200);
// 캐시 경로는 기본적으로 app의 샌드박스 디렉터리로 설정됩니다. postfixPath에 대한 전체 절대 경로 대신 상대 캐시 디렉터리만 전달하면 됩니다.
// Android 플랫폼: 비디오는 sdcard의 Android/data/your-pkg-name/files/testCache 디렉터리에 캐시됩니다. 
// iOS 플랫폼: 비디오는 샌드박스의 Documents/testCache 디렉터리에 캐시됩니다.
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");

String palyrl = "http://****";
//사전 다운로드 시작
int taskId = await TXVodDownloadController.instance.startPreLoad(palyrl, 3, 1920*1080,
  onCompleteListener:(int taskId,String url) {
    print('taskID=${taskId} ,url=${url}');
  }, onErrorListener: (int taskId, String url, int code, String msg) {
    print('taskID=${taskId} ,url=${url}, code=${code} , msg=${msg}');
  } 
);

//사전 다운로드 취소
TXVodDownloadController.instance.stopPreLoad(taskId);
```

### 3. 비디오 다운로드

비디오 다운로드를 통해 사용자는 온라인 비디오를 다운로드하고 오프라인에서 볼 수 있습니다. 또한 Player SDK는 로컬 암호화 기능을 제공하므로 다운로드한 로컬 파일은 계속 암호화되어 지정된 플레이어에서만 해독 및 재생할 수 있습니다. 이 기능은 다운로드한 비디오가 무단으로 배포되는 것을 효과적으로 방지하고 비디오 보안을 보호할 수 있습니다.

HLS 스트리밍 미디어는 로컬에 직접 저장할 수 없으므로 다운로드하여 로컬 파일로 재생할 수 없습니다. `TXVodDownloadController` 기반의 비디오 다운로드 방식을 사용하여 오프라인 HLS 재생을 구현할 수 있습니다.
>?
>-  현재 `TXVodDownloadController`는 중첩되지 않은 HLS 파일만 캐시할 수 있지만 MP4 및 FLV 파일은 캐시할 수 없습니다.
>-  플레이어 SDK는 이미 로컬 MP4 및 FLV 파일 재생을 지원합니다.

[](id:offline1)

#### 1단계: 준비 작업

`TXVodDownloadController`는 싱글톤으로 설계되었습니다. 따라서 여러 다운로드 객체를 만들 수 없습니다. 다음과 같이 사용됩니다.

```dart
// 캐시 경로는 기본적으로 app의 샌드박스 디렉터리로 설정됩니다. postfixPath에 대한 전체 절대 경로 대신 상대 캐시 디렉터리만 전달하면 됩니다.
// Android 플랫폼: 비디오는 sdcard의 Android/data/your-pkg-name/files/testCache 디렉터리에 캐시됩니다. 
// iOS 플랫폼: 비디오는 샌드박스의 Documents/testCache 디렉터리에 캐시됩니다.
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");
```

[](id:offline2)

#### 2단계: 다운로드 시작

다음과 같이 [Fileid](#fileid) 또는 [URL](#url)을 통해 다운로드를 시작할 수 있습니다.
<dx-tabs>

::: Fileid 방식[](id:fileid)
Fileid를 통해 다운로드하려면 최소한 AppID, Fileid 및 qualityId를 전달해야 합니다. 서명된 비디오의 경우 pSign도 전달해야 합니다. 특정 값이 userName에 전달되지 않으면 기본적으로 “default”가 됩니다.

>!암호화된 비디오는 Fileid 방식으로만 다운로드할 수 있으며 psign이 필요합니다.

```dart
// QUALITY_OD // 기존 해상도
// QUALITY_FLU // LD
// QUALITY_SD  // SD
// QUALITY_HD  // HD

TXVodDownloadMedialnfo medialnfo = TXVodDownloadMedialnfo();
TXVodDownloadDataSource dataSource = TXVodDownloadDataSource();
dataSource.appId = 1252463788;
dataSource.fileId = "4564972819220421305";
dataSource.quality = DownloadQuality.QUALITY_HD;
dataSource.pSign = "pSignxxxx";
medialnfo.dataSource = dataSource;
TXVodDownloadController.instance.startDonwload(medialnfo);
```
:::

::: URL 방식[](id:url)
URL 매개변수는 필수입니다. 중첩되지 않은 단일 비트레이트 HLS 파일만 지원됩니다. userName을 지정하지 않으면 "default"가 사용됩니다.

```dart
TXVodDownloadMedialnfo medialnfo = TXVodDownloadMedialnfo();
medialnfo.url = "http://1500005830.vod2.myqcloud.com/43843ec0vodtranscq1500005830/00eb06a88602268011437356984/video_10_0.m3u8";
TXVodDownloadController.instance.startDonwload(medialnfo);
```

:::

</dx-tabs>

[](id:offline3)

#### 3단계: 작업 정보 받기 

작업 정보를 수신하기 전에 먼저 콜백 listener를 설정해야 합니다.

```dart
TXVodDownloadController.instance.setDownloadObserver((event, info) {

}, (errorCode, errorMsg, info) {

});
```

다음 작업 이벤트를 받을 수 있습니다.

| 이벤트                                                  | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| EVENT_DOWNLOAD_START       | 작업이 시작됨 즉, SDK가 다운로드를 시작함                              |
| EVENT_DOWNLOAD_PROGRESS    | 작업 진행, 다운로드하는 동안 SDK는 이 API를 자주 호출하며, `mediaInfo.getProgress()`를 사용하여 현재 진행 상황 가져오기 가능 |
| EVENT_DOWNLOAD_STOP        | 작업이 중지됨, 다운로드를 중지하기 위해 `stopDownload`를 호출했을 때 이 메시지가 수신되면 다운로드 중지 성공을 나타냄 |
| EVENT_DOWNLOAD_FINISH      | 다운로드가 완료됨, 이 콜백이 수신되면 전체 파일이 다운로드된 것이며 다운로드된 파일은 TXVodPlayer에서 재생할 수 있음 |


downlodOnErrorListener 메소드가 콜백되면 다운로드 오류가 발생한 것입니다. 다운로드 중에 네트워크 연결이 끊기면 이 API가 다시 호출되고 다운로드 작업이 중지됩니다.

downloader는 한 번에 여러 파일을 다운로드할 수 있으므로 콜백 API는 `TXVodDownloadMedialnfo` 객체를 전달합니다. URL 또는 dataSource에 액세스하여 다운로드 소스를 확인하고 다운로드 진행률 및 파일 크기와 같은 기타 정보를 얻을 수 있습니다.

[](id:offline4)

#### 4단계: 다운로드 중지

`TXVodDownloadController.instance.stopDownload()` 메소드를 호출하여 다운로드를 중지할 수 있습니다. 매개변수는 다운로드가 시작될 때 전달되는 `TXVodDownloadMediaInfo` 객체입니다. **SDK는 체크포인트 재시작을 지원합니다.** 다운로드 디렉터리가 변경되지 않은 경우 파일 다운로드를 재개하면 다운로드가 중지된 지점부터 다운로드가 시작됩니다.

#### 5단계: 다운로드 관리

모든 계정 또는 지정된 계정의 다운로드 목록을 가져올 수 있습니다.

```dart
// 모든 사용자의 다운로드 목록 가져오기
// 다운로드 정보의 userName으로 다른 사용자의 다운로드 목록 구별 가능
List<TXVodDownloadMedialnfo> downloadInfoList = await TXVodDownloadController.instance.getDownloadList();
```

현재 다운로드 상태 및 진행률과 같은 Fileid의 다운로드 정보를 얻으려면 AppID', 'Fileid 및 qualityId를 전달해야 합니다.

```dart
// 비디오 다운로드 정보 가져오기
TXVodDownloadMedialnfo downloadInfo = await TXVodDownloadController.instance.getDownloadInfo(medialnfo);
int? duration = downloadInfo.duration;// 총 지속 시간 가져오기
int? playableDuration = downloadInfo.playableDuration; // 다운로드한 비디오의 재생 가능 시간 가져오기
double? progress = downloadInfo.progress;// 다운로드 진행률 가져오기
String? playPath = downloadInfo.playPath; // 오프라인 재생을 시작하기 위해 플레이어에 전달할 수 있는 오프라인 재생 경로를 가져오기
int? downloadState = downloadInfo.downloadState; // 다운로드 상태 가져오기, 자세한 내용은 STATE_xxx 상수 참고
```

```dart
// 다운로드 정보 삭제
bool result = await TXVodDownloadController.instance.deleteDownloadMediaInfo(medialnfo);
```

### 4. 암호화된 재생

비디오 암호화 솔루션은 온라인 교육과 같이 비디오 저작권을 보호해야 하는 시나리오에서 사용됩니다. 비디오 리소스를 암호화하려면 플레이어를 변경하고 비디오 소스를 암호화 및 트랜스 코딩해야 합니다. 자세한 내용은 [비디오 암호화 개요](https://www.tencentcloud.com/document/product/266/38131)를 참고하십시오.

Tencent Cloud 콘솔에서 암호화된 비디오의 appId, fileId 및 psign을 가져오고 비디오를 재생합니다.

```dart
// psign은 Player 서명입니다. 서명 소개 및 생성 방식에 관한 내용은 다음 링크를 참고하십시오. https://cloud.tencent.com/document/product/266/42436
TXPlayInfoParams params = TXPlayInfoParams(appId: 1252463788,
        fileId: "4564972819220421305", psign: "psignxxxxxxx");
_controller.startVodPlayWithParams(params);
```

### 5. 플레이어 구성 

statPlay를 호출하기 전에 setConfig를 호출하여 플레이어 연결 시간 초과 기간, 진행 콜백 간격 및 캐시된 파일의 최대 수와 같은 플레이어 매개변수를 구성할 수 있습니다. TXVodPlayConfig를 사용하면 세부 매개변수를 구성할 수 있습니다. 자세한 내용은 [API 문서](https://www.tencentcloud.com/document/product/266/49591)를 참고하십시오. 다음은 구성 예시 코드입니다.

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// preferredResolution이 구성되지 않은 경우 멀티 비트레이트 비디오 재생 중에 720 * 1280 해상도 스트림이 우선적으로 재생됨
config.preferredResolution = 720 * 1280;
config.enableAccurateSeek = true;  // 정확한 seek 활성화 여부 설정, 기본값: true
config.progressInterval = 200;  // 진행 콜백 간격을 설정합니다. 단위: 밀리초
config.maxBufferSize = 50;  // 최대 사전 로딩 버퍼 크기 설정, 단위: MB
_controller.setPlayConfig(config);
```

##### 재생 시작 시 해상도 지정

HLS 다중 비트 레이트 비디오 소스를 재생할 때 비디오 스트림 해상도 정보를 미리 알고 있으면 재생이 시작되기 전에 기본 해상도를 지정할 수 있으며 플레이어는 기본 해상도 이하에서 스트림을 선택하여 재생합니다. 이렇게 하면 재생이 시작된 후 필요한 비트스트림으로 전환하기 위해 setBitrateIndex를 호출할 필요가 없습니다.

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// 전달된 매개변수는 비디오 너비와 높이의 곱(너비 * 높이)으로, 사용자 정의 값 전달 가능, 기본 720 * 1280
config.preferredResolution = 720 * 1280;
_controller.setPlayConfig(config);
```

##### 재생 진행 콜백 간격 설정

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
config.progressInterval = 200;  // 진행 콜백 간격을 설정합니다. 단위: 밀리초
_controller.setPlayConfig(config);
```

[](id:listening)

## 플레이어 이벤트 리스닝

`TXVodPlayerController`의 `onPlayerEventBroadcast`를 통해 플레이어의 재생 이벤트를 수신하여 정보를 애플리케이션에 동기화할 수 있습니다.

### 재생 이벤트 알림(onPlayerEventBroadcast)


| 이벤트 ID                                   | 코드 | 설명                                                   |
| ----------------------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN                    | 2004 | 비디오 재생 시작됨                                               |
| PLAY\_EVT\_PLAY\_PROGRESS    | 2005 | 비디오 재생 진행률(현재 재생 진행률, 로딩 진행률 및 총 비디오 지속 시간 포함)      |
| PLAY\_EVT\_PLAY\_LOADING     | 2007 | 비디오 loading 중. 비디오 재생이 재개되면 LOADING\_END 이벤트가 보고됨 |
| PLAY\_EVT\_VOD\_LOADING\_END | 2014 | 비디오 loading이 종료되고 비디오 재생이 재개됨                        |
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seek 완료, 10.3 버전부터 지원|

#### 이벤트 중지

| 이벤트 ID                 | 코드  | 설명                                               |
| :---------------------- | :---- | :----------------------------------------------------- |
| PLAY_EVT_PLAY_END       | 2006  | 비디오 재생 종료                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | 네트워크 연결이 끊겼고 여러 번 재시도한 후에도 다시 연결할 수 없음. 플레이어를 다시 시작하여 연결을 재시도할 수 있음. |
| PLAY_ERR_HLS_KEY        | -2305 | HLS 암호 해독 key 가져오기 실패                                  |

#### 경고 이벤트

SDK의 일부 내부 이벤트를 알리는 데만 사용되는 다음 이벤트는 무시할 수 있습니다.

| 이벤트 ID                           | 코드 | 설명                                                     |
| :-------------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_WARNING_VIDEO_DECODE_FAIL    | 2101 | 현재 비디오 프레임 디코딩 실패                                           |
| PLAY_WARNING_AUDIO_DECODE_FAIL    | 2102 | 현재 오디오 프레임 디코딩 실패                                           |
| PLAY_WARNING_RECONNECT            | 2103 | 네트워크 연결 끊김 및 자동 재연결 수행(PLAY_ERR_NET_DISCONNECT 이벤트는 세 번의 시도 실패 후에 발생함) |
| PLAY_WARNING_HW_ACCELERATION_FAIL | 2106 | 하드웨어 디코더 시작 실패, 소프트웨어 디코더가 대신 사용됨                                       |

#### 연결 이벤트

다음 서버 연결 이벤트는 주로 서버 연결 시간을 측정하고 수집하는 데 사용됩니다.

| 이벤트 ID                    | 코드 | 설명                                                     |
| :------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_EVT_VOD_PLAY_PREPARED | 2013 | 플레이어가 준비되었으며 재생 시작 가능. autoPlay가 false로 설정된 경우 이 이벤트를 수신한 후 resume을 호출하여 재생을 시작해야 함 |
| PLAY_EVT_RCV_FIRST_I_FRAME | 2003 | 네트워크는 첫 번째 렌더링 가능한 비디오 데이터 패킷(IDR)을 수신                      |


#### 이미지 품질 이벤트

다음 이벤트는 이미지 변경 정보를 가져오는 데 사용됩니다.

| 이벤트 ID                       | 코드 | 설명         |
| ----------------------------- | ---- | ---------------- |
| PLAY\_EVT\_CHANGE\_RESOLUTION | 2009 | 비디오 해상도가 변경됨   |
| PLAY\_EVT\_CHANGE\_ROTATION   | 2011 | MP4 비디오가 회전됨 |

#### 비디오 정보 이벤트

| 이벤트 ID                                    | 코드 | 설명             |
| :----------------------------------------- | :--- | :------------------- |
|PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | 재생된 파일의 정보 가져오기 성공 |

fileId를 통해 비디오를 재생한 후 재생 요청이 성공하면(인터페이스: startVodPlay(TXPlayerAuthBuilder authBuilder)), SDK는 일부 요청 정보를 상위 레이어에 알리고 `TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC` 이벤트를 수신한 후 param을 구문 분석하여 비디오 정보를 얻을 수 있습니다.

| 비디오 정보                                    | 설명                                       |
| ------------------------------------------- | ------------------------------------------------- |
| EVT\_PLAY\_COVER\_URL                       | 비디오 썸네일 URL                                   |
| EVT\_PLAY\_URL                              | 비디오 재생 URL                                   |
| EVT\_PLAY\_DURATION                         | 비디오 지속 시간                                       |
| EVT_TIME                                    | 이벤트 발생 시간                                   |
| EVT_UTC_TIME                                | UTC 시간                                        |
| EVT_DESCRIPTION                             | 이벤트 설명                                       |
| EVT_PLAY_NAME                               | 비디오 이름                                       |
| EVT_IMAGESPRIT_WEBVTTURL     | 스프라이트 이미지 web vtt 설명 파일 다운로드 URL, 10.2 버전부터 지원 |
| EVT_IMAGESPRIT_IMAGEURL_LIST | 스프라이트 이미지 다운로드 URL, 10.2 버전부터 지원            |
| EVT_DRM_TYPE                 | 암호화 유형, 10.2 버전부터 지원                        |


다음은 onPlayerEventBroadcast를 사용하여 비디오 재생 정보를 가져오는 예시 코드입니다.

```dart
_controller.onPlayerEventBroadcast.listen((event) async {
  if (event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_BEGIN || event["event"] == TXVodPlayEvent.PLAY_EVT_RCV_FIRST_I_FRAME) {
  // code ...
  } else if (event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_PROGRESS) {
  // code ...
  }
});
```

[](id:status)

### 재생 상태 피드백(onPlayerNetStatusBroadcast)

상태 피드백은 푸셔의 현재 상태에 대한 실시간 피드백을 제공하기 위해 0.5초마다 한 번씩 트리거됩니다. 현재 비디오 재생 상태를 더 잘 이해할 수 있도록 SDK 내부에서 일어나는 일을 알려주는 대시보드 역할을 할 수 있습니다.

<table>
<tr><th>매개변수</th><th>설명</th></tr>
<tr>
<td>NET_STATUS_CPU_USAGE</td><td>현재의 순간 CPU 사용률</td>
</tr><tr>
<td>NET_STATUS_VIDEO_WIDTH</td><td>비디오 해상도 - 너비</td>
</tr><tr>
<td>NET_STATUS_VIDEO_HEIGHT</td><td>비디오 해상도 - 높이</td>
</tr><tr>
<td>NET_STATUS_NET_SPEED</td><td>현재 네트워크 데이터 수신 속도</td>
</tr><tr>
<td>NET_STATUS_VIDEO_FPS</td><td>스트리밍 미디어의 현재 비디오 프레임 레이트</td>
</tr><tr>
<td>NET_STATUS_VIDEO_BITRATE</td><td>스트리밍 미디어의 현재 비디오 비트 레이트, 단위: Kbps</td>
</tr><tr>
<td>NET_STATUS_AUDIO_BITRATE</td><td>스트리밍 미디어의 현재 오디오 비트 레이트, 단위: Kbps</td>
</tr><tr>
<td>NET_STATUS_VIDEO_CACHE</td><td>버퍼(jitterbuffer) 크기. 현재 버퍼 길이가 0이면 곧 지연이 발생함</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>연결된 서버 IP</td>
</tr></table>

다음은 onNetStatus를 사용하여 비디오 재생 정보를 가져오는 예시 코드입니다.

```dart
_controller.onPlayerNetStatusBroadcast.listen((event) async {
  int videoWidth = event[TXVodNetEvent.NET_STATUS_VIDEO_WIDTH];
});
```


### 비디오 재생 상태 피드백

비디오 재생 상태는 재생 상태가 전환될 때마다 알려줍니다.

열거형 클래스 TXPlayerState는 이벤트 전송에 사용됨

| 상태 | 의미   |
| ------ | ------ |
| paused | 재생 일시 중지 |
| failed | 재생 실패 |
| buffering | 버퍼링 |
| playing | 재생 중 |
| stopped | 재생 중지 |
| disposed | 컨트롤이 릴리스됨 |


다음은 onPlayerState를 사용하여 비디오 재생 상태를 가져오는 샘플 코드입니다.

```dart
_controller.onPlayerState.listen((val) { });
```

### 시스템 볼륨 레벨 수신

비디오 재생 볼륨 수준을 모니터링하는 데 도움이 되도록 SDK는 볼륨 레벨 변경 알림을 flutter 레이어의 이벤트로 캡슐화합니다. SuperPlayerPlugin을 직접 사용하여 현재 장치의 볼륨 레벨 변경을 수신할 수 있습니다.

다음은 onEventBroadcast를 사용하여 장치의 볼륨 레벨 상태를 가져오는 샘플 코드입니다.

```dart
SuperPlayerPlugin.instance.onEventBroadcast.listen((event) {
  int eventCode = event["event"];
});
```

관련 이벤트는 다음과 같습니다.

| 상태 | 코드 | 설명   |
| ------ |------ | ------ |
| EVENT_VOLUME_CHANGED | 1 | 볼륨 레벨이 변경됨 |
| EVENT_AUDIO_FOCUS_PAUSE | 2 | 볼륨 레벨 출력 및 재생 포커스가 손실됨, 이 이벤트는 Android에만 적용됨 |
| EVENT_AUDIO_FOCUS_PLAY | 3 | 볼륨 레벨 출력 포커스 가져오기 성공, 이 이벤트는 Android에만 적용됨 |

### PiP 이벤트 수신

SDK에서 사용하는 PiP는 시스템의 PiP 기능을 기반으로 하므로 PiP 모드에 들어가면 그에 따라 UI를 조정하는 데 도움이 되는 일련의 알림이 제공됩니다.

| 상태 | 코드 | 설명   |
| ------ |------ | ------ |
| EVENT_PIP_MODE_ALREADY_ENTER | 1 | PiP 모드에 들어감 |
| EVENT_PIP_MODE_ALREADY_EXIT | 2 | PiP 모드를 종료함 |
| EVENT_PIP_MODE_REQUEST_START | 3 | PiP 모드를 요청함 |
| EVENT_PIP_MODE_UI_STATE_CHANGED | 4 | pip UI 상태가 변경됨, 이 이벤트는 Android 31 이상에서만 적용됨 |
| EVENT_IOS_PIP_MODE_RESTORE_UI | 5 | UI가 재설정됨, 이 이벤트는 iOS에서만 적용됨 |
| EVENT_IOS_PIP_MODE_WILL_EXIT | 6 | 플레이어가 PiP 모드를 종료함, 이 이벤트는 iOS에서만 적용됨 |

다음은 onExtraEventBroadcast를 사용하여 PiP 이벤트를 수신하기 위한 샘플 코드입니다.

```dart
SuperPlayerPlugin.instance.onExtraEventBroadcast.listen((event) {
  int eventCode = event["event"];
});
```