## 컴포넌트 개요
TUIRoom은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 화면 공유, 뷰티 필터 및 저지연 영상 통화와 같은 기능을 App에 추가할 수 있습니다. 또한 [Android](https://intl.cloud.tencent.com/document/product/647/37283), [Windows](https://intl.cloud.tencent.com/document/product/647/44071) 및 [Mac](https://intl.cloud.tencent.com/document/product/647/44071) 플랫폼을 지원합니다. 기본 기능은 다음과 같습니다.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/0f07b6d570174f6fdc999eb67864f1f3.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9bdc61aa798c2c3926949d00a97302dc.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/37ef82ac97172967c037a523c5d09af3.png" width="250"></td>
</tr>
</tbody></table>


## 컴포넌트 통합

### 1단계: TUIRoom 컴포넌트 다운로드 및 가져오기
**cocoapods를 통해 컴포넌트 가져오기**의 구체적인 작업 단계는 다음과 같습니다.
>? 화면 공유 기능을 구현하려면 [**공식 링크**](https://intl.cloud.tencent.com/document/product/647/34615)에서 TXLiteAVSDK_ReplayKitExt.framework를 다운로드하여 프로젝트에 추가하고 "Broadcast Upload Extension" target을 생성하십시오. 구현을 위해 [데모 프로젝트](https://github.com/tencentyun/TUIRoom/tree/main/iOS/Example/TXReplayKit_Screen)를 참고할 수 있습니다.

1. [Github](https://github.com/tencentyun/TUIRoom)로 이동하여 코드를 복제하거나 다운로드하고 iOS 디렉터리의 `Resources`, `SDK` 및 `Source` 폴더와 `TUIRoom.podspec` 파일을 프로젝트에 복사합니다.
2. `Podfile` 파일에 다음 종속을 추가합니다. 그 다음 `pod install` 명령을 실행하여 가져오기를 완료합니다.
```swift
# TXLiteAVSDK
pod ’TXLiteAVSDK_TRTC’

# :path => "TXAppBasic.podspec 디렉터리의 상대 경로를 가리킵니다."
pod 'TXAppBasic', :path => "../SDK/TXAppBasic/"

# :path => "TCBeautyKit.podspec 디렉터리의 상대 경로를 가리킵니다."
pod 'TCBeautyKit', :path => "../SDK/TCBeautyKit/"

# :path => "TUIRoom.podspec 디렉터리의 상대 경로를 가리킵니다."
pod 'TUIRoom', :path => "../", :subspecs => ["TRTC"]
```

>!  `Source` 및 `Resources` 폴더와 `TUIRoom.podspec` 파일은 동일한 디렉터리에 있어야 합니다.
>-  TXAppBasic.podspec은 TXAppBasic 폴더에 있습니다.
>-  TCBeautyKit.podspec은 TCBeautyKit 폴더에 있습니다.

### 2단계: 권한 설정

오디오/비디오 기능을 사용하려면 마이크 및 카메라 권한을 부여해야 합니다. App의 Info.plist에 아래 두 항목을 추가합니다. 사용자에게 팝업되는 마이크 및 카메라 액세스 창 안내 정보입니다.
- **Privacy - Microphone Usage Description**, 마이크 사용 목적 안내 문구를 입력합니다.
- **Privacy - Camera Usage Description**, 카메라 사용 목적 안내 문구를 입력합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### 3단계: 컴포넌트 생성 및 로그인
1.  TUICore에서 TUILogin을 호출하여 로그인합니다. 다음 예를 참고하십시오.
```swift
TUILogin.initWithSdkAppID(Int32(" 사용자 sdkAppID"))
TUILogin.login("사용자 userId", userSig: "사용자 userSig", succ: {
     debugPrint("login success")
}, fail: { code, errorDes in
     debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```

**매개변수 설명**
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지에서 SecretKey는 아래와 같습니다.
- **userId**: 현재 사용자의 ID로, 문자(a-z 및 A-Z), 숫자(0-9), 하이픈(-) 및 언더바(\_)만 포함할 수 있는 문자열입니다. 사용자 계정 시스템과 일관성을 유지하는 것이 좋습니다.
- **userSig**: SDKAppId, userId 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 userSig를 온라인으로 직접 생성하거나 [데모 프로젝트](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오.

### 4단계: 그룹 오디오/비디오 인터랙션 구현

1. **방 소유자는  [TUIRoomCore#createRoom](https://intl.cloud.tencent.com/document/product/647/37282)을 통해 그룹 오디오/비디오 인터랙션 방을 만듭니다**.
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    } else {
    }
})
```
2. **다른 사용자는  [TUIRoomCore#enterRoom](https://intl.cloud.tencent.com/document/product/647/37282)을 통해 오디오/비디오 방에 입장합니다**.
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("enter room success") 
   } else {
   }
})
```
3. **방 퇴장 구현** 
	- **앵커**는  [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37282) API를 호출하여 채팅방 및 IM 그룹 채팅을 닫고 TRTC 채팅방을 종료합니다. 회의실 구성원은 그룹 해제를 알리고 TRTC 회의실을 종료하는 onDestroyRoom 콜백 메시지를 받습니다.
	- **구성원**이  [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37282) API를 호출하여 채팅방 및 IM 그룹 채팅을 종료하고 TRTC 채팅방을 종료합니다. 다른 방 구성원은 구성원이 방을 나갔음을 알리는 onRemoteUserLeave 콜백 메시지를 받습니다.
```swift
if isHomeowner {
    TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
} else {
    TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
 }
```
4. **[TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282)를 통해 화면 공유를 구현합니다**.
	- TUIRoomCore의 'startScreenCapture'를 호출하여 공유합니다.
	- 방의 다른 참석자는 'onRemoteUserScreenVideoAvailable'의 이벤트 알림을 받게 됩니다.
```swift
// 버튼을 클릭하여 화면 공유 활성화
if #available(iOS 12.0, *) {
    // 화면 공유
    let params = TRTCVideoEncParam()
    params.videoResolution = TRTCVideoResolution._1280_720
    params.resMode = TRTCVideoResolutionMode.portrait
    params.videoFps = 10
    params.enableAdjustRes = false
    params.videoBitrate = 1500
    TUIRoomCore.shareInstance().startScreenCapture(params)
    TUIRoomBroadcastExtensionLauncher.launch()
} else {
    view.window?.makeToast(.versionLowToastText)
}    
```

## FAQ
### CocoaPods는 어떻게 설치합니까?

터미널 창에 다음 명령을 입력합니다(먼저 Mac에 Ruby를 설치해야 함).
```
sudo gem install cocoapods
```

>? 요구 사항이나 피드백은 colleenyu@tencent.com으로 보내주시기 바랍니다.

