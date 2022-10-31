본 문서에서는 SDK를 프로젝트로 가져오는 방법을 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f85f7ee54d462d85290fc6f50e5ed96a.png)
## 개발 환경 요구사항
- Xcode 9.0+. 
- iOS 9.0 이상의 iPhone 또는 iPad.
- 개발자 서명 설정이 적용된 프로젝트

## 1단계: SDK 가져오기
CocoaPods를 사용하거나 SDK를 수동으로 다운로드하여 프로젝트로 가져올 수 있습니다.

### 방법1: CocoaPods 사용
1. **CocoaPods 설치**
터미널 창에 다음 명령어를 입력합니다(먼저 Mac에 Ruby를 설치해야 함).
```
sudo gem install cocoapods
```
2. **Podfile 파일 생성**
프로젝트가 있는 경로에 들어가 다음 명령 라인을 입력하면 프로젝트 경로에 Podfile 파일이 생성됩니다.
```
pod init
```
3. **Podfile 파일 편집**
프로젝트 요구 사항에 따라 적절한 버전을 선택하고 Podfile을 편집합니다:
  - **옵션1: TRTC 라이트 버전**
설치 패키지는 가장 작지만 Tencent Real-Time Communication(TRTC)과 라이브 플레이어(TXLivePlayer)의 두 가지 기능만 지원합니다. 이 버전을 선택하려면 다음과 같이 Podfile을 편집하십시오:
```
 platform : ios, ’8.0’
  
  target ’App’ do
  pod 'TXLiteAVSDK_TRTC', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_TRTC.podspec'
  end
```
   - **옵션2: Professional 프로 버전**
설치 패키지에는 TRTC, TXLivePlayer, TXLivePusher, TXVodPlayer, UGSV 및 기타 여러 기능이 포함됩니다. 이 버전을 선택하려면 Podfile 파일을 다음과 같이 편집하십시오:
```
 platform : ios, ’8.0’
  
  target ’App’ do
  pod 'TXLiteAVSDK_Professional', :podspec => 'https://liteav.sdk.qcloud.com/pod/liteavsdkspec/TXLiteAVSDK_Professional.podspec'
  end
```
4. **SDK 업데이트 및 설치**
  - 터미널 창에 다음 명령어를 입력하여 로컬 라이브러리 파일을 업데이트하고 SDK를 설치합니다.
```
pod install
```
   - 또는 다음 명령어를 사용하여 로컬 라이브러리 버전을 업데이트합니다:
```
pod update
```
pod 명령어 실행이 완료되면 SDK .xcworkspace 접미사가 통합된 프로그램 파일이 생성되며, 이를 더블클릭해 실행하면 됩니다.

### 방법2: SDK를 다운로드하여 수동으로 가져오기
1. [SDK](https://intl.cloud.tencent.com/document/product/647/34615)를 다운로드하여 로컬에서 압축을 해제합니다.
2. Xcode 프로그래밍 프로젝트를 열어 실행해야 할 target을 선택한 후 **Build Phases**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f57f1da3efefefe98a4b8c03c688fd17.png)
3. **Link Binary with Libraries**를 클릭해 펼치고 하단에 있는 ‘+’를 클릭해 종속 라이브러리를 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/25faf435d56c7c7df1f944a536dd8869.png)
4. 다운로드한 `TXLiteAVSDK_TRTC.Framework`(또는 `TXLiteAVSDK_Professional.Framework`), `TXFFmpeg.xcframework`, `TXSoundTouch.xcframework`, 및 필요한 종속 라이브러리 `GLKit.framework`, `AssetsLibrary.framework`, `SystemConfiguration.framework`, `libsqlite3.0.tbd`, `CoreTelephony.framework`, `AVFoundation.framework`, `OpenGLES.framework`, `Accelerate.framework`, `MetalKit.framework`, `libresolv.tbd`, `MobileCoreServices.framework`, `libc++.tbd`, `CoreMedia.framework`를 차례로 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8f4b4dc4f794cd0bf4159cd5b0c2a507.png)
5. **General**을 클릭하여 **Frameworks,Libraries,and Embedded Content**를 선택하고 TXLiteAVSDK_TRTC.framework에 필요한 동적 라이브러리 **TXFFmpeg.xcframework**, **TXSoundTouch.xcframework**가 추가되었는지, **Embed & Sign**이 올바르게 선택되었는지 확인하고, 그렇지 않은 경우 하단의 ‘**+**’ 아이콘을 클릭하여 차례로 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a159c5fb799cf50611387bdae7275863.png)

## 2단계: App 권한 설정
1. SDK에서 제공하는 멀티미디어 기능을 사용하려면 App에 마이크와 카메라의 사용 권한을 부여해야 합니다. App의 Info.plist에 마이크와 카메라의 사용 권한 대화 상자가 시스템에 팝업될 때 표시되는 안내 정보인 다음 두 항목을 추가합니다.
	- **Privacy - Microphone Usage Description**, 마이크 사용 목적 안내 문구를 입력합니다.
	- **Privacy - Camera Usage Description**, 카메라 사용 목적 안내 문구를 입력합니다.
![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)
2. App이 백그라운드에서 관련 기능을 실행하도록 하려면 아래와 같이 Xcode에서 현재 프로젝트를 선택하고 **Capabilities** 아래의 **Background Modes**를 **ON**으로 설정한 후 **Audio, AirPlay and Picture in Picture**를 선택합니다.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

## 3단계: 프로젝트에 SDK 참조
1단계 가져오기와 2단계 디바이스 권한 부여를 완료하면 SDK에서 제공하는 API를 프로젝트로 가져올 수 있습니다.

### Objective-C 또는 Swift API 사용
Objective-C 또는 Swift 코드에 SDK를 사용하는 방법은 다음 두 가지가 있습니다.
- **모듈 레퍼런스**: 프로젝트에 SDK API가 필요한 파일에 모듈 레퍼런스를 추가합니다.
```
@import TXLiteAVSDK_TRTC;
```
- **헤더 파일 레퍼런스**: 프로젝트에 SDK API가 필요한 파일에 구체적인 헤더 파일을 삽입합니다.
```
#import "TXLiteAVSDK_TRTC/TRTCCloud.h"
```

>? Objective-C 인터페이스 사용 방법은 [iOS&Mac API 개요](https://intl.cloud.tencent.com/document/product/647/35119)를 참고하십시오.

[](id:using_cpp)
### C++ API 사용(선택 사항)
프로젝트가 QT 또는 Electron과 같은 크로스 플랫폼 프레임워크를 통해 SDK를 가져오는 경우 `TXLiteAVSDK_TRTC.framework/Headers/cpp_interface` 디렉터리에 있는 헤더 파일을 가져옵니다:
```
#include "TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h"
```

>? C++ 인터페이스 사용 방법은 [All Platforms (C++) API 개요](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오.

