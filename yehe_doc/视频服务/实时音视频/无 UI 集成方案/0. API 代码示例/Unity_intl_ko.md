이 예시 항목은 Unity에 TRTC SDK를 빠르게 통합하여 게임에서 멀티미디어 통화를 구현하는 방법을 소개합니다.

데모에는 다음 기능이 포함되어 있습니다.
- 방 입/퇴장.
- 사용자 정의 비디오 렌더링.
- 디바이스 관리 및 음악/오디오 효과.

>?
>- 구체적인 API 기능 매개변수에 대한 설명은 [Unity API 개요](https://intl.cloud.tencent.com/document/product/647/40139)를 참고하십시오.
>- Unity 권장 버전: 2020.2.1f1c1.
>- 현재 Android, iOS, Windows, Mac(Mac은 내부 테스트 중) 플랫폼을 지원합니다.
>- `Android Build Support`, `iOS Build Support`, `Winodows Build Support`, `MacOs Build Support` 모듈을 포함해야 합니다.
>- iOS 개발에 필요한 환경 요건:
   - Xcode 11.0 이상 버전.
   - 귀하의 프로젝트에 유효한 개발자 서명이 설정되어 있는지 확인하십시오.

## 작업 단계

### 1단계: 애플리케이션 생성

1. TRTC 콘솔에 로그인하고 [[애플리케이션 관리](https://console.tencentcloud.com/trtc/app)]를 선택합니다.
2. [애플리케이션 생성]을 클릭하고 'APIExample'과 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 있는 경우 [기존 애플리케이션 선택]을 선택하고 [다음]을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### 2단계: 샘플 코드 다운로드

1. UI 없음을 선택하고 [[Github](https://github.com/LiteAVSDK/TRTC_Unity/tree/main/TRTC-Simple-Demo)]로 이동하여 SDK 및 Demo 소스 코드를 다운로드합니다.
2. [다음]을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### 3단계: 프로젝트 구성

1. 데모 프로젝트를 실행 중인 경우 [테스트]를 선택합니다. SDKAppID와 Secret key를 기록해 둡니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 이전에 다운로드한 파일을 열고 `TRTC-Simple-Demo/Assets/TRTCSDK/Demo/Tools/GenerateTestUserSig.cs`를 찾아 열고 다음 매개변수를 설정합니다.
  - SDKAPPID: PLACEHOLDER로 기본 설정되어 있으며, 실제 SDKAppID로 설정하십시오.
  - SECRETKEY: PLACEHOLDER로 기본 설정되어 있으며, 실제 Secret key로 설정하십시오.
3. [다음]을 클릭합니다.

>?
>- 본 문서에서 설명하는 UserSig를 생성하는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 쉽게 디컴파일되고 역전될 수 있으며, 키가 공개되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 TRTC-Simple-Demo의 로컬 실행 및 디버깅에만 적합합니다**.
>- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. 자세한 내용은 [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

### 4단계: 데모 컴파일 및 실행

#### Android 플랫폼

1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하여 Android로 전환합니다.
![](https://main.qcloudimg.com/raw/4464eb891829e3505a59c8ec00cc2414.png)
2. 실제 Android 기기에 연결하고 [Build And Run]을 클릭하여 Demo를 실행합니다.
3. 먼저 enterRoom을 호출하고 다른 API를 테스트합니다. 데이터 표시 창에는 통화 성공 여부가 표시되고 다른 창에는 콜백 정보가 표시됩니다.

#### iOS 플랫폼

1. 상단 메뉴에서 `TRTC 빌드 및 구성 툴`을 엽니다.
2. `빌드&구성 iOS`를 클릭하여 프로젝트를 생성합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d7aa3153469c10b2dfe35db31bebbbf2.png)
3. xcode로 생성된 프로젝트(Unity-iPhone.xcodeproj)를 엽니다.
4. [기본 TRTC sdk](https://comm.qq.com/trtc/TRTC_9.7.0.11440_iOS.zip)를 다운로드합니다. General을 클릭하고 Frameworks, Libraries and Embedded Content를 선택하고 하단의 ‘+’를 클릭하여 필요한 동적 라이브러리(FFmpeg.xcframework 및 SoundTouch.xcframework)를 추가하고 Embed & Sign을 클릭합니다.
   ![](https://imgcache.qq.com/operation/dianshi/other/unity.ca7b6e717bf7b34e4f08a7e688ff59bf49d92217.png)
5. 실제 iOS 장치에 연결하여 프로젝트를 디버그합니다.

#### Windows 플랫폼

1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하면 `PC, Mac & Linux Standalone`, Target Platform으로 전환되어 Windows를 선택합니다.
   ![](https://main.qcloudimg.com/raw/580764f661c06cf71c4952727c409c5e.png)
2. [Build And Run]을 클릭하면 Demo가 실행됩니다.

#### macOS 플랫폼

1. Unity Editor를 설정하고 [File]>[Build Setting]을 클릭하면 `PC, Mac & Linux Standalone`, Target Platform으로 전환되어 macOS를 선택합니다.
   ![](https://main.qcloudimg.com/raw/6f3f9c21aa9eeadd7a4e3be377b2a6b3.png)
2. [Build And Run]을 클릭하면 Demo가 실행됩니다.
3. Unity Editor로 시뮬레이터를 실행하려면 `Device Simulator Package`를 설치해야 합니다.
4. [Window]>[General]>[Device Simulator]를 클릭합니다.
   ![](https://main.qcloudimg.com/raw/79f707b89553528956a888f48b4d4d6d.png)

[](id:demo)
## Demo 예시
Demo는 지금까지 런칭된 대부분의 API를 통합하며, 테스트 및 API 호출에 대한 참고로 사용할 수 있습니다. API에 대한 자세한 내용은 [SDK API(Unity)](https://intl.cloud.tencent.com/zh/document/product/647/40139)를 참고하십시오.
>? 데모 최신 버전의 UI는 다르게 보일 수 있습니다.

## 디렉터리 구조
```
├─Assets
├── Editor                        // Unity 에디터 스크립트
│   ├── BuildScript.cs            // Unity 에디터 build 메뉴
│   ├── IosPostProcess.cs         // Unity 에디터로 ios 애플리케이션 스크립트 구축
├── Plugins
│   ├── Android                   
│   │   ├── AndroidManifest.xml   //Android 애플리케이션 구성 파일
├── StreamingAssets               // Unity Demo 멀티미디어 스트림 파일
├── TRTCSDK
    ├── Demo                      // Unity 예시 Demo
    ├── SDK                       // TRTC Unity SDK
        ├── Implement             // TRTC Unity SDK 구현
        ├── Include               // TRTC Unity SDK 헤더 파일
        └── Plugins               // TRTC Unity SDK 다양한 플랫폼 기반 구현
            
```