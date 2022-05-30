본 문서에서는 Tencent Cloud TRTC SDK(Flutter)를 귀하의 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

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

## SDK 통합

Flutter SDK를 [pub 라이브러리](https://pub.dev/packages/tencent_trtc_cloud)에 배포했다면, 'pubspec.yaml' 설정을 통해 자동으로 업데이트를 다운로드할 수 있습니다.
1. 항목의 'pubspec.yaml'에 다음과 같이 종속을 작성합니다.
```
dependencies:
  tencent_trtc_cloud: 최신 버전 넘버
```
2. **카메라**와 **마이크**의 권한을 활성화하면, 음성 통화 기능을 활성화할 수 있습니다.
    <dx-tabs>
    ::: iOS\s
  1. 'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
2. 필드 'io.flutter.embedded_views_preview'를 추가하고 설정값을 YES로 합니다.
    :::
    ::: macOS\s
  1. 'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>App이 사진첩에 액세스하려면 동의 필요</string>
```
2. macos/Runner/*.entitlements` 파일에 `com.apple.security.network.client`와 `com.apple.security.network.server`를 추가해야 합니다.
   추가하면 다음 이미지와 같아집니다.
   ![](https://main.qcloudimg.com/raw/13f3eab720ec1da03b149db1a7240d6d.png)

3. Link Binary with Libraries를 클릭해 펼치고 하단에 있는 +를 클릭해 종속 라이브러리를 추가합니다.
   ![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)

4. 필요한 종속성 라이브러리인 `libbz2.1.0.tbd`를 추가합니다.
   추가하면 다음 이미지와 같아집니다.
     ![](https://imgcache.qq.com/operation/dianshi/other/lib.7518607f9764321c99fbcf14348715b65563bca2.png)
     :::
     :::  Android\s

  1. '/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.

  2. 'xmlns:tools="http://schemas.android.com/tools"'를 manifest에 추가합니다.

  3. tools:replace="android:label"`을 application에 추가합니다.

<dx-alert infotype="explain">이 단계를 수행하지 않으면 [Android Manifest merge failed 컴파일 실패](https://intl.cloud.tencent.com/document/product/647/39242) 문제가 발생합니다.</dx-alert>

![이미지](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
::: Windows\s
1. Windows 지원 활성화: `flutter config --enable-windows-desktop`.
2. `flutter run -d windows`.
:::
</dx-tabs>


## FAQ
- [iOS 패키지 실행 시 Crash가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [iOS에서 비디오가 표시되지 않습니다. (Android는 정상)](https://intl.cloud.tencent.com/document/product/647/39242)
- [SDK 버전 업데이트 후 iOS CocoaPods 실행 시 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Android Manifest merge failed 컴파일에 실패합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [서명이 없어 실제 기기에서 디버깅 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [플러그 인 내 swift 파일 추가/삭제 후, build 시 해당 파일을 찾을 수 없습니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run 오류 “Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Pod install 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run 실행 시 iOS 버전에 오류가 발생합니다.](https://intl.cloud.tencent.com/document/product/647/39242)

