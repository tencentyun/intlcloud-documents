## 적용 시나리오
CDN 라이브 방송 시청은 'CDN 릴레이 라이브 방송'이라고도 합니다. TRTC는 UDP 프로토콜을 채택해 멀티미디어 데이터를 전송하며, LVB CDN은 데이터 전송 시 RTMP\HLS\FLV 등 프로토콜을 채택합니다. 따라서 TRTC의 멀티미디어 데이터를 라이브 방송 CDN으로 **릴레이**해야 시청자들이 라이브 방송 CDN으로 시청할 수 있습니다.

CDN를 사용해 TRTC를 시청하면 다음의 두 문제를 해결할 수 있습니다.
- **문제1: 고도의 동시 접속 시청**
TRTC의 딜레이 조건을 고려한 단일 방의 최대 인원 수는 10만 명입니다. CDN를 적용할 경우, 딜레이가 다소 길지만 10만 명 이상의 동시 시청이 가능하며, 비용도 보다 저렴합니다.
- **문제2: 모바일 웹 사이트 재생**
TRTC는 WebRTC 프로토콜의 접근을 지원하지만 Chrome 브라우저에서 주로 사용되며 모바일 기기의 브라우저와 호환 시 기능이 저하됩니다. 특히 Android 휴대폰의 브라우저는 WebRTC를 효과적으로 지원하지 못합니다. 따라서 모바일 기기의 Web 화면으로 라이브 콘텐츠를 공유하려면 HLS(m3u8) 재생 프로토콜을 사용하시길 권장합니다. HLS 프로토콜을 적용할 때 라이브 방송 CDN의 능력도 매우 중요합니다.


