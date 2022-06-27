## 컴포넌트 개요

TUICalling은 오픈 소스 오디오/비디오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 ‘1:1 음성/영상 통화’ 및 ‘그룹 음성/영상 통화’ 및 오프라인 통화와 같은 App 지원 시나리오를 만들 수 있습니다. 또한 Android, Web, Flutter 및 UniApp 플랫폼을 지원합니다. 기본 기능은 다음과 같습니다.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png" </td>
</tr>
</tbody></table>


## 컴포넌트 통합

### 1단계: TUICalling 컴포넌트 가져오기

**cocoapods를 통해 컴포넌트를 가져오려면** 다음 단계를 따르십시오.
1. 프로젝트의 `Podfile`과 같은 수준에 `TUICalling` 폴더를 만듭니다.
2. [**GitHub/TUICalling**](https://github.com/tencentyun/TUICalling)으로 이동하여 코드를 복제 또는 다운로드하고 [**TUICalling/iOS/**](https://github.com/tencentyun/TUICalling/tree/main/iOS) 디렉터리의 `Source` 및 `Resources` 폴더와 `TUICalling.podspec` 파일을 `1단계`에서 만든 TUICalling 폴더에 복사합니다.
3. Podfile에 다음 종속성을 추가하고 `pod install`을 실행하여 가져오기를 완료합니다.
```
# :path => "TUICalling.podspec의 상대 경로를 가리킵니다"
pod 'TUICalling', :path => "TUICalling/TUICalling.podspec", :subspecs => ["TRTC"]
```

>!  `Source` 및 `Resources` 폴더와 `TUICalling.podspec` 파일은 동일한 디렉터리에 있어야 합니다.

### 2단계: 권한 구성

오디오/비디오 기능을 사용하려면 마이크 및 카메라 권한을 부여해야 합니다. App의 Info.plist에 아래 두 항목을 추가합니다. 해당 콘텐츠는 사용자가 마이크 및 카메라 액세스 팝업 창에서 보는 것입니다.

```
<key>NSCameraUsageDescription</key>
<string>CallingApp이 이미지가 포함된 동영상을 촬영하려면 카메라에 액세스 필요</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingApp이 오디오가 포함된 동영상을 촬영하려면 마이크에 액세스 필요</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### 3단계: 컴포넌트 생성 및 초기화

<dx-tabs>
:::  Objective-C
```
// 1. 컴포넌트에 로그인
[TUILogin initWithSdkAppID:@"사용자 SDKAppID"];
[TUILogin login:@"사용자 UserID" userSig:@"사용자 UserSig" succ:^{
    NSLog(@"login success");
} fail:^(int code, NSString *msg) {
    NSLog(@"login failed, code: %d, error: %@", code, msg);
}];

// 2. TUICalling 인스턴스 초기화
[TUICalling shareInstance];
```
:::
::: Swift
```
// 1. 컴포넌트에 로그인
TUILogin.initWithSdkAppID("사용자 SDKAppID")
TUILogin.login("사용자 UserID", userSig: "사용자 UserSig") {
    print("login success")
} fail: { code, message in
    print("login failed, code: \(code), error: \(message ?? "nil")")
}

// 2. TUICalling 인스턴스 초기화
TUICalling.shareInstance()
```
:::
</dx-tabs>

**매개변수 설명**:
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지로 이동한 후, SecretKey는 아래와 같습니다.
- **userId**: 문자열이며 최대 32바이트의 문자와 숫자를 포함할 수 있는 현재 사용자 ID입니다(특수 기호는 지원되지 않음). 실제 계정 시스템에 따라 사용자 정의할 수 있습니다.
- **userSig**: SDKAppId, UserID 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 UserSig를 온라인으로 직접 생성하거나 [TUICalling 데모 프로젝트](https://github.com/tencentyun/TUICalling/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L39)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오

### 4단계: 음성/영상 통화 걸기

- TUICalling#call 을 통한 1:1 음성/영상 통화
<dx-codeblock>
:::  Objective-C Objectivec
// 1:1 영상 통화를 시작합니다. userId가 1111이라고 가정합니다.
[[TUICalling shareInstance] call:@[@"1111"] type:TUICallingTypeVideo];
:::
::: Swift Swift
// 1:1 영상 통화를 시작합니다. userId가 1111이라고 가정합니다.
TUICalling.shareInstance().call(userIDs: ["1111"], type: .video)
:::
</dx-codeblock>
- 그룹 영상 통화 걸기 TUICalling#call
<dx-codeblock>
:::  Objective-C Objectivec
// 그룹 영상 통화를 시작합니다. userId 값이 1111, 2222, 3333이라고 가정합니다.
[[TUICalling shareInstance] call:@[@"1111", @"2222", @"3333"] type:TUICallingTypeVideo];
:::
::: Swift Swift
// 그룹 영상 통화를 시작합니다. userId 값이 1111, 2222, 3333이라고 가정합니다.
TUICalling.shareInstance().call(userIDs: ["1111", "2222", "3333"], type: .video)
:::
</dx-codeblock>

>? 수신자가 3단계를 완료한 후(즉, 로그인 성공 후) 다시 호출 요청을 수신하면 TUICalling 컴포넌트는 해당 호출 응답 UI를 자동으로 표시합니다.

### 5단계: 오프라인 푸시 기능 추가(옵션)
상기 4단계가 완료되면 영상 통화를 걸고 받을 수 있습니다. 그러나 비즈니스 시나리오에서 ‘App 프로세스가 종료’되거나 ‘백그라운드에서 실행’된 후에도 음성/영상 통화 요청을 정상적으로 수신할 수 있어야 하는 경우 TUICalling 컴포넌트에 오프라인 푸시 기능을 추가해야 합니다. 자세한 내용은 [**오프라인 푸시(iOS)**](https://intl.cloud.tencent.com/document/product/1047/39157)를 참고하십시오.

### 6단계: 상태 수신 기능 추가(옵션)

통화 시작 및 종료와 같이 비즈니스에서 통화 상태 수신 을 위해서는 다음 이벤트를 수신하십시오.
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICalling shareInstance] setCallingListener:self];

- (BOOL)shouldShowOnCallView {
    return YES;
}

- (void)callStart:(nonnull NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController {

}

- (void)callEnd:(nonnull NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(float)totalTime {

}

- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(nonnull NSString *)message {

}
:::
::: Swift Swift
TUICalling.shareInstance().setCallingListener(listener: self)

public func shouldShowOnCallView() -> Bool {
    return true
}
    
public func callStart(userIDs: [String], type: TUICallingType, role: TUICallingRole, viewController: UIViewController?) {

}
    
public func callEnd(userIDs: [String], type: TUICallingType, role: TUICallingRole, totalTime: Float) {

}
    
public func onCallEvent(event: TUICallingEvent, type: TUICallingType, role: TUICallingRole, message: String) {

}
:::
</dx-codeblock>

### 7단계: 플로팅 창 기능 추가(옵션)

비즈니스에서 플로팅 창 기능 을 활성화하려면 TUICalling 컴포넌트 초기화 중에 `TUICalling.shareInstance().enableFloatWindow(enable: true)`를 호출합니다.

>? 현재 컴포넌트는 in-app 플로팅 창만 지원합니다(최소화 및 이전 페이지로 돌아가기).

## FAQ

### TUICalling 컴포넌트는 사용자 정의 벨소리를 지원합니까?

지원합니다. TUICalling#setCallingBell 을 호출하여 이를 구현할 수 있습니다.

### CocoaPods는 어떻게 설치합니까?

터미널 창에 다음 명령어를 입력합니다(먼저 Mac에 Ruby를 설치해야 함).
```
sudo gem install cocoapods
```

### TUICalling을 백그라운드에서 실행할 수 있습니까?

지원합니다. SDK를 백그라운드에서 실행하려면 프로젝트를 선택하고 **Capabilities** 탭에서 **Background Modes**를 **ON**으로 설정하고 아래와 같이 **Audio, AirPlay and Picture in Picture**를 선택합니다.
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

>? 요구 사항이나 피드백이 있는 경우 colleenyu@tencent.com으로 문의하십시오.
