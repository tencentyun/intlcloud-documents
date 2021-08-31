본 문서에서는 Tencent Cloud TRTC Demo(Flutter)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- Flutter 2.0 이상 버전
- Android 개발:
  - Android Studio 3.5 이상 버전
  - 앱에서 Android 4.1 이상 버전의 디바이스 요구됨
- iOS 개발:
  - Xcode 11.0 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국대륙 내 TRTC 인스턴스를 구매할 수 없습니다.

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
2. `/lib/debug/GenerateTestUserSig.dart` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.java` 파일에서 관련 매개변수를 설정합니다.
<ul><li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
	<li/>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
4. 붙여넣기 완료 후 [복사 및 붙여넣기 완료, 다음 단계]를 클릭하면 생성됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>!
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 App에서 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

### 4단계: 컴파일 실행
1. `flutter pub get`을 실행합니다.
2. 컴파일 실행 디버깅:
####  Android
1. `flutter run`을 실행합니다.
2. Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램을 엽니다.
3. [실행]을 클릭합니다.
#### iOS
1. XCode(11.0 버전 이상)를 사용해 소스 코드 디렉터리에 있는 `/ios 프로그램`을 엽니다.
2. Demo 프로그램을 컴파일 및 실행합니다.



## FAQ

- [2대의 휴대폰에서 동시에 Demo를 실행했을 때, 서로의 화면이 보이지 않는 이유는 무엇인가요?](https://intl.cloud.tencent.com/document/product/647/39242)
- [방화벽에 어떤 제한이 있나요?](https://intl.cloud.tencent.com/document/product/647/39242)
- [iOS 패키징에 Crash가 실행됩니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [iOS에서 비디오가 표시되지 않습니다.(Android는 정상)](https://intl.cloud.tencent.com/document/product/647/39242)
- [SDK 버전 업데이트 후 iOS CocoaPods 실행 시 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Android Manifest merge failed 컴파일에 실패합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [서명이 없어 실제 기기에서 디버깅 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [플러그 인 내의 swift 파일에 추가/삭제 후, build 시 상응하는 파일을 찾을 수 없습니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run 오류 “Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Pod install 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run 시 iOS 버전에 따른 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)



