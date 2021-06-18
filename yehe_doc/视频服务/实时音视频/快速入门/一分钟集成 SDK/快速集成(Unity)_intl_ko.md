본 문서는 Tencent Cloud TRTC SDK(Unity)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 아래의 절차에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

## 환경 요건
* Unity 권장 버전: 2020.2.1f1c1
* 현재 Android, iOS, Windows, Mac(Mac은 내부 테스트 중) 플랫폼을 지원합니다.
* `Android Build Support`, `iOS Build Support`, `Winodows Build Support`, `MacOs Build Support` 모듈을 포함해야 합니다.
- iOS 개발에 필요한 환경 요건:
  - Xcode 11.0 이상 버전
  - 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## SDK 통합
1. SDK 및 관련 [Demo 소스 코드](https://tccweb-1258344699.cos.ap-nanjing.myqcloud.com/sdk/trtc/unity/TRTCUnitySDK.zip)를 다운로드합니다.
2. 압축 해제 후 프로젝트에 있는 `TRTCUnitySDK/Assets/TRTCSDK/SDK` 폴더를 프로젝트의 Assets 디렉터리에 복사합니다.

## FAQ
### Android가 네트워크 권한 문제를 알려주나요?
프로젝트에 있는 `/Assets/Plugins/AndroidManifest.xml` 파일을 같은 레벨의 디렉터리에 넣습니다.

### Android는 멀티미디어에 대한 권한이 없나요?
Android의 마이크와 카메라에 대한 권한은 수동으로 신청해야 하며 구체적인 방법은 아래의 코드를 참조하십시오.
```
#if PLATFORM_ANDROID
if (!Permission.HasUserAuthorizedPermission(Permission.Microphone))
 {
     Permission.RequestUserPermission(Permission.Microphone);
 }
 if (!Permission.HasUserAuthorizedPermission(Permission.Camera))
 {
     Permission.RequestUserPermission(Permission.Camera);
 }
 #endif
```  
