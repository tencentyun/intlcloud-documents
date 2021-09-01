본 문서에서는 Tencent Cloud TRTC Demo(Android)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- 최소 Android 4.1(SDK API Level 16) 호환, Android 5.0(SDK API Level 21) 이상 권장
- Android Studio 3.5 이상 버전
- 앱에서 Android 4.1 이상 디바이스 요구됨

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 내 TRTC 서비스를 구매할 수 없습니다.

## 작업 순서
[](id:step1)
### 1단계: 신규 애플리케이션 생성

1. TRTC 콘솔에 로그인한 후, [개발 지원]>[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)을 선택합니다.
2. 애플리케이션 명칭(예: TestTRTC)을 입력한 후 [생성]을 클릭합니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드

1. 실제 비즈니스 수요에 따라 SDK 및 관련 Demo 소스 코드를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:step3)
### 3단계: Demo 프로그램 파일 설정

1. 설정 변경 페이지로 들어가서 다운로드한 소스 패키지에 적합한 개발 환경을 선택합니다.
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
	<ul>
	<li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
	<li/>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
4. 붙여넣기 완료 후 [복사 및 붙여넣기 완료, 다음 단계]를 클릭하면 생성됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 App에서 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

### 4단계: 컴파일 실행
Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램인 `TRTCScenesDemo`를 열고 [실행]을 클릭합니다.

## FAQ
### 1. 키 조회 시 공개키와 개인키의 정보만 획득할 수 있습니다. 키는 어떻게 획득하나요?
TRTC SDK 6.6 버전(2019년 08월)부터 새로운 서명 알고리즘 HMAC-SHA256이 적용되었습니다. 이전에 생성된 애플리케이션은 서명 알고리즘을 업데이트해야 새로운 암호화 키를 획득할 수 있습니다. 업데이트를 진행하지 않을 경우 [기존 버전 알고리즘 ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)을 계속 사용할 수 있으며, 이미 업데이트한 경우 필요에 따라 기존/신규 알고리즘을 전환할 수 있습니다.

업데이트/전환 작업:
 1. [TRTC 콘솔](https://console.cloud.tencent.com/trtc)에 로그인합니다.
 2. 왼쪽 메뉴에서 [애플리케이션 관리]를 선택한 후 타깃 애플리케이션이 속한 행의 [애플리케이션 정보]를 클릭합니다.
 3. [퀵 스타트] 탭을 선택한 후 [2단계: UserSig 발급 키 획득]의 [업데이트], [비대칭 암호화] 또는 [HMAC-SHA256]을 클릭합니다.
  - 업데이트:
  - 기존 버전 알고리즘 ECDSA-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/a8737123c1e3cc0f7eb34901ed2629f7.png)
  - 신규 버전 알고리즘 HMAC-SHA256으로 전환- 최신 버전 알고리즘 HMAC-SHA256으로 전환:
      ![](https://main.qcloudimg.com/raw/701fcde1a562bf9fbbb0d426948e311e.png)

### 2. 2대의 휴대폰에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇인가요?
2대의 휴대폰에서 Demo를 실행할 경우 각자 다른 UserID를 사용해야 합니다. TRTC에서는 동일 UserID(SDKAppID가 다를 경우 제외)를 2개의 단말에서 동시에 사용할 수 없습니다.

### 3. 방화벽에 어떤 제한이 있나요?
SDK는 UDP 프로토콜을 통해 멀티미디어를 전송하므로, UDP를 차단하는 공용 네트워크에서는 사용할 수 없습니다. 이와 유사한 문제가 발생하는 경우 [기업용 방화벽 제한 대응](https://intl.cloud.tencent.com/document/product/647/35164)을 참조하여 진단 및 해결하십시오.
