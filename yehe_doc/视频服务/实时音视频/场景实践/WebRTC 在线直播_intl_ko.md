## 효과

본 문서는 Web 브라우저 종속만으로 푸시 스트림, 풀 스트림, 채팅방, 인터랙션 마이크 연결을 포함한 온라인 라이브 방송 기능을 빠르게 구현하는 방법을 소개합니다.

## 구현 원리

[**TWebLive**]
는 Tencent Cloud의 TRTC, IM, CDN 등의 서비스를 기반으로 구성된 Web 라이브 방송 모듈입니다. 몇 개의 코드만으로 간편하게 다음과 같은 푸시 스트림, 풀 스트림, 채팅방 기능을 구현할 수 있습니다.

### 푸시 스트림
푸시 스트림이 필요할 경우 Pusher(푸시 스트림) 객체를 생성하고, 3단계만으로 간편하게 설정할 수 있습니다.
```
<div id="pusherView" style="width:100%; height:auto;"></div>
<script>
// 1. Pusher(푸시 스트림) 객체 생성
let pusher = TWebLive.createPusher({ userID: 'your userID' });

// 2. 렌더링 인터페이스를 설정하고 마이크에서 오디오, 카메라에서 비디오(기본값 720p) 수집
pusher.setRenderView({
  elementID: 'pusherView',
  audio: true,
  video: true
}).then(() => {

// 3. sdkappid roomid 등의 정보를 입력하고 푸시 스트림
  // url은 반드시 `room://`으로 시작해야 함
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
```
### 풀 스트림
풀 스트림이 필요할 경우 Player(플레이어) 객체를 생성하고, 3단계만으로 간편하게 설정할 수 있습니다.

```
<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1. Player(플레이어) 객체 생성
let player = TWebLive.createPlayer();

// 2. 렌더링 인터페이스 설정
player.setRenderView({ elementID: 'playerView' });

// 3-1. flv 또는 hls 등 포맷의 CDN 재생 주소를 입력하고, 해당 URL은 반드시 `https://`로 시작해야 함
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // 실제 사용 가능한 재생 주소로 대체
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // 실제 사용 가능한 재생 주소로 대체

// 3-2. `room://`으로 시작하는 WebRTC 재생 주소를 입력할 수도 있으며, 해당 주소로 매우 낮은 재생 딜레이를 실현할 수 있음
let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
```
### 채팅방
호스트와 시청자가 채팅 인터랙션 시 IM 객체를 생성하고, 3단계만으로 간편하게 메시지를 주고받을 수 있습니다.

```
// 1. IM 객체와 수신 이벤트 생성
let im = TWebLive.createIM({
  SDKAppID: 0 // 액세스 시 0이 사용자의 IM 애플리케이션 SDKAppID로 대체 필요
});
// IM_READY IM_TEXT_MESSAGE_RECEIVED 등 이벤트 수신
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// 액세스 측에서 해당 이벤트를 수신한 후, SDK를 호출해 메시지 등 발송 가능
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// 텍스트 메시지 수신 후 화면에 표시
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2. IM 서비스에 로그인
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // 로그인 성공
  if (imResponse.data.repeatLogin === true) {
    // 계정 로그인 여부와 해당 로그인 작업이 중복 로그인인지 식별
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // 로그인 실패 관련 정보
});