## 원리 분석
Tencent Cloud는 릴레이 트랜스 코딩 클러스터를 통해 TRTC의 멀티미디어 데이터를 라이브 방송 CDN 시스템에 릴레이합니다. 이 클러스터는 TRTC가 채택한 UDP 프로토콜을 표준적인 라이브 방송 RTMP 프로토콜로 전환합니다.
<span id="directCDN"></span>
**단일 화면의 릴레이 라이브 방송**
TRTC 방에 호스트가 1인일 경우, TRTC의 릴레이 푸시 스트림은 표준 RTMP 프로토콜의 다이렉트 스트리밍과 기능이 동일합니다. 단, TRTC가 채택하는 UDP는 RTMP에 비해 취약한 네트워크 환경에서도 뛰어난 성능을 선보입니다.
![](https://main.qcloudimg.com/raw/23ac68cb46b06cc4eb6000fa98500dc4.jpg)

<span id="mixCDN"></span>
**혼합 화면의 릴레이 라이브 방송**
TRTC는 끊김 없는 멀티미디어 인터랙션 기능을 구현합니다. 단일 방에 호스트가 다수이며, CDN 시청으로 단일 멀티미디어 화면을 불러오고자 할 때 [클라우드 혼합 스트림 서비스](https://intl.cloud.tencent.com/document/product/647/34618)를 이용해 다중 화면을 하나로 합성해야 합니다. 이때 다음 그림과 같은 원리로 작동합니다.
![](https://main.qcloudimg.com/raw/77eeed776e61c3a6bd0e1669e5747727.jpg)

> **다중 CDN 화면은 왜 바로 재생할 수 없나요?**
>다중 CDN 화면은 재생 시 각 화면의 딜레이 조건을 맞추기가 까다롭습니다. 또한 다중 화면은 다운로드 트래픽이 단일 화면에 비해 많이 소요되기 때문에 업계에서는 보통 클라우드 혼합 스트림 방식을 채택합니다.

## 전제 조건
Tencent의 [LVB](https://console.cloud.tencent.com/live) 서비스를 개통했다면 라이브 방송 재생에 관한 정부 관련 기관의 규정에 따라 재생 도메인을 설정해야 합니다. 자세한 내용은 [자체 도메인 추가](https://intl.cloud.tencent.com/document/product/267/35970)를 참조하십시오.

## 사용 방법

<span id="step1"></span>
### 1단계: 릴레이 푸시 스트림 기능 활성화

1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. 왼쪽 메뉴에서 [애플리케이션 관리]를 선택한 후 대상 애플리케이션이 속한 라인의 [기능 설정]을 클릭합니다.
3. [릴레이 푸시 스트림 설정]에서 [릴레이 푸시 스트림 활성화] 오른쪽의 ![](https://main.qcloudimg.com/raw/5f58afe211aa033037e5c0b793023b49.png)를 클릭하면 [릴레이 푸시 스트림 기능 활성화] 팝업창이 뜹니다. 팝업창에서 [릴레이 푸시 스트림 기능 활성화]를 클릭하면 활성화됩니다.

<span id="step2"></span>
### 2단계: 재생 도메인 및 CNAME 설정
1. [LVB 콘솔](https://console.cloud.tencent.com/live/)에 로그인합니다.
2. 왼쪽 메뉴에서 [도메인 관리]를 선택하면 도메인 목록에 `xxxxx.livepush.myqcloud.com` 형식의 푸시 스트림 도메인이 추가된 것을 확인할 수 있습니다. xxxxx는 숫자로 이루어져 있으며, bizid라고 부릅니다. TRTC 콘솔 > [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) > [애플리케이션 정보]에서 bizid 정보를 조회할 수 있습니다.
3. [도메인 추가]를 클릭한 뒤 등록한 재생 도메인을 입력합니다. [재생 도메인]으로 도메인 유형을 선택한 뒤 가속 리전(기본값은 [중국대륙])을 선택하고 [확인]을 클릭합니다.
4. 도메인 추가가 완료되면 시스템은 자동으로 CNAME 도메인(`.liveplay.myqcloud.com` 형식이 뒤에 붙음) 이름을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으므로 도메인 서비스 제공 업체에서 CNAME 설정을 완료해야 합니다. 설정이 적용되면 바로 LVB 서비스를 이용할 수 있으며, 자세한 내용은 [CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참조하십시오.

> **푸시 스트림 도메인 추가 불필요**, [1단계](#step1)에서 릴레이 라이브 방송 기능을 활성화하면 Tencent Cloud는 Live Video Broadcasting 콘솔에 `xxxxx.livepush.myqcloud.com` 형식의 푸시 스트림 도메인을 기본값으로 추가합니다. 해당 도메인은 Tencent Cloud LVB 서비스와 TRTC 서비스 사이에 약정한 기본 푸시 스트림 도메인으로서 수정할 수 없습니다.

<span id="step3"></span>
### 3단계: TRTC 멀티미디어 스트림을 라이브 방송 streamId과 조인
릴레이 푸시 스트림 기능을 활성화하면 TRTC 방의 각 화면에 맞는 재생 주소가 각각 할당되며, 주소 포맷은 다음과 같습니다.
```
http://재생 도메인/live/[streamId].flv
```
주소에 포함된 streamId는 라이브 방송 스트림의 유일한 식별자입니다. streamId를 직접 설정할 수 있으며, 기본값으로 생성된 것을 사용해도 됩니다.

#### 방법1: streamId의 사용자 정의
`TRTCCloud`의 `enterRoom` 함수를 호출한 뒤 `TRTCParams` 중 `streamId` 매개변수를 설정해 라이브 방송 스트림 ID를 정합니다.
iOS기기의 Objective-C 코드 예시

```Objective-C
TRTCCloud *trtcCloud = [TRTCCloud sharedInstance];
TRTCParams *param = [[TRTCParams alloc] init];
param.sdkAppId = 1400000123;     // TRTC의 SDKAppID은 애플리케이션 생성 뒤 획득
param.roomId   = 1001;           // 방 번호
param.userId   = @"rexchang";    // 사용자 이름
param.userSig  = @"xxxxxxxx";    // 로그인 서명
param.role     = TRTCRoleAnchor; // 역할: 호스트
param.streamId = @"stream1001";  // 스트림 ID
[trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE]; // LIVE 모드를 사용하십시오.
```
userSig 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166) 을 참조하십시오.

#### 방법2: 시스템의 streamId 지정
자동 릴레이 푸시 스트림 실행 후 streamId를 사용자 정의하지 않은 경우, 시스템에서 streamId 하나를 디폴트로 생성합니다. 생성 규칙은 다음과 같습니다.

- **streamId가 사용되는 필드 어셈블리**
  - SDKAppID: [콘솔](https://console.cloud.tencent.com/trtc/app) > [애플리케이션 관리] > [애플리케이션 정보]에서 조회할 수 있습니다.
  - bizid: [콘솔](https://console.cloud.tencent.com/trtc/app) > [애플리케이션 관리] > [애플리케이션 정보]에서 조회할 수 있습니다.
  - roomId: `enterRoom` 함수의 매개변수 `TRTCParams`에서 지정합니다.
  - userId: `enterRoom` 함수의 매개변수 `TRTCParams`에서 지정합니다.
  - streamType: 카메라 화면은 main, 스크린 공유는 aux입니다(WebRTC은 동시에 한 채널의 업스트림만 지원하기 때문에 WebRTC의 스크린 공유 시 스트림 타입은 main임).

- **streamId 어셈블리 계산 규칙**
 <table>
<tr>
<th>어셈블리</th>
<th>2020년 01월 09일 및 이후 생성된 애플리케이션</th>
<th>2020년 01월 09일 이전 생성 및 사용된 애플리케이션</th>
</tr>
<tr>
<td>어셈블리 규칙</td>
<td>streamId = urlencode(sdkAppId_roomId_userId_streamType)</td>
<td>StreamId = bizid_MD5(roomId_userId_streamType)</td>
</tr>
<tr>
<td>계산 예시</td>
<td>예: sdkAppId = 12345678, roomId = 12345, userId = userA, 사용자가 카메라 사용했음<br>그렇다면: streamId = 12345678_12345_userA_main</td>
<td>예: bizid = 1234, roomId = 12345, userId = userA, 사용자가 카메라 사용했음<br>그렇다면: streamId = 1234_MD5(12345_userA_main) = 1234_8D0261436C375BB0DEA901D86D7D70E8</td>
</tr>
</table>


<span id="step4"></span>
### 4단계: 다중 화면 제어를 위한 혼합 방법

혼합한 라이브 방송 화면을 획득하고 싶은 경우 TRTCCloud의 `setMixTranscodingConfig` 인터페이스를 호출하여 클라우드 혼합 스트림 트랜스 코딩을 실행해야 합니다. 해당 인터페이스의 매개변수 `TRTCTranscodingConfig`로 설정할 수 있습니다.
 - 각 서브 화면의 노출 위치 및 사이즈
 - 혼합 화면의 화질 및 인코딩 매개변수

화면 레이아웃에 관한 자세한 설정 방법은 [클라우드 혼합 스트림 트랜스 코딩](https://intl.cloud.tencent.com/document/product/647/34618)을 참조하십시오. 프로세스 전반에 걸친 각 모듈의 관계는 [원리 분석](#mixCDN)에서 확인할 수 있습니다.

> `setMixTranscodingConfig`는 단말에서 스트림을 혼합하지 않습니다. 혼합 스트림 설정을 클라우드로 보내면 클라우드 서버에서 스트림을 혼합하고 트랜스 코딩을 실시합니다. 혼합 스트림과 트랜스 코딩은 모두 원시 멀티미디어를 디코딩한 뒤 2차 인코딩하기 때문에 프로세스 시간이 다소 소요됩니다. 따라서 혼합 화면 시청 시 개별 화면보다 딜레이 시간이 1초~2초 더 걸립니다.

<span id="step5"></span>
### 5단계: 재생 주소 가져오기 및 재생 링크
[2단계](#step2)와 [3단계](#step3)에서 각각 재생 도메인 설정 및 streamId 매핑을 마치면 라이브 방송을 위한 재생 주소가 할당됩니다. 재생 주소의 표준 포맷은 다음과 같습니다.
```
http://재생 도메인/live/[streamId].flv
```

예를 들어, 재생 도메인이 `live.myhost.com`이면 방 입장 매개변수를 이용해 방(1001)에 입장한 userA의 라이브 방송 스트림 ID를 streamId = "streamd1001"로 지정합니다.
다음과 같은 세 개의 재생 주소가 할당됩니다.
```
 rtmp 프로토콜 기반의 재생 주소: rtmp://live.myhost.com/live/streamd1001
 flv 프로토콜 기반의 재생 주소: http://live.myhost.com/live/streamd1001.flv
 hls 프로토콜 기반의 재생 주소: http://live.myhost.com/live/streamd1001.m3u8
```

접두사가 `http`이고, 확장자가 `.flv`인 **http - flv** 주소를 권장합니다. 이 재생 주소는 딜레이가 짧아 끊김 없는 재생이 가능하며, 안정성과 신뢰성이 우수합니다.
플레이어 선택 시 다음 권장 사항을 참조하시기 바랍니다.

| 플랫폼  | API 개요 | 지원 포맷|
|:-------:|:-------:|-------|
| iOS App|   TXLivePlayer(iOS) | FLV 권장 |
| Android App | TXLivePlayer(Android) | FLV 권장 |
| Web 브라우저 |  - |  데스크톱 Chrome 브라우저 FLV 지원 <br> Mac Safari 및 모바일 휴대폰 브라우저는 HLS만 지원 |
|WeChat 미니프로그램|   [&lt;live-player&gt; 태그](https://developers.weixin.qq.com/miniprogram/en/dev/component/live-player.html)| FLV 권장 |


<span id="step6"></span>
### 6단계: 재생 시 딜레이 개선

릴레이 라이브 방송 실행 후의 http - flv 주소는 라이브 방송 CDN을 경유해 확산 및 분배되기 때문에 TRTC 라이브 룸에서 바로 통화할 때보다 시청 시 긴 딜레이가 발생합니다.
현재 Tencent Cloud의 라이브 방송 CDN 기술을 기반으로 TXLivePlayer를 실행할 경우 다음 표와 같은 딜레이가 발생합니다.

| 릴레이 스트림 타입스튜디오 | TXLivePlayer 재생 모드 |  평균 딜레이 |  실제 테스트 결과 |
|:-------:|:-------:|:--------:|:---------:|
| 개별 화면 | 고속 모드(권장) | **2초 ~ 3초** | 하단 그림의 왼쪽 대조표(주황색)|
| 혼합 화면 | 고속 모드(권장) | **4초 ~ 5초** | 하단 그림의 오른쪽 대조표(파란색)|

하단 그림은 동일 사양 휴대폰을 대상으로 한 실제 테스트 결과입니다. 왼쪽 iPhone 6s는 TRTC SDK로 라이브 생방송을 진행했고, 오른쪽 샤오미6는 TXLivePlayer로 FLV 프로토콜 기반의 라이브 방송 스트림을 재생했습니다.


실제 테스트 결과, 딜레이가 상단 표의 수치보다 길다면 다음 제시하는 방법으로 딜레이 현상을 개선할 수 있습니다.

- **TRTC SDK에 포함된TXLivePlayer 사용**
일반적인 ijkplayer 또는 ffmpeg는 ffmpeg 기반의 커널 패키지 플레이어로 딜레이 제어력이 취약합니다. 이 플레이어로 상술한 라이브 방송 스트림 주소를 재생할 경우 딜레이를 제어할 수 없습니다. TXLivePlayer는 자체 개발한 재생 엔진이 탑재돼 있어 딜레이 제어가 가능합니다.

- **TXLivePlayer 재생 모드를 고속 모드로 설정**
TXLivePlayerConfig의 매개변수 세 개를 설정하여 고속 모드를 구현할 수 있습니다. 다음은 iOS를 예시로 한 것입니다.
iOS기기의 Objective-C 코드 예시
```
 // TXLivePlayer의 재생 모드를 고속 모드로 설정
    TXLivePlayerConfig * config = [[TXLivePlayerConfig alloc] init];
    config.bAutoAdjustCacheTime = YES;
    config.minAutoAdjustCacheTime = 1; // 최소 버퍼 1초
    config.maxAutoAdjustCacheTime = 1; // 최대 버퍼 1초
    [player setConfig:config];
    // 라이브 방송 재생 실행
```

<span id="expense"></span>
## 관련 비용

CDN 라이브 방송 시청에 따른 과금은 **시청 비용**과 **트랜스 코딩 비용**이 있습니다. 시청 비용은 기본 요금이며, 트랜스 코딩 비용은 [다중 화면 혼합](#mixCDN) 실행 시 부과됩니다.

>다음 제시되는 가격은 참고용 예시입니다. 실제 가격과 다를 경우 [Live Video Broadcasting > LVB](https://intl.cloud.tencent.com/document/product/267/2819)의 과금 사항을 확인하시기 바랍니다.

### 시청 비용: 라이브 방송 CDN 시청 시 발생하는 요금

라이브 방송 CDN으로 시청 시 **Live Video Broadcasting(LVB)**에서 시청으로 발생한 다운스트림 트래픽/대역폭 요금을 수취합니다. 실제 니즈에 맞춰 본인이 원하는 과금 방식을 선택할 수 있으며, 트래픽에 따른 과금 방식이 디폴트로 정해져 있습니다.


### 트랜스 코딩 비용: 다중 화면 혼합 시 발생하는 요금
[다중 화면 혼합](#mixCDN)을 실행하면 스트림 혼합을 위해 디코딩과 인코딩이 일어나고, 이에 따른 별도의 혼합 스트림 트랜스 코딩 요금이 발생합니다. 혼합 스트림 트랜스 코딩은 해상도 크기와 트랜스 코딩 시간에 따라 요금이 책정되며, 호스트가 채택한 해상도가 높고, 마이크 연결 시간(보통 마이크 연결 시 혼합 스트림 트랜스 코딩 필요)이 길수록 요금도 높습니다.

## FAQ
**방 입장 인원이 1명인데도 화면이 끊기고 흐릿한 이유는 무엇인가요?**
`enterRoom`의 TRTCAppScene 매개변수를 **TRTCAppSceneLIVE**로 지정합니다.
VideoCall 모드는 영상 통화에 최적화되어 있어 방에 1명의 사용자만 있을 경우 화면이 사용자의 네트워크 트래픽을 절약하기 위해 낮은 비트 레이트와 프레임 레이트를 유지하기 때문에 화면이 끊기고 흐릿한 것처럼 느껴질 수 있습니다.
