본 문서에서는 Tencent Cloud의 Web 라이브 방송 인터랙션 컴포넌트를 빠르게 실행하는 체험용 Demo를 소개합니다.

## 효과


## 환경 요건

- 최신 버전의 Chrome 브라우저를 사용해 주십시오.
- TWebLive는 다음 포트에 종속되어 데이터를 전송합니다. 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [홈페이지 Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
  - TCP 포트: 8687
  - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
  - 도메인: qcloud.rtc.qq.com

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 내 TRTC 인스턴스를 구매할 수 없습니다.

## 작업 순서
<span id="step1"></span>
### 1단계: 신규 애플리케이션 생성

1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
2. [Application Management](https://console.cloud.tencent.com/trtc/app)로 이동하여 [Create Application]을 클릭하고 애플리케이션 이름(예: `testtrtc`)을 입력한 후 [Confirm]을 클릭합니다.
<span id="step2"></span>
### 2단계: SDKAppID와 키 획득

1. 애플리케이션 리스트에서 새로 생성한 애플리케이션을 찾아 오른쪽에 있는 [Application Info]를 클릭해 상세 페이지로 진입하면 `SDKAppID` 정보를 복사 및 저장할 수 있습니다.
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
2. [Quick Start] 탭을 클릭하고 [Step 2: obtain the secret key to issue UserSig] 탭에서 [Copy Secret Key]를 클릭합니다.
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>! 키 정보가 노출되지 않도록 잘 보관해 주십시오.
<span id="step3"></span>
### 3단계: Demo 소스 다운로드 및 설정

1. Tencent Cloud Web 라이브 방송 인터랙션 구성 요소 Demo 프로그램을 다운로드합니다. [다운로드 주소](https://github.com/tencentyun/TWebLive)
2. `TWebLive/dist/debug/GenerateTestUserSig.js` 파일을 열고 관련 매개변수를 설정합니다.
 - SDKAPPID: [2단계](#step2)에서 획득한 실제 애플리케이션 `SDKAppID`로 설정합니다.
 - SECRETKEY: [2단계](#step2)에서 획득한 실제 키 정보로 설정합니다.




>!
>- UserSig 로컬 계산 방식은 로컬 개발 디버깅에만 사용됩니다. 직접 온라인에 배포하지 마십시오. 일단 `SECRETKEY`가 노출되면 해커가 귀하의 Tencent Cloud 트래픽을 남용할 수 있습니다.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 귀하의 서버에 통합하고 App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 귀하의 App이 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/1047/34385)을 참조하십시오.
<span id="step4"></span>
### 4단계: Demo 실행

Chrome 브라우저에서 `dist` 디렉터리의 `index.html` 파일을 열면 Demo가 실행됩니다.

>!
>- 일반적으로 체험용 Demo는 서버에 배포가 필요하며, `https://도메인/xxx`으로 액세스하거나 직접 로컬에서 서버를 구축하여 `localhost:포트`를 통해 액세스할 수 있습니다.
- 현재 데스크톱 Chrome 브라우저가 TRTC 데스크톱 브라우저 SDK를 비교적 완벽하게 지원하므로 Chrome 브라우저를 사용하여 체험하는 것을 권장합니다.

**Demo 실행 인터페이스는 다음과 같습니다.**

TWebLive는 카메라와 마이크를 사용하여 멀티미디어를 수집하며 체험 과정에서 Chrome 브라우저에서 관련 안내를 수신할 수 있습니다. [허용]을 클릭하십시오.

## 플랫폼 지원

WebRTC는 Google이 최초 출시한 기술입니다. 현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android 플랫폼의 브라우저)에서의 지원은 완전하지 못할 수 있습니다.

- 응용 시나리오가 주로 교육 분야라면 교사는 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션을 사용하길 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.

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
|   Android   |       모바일 QQ 브라우저       |         -          |    미지원    |    미지원    |
|   Android   |       모바일 UC 브라우저       |         -          |    미지원    |    미지원    |
|   Android   |   WeChat 내부 웹 페이지(TBS 커널)   |         -          |     지원     |     지원     |
|   Android   |  WeChat 내부 웹 페이지(XWEB 커널)   |         -          |     지원     |    미지원    |

>! H.264 버전 권한 제한으로 인해 화웨이 시스템의 Chrome 브라우저와 Chrome WebView 커널의 브라우저에서는 TRTC 데스크톱 브라우저 SDK가 정상적으로 실행되지 않습니다.

## FAQ

### 1. 키 조회 시 공개키와 프라이빗 키 정보만 획득할 수 있습니다. 키는 어떻게 획득합니까?

TRTC SDK 6.6 버전(2019년 08월)부터 신규 서명 알고리즘인 HMAC-SHA256이 활성화됩니다. 이전 버전에서 애플리케이션을 생성한 경우 먼저 서명 알고리즘을 업그레이드한 후 신규 암호화 키를 획득할 수 있습니다.

### 2. 클라이언트에서 “RtcError: no valid ice candidate found” 오류가 발생합니다. 어떻게 처리해야 합니까?

해당 오류는 TRTC 데스크톱 브라우저 SDK가 STUN 홀 펀칭 실패 시 발생합니다. 환경 요건에 따라 방화벽 설정을 확인해 주십시오.

### 3. 클라이언트에서 "RtcError: ICE/DTLS Transport connection failed" 또는 “RtcError: DTLS Transport connection timeout” 오류가 발생합니다. 어떻게 처리해야 합니까?

해당 오류는 TRTC 데스크톱 브라우저 SDK가 MediaConnect 터널 구축 실패 시 발생합니다. 환경 요건에 따라 방화벽 설정을 확인해 주십시오.

### 4. 10006 error가 발생합니다. 어떻게 처리해야 합니까?

`"Join room failed result: 10006 error: service is suspended, if charge is overdue, renew it"` 오류가 발생하는 경우, TRTC 애플리케이션의 서버가 사용 가능한 상태인지 확인하십시오.
[TRTC 콘솔](https://console.cloud.tencent.com/rav)에 로그인하여 생성한 애플리케이션을 클릭한 후 [Account Information]을 클릭하면 서버 상태를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)


## 관련 문서

- [TWebLive 인터페이스 매뉴얼](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [온라인 Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
