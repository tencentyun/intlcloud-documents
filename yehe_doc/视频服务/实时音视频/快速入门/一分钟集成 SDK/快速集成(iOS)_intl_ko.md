본 문서에서는 Tencent Cloud TRTC SDK(iOS)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.

## 개발 환경 요구사항
- Xcode 9.0+. 
- iOS 9.0 이상의 iPhone 또는 iPad.
- 개발자 서명 설정이 적용된 프로젝트.

## TRTC SDK 통합
CocoaPods 자동 로딩 방식을 사용하거나, 먼저 SDK를 다운로드한 후 현재 프로그래밍 프로젝트에 가져옵니다.

### CocoaPods
#### 1. CocoaPods 설치
터미널 창에 다음 명령어를 입력합니다. 사전에 Mac에 Ruby 환경 설치가 필요합니다.
```
sudo gem install cocoapods
```

#### 2. Podfile 파일 생성
프로젝트가 있는 경로에 들어가 다음 명령 라인을 입력하면 프로젝트 경로에 Podfile 파일이 생성됩니다.
```
pod init
```

#### 3. Podfile 파일 편집
Podfile 파일을 편집하고 필요에 따라 적합한 SDK 버전을 선택합니다.
- [라이트 버전](https://intl.cloud.tencent.com/document/product/647/34615): 설치 패키지 중 용량이 가장 작은 버전이지만, TRTC와 CDN 재생(TXLivePlayer) 기능을 지원합니다.
```
 platform : ios, ’8.0’
  
  target ’App’ do
  pod ’TXLiteAVSDK_TRTC’, :podspec => ’http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC.podspec’
  end
```

- [프로 버전](https://intl.cloud.tencent.com/document/product/647/34615): TRTC 외 RTMP 푸시 스트리밍(TXLivePusher), CDN 재생(TXLivePlayer), VOD 재생(TXVodPlayer), UGSV 등 다양한 기능을 지원합니다.
```
 platform : ios, ’8.0’
  
  target ’App’ do
  pod ’TXLiteAVSDK_Professional’, :podspec => ’http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_Professional.podspec’
  end
```

CocoaPod 공식 소스를 사용할 수 있으나 로딩 속도가 비교적 느릴 수 있습니다.
```
   platform : ios, ’8.0’
   source ’https://github.com/CocoaPods/Specs.git’
   
   target ’App’ do
   pod ’TXLiteAVSDK_TRTC’
   end
```

#### 4. SDK 업데이트 및 설치
터미널 창에 다음 명령어를 입력하여 로컬 라이브러리 파일을 업데이트하고 TRTC SDK를 설치합니다.
```
pod install
```
또는 다음 명령어를 사용하여 로컬 라이브러리 버전을 업데이트합니다.
```
pod update
```

pod 명령어 실행이 완료되면 SDK .xcworkspace 접미사가 통합된 프로그램 파일이 생성되며, 이를 더블클릭해 실행하면 됩니다.
>? 필요한 시스템 종속 라이브러리 **Accelerate.framework**를 수동으로 추가해야 합니다.

### 수동 통합
1. [TRTC - SDK ](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/SDK)를 다운로드한 후, 압축을 해제합니다.
2. Xcode 프로그래밍 프로젝트를 열어 실행해야 할 target을 선택한 후 **Build Phases**를 선택합니다.
 ![](https://main.qcloudimg.com/raw/85509cc24bd958e7b9978e11937597c5.png)
3. **Link Binary with Libraries**를 클릭해 펼치고 하단에 있는 ‘+’를 클릭해 종속 라이브러리를 추가합니다.
 ![](https://main.qcloudimg.com/raw/54be71cc14ec79ce642216612544a8a4.png)
4. 다운로드한 TRTC SDK Framework와 이에 필요한 종속 라이브러리 **libc++.tbd**, **Accelerate.framework**, **libresolv.tbd**, **AVFoundation.framework**를 순서대로 추가합니다.
 ![](https://main.qcloudimg.com/raw/2fa94b7f81c7e9c4ac09733782e79c10.png)


## 카메라와 마이크 사용 권한 허용
SDK의 멀티미디어 기능을 사용하려면 마이크와 카메라의 사용 권한 허용이 필요합니다. 앱의 Info.plist에 마이크와 카메라의 사용 권한 대화 상자가 시스템에 팝업될 때 표시되는 안내 정보인 다음 두 항목을 추가합니다.
- **Privacy - Microphone Usage Description**, 마이크 사용 목적 안내 문구를 입력합니다.
- **Privacy - Camera Usage Description**, 카메라 사용 목적 안내 문구를 입력합니다.

![](https://main.qcloudimg.com/raw/7c483aae65f64cd2bf35b55d9c896a52.png)


## TRTC SDK 레퍼런스
TRTC SDK는 두 가지 호출 방식을 지원하며, 이 중 한 방법을 선택하여 사용할 수 있습니다.
### 방법1: Objective-C 또는 Swift 인터페이스를 통해 TRTC SDK 참고
Objective-C 또는 Swift 코드에 SDK를 사용하는 방법은 다음 두 가지가 있습니다.
- **모듈 레퍼런스**: 프로젝트에 SDK API가 필요한 파일에 모듈 레퍼런스를 추가합니다.
```
@import TXLiteAVSDK_TRTC;
```
- **헤더 파일 레퍼런스**: 프로젝트에 SDK API가 필요한 파일에 구체적인 헤더 파일을 삽입합니다.
```
#import TXLiteAVSDK_TRTC/TRTCCloud.h
```


[](id:using_cpp)
### 방법2: C++ 인터페이스를 통해 TRTC SDK 참고
1. **헤더 파일 레퍼런스**: C++ 인터페이스를 사용하여 iOS 애플리케이션을 개발하는 경우, `TXLiteAVSDK_TRTC.framework/Headers/cpp_interface` 디렉터리의 헤더 파일을 삽입하십시오.
```
#include TXLiteAVSDK_TRTC/cpp_interface/ITRTCCloud.h
```
2. **네임스페이스 사용**: trtc 네임스페이스에는 C++ 전체 플랫폼 인터페이스의 방법 및 유형 등이 정의되어 있습니다. 더 간략한 코딩을 위해 직접 trtc 네임스페이스를 사용하길 권장합니다.
```
using namespace trtc;
```

>? C++ 인터페이스 사용 방법은 [전체 플랫폼 (C++) API 개요](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오.

## FAQ
### 1. TRTC SDK는 백그라운드 실행을 지원합니까?
지원합니다. 백그라운드에서 관련 기능 실행이 필요하다면 현재 프로그래밍 프로젝트를 선택한 후 **Capabilities**의 **Background Modes**를 **ON**으로 설정하고 **Audio, AirPlay and Picture in Picture**를 선택합니다. (다음 이미지 참고)
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)
