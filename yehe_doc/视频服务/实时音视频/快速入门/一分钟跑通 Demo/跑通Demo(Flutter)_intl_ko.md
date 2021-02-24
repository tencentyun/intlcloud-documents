본 문서에서는 Tencent Cloud TRTC Demo(Flutter)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건
- Flutter 1.12 이상 버전
- Android 개발:
  - Android Studio 3.5 이상 버전
  - 앱에서 Android 4.1 이상 버전의 디바이스 요구됨
- iOS 개발:
  - Xcode 11.0 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다. 실명 인증을 하지 않은 사용자는 중국 대륙 내 TRTC 인스턴스를 구매할 수 없습니다.

## 작업 순서

[](id:step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 보조] > [빠른 Demo 활성화](https://console.cloud.tencent.com/trtc/quickstart)를 선택합니다.
2. [시작하기]를 클릭하고 애플리케이션 명칭(예: 'TestTRTC')을 입력한 후 [애플리케이션 생성]을 클릭합니다.

<span id="step2"></span>

### 2단계: SDK와 Demo 소스 코드 다운로드
1. [Github](https://github.com/c1avie/trtc_demo)를 클릭해 Github로 리디렉션한 뒤, SDK 및 관련된 Demo 소스 코드를 다운로드합니다.
![](https://main.qcloudimg.com/raw/7a4343e8004f1a459637267aa934db13.png)
2. 다운로드 완료 후, TRTC 콘솔로 돌아가 [다운로드 완료, 다음 단계]를 클릭하면 SDKAppID와 키 정보를 조회할 수 있습니다.


[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. [2단계](#step2)에서 다운로드한 소스 패키지를 압축 해제합니다.
2. '/lib/debug/GenerateTestUserSig.dart' 파일을 찾아 엽니다.
3. 'GenerateTestUserSig.java' 파일에서 관련 매개변수를 설정합니다.
<ul><li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
	</li>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.
<img src="https://main.qcloudimg.com/raw/8933718aafec140c01ea5bae0bf8cace.png"/>
4. TRTC 콘솔로 돌아가 [붙여넣기 완료, 다음 단계]를 클릭합니다.
5. [가이드 닫기, 콘솔 관리 애플리케이션 열기]를 클릭합니다.

>!
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 본 방법에서의 SECRETKEY는 디컴파일로 크래킹되기 쉬워, 일단 키가 유출되면 해커가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 정확한 UserSig 발급 방식은 다음과 같습니다. UserSig 계산 코드를 사용자 서버에 통합하고, App 방향의 인터페이스를 제공합니다. UserSig가 필요할 때 App에서 비즈니스 서버로 동적 UserSig를 요청합니다. 자세한 내용은 [서버의 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오.

### 4단계: 컴파일 실행
1.'flutter pub get'을 실행합니다.
2.컴파일 실행 디버깅:

#### Android
1. 'flutter run'을 실행합니다.
2. Android Studio(3.5 버전 이상)를 사용하여 오픈 소스 프로그램을 엽니다.
3. [실행]을 클릭합니다.

#### iOS
1. XCode(11.0 버전 이상)를 사용해 오픈 소스 디렉터리에 있는 '/ios 프로그램'을 엽니다.
2. Demo 프로그램을 컴파일 및 실행합니다.




## FAQ

- [2대의 모바일에서 동시에 Demo를 실행할 경우 서로의 화면이 보이지 않는 이유는 무엇인가요?](https://intl.cloud.tencent.com/zh/document/product/647/39242#que1)
- [방화벽에 어떤 제한이 있나요?](hhttps://intl.cloud.tencent.com/zh/document/product/647/39242#que2)
- [iOS 패키징에 Crash가 실행됩니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que3)
- [iOS에서 비디오가 표시되지 않습니다(Android는 정상).](https://intl.cloud.tencent.com/zh/document/product/647/39242#que4)
- [SDK 버전 업데이트 후 iOS CocoaPods 실행 시 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que5)
- [Android Manifest merge failed 컴파일에 실패합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)
- [서명이 없어 실제 기기에서 디버깅 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que7)
- [플러그 인 내에 swift 파일에 추가/삭제 후, build 시 상응하는 파일을 찾을 수 없습니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que8)
- [Run 오류 "Info.plit, error: No value at that key path or invalid key path: NSBonjourServices"가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que9)
- [Pod install 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que10)
- [Run 시 iOS 버전에 따른 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que11)