// 3. 라이브 룸 입장
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // 라이브 룸 입장 성공
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: // 라이브 룸에 들어간 상태
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // 라이브 룸 입장 실패 관련 정보
});
```

>? 개발자의 개발 작업 및 인건비를 더욱 절약하기 위해 TWebLive SDK를 기반으로 PC와 모바일 브라우저 모두에 적합한 [Demo](https://github.com/tencentyun/TWebLive)를 제공하며, Github에 오픈 소스를 제공합니다. 개발자는 프로젝트를 로컬로 fork&clone한 후 약간 수정하면 Demo를 바로 시작할 수 있습니다. 또는 프로젝트에 통합하여 배포 및 런칭할 수 있습니다.

## 액세스 방법

<span id="step1"></span>
### 1단계: 애플리케이션 생성
먼저 TRTC 콘솔에서 TRTC 애플리케이션을 생성해야 합니다. Tencent Cloud는 기본적으로 해당 TRTC 애플리케이션에 동일한 SDKAppID를 가진 IM 애플리케이션을 바인딩합니다.

1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)로 이동하여 [애플리케이션 생성]을 클릭하고, 애플리케이션 이름을 입력한 후 [확인]을 클릭하여 TRTC 애플리케이션을 생성합니다.

<span id="step2"></span>
### 2단계: SDKAppID 및 키 획득
1. [애플리케이션 리스트](https://console.cloud.tencent.com/trtc/app)에서 타깃 애플리케이션 오른쪽에 있는 [애플리케이션 정보]를 클릭하여 상세 페이지로 이동합니다.
2. [애플리케이션 정보] 모듈에서 복사 버튼을 클릭해 SDKAppID 정보를 기록합니다.
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
3. [퀵 스타트] 탭을 선택하고 [2단계: UserSig 발급 키 획득] 태그에서 [키 복사]를 클릭합니다.
    ![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>!
>- UserSig 로컬 계산 방식은 로컬 개발 디버깅에만 사용됩니다. 직접 온라인에 배포하지 마십시오. 일단 `SECRETKEY`가 노출되면 해커가 사용자의 Tencent Cloud 트래픽을 남용할 수 있습니다.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 App에서 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

<span id="step3"></span>
### 3단계: CDN 라이브 방송 서비스 활성화(옵션)
CDN 라이브 방송 풀 스트림 기능을 활성화하려면 Tencent Cloud CSS 서비스를 활성화해야 합니다. 다음 방법에 따라 활성화할 수 있습니다.
>1. [애플리케이션 관리]>[기능 설정]의 [자동 릴레이 푸시 스트림 활성화](https://intl.cloud.tencent.com/document/product/647/39080)에서 릴레이 푸시 스트림 기능을 활성화합니다. 해당 기능을 활성화하면 TRTC 방 안에 있는 모든 채널의 화면이 해당 재생 주소로 준비됩니다.
2. [Tencent CSS 콘솔](https://console.cloud.tencent.com/live/)에서 재생 도메인을 설정하고 CNAME 설정을 완료합니다. 자세한 방법은 [CDN 라이브 방송 시청 실행](https://intl.cloud.tencent.com/document/product/647/35242) 문서를 참조하십시오.


<span id="step4"></span>

### 4단계: Demo 소스 코드 다운로드 및 설정
1. [Tencent Cloud Web 라이브 방송 인터랙션 모듈 Demo 프로그램](https://github.com/tencentyun/TWebLive)을 다운로드합니다.
2. `TWebLive/dist/debug/GenerateTestUserSig.js` 파일을 열고 관련 매개변수를 설정합니다. <ul style="margin:0">
   <li/>SDKAPPID: <a href="#step2">1단계</a>에서 획득한 실제 애플리케이션 SDKAppID로 설정합니다.
    <li/>SECRETKEY: <a href="#step2">2단계</a>에서 획득한 실제 키 정보로 설정합니다.
    <li/>PLAYDOMAIN: CDN으로 시청할 재생 도메인을 설정합니다. CDN 라이브 방송 시청이 필요하지 않은 경우 해당 설정은 생략 가능합니다.
    </ul>
3. Demo 소스 코드 통합:
#### npm을 이용한 패키지 설치
1. 프로젝트에서 npm을 통해 `tim-js-sdk`, `trtc-js-sdk`, `tweblive`의 최신 버전을 설치합니다.
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
>? 프로젝트에 이미 `tim-js-sdk` 또는 `trtc-js-sdk`가 통합되어 있는 경우, 직접 최신 버전으로 업데이트하면 됩니다.
2. 프로젝트에 tweblive를 가져옵니다.
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```

#### script를 이용한 외부 링크 태그
script를 통한 외부 링크 태그 방법으로 가져올 경우, `tim-js.js`, `trtc.js`, `tweblive.js`를 프로젝트에 복사하고 순서대로 가져옵니다.
```
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```

<span id="step5"></span>

### 5단계: Demo 실행

Chrome 브라우저에서 `dist` 디렉터리의 `index.html` 파일을 열면 Demo가 실행됩니다.

>!
>
>- 일반적으로 체험용 Demo는 서버에 배포가 필요하며, `https://도메인/xxx`로 액세스하거나 직접 로컬에서 서버를 구축하여 `localhost:포트`를 통해 액세스할 수 있습니다.
>- 현재 데스크톱 Chrome 브라우저가 TRTC 데스크톱 브라우저 SDK를 비교적 완벽하게 지원하므로 Chrome 브라우저를 사용하여 체험하는 것을 권장합니다.
>- TWebLive는 카메라와 마이크를 사용하여 멀티미디어를 수집하며 체험 과정에서 Chrome 브라우저에서 관련 안내를 수신할 수 있습니다. [허용]을 클릭하십시오.

