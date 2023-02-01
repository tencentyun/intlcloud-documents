본문은 iOS용 RT-Cube의 LiteAVSDK_Player를 프로젝트에 빠르게 통합하는 방법을 설명합니다.


## 개발 환경 요구사항
- Xcode 9.0+.
- iOS 9.0 이상의 iPhone 또는 iPad.
- 개발자 서명 설정이 적용된 프로젝트.

## SDK 통합
CocoaPods를 사용하여 SDK를 자동으로 로드하거나 SDK를 수동으로 다운로드하고 프로젝트로 가져올 수 있습니다.

[](id:cocoapods)
### CocoaPods를 통한 통합
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
	버전 선택이 가능한 CocoaPod의 공식 소스를 사용하십시오. Podfile을 편집합니다.
	
	최신 버전의 TXLiteAVSDK_Player_Premium을 포드로 직접 통합합니다.
```objective
platform: ios, '9.0'
source ’https://github.com/CocoaPods/Specs.git’

target ’App’ do
pod 'TXLiteAVSDK_Player_Premium'
end
```
특정 버전을 지정해야 하는 경우 podfile 파일에 다음 종속성을 추가할 수 있습니다.
```objective-c
pod 'TXLiteAVSDK_Player', '~> 110.8.29000'
```

4. **SDK 업데이트 및 설치**
  - 터미널 창에 다음 명령을 입력하여 로컬 리포지토리 파일을 업데이트하고 LiteAVSDK를 설치합니다.
```
pod install
```

  - 또는 다음 명령을 실행하여 로컬 리포지토리를 업데이트합니다.
```
pod update
```
LiteAVSDK와 통합된 XCWORKSPACE 프로젝트 파일이 생성됩니다. 더블클릭하여 파일을 엽니다.

[](id:manual)
### 수동 SDK 통합
1. 최신 버전의 [TXLiteAVSDK_Player_Premium](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_Player_Premium_iOS_latest.zip)에서 SDK + Demo 패키지를 다운로드합니다.
2. 통합할 프로젝트에 SDK/TXLiteAVSDK_Player_Premium.framework를 추가하고, `Do Not Embed`를 선택합니다.
3. 프로젝트 Target의 -ObjC를 구성해야 합니다. 그렇지 않으면 SDK 범주를 로드할 수 없기 때문에 Crash가 발생합니다.

```objective-c
Xcode 열기 -> 해당 Target 선택 -> "Build Setting" Tab 선택 -> "Other Link Flag" 검색 -> "-ObjC" 입력
```

4. 해당 라이브러리 파일 추가(SDK 디렉터리에 있음)
   **TXFFmpeg.xcframework**: .xcframework 파일을 프로젝트에 추가하고, “General - Frameworks, Libraries, and Embedded Content”에서 “Embed&Sign”으로 설정하고, “Project Setting - Build Phases - Embed Frameworks”에서 확인하고, ”Code Sign On Copy“ 옵션을 선택 상태로 설정합니다. 다음 이미지와 같습니다.
    **TXSoundTouch.xcframework**: .xcframework 파일을 프로젝트에 추가하고, “General - Frameworks, Libraries, and Embedded Content”에서 “Embed&Sign”으로 설정하고, “Project Setting - Build Phases - Embed Frameworks”에서 확인하고, “Code Sign On Copy” 옵션을 선택 상태로 설정합니다. 다음 이미지와 같습니다.<br>
    <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b226decc76c33eff8c3f5b4cc4246bea.png" />
   <br>
   동시에, Xcode의 “Build Settings - Search Paths”로 전환하고, “Framework Search Paths”에서 위의 Framework가 있는 경로를 추가합니다.
	
	 **MetalKit.framework**: Xcode를 열고, “project setting - Build  Phases - Link Binary With Libraries”를 선택하고 왼쪽 하단 모서리에서 “+”를 클릭한 다음 “MetalKit”을 입력하여 프로젝트에 추가합니다. 아래 이미지와 같습니다.<br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8ab7576dcc8bbe7b36396955ca06b186.png" />
   <br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/8480798e5ba897077ed3cef8ebc12f2e.png" />
   <br>

	 **ReplayKit.framework**: Xcode를 열고, “project setting - Build  Phases - Link Binary With Libraries”를 선택하고, 왼쪽 하단 모서리에서 “+”를 클릭한 다음 “ReplayKit”을 입력하고, 프로젝트에 추가합니다. 아래 이미지와 같습니다.<br>
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/aa07f3d4963ee703505a14a743f61a68.png" />
   <img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/12491d4a64aa6df44e6a966e80ca54de.png" />
   <br>
   같은 방식으로 다음 시스템 라이브러리를 추가합니다.
   <br><b>시스템 Framework 라이브러리</b>：SystemConfiguration, CoreTelephony, VideoToolbox, CoreGraphics, AVFoundation, Accelerate, MobileCoreServices<br>
   <b>시스템 Library:</b> libz, libresolv,  libiconv, libc++, libsqlite3

