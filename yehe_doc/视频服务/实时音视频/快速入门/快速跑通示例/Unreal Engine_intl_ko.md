본문은 Tencent Cloud TRTC Demo(Unreal Engine)를 빠르게 실행하는 방법을 소개합니다.

>! 현재 Windows, MacOs, ios, Android를 지원합니다.

## 환경 요건
- Unreal Engine 4.27.1 이상 버전 권장.
- **Android 개발:**
  - Android Studio 4.0 이상 버전.
  - Visual Studio 2017 15.6 이상 버전.
  - 실제 기기 디버깅만 지원
- **iOS & macOS 개발:**
  - Xcode 11.0 이상 버전.
  - osx 시스템 10.11 이상 버전
  - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.
- **Windows 개발:**
    - 운영 체제: Windows 7 SP1 이상(x86-64 기반 64비트 운영 체제).
    - 디스크 공간: IDE 및 일부 툴 설치 외에 최소 1.64GB의 공간 필요.
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/) 설치.

## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com) 계정이 있으며, 실명인증을 완료해야 합니다.

## 작업 단계
[](id:step1)
### 1단계: 신규 애플리케이션 생성
1. TRTC 멀티미디어 콘솔에 로그인한 후, [개발 지원] > [[Demo 빠른 실행](https://console.cloud.tencent.com/trtc/quickstart)]을 선택합니다.
2. [애플리케이션 생성]을 클릭하고 `TestTRTC`와 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 생성된 경우 [기존 애플리케이션 선택]을 클릭합니다.
3. 실제 비즈니스 필요에 따라 태그를 추가하거나 편집하고 [생성]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f5fbbe70b7139531600e763846051a54.png)

>?
>- 애플리케이션 이름은 숫자, 중국어, 영어, 언더바만 포함할 수 있으며 15자를 초과할 수 없습니다.
>- 태그는 Tencent Cloud에서 다양한 리소스를 식별하고 구성하는 데 사용됩니다. 예를 들어, 기업이 여러 사업부를 가지고 있고, 각 부서에는 하나 이상의 TRTC 애플리케이션이 있을 수 있는데, 이 경우 기업은 TRTC 애플리케이션에 태그를 추가하여 부서 정보를 표시할 수 있습니다. 태그는 필수 사항이 아니며, 실제 비즈니스 니즈에 따라 추가하거나 편집할 수 있습니다.

[](id:step2)
### 2단계: SDK와 Demo 소스 코드 다운로드
1. 실제 비즈니스 필요에 따라 SDK 및 관련 [Demo 소스 코드](https://comm.qq.com/sdk/trtc/UE4/TRTC_Demo.zip)를 다운로드합니다(문의 사항은 QQ그룹 번호: 764231117 추가 후 상담).
2. 다운로드 완료 후 [다운로드 완료, 다음 단계]를 클릭합니다.

[](id:step3)
### 3단계: Demo 프로그래밍 파일 설정
1. 설정 변경 페이지로 이동하여 다운로드한 소스 패키지에 따라 해당하는 개발 환경을 선택합니다.
2. `/TRTC_Demo/Source/debug/include/DebugDefs.h` 파일을 찾아 엽니다.
3. `DebugDefs.h` 파일에서 관련 매개변수를 설정합니다.
<ul><li/>SDKAPPID: 기본값 0 , 실제 SDKAppID로 설정하십시오.
	<li/>SECRETKEY: 기본값 ‘ ’ , 실제 키 정보로 설정하십시오.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>

4. 붙여넣기 완료 후 [붙여넣기 완료, 다음 단계]를 클릭하면 생성이 완료됩니다.
5. 컴파일 완료 후 [콘솔 개요로 돌아가기]를 클릭합니다.

>?
>- 본 문서의 UserSig 생성 방법은 클라이언트 코드에서 SECRETKEY를 설정하는 것입니다. 이 방법에서 SECRETKEY는 디컴파일로 크래킹되기 쉬우므로, 키가 유출되면 해커가 귀하의 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **해당 방법은 로컬 Demo 실행 및 기능 디버깅용으로만 적합합니다**.
>- 올바른 UserSig 배포 방식은 UserSig 컴퓨팅 코드를 귀하의 서버에 통합하고, App 지향 인터페이스를 제공하는 것입니다. UserSig가 필요할 때, App은 비즈니스 서버에 동적 UserSig 가져오기 요청을 발송합니다. 자세한 내용은 [서버에서 UserSig 생성](https://intl.cloud.tencent.com/document/product/647/35166#Server)을 참고하십시오.

[](id:step4)
### 4단계: 컴파일 패키지 실행
1. 더블 클릭 하여 `/TRTC_Demo/TRTC_Demo.uproject`를 엽니다.
2. 컴파일 실행 디버깅:
<dx-tabs>
::: macOS\s
1. File -> Package Project -> Mac
2. 권한을 설정합니다. 이전 단계에서 컴파일된 xxx.app 파일을 우클릭하고 - ‘패키지 콘텐츠 표시’를 선택합니다. 
![](https://qcloudimg.tencent-cloud.cn/raw/3eb106ee3307c206dff5314a43920132.png)
3. ‘Contents->Info.plist’로 이동합니다.
4. ‘Information Property List’를 선택하고 다음 두 가지 권한을 추가합니다.
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
5. 현재 UE4 editor에서 실행 중인 경우 **UE4Editor.app** 파일을 찾아 상기 단계에 따라 권한을 추가해야 합니다.
:::
::: Windows\s
1. File->Package Project->Windows->Windows(64-bit)
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s
1. iOS에서도 다음 권한이 필요합니다.
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```
info.plist에 상기 권한을 추가하려면 **Edit->Project Settings->Platforms: iOS**로 이동하여  
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```
Additional Plist Data에 추가합니다.
2. 마지막으로 프로젝트를 패키징합니다. File -> Package Project -> iOS
:::
:::  Android\s
1. 개발 디버깅: 자세한 내용은 [Android 시작하기](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/GettingStarted/) 참고
2. 패키징 프로젝트: 자세한 내용은 [Android 프로젝트 패키징](https://docs.unrealengine.com/4.27/zh-CN/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/) 참고
:::
</dx-tabs>
## Demo 실행
1:1 영상 통화 구현은 Demo에서 제공되며, 테스트 및 호출 참고 자료로 활용 가능합니다. API 문서는 [C++ 전체 플랫폼 API](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오.
>? UI에 일부 조정 업데이트가 있을 수 있으니 최신 버전을 기준으로 하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/e81338b3f3cf22c73744bcfbcf8955d2.png)

## TRTC 전체 플랫폼 C++ API 문서
[중국어 문서](https://liteav.sdk.qcloud.com/doc/api/zh-cn/md_introduction_trtc_zh_Cplusplus_Brief.html)

[영어 문서](https://liteav.sdk.qcloud.com/doc/api/en/md_introduction_trtc_en_Cplusplus_Brief.html)

## FAQ
### TRTC 로그는 어떻게 조회합니까?
TRTC 로그는 기본적으로 `.xlog`로 압축 및 암호화됩니다. 주소는 다음과 같습니다.
- **iOS**: sandbox 의 `Documents/log`.
- **Android**:
	- 6.7 이하 버전: `/sdcard/log/tencent/liteav`
	- 6.8 이후 버전: `/sdcard/Android/data/패키지명/files/log/tencent/liteav/`

### macos UE4 editor 튕김
**UE4Editor.app** info.plist에 오디오/비디오 권한이 설정되어 있는지 확인하십시오.
```
<key>NSCameraUsageDescription</key>
<string>카메라 권한을 부여해야 정상적으로 영상 통화할 수 있습니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>마이크 권한을 부여해야 정상적으로 음성 통화할 수 있습니다.</string>
```

### 안드로이드 ‘Attempt to construct staged filesystem reference from absolute path"’오류 보고
UE4 프로젝트를 비활성화하고, cmd를 엽니다.
>adb shell
>cd sdcard
>ls (you should see the UE4Game directory listed)
>rm -r UE4Game
프로젝트를 다시 컴파일합니다.
