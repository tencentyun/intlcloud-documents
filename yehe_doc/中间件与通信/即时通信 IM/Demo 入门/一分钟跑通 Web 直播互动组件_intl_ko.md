TWebLive, 즉 Tencent Cloud Web 라이브 방송 인터랙션 컴포넌트는 Tencent Cloud 단말 R&D 팀에서 출시한 새로운 SDK로, Tencent Cloud TRTC, IM 및 TCPlayer가 통합되어 있으며, Web 라이브 방송 인터랙션 시나리오에서 자주 사용하는 기능(푸시 스트림, 마이크 On/Off, 카메라 On/Off, WeChat 공유 및 시청, 채팅, 좋아요 등)이 포함되어 있고, 간편하게 사용할 수 있는 [API](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)도 캡슐화되어 있어, Web 푸시 스트림 및 풀 스트림, 실시간 채팅 인터랙션 기능을 빠르게 구현할 수 있습니다. [Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)를 사용을 통해 체험해보실 수 있습니다.

## TWebLive의 장점
개발자가 [TWebLive SDK](https://www.npmjs.com/package/tweblive)를 연결하면 Flash 푸시 스트림 방식을 완벽히 대체할 수 있으며 Web 푸시 스트림, Web 저지연 시청, CDN 시청, 실시간 채팅 인터랙션(또는 댓글 자막) 기능을 구현하기 위한 복잡한 과정과 시간을 대폭 줄여줍니다. 다음 예시를 참고하십시오.

<dx-tabs>
::: 푸시 스트리밍
푸시 스트리밍이 필요할 경우 Pusher(푸시 스트리밍) 객체를 생성하면 되며, 세 단계만으로 간편하게 설정할 수 있습니다.
<dx-codeblock>
::: html html

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
:::
</dx-codeblock>
:::
::: 풀 스트리밍
풀 스트리밍이 필요할 경우 Player(플레이어) 객체를 생성하면 되며, 세 단계만으로 간편하게 설정할 수 있습니다.

<dx-codeblock>
::: html html

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

// 3-2. `room://`으로 시작하는 WebRTC 재생 주소를 입력할 수도 있으며, 해당 주소로 초저지연 재생 구현 가능
let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: 채팅방
호스트와 시청자의 채팅 인터랙션은 IM 객체를 생성하면 되며, 세 단계만으로 간편하게 메시지를 주고받을 수 있습니다.

<dx-codeblock>
::: javascript javascript
// 1. IM 객체 생성 및 이벤트 구독
let im = TWebLive.createIM({
  SDKAppID: 0 // 연결 시 0을 사용자의 IM 애플리케이션 SDKAppID로 대체
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
// 연결측에서 해당 이벤트를 수신한 후, SDK를 호출해 메시지 발송 등 기능 활성화 가능
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// 텍스트 메시지 수신 후 화면에 표시
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2. IM 서비스에 로그인
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // 로그인 성공
  if (imResponse.data.repeatLogin === true) {
    // 계정 로그인 여부와 중복 로그인 여부를 나타냄
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
:::
</dx-codeblock>
:::
</dx-tabs>

개발자의 개발 작업 및 인력 절감을 위해, TWebLive SDK를 기반으로 PC와 모바일 브라우저 모두에 적합한 [Demo](https://github.com/tencentyun/TWebLive)를 제공하고 Github에 오픈 소스를 제공합니다. 개발자는 fork&clone 프로젝트를 로컬에서 약간만 수정하면 Demo를 실행하거나 자체 프로젝트에 통합하여 배포 및 런칭할 수 있습니다.

## 작업 절차
### 1단계: 애플리케이션 생성
<dx-tabs>
::: TRTC 기반
[TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에서 왼쪽 메뉴의 [애플리케이션 관리]>[애플리케이션 생성]을 클릭하고 애플리케이션 이름을 입력한 후 [확인]을 클릭하여 TRTC 애플리케이션을 생성합니다. 생성이 완료되면 SDKAPPID를 저장하십시오.
![](https://main.qcloudimg.com/raw/871c535f4b539ad7791f10d57ef0a9f3.png)

>?동시에 동일한 SDKAppID를 가진 IM 애플리케이션이 자동 생성됩니다.
:::
::: \sIM 기반
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하고 [애플리케이션 생성]을 클릭하면 대화 상자가 나타납니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
2. 애플리케이션 이름을 입력한 후 [확인]을 클릭하면 애플리케이션이 생성됩니다.
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
3. [IM 콘솔](https://console.cloud.tencent.com/im)의 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 생성 시간 및 만료 시간을 확인할 수 있습니다.
:::
</dx-tabs>

### 2단계: 서비스 활성화 및 키 가져오기
<dx-tabs>
::: TRTC 기반
1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에서 왼쪽 메뉴의 [애플리케이션 관리]를 클릭한 뒤, 사용자가 생성한 TRTC에서 [기능 설정]을 클릭하여 애플리케이션 상세 보기로 들어갑니다.
![](https://main.qcloudimg.com/raw/bafd4eae90bd282b4f82421172d67e39.png)
2. [릴레이 푸시 스트림 활성화]를 클릭하고 릴레이 푸시 스트림 방식을 전역 자동 릴레이로 선택합니다. 릴레이 푸시 스트림 기능을 활성화하면 TRTC 방 안의 각 채널 화면마다 해당되는 재생 주소가 할당됩니다.
![](https://main.qcloudimg.com/raw/a153540779d95dff8a9b381b3566b36e.png)
>?CDN 라이브 방송을 시청하지 않는 경우, 릴레이 푸시 스트림 활성화 단계를 생략할 수 있습니다.
3. [퀵 스타트]를 클릭하여 키 정보를 조회할 수 있습니다. 키를 저장하십시오. [](id:step2)
![](https://main.qcloudimg.com/raw/8ec16ab9cab85e324a347dea511f7e4e.png)
4. [Tencent Cloud CSS 콘솔](https://console.cloud.tencent.com/live/)에서 재생 도메인을 설정하고 CNAME 설정을 완료합니다. 자세한 작업 가이드는 [CDN 라이브 방송 시청 실행](https://intl.cloud.tencent.com/document/product/647/35242) 문서를 참고하십시오.
>?CDN 라이브 방송을 시청하지 않는 경우, 재생 도메인 설정 단계를 생략할 수 있습니다.
:::
::: \sIM 기반
1. [IM 콘솔](https://console.cloud.tencent.com/im)의 전체보기 페이지에서 새로 생성한 IM 애플리케이션을 클릭하면 해당 애플리케이션의 기본 설정 페이지로 리디렉션됩니다. [기본 정보]에서 [키 표시]를 클릭하여 키 정보를 복사 및 저장합니다.
![](https://main.qcloudimg.com/raw/610dee5720e94e324a48b44f4728816a.png)
  >! 키 정보가 유출되지 않도록 잘 보관하십시오.
2. 해당 애플리케이션의 기본 설정 페이지에서 Tencent Cloud TRTC 서비스를 활성화합니다.
![](https://main.qcloudimg.com/raw/8fb2940618dfb8b7ea06eecd62212468.png)
:::
</dx-tabs>

### 3단계: Demo 다운로드 및 설정
1. [Tencent Cloud TWebLive 컴포넌트 Demo 프로젝트](https://github.com/tencentyun/TWebLive)를 다운로드 합니다.
2. `TWebLive/dist/debug/GenerateTestUserSig.js` 파일을 열고 관련 매개변수를 설정합니다.
 - SDKAPPID: [1단계](#step1)에서 획득한 실제 애플리케이션 SDKAppID로 설정합니다.
 - SECRETKEY: [2단계](#step2)에서 획득한 실제 키 정보로 설정합니다.
 - PUSHDOMAIN: CDN시청 시, 푸시 도메인을 설정합니다. (CDN 라이브 방송을 시청하지 않는 경우, 해당 설정 단계를 생략할 수 있습니다).
3. 프로젝트에서 npm을 통해 tim-js-sdk, trtc-js-sdk, tweblive의 최신 버전을 설치합니다. 프로젝트에 이미 tim-js-sdk 또는 trtc-js-sdk가 통합되어 있는 경우, 그대로 최신 버전으로 업데이트하면 됩니다.
<dx-codeblock>
::: 1 javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
:::
</dx-codeblock>
4. 프로젝트에 tweblive를 가져옵니다.
<dx-codeblock>
::: 1 javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
:::
</dx-codeblock>
5. script 태그를 통해 JS files를 가져올 경우, tim-js.js, trtc.js, tweblive.js를 프로젝트에 복사하고 순서대로 가져옵니다.
<dx-codeblock>
::: 1 javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
:::
</dx-codeblock>

>!
>- UserSig 로컬 계산 방식은 로컬 개발 디버깅에만 사용됩니다. 직접 온라인에 배포하지 마십시오. 일단 `SECRETKEY`가 노출되면 해커가 귀하의 Tencent Cloud 트래픽을 남용할 수 있습니다.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

### 4단계: Demo 실행
Chrome 브라우저에서 `dist` 리스트의 `index.html` 문서를 열면 Demo가 실행됩니다.
>!
>
>- 일반적으로 체험용 Demo는 서버에 배포가 필요하며, `https://도메인/xxx`으로 액세스하거나 직접 로컬에서 서버를 구축하여 `localhost:포트`를 통해 액세스할 수 있습니다.
- 현재 데스크톱 Chrome 브라우저가 TRTC 데스크톱 브라우저 SDK를 비교적 완벽하게 지원하므로 Chrome 브라우저를 사용하여 체험하는 것을 권장합니다.
>- TWebLive는 카메라와 마이크를 사용하여 멀티미디어를 수집하며, 체험 과정에서 Chrome 브라우저로부터 관련 알림을 수신하게 될 수 있습니다. 이 경우 [허용]을 클릭하십시오.


## 아키텍처 및 플랫폼 지원

### TWebLive 아키텍처
TWebLive 아키텍처 설계는 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/ab2b13a441da8b0631cc664f95ad18db.png)
Web 푸시와 Web 저지연 시청은 WebRTC 기술이 적용됩니다.

- 모바일 환경에서는 미니프로그램 솔루션 사용을 권장합니다. WeChat 및 모바일 QQ 미니프로그램 모두 지원되며, 각 플랫폼의 Native 기술로 구현되어, 더 나은 멀티미디어 성능을 제공하고, 주요 휴대폰 브랜드에 최적화되어있습니다.
- 교육 시나리오의 경우, 교사는 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션을 사용하길 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.
>? WebRTC는 Google이 최초 출시한 기술입니다. 현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android 플랫폼의 브라우저)에서의 지원은 완전하지 못할 수 있습니다.

### TWebLive 지원 플랫폼

|  운영 체제   |          브라우저 유형          | 브라우저 최저 버전 요구사항 | 수신(재생) | 발송(마이크) |
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
| iOS 12.1.4+ |         WeChat 내장 브라우저         |         -          |     지원     |    미지원    |
|   Android   |       모바일 QQ 브라우저       |         -          |    미지원    |    미지원    |
|   Android   |       모바일 UC 브라우저       |         -          |    미지원    |    미지원    |
|   Android   |   WeChat 내장 브라우저(TBS 커널)   |         -          |     지원     |     지원     |
|   Android   |  WeChat 내장 브라우저(XWEB 커널)   |         -          |     지원     |    미지원    |

>! H.264 버전 권한 제한으로 인해, Huawei 디바이스 상의 Chrome 브라우저와 Chrome WebView 커널의 브라우저에서는 TRTC 데스크톱 브라우저 SDK가 정상적으로 실행되지 않습니다.
[](id:sos)
## 주의 사항

- TRTC 애플리케이션과 IM 애플리케이션의 SDKAppID가 동일해야만 계정 및 인증을 중복 사용할 수 있습니다.
>- 로컬 UserSig 컴퓨팅 방식은 로컬 개발 디버깅에만 사용하고 온라인에 배포하지 마십시오. SECRETKEY가 노출되면 해커가 사용자의 Tencent Cloud 트래픽을 도용할 수 있습니다. 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참고하십시오.

## FAQ
<dx-accordion>
::: 1.\s키 조회 시 공개키와 프라이빗 키 정보만 획득할 수 있습니다. 키는 어떻게 획득하나요?
2019년 8월 이전에 생성된 TRTC와 IM 애플리케이션(SDKAppID)는 기본적으로 공개키와 개인키를 구분하는 ECDSA-SHA256 서명 알고리즘을 사용하도록 되어 있습니다. 따라서 키 사용 시 HMAC-SHA256 서명 알고리즘으로 업그레이드하는 것을 권장합니다.

- IM 업그레이드 방법은 [기본 설정](https://intl.cloud.tencent.com/document/product/1047/34540)을 참고하십시오.
- TRTC 업그레이드 방법은 [UserSig 관련 질문](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.
:::
::: 2.\s클라이언트에서 “RtcError:\sno\svalid\sice\scandidate\sfound” 오류가 발생합니다. 어떻게 처리해야 하나요?
해당 오류는 데스크톱 브라우저용 TRTC SDK가 STUN 홀 펀칭에 실패할 경우 발생합니다. 환경 요건에 따라 방화벽 설정을 확인해 주십시오. 설정이 완료되면 공식 웹사이트의 [Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
- TCP 포트: 8687
- UDP 포트: 8000, 8080, 8800, 843, 443, 16285
- 도메인: qcloud.rtc.qq.com
:::
::: 3.\s클라이언트에서 “RtcError:\sICE/DTLS\sTransport\sconnection\sfailed” 또는 \s“RtcError:\sDTLS\sTransport\sconnection\stimeout” 오류가 발생합니다. 어떻게 처리해야 하나요?
해당 오류는 데스크톱 브라우저용 TRTC SDK가 STUN 홀 펀칭에 실패할 경우 발생합니다. 환경 요건에 따라 방화벽 설정을 확인해 주십시오. 설정이 완료되면 공식 웹사이트의 [Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
- TCP 포트: 8687
- UDP 포트: 8000, 8080, 8800, 843, 443, 16285
- 도메인: qcloud.rtc.qq.com
:::
::: 4.\s10006\serror\s가 발생합니다. 어떻게 처리해야 하나요?
`"Join room failed result: 10006 error: service is suspended, if charge is overdue, renew it"` 오류가 발생하는 경우, [TRTC 콘솔](https://console.cloud.tencent.com/rav)에 로그인하여 생성한 애플리케이션을 클릭한 후 [계정 정보]를 클릭하여 계정 정보 페이지에서 TRTC 애플리케이션의 서비스 상태가 사용 가능한 상태인지 확인합니다.
![](https://main.qcloudimg.com/raw/13c9b520ea333804cffb4e2c4273fced.png)
:::
::: 5.\sWebRTC\s 저지연 재생 시, iOS\s 풀 스트림 재생이 불가한 경우 어떻게 합니까？
1. tweblive sdk를 1.2.0 버전으로 업그레이드합니다.
2. `player.startPlay()` 메소드 호출 후, `PLAYER_AUTOPLAY_NOT_ALLOWED` 브라우저가 자동 재생을 허용하지 않음을 수신합니다.
3. 자동 재생 불가를 수신 후, 재생 버튼이 나타나며 이를 클릭하면 [resumePlay()](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/Player.html#resumePlay) 메소드가 호출되고 재생이 복구됩니다.
>?iOS는 자동 재생이 제한되어 있습니다. [자동 재생 제한 해결 방법](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)을 참고하십시오.
:::
</dx-accordion>

## 결론

본 문서에서는 Tencent Cloud의 새로운 Web 라이브 방송 인터랙션 컴포넌트인 TWebLive에 대해 소개했습니다. 개발자는 해당 SDK를 연결하여 간편하게 Web 푸시, Web 저지연 시청, CDN 시청, 실시간 채팅 인터랙션(또는 댓글 자막) 등의 기능을 실현할 수 있으며, 기존의 Flash 푸시 스트림 방식을 완벽히 대체할 수 있습니다.

또한 자세한 연결 방법 및 [온라인 Demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)를 제공합니다. 현재 TWebLive는 주요 데스크톱 브라우저에서 보다 나은 지원을 제공하며, 모바일에서는 미니프로그램의 솔루션을 지원합니다.

향후 Tencent Cloud는 푸시 스트림 측에서의 화면 공유, 이미지 메시지 인터랙션, 시청자 측에서의 다중 채널 시청(WebRTC 저지연 채널 및 CDN 채널), 호스트와 시청자 마이크 연결 인터랙션 등과 같은 전면적인 라이브 방송 기능 서비스를 제공할 예정입니다.

참고 자료:

- [TWebLive 인터페이스 매뉴얼](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html)
- [Demo 체험](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)
