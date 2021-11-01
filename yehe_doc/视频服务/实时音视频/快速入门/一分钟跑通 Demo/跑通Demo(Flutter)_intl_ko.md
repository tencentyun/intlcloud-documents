본 문서에서는 Tencent Cloud TRTC Demo(Flutter)를 빠르게 실행하는 방법을 소개합니다.

>! 현재 Windows/MacOs는 오디오만 지원하며 비디오 인터페이스는 지원되지 않습니다. Android/iOS는 영상 통화를 지원합니다.

## 환경 요건
- Flutter 2.0 또는 이후 버전.
- **Android 개발: **
  - Android Studio 3.5 또는 이후 버전.
  - Android 4.1 또는 이후 버전의 디바이스.
- **iOS & macOS 개발: **
  - Xcode 11.0 또는 이후 버전.
  - osx 시스템 버전은 10.11 및 이후 버전이 요구됩니다.
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- **Windows 개발: **
    - 운영 체제: Windows 7 SP1 이상(x86-64 기반 64비트 운영 체제).
    - 디스크 공간: IDE 및 일부 툴 설치 외에 최소 1.64GB의 공간이 있어야 합니다.
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)를 설치합니다.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com) 계정이 있으며, 실명인증을 완료해야 합니다.

## 작업 단계
[](id:step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원] > [[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)]을 선택합니다.
2. [애플리케이션 생성]을 클릭하고 `TestTRTC`와 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 생성된 경우 [기존 애플리케이션 선택]을 클릭합니다.
3. 실제 비즈니스 필요에 따라 태그를 추가하거나 편집하고 [생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)
>?
>- 애플리케이션 이름은 숫자, 중국어, 영어, 언더바만 포함할 수 있으며 15자를 초과할 수 없습니다.
>- 태그는 Tencent Cloud에서 다양한 리소스를 식별하고 구성하는 데 사용됩니다. 예를 들어, 기업이 여러 사업부를 가지고 있고, 각 부서에는 하나 이상의 TRTC 애플리케이션이 있을 수 있는데, 이 경우 기업은 TRTC 애플리케이션에 태그를 추가하여 부서 정보를 표시할 수 있습니다. 태그는 필수 사항이 아니며, 실제 비즈니스 니즈에 따라 추가하거나 편집할 수 있습니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 요구사항에 따라 SDK 및 관련 [Demo 소스 코드](https://github.com/tencentyun/TRTCFlutterScenesDemo)를 다운로드합니다.
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)


[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `/example/lib/debug/GenerateTestUserSig.dart` 파일을 찾아 엽니다.
3. `GenerateTestUserSig.dart` 파일에서 관련 매개변수를 설정합니다.
<ul><li/>SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
	<li/>SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>?
>- 본 문서의 UserSig는 클라이언트 코드에서 SECRETKEY를 설정하여 생성합니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.

[](id:step4)
### 4단계: 컴파일 실행
1. `flutter pub get`을 실행합니다.
2. 컴파일 실행 디버깅:
<dx-tabs>
:::  Android\s
1. 'flutter run'을 실행합니다.
2. Android Studio(3.5 버전 이상)를 사용하여 소스 코드 프로그램을 열고 [실행]을 클릭합니다.
:::
::: iOS\s
Xcode(11.0 및 이후 버전)를 사용하여 소스 코드 디렉터리에서 `/ios` 프로젝트를 엽니다. Demo 프로젝트를 컴파일하고 실행합니다.
:::
::: Windows\s
1. Windows 지원 활성화: `flutter config --enable-windows-desktop`.
2. `flutter run -d windows`.
:::
::: macOS\s
1. macOS 지원 활성화: `flutter config --enable-macos-desktop`.
2. `flutter run -d macos` 실행.
:::
</dx-tabs>

## FAQ
### TRTC 로그는 어떻게 조회합니까?
TRTC 로그는 기본적으로 `.xlog`로 압축 및 암호화됩니다. 주소는 다음과 같습니다.
- **iOS**: sandbox 의 `Documents/log`.
- **Android**:
	- 6.7 및 이전 버전: `/sdcard/log/tencent/liteav`.
	- 6.8 이후 버전: `/sdcard/Android/data/패키지명/files/log/tencent/liteav/`.

### iOS에서 비디오가 표시되지 않습니다. (Android는 문제 없음)
info.plist에서，`io.flutter.embedded_views_preview`가 YES인지 확인하십시오. 

### Android Manifest merge failed 컴파일에 실패합니다.
'/example/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
    1. `xmlns:tools="http://schemas.android.com/tools"`를 manifest에 추가합니다.
    2. `tools:replace="android:label"`을 application에 추가합니다.
![이미지](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

>? 더 많은 FAQ는 [Flutter FAQ](https://intl.cloud.tencent.com/document/product/647/39242)를 참고하십시오.

