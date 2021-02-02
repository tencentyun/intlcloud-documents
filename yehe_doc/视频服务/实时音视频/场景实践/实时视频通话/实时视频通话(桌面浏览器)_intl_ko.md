본 문서에서는 브라우저에서 비디오 통화를 실행하는 솔루션을 소개하며, 다음과 같이 두 장으로 나뉘어 있습니다.
- 1. 서비스 활성화 및 Tencent Cloud에서 제공하는 Demo 제작 방법 소개
- 2. TRTCCalling 모듈을 사용한 비디오 통화 기능의 빠른 구축 방법 소개

## 환경 요건
최신 버전의 Chrome 브라우저를 사용하십시오. 현재 데스크톱 Chrome 브라우저가 TRTC 데스크톱 브라우저 SDK를 비교적 완벽하게 지원하므로 Chrome 브라우저를 사용하여 체험하는 것을 권장합니다.

TRTCCalling은 다음 포트에 종속되어 데이터를 전송합니다. 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [홈페이지 Demo](https://demo-1252463788.cos.ap-shanghai.myqcloud.com/trtccalling/demo/index.html)에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
  - TCP 포트: 8687
  - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
  - 도메인: qcloud.rtc.qq.com

현재 해당 솔루션에서 지원하는 플랫폼은 다음과 같습니다.

| 운영 체제 |          브라우저 유형          | 브라우저 최저 버전 요구사항 |
| :------: | :--------------------------: | :----------------: |
|  Mac OS  |     데스크톱 Safari 브라우저     |        11+         |
|  Mac OS  |     데스크톱 Chrome 브라우저     |        56+         |
|  Mac OS  |     데스크톱 Firefox 브라우저     |        56+         |
|  Mac OS  |      데스크톱 Edge 브라우저       |        80+         |
| Windows  |     데스크톱 Chrome 브라우저     |        56+         |
| Windows  | 데스크톱 QQ 브라우저(고속 커널) |       10.4+        |
| Windows  |    데스크톱 Firefox 브라우저     |        56+         |
| Windows  |      데스크톱 Edge 브라우저      |        80+         |

## 테스트 Demo 제작


<span id="step1"></span>
### 1단계: 신규 애플리케이션 생성

1. [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국대륙 실시간 비디오 통화 인스턴스를 구매할 수 없습니다.
2. TRTC 콘솔에 로그인한 후, [Development Assistance] > [Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
3. [시작하기]를 클릭하고 애플리케이션 이름(예: `TestTRTC`)을 입력한 후 [Create Application]을 클릭합니다.

<span id="step2"></span>

### 2단계: SDK와 Demo 소스 코드 다운로드
1. 커서를 상응하는 카드로 이동한 후 [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Web/TRTCScenesDemo/trtc-calling-web)를 클릭하여 Github(또는 [ZIP](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/H5_latest.zip?_ga=1.195966252.185644906.1567570704) 클릭)로 이동한 뒤 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 확인할 수 있습니다.

<span id="step3"></span>
### 3단계: Demo 프로그래밍 파일 설정

1. [2단계](#step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. `Web/TRTCScenesDemo/trtc-calling-web/public/debug/GenerateTestUserSig.js` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
  - SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  - SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!
>본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 본 방법에서의 SECRETKEY는 디컴파일로 크래킹되기 쉬워, 일단 키가 유출되면 해커가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 App이 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

<span id="step4"></span>

### 4단계: Demo 실행
1. npm 명령 프롬프트에 다음 명령어를 순서대로 입력합니다.
```
npm install
npm run serve
```
2. Chrome 브라우저를 실행하여 `http://localhost:8080/` 링크를 엽니다. 모두 정상적으로 실행되면 다음 이미지와 같이 Demo 실행 인터페이스가 표시됩니다.
3. 사용자 userid를 입력하고 [Log In]을 클릭한 후 [비디오 통화]를 선택합니다.
4. 호출할 userid를 입력하고 [호출]을 클릭합니다.
5. 바로 비디오 통화를 진행할 수 있습니다.


## 비디오 통화 구축
### 1단계: TRTCCalling 모듈 통합

>?
>- v0.6.0 버전부터 종속 패키지[trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk), [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk), [tsignaling](https://www.npmjs.com/package/tsignaling)를 수동 설치해야 합니다.
>- trtc-calling-js.js 용량을 축소하고 액세스측에서 사용한 trtc-js-sdk, tim-js-sdk, tsignaling과 충돌이 발생하지 않도록 trtc-calling-js.js에 trtc-js-sdk, tim-js-sdk, tsignaling을 패키징하지 않았으니 사용 전에 수동으로 종속 패키지를 설치하십시오.

```javascript javascript
  npm i trtc-js-sdk --save
  npm i tim-js-sdk --save
  npm i tsignaling --save
  npm i trtc-calling-js --save
  //script 방식으로 trtc-calling-js를 사용하는 경우 순서에 따라 먼저 trtc.js를 수동으로 가져와야 합니다.
  <script src="./trtc.js"></script>
  // 이어서 tim-js.js 수동으로 가져오기
  <script src="./tim-js.js"></script>
  // 그리고 다시 tsignaling.js 수동으로 가져오기
  <script src="./tsignaling.js"></script>
  // 마지막으로 다시 trtc-calling-js.js 수동으로 가져오기
  <script src="./trtc-calling-js.js"></script>
```

### 2단계: TRTCCalling 객체 생성
TRTCCalling 객체를 생성하고 SDKAppID 매개변수를 귀하의 SDKAppID로 설정합니다.
```javascript javascript
import TRTCCalling from 'trtc-calling-js';

let options = {
  SDKAppID: 0 // 액세스 시 0이 귀하의 SDKAppID로 대체됩니다.
};
const trtcCalling = new TRTCCalling(options);
```

### 3단계: 로그인 완성
login 함수를 호출하여 로그인 작업을 완성합니다. 매개변수 중 userID는 사용자명이며, userSig는 사용자 서명입니다. userSig의 계산 방법은 [userSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

```javascript
trtcCalling.login({
  userID,
  userSig,
});
```

### 4단계: 1대1 통화 구현
#### 발신자: 다른 사용자 호출
```javascript
trtcCalling.call({
  userID,  //사용자 ID
  type: 2, //통화 유형, 0 - 알 수 없음, 1 - 음성 통화, 2 - 비디오 통화
  timeout  //초대 초과 시간, 단위 s(초)
});
```

#### 수신자: 새로운 호출을 받는 사용자
```javascript
// 수신
trtcCalling.accept({
  inviteID, //초대 ID, 초대 1회 식별
  roomID,   //통화 방 번호 ID
  callType  //0 - 알 수 없음, 1 - 음성 통화, 2 - 비디오 통화
});
//거절
trtcCalling.reject({ 
  inviteID, //초대 ID, 초대 1회 식별
  isBusy //통화 중 여부, 0 - 알 수 없음, 1 - 음성 통화, 2 - 비디오 통화
  })
```

#### 로컬 카메라 켜기
```javascript
trtcCalling.openCamera()
```

#### 원격 비디오 화면 표시
```javascript
trtcCalling.startRemoteView({
  userID, //원격 사용자 ID
  videoViewDomID //해당 사용자 데이터를 해당 DOM ID 노드로 렌더링
})
```

#### 로컬 미리보기 화면 표시
```javascript
trtcCalling.startLocalView({
  userID, //로컬 사용자 ID
  videoViewDomID //해당 사용자 데이터를 해당 DOM ID 노드로 렌더링
})
```

#### 끊기
```javascript
trtcCalling.hangup()
```