### 플랫폼 지원

WebRTC 기술은 Web 푸시 스트림 및 Web 저딜레이 시청에 이용되며, Google에서 최초로 출시한 기술입니다. 현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android의 브라우저)에서의 지원은 완전하지 못할 수 있습니다.

- 응용 시나리오가 주로 교육 분야라면 교사는 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션을 사용하기를 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.

|  운영 체제   |          브라우저 유형          | 브라우저 최저 버전 요구사항 | 수신(재생) | 발송(마이크 켜짐) |
| :---------: | :--------------------------: | :----------------: | :----------: | :----------: |
|   Mac OS    |     데스크톱 Safari 브라우저     |        11+         |     지원     |     지원     |
|   Mac OS    |     데스크톱 Chrome 브라우저     |        56+         |     지원     |     지원     |
|   Mac OS    |     데스크톱 Firefox 브라우저     |        56+         |     지원     |     지원     |
|   Mac OS    |     데스크톱 Edge 브라우저     |        80+         |     지원     |     지원     |
|   Windows   |     데스크톱 Chrome 브라우저     |        56+         |     지원     |     지원     |
|   Windows   | 데스크톱 QQ 브라우저(고속 커널) |       10.4+        |     지원     |     지원     |
|   Windows   |    데스크톱 Firefox 브라우저     |        56+         |     지원     |     지원     |
|   Windows   |      데스크톱 Edge 브라우저      |        80+         |     지원     |     지원     |
| iOS 11.1.2+ |     모바일 Safari 브라우저     |        11+         |     지원     |     지원     |
| iOS 12.1.4+ |         WeChat 내부 웹페이지         |         -          |     지원     |    미지원    |
| iOS 14.3+   |         WeChat  내부 웹페이지         |   6.5+(WeChat 버전) |     지원     |    지원     |
|   Android   |       모바일 QQ 브라우저       |         -          |    미지원    |    미지원    |
|   Android   |       모바일 UC 브라우저       |         -          |    미지원    |    미지원    |
|   Android   |   WeChat 내부 웹페이지(TBS 커널)   |         -          |     지원     |     지원     |
|   Android   |  WeChat 내부 웹페이지(XWEB 커널)   |         -          |     지원     |    미지원    |

>! H.264 버전 권한 제한으로 인해 화웨이 시스템의 Chrome 브라우저와 Chrome WebView 커널의 브라우저에서는 TRTC 데스크톱 브라우저 SDK가 정상적으로 실행되지 않습니다.

## FAQ
**1. 키 조회 시 공개키와 개인키 정보만 획득할 수 있습니다. 키는 어떻게 획득하나요?**

TRTC SDK 6.6 버전(2019년 08월)부터 신규 서명 알고리즘인 HMAC-SHA256이 활성화됩니다. 이전 버전에서 애플리케이션을 생성한 경우 먼저 서명 알고리즘을 업그레이드해야 신규 암호화 키를 획득할 수 있습니다.

**2. 클라이언트에서 “RtcError:no valid ice candidate found” 오류가 발생합니다. 어떻게 처리해야 하나요?**

해당 오류는 TRTC 데스크톱 브라우저 SDK가 STUN 홀 펀칭 실패 시 발생합니다. 환경 요건에 따라 방화벽 설정을 확인해 주십시오.

**3. 클라이언트에서 “RtcError: ICE/DTLS Transport connection failed” 또는 “RtcError: DTLS Transport connection timeout” 오류가 발생합니다. 어떻게 처리해야 하나요?**

해당 오류는 TRTC 데스크톱 브라우저 SDK가 STUN 홀 펀칭 실패 시 발생합니다. 환경 요건에 따라 방화벽 설정을 확인해 주십시오.

**4. 10006 error가 발생합니다. 어떻게 처리해야 하나요?**

`"Join room failed result: 10006 error: service is suspended, if charge is overdue, renew it"` 오류가 발생하는 경우, [TRTC 콘솔](https://console.cloud.tencent.com/rav)에 로그인하여 생성한 애플리케이션을 클릭한 후 [계정 정보]를 클릭하여 계정 정보 페이지에서 TRTC 애플리케이션의 서비스 상태가 사용 가능한 상태인지 확인합니다.
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)

## 참고 자료

- [TWebLive API 매뉴얼](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [온라인 Demo]


