## 컴포넌트 개요
TUIRoom은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 화면 공유, 뷰티 필터 및 저지연 영상 통화와 같은 기능을 App에 추가할 수 있습니다. 또한 [Android](https://intl.cloud.tencent.com/document/product/647/37283), [Windows](https://intl.cloud.tencent.com/document/product/647/44071) 및 [Mac](https://intl.cloud.tencent.com/document/product/647/44071) 플랫폼을 지원합니다. 기본 기능은 다음과 같습니다.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2944bac3c5d348b06d2a11c439783b48.png"></td>
</tr>
</tbody></table>

## 컴포넌트 통합

### 1단계: TUIRoom 컴포넌트 가져오기

**cocoapods를 통해 컴포넌트를 가져오려면** 다음 단계를 따르십시오.
1. 프로젝트의 `Podfile`과 같은 수준에 `TUIRoom` 폴더를 만듭니다.
2. [**Github/TUIRoom**](https://github.com/tencentyun/TUIRoom)으로 이동하고 클론/다운로드 코드를 선택한 다음 [**TUIRoom/iOS/**](https://github.com/tencentyun/TUIRoom/tree/main/iOS) 디렉터리에 `Source`, `Resources`, `TUIBeauty`, `TXAppBasic` 폴더 및 `TUIRoom.podspec` 파일을 `1단계`에서 생성한 TUIRoom 폴더에 복사합니다.
3. Podfile에 다음 종속성을 추가하고 `pod install`을 실행하여 가져오기를 완료합니다.
```
# :path => "TUIRoom.podspec의 상대 경로를 가리킵니다"
pod 'TUIRoom', :path => "./TUIRoom/TUIRoom.podspec", :subspecs => ["TRTC"]
# :path => "TXAppBasic.podspec의 상대 경로를 가리킵니다"
pod 'TXAppBasic', :path => "./TUIRoom/TXAppBasic/"
# :path => "TUIBeauty.podspec의 상대 경로를 가리킵니다"
pod 'TUIBeauty', :path => "./TUIRoom/TUIBeauty/"
```

>!  `Source` 및 `Resources` 폴더와 `TUIRoom.podspec` 파일은 동일한 디렉터리에 있어야 합니다.
>-  TXAppBasic.podspec은 TXAppBasic 폴더에 있습니다.
>-  TUIBeauty.podspec은 TCBeautyKit 폴더에 있습니다.

### 2단계: 권한 구성

오디오/비디오 기능을 사용하려면 마이크 및 카메라 권한을 부여해야 합니다. App의 Info.plist에 아래 두 항목을 추가합니다. 해당 콘텐츠는 사용자가 마이크 및 카메라 액세스 팝업 창에서 보는 것입니다.

```
<key>NSCameraUsageDescription</key>
<string>RoomApp은 이미지가 포함된 비디오를 촬영하려면 카메라에 액세스해야 합니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>RoomApp은 오디오가 포함된 비디오를 녹화하려면 마이크에 액세스해야 합니다.</string>
```
![](https://main.qcloudimg.com/raw/54cc6989a8225700ff57494cba819c7b.jpg)

### 3단계: TUI 컴포넌트 생성 및 초기화

<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;
@import TUICore;

// 1. 컴포넌트에 로그인
[TUILogin login:@"귀하의 SDKAppID" userID:@"귀하의 UserID" userSig:@"귀하의 UserSig" succ:^{
        
} fail:^(int code, NSString *msg) {
        
}];
// 2. TUIRoom 인스턴스 초기화
TUIRoom *tuiRoom = [TUIRoom sharedInstance];
```
:::
::: Swift Swift
import TUIRoom
import TUICore

// 1. 컴포넌트에 로그인
TUILogin.login("귀하의 SDKAppID", userID: "귀하의 UserID", userSig: "귀하의 UserSig") {
        
} fail: { code, msg in
        
}

// 2. TUIRoom 인스턴스 초기화
let tuiRoom = TUIRoom.sharedInstance
```
:::
</dx-codeblock>

**매개변수 설명**:
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지로 이동한 후, SecretKey는 아래와 같습니다.
- **userId**: 문자열이며 최대 32바이트의 문자와 숫자를 포함할 수 있는 현재 사용자 ID입니다(특수 기호는 지원되지 않음). 실제 계정 시스템에 따라 사용자 정의할 수 있습니다.
- **UserSig**: SDKAppId, UserID 및 SecretKey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [TUIRoom 데모 프로젝트](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.


### 4단계: 그룹 오디오/비디오 인터랙션 구현
1. **방 주인은 그룹 오디오/비디오 인터랙션 방을 만듭니다**.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[tuiRoom createRoomWithRoomId:12345 speechMode:TUIRoomFreeSpeech isOpenCamera:YES isOpenMicrophone:YES];
:::
::: Swift Swift
import TUIRoom

tuiRoom.createRoom(roomId: 12345, speechMode: .freeSpeech, isOpenCamera: true, isOpenMicrophone: true)
```
:::
</dx-codeblock>
2. **다른 사용자가 오디오/비디오 방에 입장합니다**.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[tuiRoom enterRoomWithRoomId:12345 isOpenCamera:YES isOpenMicrophone:YES]
:::
::: Swift Swift
import TUIRoom

tuiRoom.enterRoom(roomId: 12345, isOpenCamera: true, isOpenMicrophone: true)
```
:::
</dx-codeblock>

### 5단계: 방 관리(옵션)
1. **방 주인은 [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37282)을 통해 방을 해산합니다**.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[[TUIRoomCore shareInstance] destroyRoom:^(NSInteger code, NSString * _Nonnull message) {
            
}];
```
:::
::: Swift Swift
import TUIRoom

TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
    guard let self = self else { return }
    self.navigationController?.popViewController(animated: true)
}
```
:::
</dx-codeblock>
2. **다른 구성원은 [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37282)을 통해 방을 나갑니다**.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[[TUIRoomCore shareInstance] leaveRoom:^(NSInteger code, NSString * _Nonnull message) {
            
}];
```
:::
::: Swift Swift
import TUIRoom

TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
    guard let self = self else { return }
    self.navigationController?.popViewController(animated: true)
}
```
:::
</dx-codeblock>

### 6단계: 화면 공유(옵션)
화면 공유 활성화  [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282). 화면 공유 프로젝트 설정은 [실시간 화면 공유(iOS)](https://intl.cloud.tencent.com/document/product/647/37338)를 참고하십시오.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;
@import TXLiteAVSDK_Professional;

TRTCVideoEncParam *params = [[TRTCVideoEncParam alloc] init];
params.videoResolution = TRTCVideoResolution_1280_720;
params.resMode = TRTCVideoResolutionModePortrait;
params.videoFps = 10;
params.enableAdjustRes = NO;
params.videoBitrate = 1500;

[[TUIRoomCore shareInstance] startScreenCapture:param];
```
:::
::: Swift  Swift
import TUIRoom

 // 화면 공유
let params = TRTCVideoEncParam()
params.videoResolution = TRTCVideoResolution._1280_720
params.resMode = TRTCVideoResolutionMode.portrait
params.videoFps = 10
params.enableAdjustRes = false
params.videoBitrate = 1500
TUIRoomCore.shareInstance().startScreenCapture(params)

```
:::
</dx-codeblock>


## FAQ

### CocoaPods는 어떻게 설치합니까?

터미널 창에 다음 명령어를 입력합니다(먼저 Mac에 Ruby를 설치해야 함).
```
sudo gem install cocoapods
```

>? 요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의하십시오.

