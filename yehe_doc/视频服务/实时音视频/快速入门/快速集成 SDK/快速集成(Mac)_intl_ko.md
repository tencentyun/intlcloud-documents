본 문서에서는 Tencent Cloud TRTC SDK(Mac)를 프로젝트에 빠르게 통합할 수 있는 방법에 대해 소개합니다. 다음 절차에 따라 설정하면 SDK 통합 작업을 완료할 수 있습니다.


## 개발 환경 요구사항
- Xcode 9.0+.
- OS X10.10+의 Mac 디바이스
- 개발자 서명 설정이 적용된 프로젝트

## TRTC SDK 통합
CocoaPods 자동 로딩 방식을 사용하거나, 먼저 수동으로 SDK를 다운로드한 후 현재 프로그래밍 프로젝트에 가져옵니다.

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
다음 두 가지 설정 방법으로 Podfile 파일을 설정할 수 있습니다.
- 방법1: Tencent Cloud LiteAV SDK의 pod 경로 사용
<dx-codeblock>
::: pod 경로
	platform: osx, '10.10'
	
	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac', :podspec => 'http://pod-1252463788.cosgz.myqcloud.com/liteavsdkspec/TXLiteAVSDK_TRTC_Mac.podspec'
	end
:::
</dx-codeblock>
- 방법2: CocoaPod 공식 소스를 사용하여 선택 버전 지원
<dx-codeblock>
::: pod 경로
	platform: osx, '10.10'
	source ’https://github.com/CocoaPods/Specs.git’
	
	target 'Your Target' do
	pod 'TXLiteAVSDK_TRTC_Mac'
	end
:::
</dx-codeblock>

#### 4. SDK 설치 및 업데이트
터미널 창에 다음 명령어를 입력하여 TRTC SDK를 실행합니다.
```
pod install
```
또는 다음 명령어를 사용하여 로컬 라이브러리 버전을 업데이트합니다.
```
pod update
```

pod 명령어 실행이 완료되면 SDK `.xcworkspace` 접미사가 통합된 프로그램 파일이 생성되며, 이를 더블클릭해 실행하면 됩니다.

### 수동 통합
1. [TRTC-SDK ](https://github.com/LiteAVSDK/TRTC_Mac)의 Mac 버전을 다운로드합니다.
2. Xcode 프로그래밍 프로젝트를 열어 1단계에서 다운로드한 framework를 귀하의 프로그래밍에 가져옵니다.
3. 실행해야 할 target을 선택하고 Build Phases를 선택합니다.
![](https://main.qcloudimg.com/raw/b5097f8ac4cbaa5044d92b2a96ea2b9e.jpg)
4. **Link Binary with Libraries**를 클릭해 펼치고 하단에 있는 +를 클릭해 종속 라이브러리를 추가합니다.
![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)
5. 다운로드한 SDK Framework와 이에 필요한 종속 라이브러리 `AudioUnit.framework`, `libc++.tbd`, `Accelerate.framework`를 순서대로 추가합니다.  
추가하면 다음 이미지와 같아집니다.
![](https://main.qcloudimg.com/raw/258ffc87c493d23cf591bb2ff9102677.png)

## 카메라와 마이크 사용 권한 허용
SDK의 멀티미디어 기능을 사용하려면 마이크와 카메라의 사용 권한 허용이 필요합니다. 앱의 Info.plist에 마이크와 카메라의 사용 권한 대화 상자가 시스템에 팝업될 때 표시되는 안내 정보인 다음 두 항목을 추가합니다.
- **Privacy - Microphone Usage Description**, 마이크 사용 목적 안내 문구를 입력합니다.
- **Privacy - Camera Usage Description**, 카메라 사용 목적 안내 문구를 입력합니다.
다음 이미지 참고:
![](https://main.qcloudimg.com/raw/ce02c335f1a6413fb37adb0ed20a9603.png) 

App에서 **App Sandbox** 또는 **Hardened Runtime**을 활성화한 경우 `Network`, `Camera`, `Audio Input` 항목을 선택해야 합니다.
- 다음 이미지와 같이 App Sandbox를 설정합니다.
![](https://main.qcloudimg.com/raw/b77d2ab814e6e14e8bed17efdcbee1a6.png)
- 다음 이미지와 같이 Hardened Runtime을 설정합니다.
![](https://main.qcloudimg.com/raw/2b569e1c95bb4c97b7045112d6e3ce9c.png)

## TRTC SDK 레퍼런스
TRTC SDK는 두 가지 호출 방식을 지원하며, 이 중 한 방법을 선택하여 사용할 수 있습니다:
### 방법1: Objective-C 또는 Swift 인터페이스를 통해 TRTC SDK 참고
Objective-C 또는 Swift 코드에 SDK를 사용하는 방법은 다음 두 가지가 있습니다.
- **모듈 레퍼런스**: 프로젝트에 SDK API가 필요한 파일에 모듈 레퍼런스를 추가합니다.
```
@import TXLiteAVSDK_TRTC_Mac;
```
- **헤더 파일 레퍼런스**: 프로젝트에 SDK API가 필요한 파일에 구체적인 헤더 파일을 삽입합니다.
```
#import TXLiteAVSDK_TRTC_Mac/TRTCCloud.h
```

[](id:using_cpp)
### 방법2: C++ 인터페이스를 통해 TRTC SDK 참고
1. **헤더 파일 레퍼런스**: C++ 인터페이스를 사용하여 Mac 애플리케이션을 개발하는 경우, `TXLiteAVSDK_TRTC_Mac.framework/Headers/cpp_interface` 디렉터리의 헤더 파일을 삽입하십시오.
```
#include TXLiteAVSDK_TRTC_Mac/cpp_interface/ITRTCCloud.h
```
2. **네임스페이스 사용**: trtc 네임스페이스에는 C++ 전체 플랫폼 인터페이스의 인터페이스 및 유형 등이 정의되어 있습니다. 더 간략한 코딩을 위해 직접 trtc 네임스페이스를 사용하길 권장합니다.
```
using namespace trtc;
```

>? C++ 인터페이스 사용 방법은 [전체 플랫폼 (C++) API 개요](https://intl.cloud.tencent.com/document/product/647/35131)를 참고하십시오.
