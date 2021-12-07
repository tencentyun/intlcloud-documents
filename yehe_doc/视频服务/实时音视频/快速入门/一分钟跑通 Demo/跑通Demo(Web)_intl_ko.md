본 문서에서는 Tencent Cloud TRTC Web SDK Demo를 빠르게 실행하는 방법을 소개합니다.

## 지원 플랫폼

WebRTC는 Google이 최초 출시한 기술입니다. 현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android의 브라우저)에서의 지원은 완전하지 못할 수 있습니다.
- 교육 시나리오의 경우, 강의측에 안정성이 더 높은 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션 사용을 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다.

Tencent Cloud TRTC Web SDK의 상세 지원 관련 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/41664)을 참고하십시오.
>! 
>- 브라우저에서 [TRTC Web SDK 기능 테스트 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC의 모든 기능이 지원되는지 테스트할 수 있습니다(예: WebView 등 브라우저 환경).
>- H.264 버전 권한 제한으로 인해 Huawei 시스템의 Chrome 브라우저와 Chrome WebView 커널의 브라우저에서는 TRTC Web SDK가 정상적으로 실행되지 않습니다.

[](id:requirements)
## 환경 요건
- 최신 버전의 Chrome 브라우저를 사용해 주십시오.
- TRTC Web SDK는 다음 포트에 종속되어 데이터를 전송합니다. 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [공식 Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html)를 통해 설정이 적용되었는지 확인할 수 있습니다.

자세한 내용은 [방화벽 제한 대응 관련 질문](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.

## URL 도메인 프로토콜 제한
| 응용 시나리오     | 프로토콜             | 수신(재생) | 발송(마이크 켜짐) | 화면 공유 | 비고 |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| 프로덕션 환경     | HTTPS 프로토콜        | 지원         | 지원         | 지원     | 권장 |
| 프로덕션 환경     | HTTP 프로토콜         | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | http://localhost | 지원         | 지원         | 지원     | 권장 |
| 로컬 개발 환경 | http://127.0.0.1 | 지원         | 지원         | 지원     |      |
| 로컬 개발 환경 | http://[로컬 IP]  | 지원         | 미지원       | 미지원   |      |
| 로컬 개발 환경 | file:///         | 지원         | 지원         | 지원     |      |

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계

[](id:step1)

### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, **개발 지원**>**[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)**을 선택합니다.
2. **애플리케이션 생성**을 클릭하고 `TestTRTC`와 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 생성된 경우 **기존 애플리케이션 선택**을 클릭합니다.
3. 실제 비즈니스 요구에 따라 태그를 추가하거나 편집하고 **생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)
>?
>- 애플리케이션 이름은 숫자, 중국어, 영어, 언더바만 포함할 수 있으며 15자를 초과할 수 없습니다.
>- 태그는 Tencent Cloud에서 다양한 리소스를 식별하고 구성하는 데 사용됩니다. 예를 들어, 기업이 여러 사업부를 가지고 있고, 각 부서에는 하나 이상의 TRTC 애플리케이션이 있을 수 있는데, 이 경우 기업은 TRTC 애플리케이션에 태그를 추가하여 부서 정보를 표시할 수 있습니다. 태그는 필수 사항이 아니며, 실제 비즈니스 니즈에 따라 추가하거나 편집할 수 있습니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 **‘다운로드 완료, 다음 단계’**를 클릭합니다.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `Web/base-js/js/debug/GenerateTestUserSig.js` 파일을 엽니다.
3. `GenerateTestUserSig.js` 파일에서 관련 매개변수를 설정합니다.
  <ul><li>SDKAPPID: 0으로 기본 설정되어 있으며 실제 SDKAppID로 설정하십시오.</li>
  <li>SECRETKEY: 공백으로 기본 설정되어 있으며 실제 키 정보로 설정하십시오.</li></ul> 
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 **붙여넣기 완료, 다음 단계** 를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 **콘솔 개요로 돌아가기**를 클릭합니다.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

### 4단계: Demo 실행
Chrome 브라우저에서 Demo의 루트 디렉터리에 있는 `index.html` 파일을 열면 Demo가 실행됩니다.

>!
> - 일반적으로 체험용 Demo는 서버에 배포가 필요하며, `https://도메인/xxx`로 액세스하거나 직접 로컬에서 서버를 구축하여 `localhost:포트`를 통해 액세스할 수 있습니다.
> - 현재 데스크톱 Chrome 브라우저가 TRTC Web SDK를 비교적 완벽하게 지원하므로 Chrome 브라우저를 사용하여 체험하는 것을 권장합니다.


- **방 추가**를 클릭하여 멀티미디어 통화 방을 추가하고 로컬 멀티미디어 스트림을 배포합니다.
 여러 페이지를 열어 모든 페이지에서 **방 추가**를 클릭하면, 정상 실행된 경우 여러 화면을 보면서 TRTC 통화 시뮬레이션을 할 수 있습니다.
- 카메라 아이콘을 클릭하면 카메라 디바이스를 선택할 수 있습니다.
- 마이크 아이콘을 클릭하면 마이크 디바이스를 선택할 수 있습니다.
>?WebRTC는 카메라와 마이크를 사용하여 멀티미디어를 수집합니다. 체험 과정에서 Chrome 브라우저로부터 관련 안내를 수신할 수 있습니다. **허용**을 클릭하십시오.


## FAQ
### 1. 키 조회 시 공개키와 프라이빗 키 정보만 획득할 수 있습니다. 키는 어떻게 획득합니까?
TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트를 진행하지 않을 경우 [기존 버전 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있으며, 이미 업데이트한 경우 필요에 따라 기존/신규 알고리즘을 전환할 수 있습니다.

업데이트/전환 작업:
 1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
 2. 왼쪽 메뉴에서 **애플리케이션 관리**를 선택한 후 대상 애플리케이션이 속한 행의 **애플리케이션 정보**를 클릭합니다.
 3. **퀵 스타트** 탭을 선택하고 **2단계: UserSig 발급 키 획득** 에서 **업데이트**, **비대칭 암호화** 또는 **HMAC-SHA256**을 클릭합니다.
  - 업데이트
  - 기존 버전 알고리즘 ECDSA-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - 신규 버전 알고리즘 HMAC-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. 클라이언트에서 ‘RtcError: no valid ice candidate found’ 오류가 발생합니다. 어떻게 처리해야 합니까?
해당 오류는 TRTC Web SDK STUN 홀 펀칭 실패 시 발생합니다. [환경 요건](#requirements)에 따라 방화벽 설정을 확인해 주십시오.

### 3. 클라이언트에서 ‘RtcError: ICE/DTLS Transport connection failed’ 또는 ‘RtcError: DTLS Transport connection timeout’ 오류가 발생합니다. 어떻게 처리해야 합니까?
해당 오류는 TRTC Web SDK MediaConnect 터널 구축 실패 시 발생합니다. [환경 요건](#requirements)에 따라 방화벽 설정을 확인해 주십시오.

### 4. 10006 error가 발생합니다. 어떻게 처리해야 합니까?
‘Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it’ 오류가 발생하는 경우 TRTC 애플리케이션의 서버 상태가 정상인지 확인합니다.
[TRTC 콘솔](https://console.cloud.tencent.com/rav)에 로그인하여 생성한 애플리케이션을 클릭한 후 **계정 정보**를 클릭하면 서비스 상태를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)
