본 문서에서는 Tencent Cloud TRTC SDK(Flutter)를 귀하의 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

## 환경 요건
- Flutter 2.0 이상 버전
- Android 개발:
  - Android Studio 3.5 이상 버전
  - 앱에서 Android 4.1 이상 버전의 디바이스 요구됨
- iOS 개발:
  - Xcode 11.0 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## SDK 통합

Flutter SDK를 [pub 라이브러리](https://pub.dev/packages/tencent_trtc_cloud)에 배포했다면, 'pubspec.yaml' 설정을 통해 자동으로 업데이트를 다운로드할 수 있습니다.
1. 항목의 'pubspec.yaml'에 다음과 같이 종속을 작성합니다.
```
dependencies:
  tencent_trtc_cloud: 최신 버전 넘버
```
2. **카메라**와**마이크**의 권한을 활성화하면, 음성 통화 기능을 활성화할 수 있습니다.
#### iOS
1. 'Info.plist'에 카메라와 마이크에 대한 권한을 추가해 신청해야 합니다.
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
2. 필드 'io.flutter.embedded_views_preview'를 추가하고 설정값을 YES로 합니다.

#### Android
1. '/android/app/src/main/AndroidManifest.xml' 파일을 엽니다.
2. 'xmlns:tools="http://schemas.android.com/tools"'를 manifest에 추가합니다.
3. 'tools:replace="android:label"'을 application에 추가합니다.
>? 이 단계를 수행하지 않으면 [Android Manifest merge failed 컴파일 실패](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6) 문제가 발생합니다.


![이미지](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)






## FAQ
- [iOS 패키징에 Crash가 실행됩니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que3)
- [iOS에서 비디오가 표시되지 않습니다(Android는 정상).](https://intl.cloud.tencent.com/zh/document/product/647/39242#que4)
- [SDK 버전 업데이트 후 iOS CocoaPods 실행 시 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que5)
- [Android Manifest merge failed 컴파일에 실패합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que6)
- [서명이 없어 실제 기기에서 디버깅 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que7)
- [플러그 인 내에 swift 파일에 추가/삭제 후, build 시 상응하는 파일을 찾을 수 없습니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que8)
- [Run 오류 "Info.plit, error: No value at that key path or invalid key path: NSBonjourServices"가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que9)
- [Pod install 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que10)
- [Run 시 iOS 버전에 따른 오류가 발생합니다.](https://intl.cloud.tencent.com/zh/document/product/647/39242#que11)


