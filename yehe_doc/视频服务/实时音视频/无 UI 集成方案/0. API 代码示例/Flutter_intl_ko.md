본 문서에서는 Tencent Cloud TRTC Demo(Flutter)를 빠르게 실행하는 방법을 소개합니다.

>! 현재 Windows/MacOs에서는 화면 공유 및 디바이스 선택 기능이 지원되지 않습니다.

## 환경 요건
- Flutter 2.0 또는 이후 버전.
- **Android 개발:**
  - Android Studio 3.5 이상 버전
  - Android 4.1 이상 버전의 디바이스
- **iOS & macOS 개발:**
  - Xcode 11.0 이상 버전
  - osx 시스템 10.11 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- **Windows 개발:**
    - 운영 체제: Windows 7 SP1 이상(x86-64 기반 64비트 운영 체제).
    - 디스크 공간: IDE 및 일부 툴 설치 외에 최소 1.64GB의 공간 필요.
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/) 설치.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com) 계정이 있어야 합니다.

## 작업 단계

### 1단계: 애플리케이션 생성

1. TRTC 콘솔에 로그인하고 왼쪽 사이드바에서 [[애플리케이션 관리](https://console.tencentcloud.com/trtc/app)]를 선택합니다.
2. [애플리케이션 생성]을 클릭하고 'APIExample'과 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 있는 경우 [기존 애플리케이션 선택]을 선택하고 [다음]을 클릭합니다
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### 2단계: 샘플 코드 다운로드

1. UI 없음을 선택하고 [[Github](https://github.com/LiteAVSDK/TRTC_Flutter/tree/master/TRTC-Simple-Demo)]로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
2. [다음]을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### 3단계: 프로젝트 구성

1. 데모 프로젝트를 실행 중인 경우 [테스트]를 선택합니다. SDKAppID와 Secret key를 기록해 둡니다
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 이전에 다운로드한 파일을 열고 `/lib/debug/GenerateTestUserSig.dart`를 찾아 열고 다음 매개변수를 설정합니다.
  - SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
  - SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 Secret key로 설정하십시오.
3. [다음]을 클릭합니다.

>?
>- 이 문서에서 설명하는 UserSig를 생성하는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 쉽게 디컴파일되고 역전될 수 있으며, 키가 공개되면 해커가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 TRTC-Simple-Demo의 로컬 실행 및 디버깅에만 적합합니다**.
>- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

### 4단계: 데모 컴파일 및 실행

1. `flutter pub get` 실행
2. 프로젝트를 빌드하고 실행합니다.

#### Android:

1. 'flutter run' 실행
2. Android Studio(3.5 이상 버전)로 데모 프로젝트를 열고 프로젝트를 [실행]합니다.

#### iOS:

1. `cd ios` 실행
3. 'pod install' 실행
2. XCode(11.0 버전 이상)를 사용하여 소스 코드 디렉터리에서 `/ios`를 엽니다. Demo 프로젝트를 컴파일하고 실행합니다.

#### windows:

1. windows 지원 활성화: `flutter config --enable-windows-desktop` 실행
2. `flutter run -d windows` 실행

#### macOS

1. macOS 지원 활성화: `flutter config --enable-macos-desktop` 실행
2. `cd macos` 실행
3. 'pod install' 실행
4. `flutter run -d macos` 실행


## FAQ
### TRTC 로그는 어떻게 조회합니까?
TRTC 로그는 기본적으로 `.xlog`로 압축 및 암호화됩니다. 주소는 다음과 같습니다.
- **iOS**: sandbox 의 `Documents/log`.
- **Android**:
	- 6.7 이하 버전: `/sdcard/log/tencent/liteav`.
	- 6.8-8.5 버전: `/sdcard/Android/data/패키지명/files/log/tencent/liteav/`.

### 비디오가 Android에서는 표시되지만 iOS에서는 표시되지 않으면 어떻게 해야 하나요?
프로젝트의 info.plist에서, `io.flutter.embedded_views_preview`의 값이 YES인지 확인하십시오. 

### Android Studio에서 Manifest merge failed 오류가 발생하면 어떻게 해야 하나요?
'/example/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
    
1. `xmlns:tools="http://schemas.android.com/tools"`를 manifest에 추가합니다.
2. `tools:replace="android:label"`을 application에 추가합니다.
![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

>? 더 많은 FAQ는 [Flutter FAQ](https://intl.cloud.tencent.com/document/product/647/39242)를 참고하십시오.