#### PIP(Picture-In-Picture) 기능

PIP 기능을 사용해야 하는 경우 아래 이미지와 같이 구성하고, 해당 기능이 없으면 생략해도 됩니다.

1. iOS용 PIP를 사용하려면 SDK를 버전 10.3 이상으로 업그레이드하십시오.
2. PIP 기능을 사용할 때 백그라운드 모드를 활성화해야 합니다. XCode는 해당 Target -> Signing & Capabilities -> Background Modes를 선택하고 "Audio, AirPlay, and Picture in Picture"를 확인합니다. 아래 이미지와 같습니다.
<img style="width:400px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/116e1e741f80d810502221fd143d8434.png" />

## SDK 가져오기
프로젝트 코드에서 SDK를 가져오는 방법에는 두 가지가 있습니다.
- **방법1:** 프로젝트에서 SDK의 API를 사용해야 하는 파일에 SDK 모듈을 가져옵니다.
```
@import TXLiteAVSDK_Player_Premium;
```
- **방법2:** 프로젝트에서 SDK의 API를 사용해야 하는 파일에서 특정 헤더 파일을 가져옵니다.
```
#import "TXLiteAVSDK_Player_Premium/TXLiteAVSDK.h"
```

## License 구성
1. [License 신청](https://www.tencentcloud.com/document/product/266/51098)을 클릭하여 [Adding and Renewing a License](https://www.tencentcloud.com/document/product/266/51098#.E7.94.B3.E8.AF.B7.E6.B5.8B.E8.AF.95.E7.89.88-license)에 설명된 대로 트라이얼 License를 신청합니다. License가 구성되지 않은 경우 비디오 재생이 실패합니다. licenseURL과 암호 해독 key라는 두 개의 문자열을 받게 됩니다.
2. App이 LiteAVSDK의 기능을 호출하기 전에 다음 구성을 완료하십시오(가급적이면 `- [AppDelegate application:didFinishLaunchingWithOptions:]`에서).
```objc
@import TXLiteAVSDK_Player_Premium;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<획득한 licenseUrl>";
    NSString * const licenceKey = @"<획득한 key>";
    
    //TXLiveBase는 "TXLiveBase.h" 헤더 파일에 위치
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    // TXLiveBase.delegate = self;
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}

#pragma mark - TXLiveBaseDelegate
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    NSLog(@"onLicenceLoaded: result:%d reason:%@", result, reason);
}
@end
```

## 조회 방법

License가 성공적으로 구성되면 아래 API를 호출하여 License 정보를 볼 수 있습니다. 구성이 적용되는 데 시간이 걸릴 수 있습니다. 정확한 소요 시간은 네트워크 상태에 따라 다릅니다.

```swift
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```

[](id:faq)

## FAQ
1. 내 프로젝트가 CSS, TRTC 및 Player와 같은 LiteAVSDK의 여러 버전을 통합하여 중복 기호 오류가 발생하면 어떻게 해야 합니까?

둘 이상의 LiteAVSDK 버전(MLVB, Player, TRTC, UGSV)을 통합하면 프로젝트를 빌드할 때 라이브러리 충돌 오류가 발생합니다. SDK의 기본 라이브러리 간에 일부 기호 파일이 공유되기 때문입니다. 문제 해결을 위해 MLVB, Player, TRTC, UGSV의 기능이 포함된 All-in-One SDK를 통합하는 것을 권장합니다. 자세한 내용은 [SDK 다운로드](https://www.tencentcloud.com/document/product/266/50561)를 참고하십시오.

