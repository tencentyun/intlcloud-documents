본문에서는 TUICallKit 컴포넌트의 액세스를 최단 시간에 완료하는 방법에 대해 설명합니다. 본 문서를 따르면, 다음 몇 가지 주요 단계를 한 시간 내에 완료하고 최종적으로 UI 인터페이스로 영상 통화 기능을 얻을 수 있습니다.

## 환경 준비

iOS 9.0 (API level 16) 이상.

[](id:step1)
##  1단계: 서비스 활성화

TUICallKit은 Tencent Cloud의 두 가지 유료 PaaS 서비스 [Instant Messaging(IM)](https://www.tencentcloud.com/document/product/1047) 및 [Tencent Real-Time Communication(TRTC)](https://www.tencentcloud.com/document/product/647)을 기반으로 하는 오디오/비디오 통신 컴포넌트입니다. 아래 단계에 따라 관련 서비스를 활성화하고 60일 무료 베타 서비스를 체험할 수 있습니다.

1. [IM 콘솔](https://console.tencentcloud.com/im)에 로그인하고 **애플리케이션 생성**을 클릭하고 팝업 대화 상자에 애플리케이션 이름을 입력하고 **확인**을 클릭합니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/c9a076ece348019d689c6c562b6a3c78.png)

2. 방금 만든 애플리케이션을 클릭하여 기본 구성 페이지로 들어갑니다. TUICallKit의 7일 무료 평가판을 보려면 페이지 오른쪽 하단 모서리에 있는 TRTC 활성화에서 무료 평가판을 클릭하십시오. 애플리케이션을 공식 릴리스하려면 [문의](https://intl.cloud.tencent.com/contact-us) 하십시오.
![img](https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png)

>! 다양한 비즈니스 요구 사항에 따라 IM 음성/영상 통화 기능의 다양한 유료 버전을 사용할 수 있습니다. 사용 가능한 기능에 대해 자세히 알아보고 적합한 버전을 구입하려면 [문의](https://intl.cloud.tencent.com/contact-us)하십시오.

3. 같은 페이지에서 **SDKAppID**와 **키(SecretKey)**를 찾아 기록해 둡니다. [4단계: TUI 컴포넌트 로그인](#step4)에서 사용될 예정입니다.
![img](https://qcloudimg.tencent-cloud.cn/raw/c3158845c9c0227a2da9eea8c0a975bb.png)


>? **참고:** **무료 평가판**을 클릭하면 이전에 [TRTC](https://www.tencentcloud.com/document/product/647/35078) 서비스를 사용한 적이 있는 일부 사용자에게 다음 메시지가 표시됩니다.
>```java
[-100013]:TRTC service is  suspended. Please check if the package balance is 0 or the Tencent Cloud accountis in arrears
>```
>새로운 IM 음성 및 영상 통화 기능은 [TRTC](https://www.tencentcloud.com/document/product/647/35078) 및 [IM](https://www.tencentcloud.com/document/product/1047)의 두 가지 기본 PaaS 서비스가 통합되어 있으므로, [TRTC](https://www.tencentcloud.com/document/product/647/35078)의 무료 할당량(10000분)이 만료되거나 소진되면 이 서비스를 활성화할 수 없습니다. 예시 이미지와 같이 [TRTC 콘솔](https://console.tencentcloud.com/trtc/app)을 클릭하여 SDKAppID에 해당하는 애플리케이션 관리 페이지에서 후불 기능을 활성화한 후 다시 **애플리케이션을 활성화**하면 음성 및 영상 통화 기능을 정상적으로 체험할 수 있습니다.


[](id:step2)
## 2단계: 컴포넌트 가져오기

CocoaPods를 사용하여 다음과 같이 컴포넌트를 가져옵니다.
1. `Podfile`에 다음 종속성을 추가합니다.

```shell
pod 'TUICallKit'
```

2. 다음 명령을 실행하여 컴포넌트를 설치합니다.
```shell
pod install
```
최신 버전의 TUICallKit을 설치할 수 없는 경우 다음 명령을 실행하여 로컬 CocoaPods 저장소 목록을 업데이트하십시오.
```shell
pod repo update
```

[](id:step3)
## 3단계: 프로젝트 구성 완료
오디오/비디오 기능을 사용하려면 마이크 및 카메라 권한을 부여해야 합니다. App의 Info.plist에 아래 두 항목을 추가합니다. 해당 콘텐츠는 사용자가 마이크 및 카메라 액세스 팝업 창에서 보는 것입니다.

```objectivec
<key>NSCameraUsageDescription</key>
<string>CallingApp이 이미지가 포함된 동영상을 촬영하려면 카메라에 액세스 필요</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingApp이 오디오가 포함된 동영상을 촬영하려면 마이크에 액세스 필요</string>
```
![img](https://qcloudimg.tencent-cloud.cn/raw/5579558165eae672db5259a8989fe5d4.png)

[](id:step4)
## 4단계: TUI 컴포넌트 로그인
프로젝트에 다음 코드를 추가하는 것은 TUICore에서 관련 인터페이스를 호출하여 TUI 컴포넌트의 로그인을 완료하는 것입니다. TUICallKit의 다양한 기능은 로그인이 성공한 후에야 정상적으로 사용할 수 있기 때문에 이 단계는 매우 중요합니다. 따라서 관련 매개변수가 올바르게 구성되었는지 확인하십시오.

<dx-codeblock>
:::  Objective-C Objectivec
// 컴포넌트에 로그인
[TUILogin login:1400000001           // // 1단계에서 얻은 SDKAppID로 교체하십시오
         userID:@"denny"             // UserID로 교체하십시오
         userSig:@"xxxxxxxxxxx"      // 콘솔에서 UserSig를 계산하고 여기에 입력할 수 있습니다
            succ:^{
    NSLog(@"login success");
} fail:^(int code, NSString *msg) {
    NSLog(@"login failed, code: %d, error: %@", code, msg);
}
:::
::: Swift
// 컴포넌트에 로그인
TUILogin.login(1400000001,                   // // 1단계에서 얻은 SDKAppID로 교체하십시오
            userID: "denny",                 // UserID로 교체하십시오
            userSig: "xxxxxxxxxxx") {        // 콘솔에서 UserSig를 계산하고 여기에 입력할 수 있습니다
    print("login success")
} fail: { (code, message) in
    print("login failed, code: \(code), error: \(message ?? "nil")")
}
:::
</dx-codeblock>

**매개변수 설명**:
여기에서는 login 함수에 사용되는 몇 가지 주요 매개변수에 대해 자세히 설명합니다.
- sdkAppId: 1단계의 마지막 순서에서 이미 얻었으므로 여기서 더 이상 반복하지 않습니다.
- userId: 현재 사용자 ID입니다. 영어 알파벳(a-z, A-Z), 숫자(0~9), 하이픈(-), 언더바(\_)의 문자열로 구성합니다.
- userSig: 현재 사용자가 TRTC 서비스를 사용할 수 있는지 여부를 확인하기 위해 Tencent Cloud에서 사용하는 인증 자격 증명입니다. 3단계에서 획득한 SecretKey를 사용하여 SDKAppID, UserID 등의 정보를 암호화하여 얻을 수 있습니다. 콘솔에서 [UserSig 생성](https://console.tencentcloud.com/trtc/app) 버튼을 클릭하여 임시 UserSig를 생성할 수 있습니다.
자세한 내용은 [UserSig 계산 방법](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.

> ! 
>- **이 단계는 지금까지 개발자들로부터 가장 많은 피드백을 받은 단계이기도 합니다. 자주 발생하는 문제는 다음과 같습니다:** 
    - sdkAppId 설정 오류. 중국 사이트의 SDKAppID는 일반적으로 140으로 시작하는 10자리 정수입니다.
    - userSig가 암호화 키(Secretkey)와 일치하지 않는 경우 SecretKey를 userSig로 직접 구성하지 않고 sdkAppId, userId, 만료 시간 등의 정보를 Secretkey로 암호화하여 userSig를 얻습니다.
    - userId는 ‘1’, ‘123’, ‘111’ 등의 간단한 문자열로 설정됩니다. **TRTC는 동일한 UserID의 다중 단말 로그인을 지원하지 않기 때문에**, 여러 사람이 공동으로 개발할 경우,‘1’, ‘123’, ‘111’과 같은 userId는 동료에 의해 쉽게 점유되어 로그인 실패의 원인이 될 수 있으므로 디버깅할 때 인식도가 높은 userId를 설정하는 것이 좋습니다.
>- Github의 예시 코드는 genTestUserSig 함수를 사용하여 현재 액세스 프로세스를 더 빠르게 실행할 수 있도록 로컬에서 userSig를 계산하지만 이 솔루션은 App 코드에 SecretKey를 노출하므로 SecretKey를 업그레이드하고 보호하려면 userSig의 계산 로직을 서버에 두는 것을 강력히 권장합니다. App은 TUICallKit 컴포넌트가 사용될 때마다 서버에서 실시간으로 계산된 userSig를 요청합니다.

[](id:step5)
## 5단계: 전화 걸기
### 1:1 영상 통화
TUICallKit의 call 함수를 호출하고 통화 유형 및 수신자의 userId를 지정하여 음성 또는 영상 통화를 시작할 수 있습니다.
<dx-codeblock>
:::  Objective-C Objectivec
// 1:1 영상 통화 시작(userId가 mike라고 가정)
[[TUICallKit createInstance] call:@"mike" callMediaType:TUICallMediaTypeVideo];
:::
::: Swift
// 1:1 영상 통화 시작(userId가 mike라고 가정)
TUICallKit.createInstance().call(userId: "mike", callMediaType: .video)
:::
</dx-codeblock>

| 매개변수       |  유형  | 의미 |
|-----|-----|-----|
| userId | String | 타깃 사용자의 UserID: `"mike"` |
| callMediaType | TUICallMediaType | 통화의 미디어 유형. 예시: `TUICallMediaTypeVideo` |

### 그룹 영상 통화
TUICallKit의 groupCall 함수를 호출하고 통화 유형 및 수신자의 UserID 목록을 지정하여 그룹 내에서 음성 또는 영상 통화를 시작할 수 있습니다.
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] groupCall:@"12345678" userIdList:@[@"denny", @"mike", @"tommy"] callMediaType:TUICallMediaTypeVideo];
:::
::: Swift
TUICallKit.createInstance().groupCall(groupId: "12345678", userIdList: ["denny", "mike", "tommy"], callMediaType: .video)
:::
</dx-codeblock>

| 매개변수       |  유형  | 의미 |
|-----|-----|-----|
| groupId | String | 그룹 ID. 예시: `@"12345678"` |
| userIdList | Array | 대상 사용자의 userId 값 목록, 예시: `@[@"denny", @"mike", @"tommy"]` |
| callMediaType | TUICallMediaType | 통화의 미디어 유형. 예시: `TUICallMediaTypeVideo` |

>? 
>- [Android, iOS, macOS](https://www.tencentcloud.com/document/product/1047/48466) 지침에 따라 그룹을 생성할 수 있습니다. [IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286)을 사용하여 채팅 및 통화 시나리오를 원스톱으로 통합할 수도 있습니다.
>- TUICallKit은 현재 그룹에 속하지 않은 사용자 간의 다중 사용자 영상 통화를 지원하지 않습니다. 필요한 경우 colleenyu@tencent.com으로 문의하십시오.

[](id:step6)
## 6단계: 전화 수신
**4단계** 이후에 전화가 오면 TUICallKit 컴포넌트가 자동으로 전화 응답 UI를 표시합니다.

[](id:step7)
## 7단계: 더 많은 특성
### 1. 닉네임 및 프로필 사진 설정
닉네임이나 프로필 사진을 사용자 지정하려면 다음 인터페이스를 사용하여 업데이트할 수 있습니다.
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] setSelfInfo:@"대화명" avatar:@"프로필 사진 url" succ:^{

} fail:^(int code, NSString *errMsg) {

}];
:::
::: Swift
TUICallKit.createInstance().setSelfInfo(nickname: "대화명", avatar: "프로필 사진 url", succ: {

}) { code, desc in

}
:::
</dx-codeblock>

> ! 사용자 개인정보 제한으로 인해 친구가 아닌 사용자와의 통화 시 수신자의 닉네임 및 프로필 사진 업데이트가 딜레이될 수 있으며, 통화 성공 후 원활하게 업데이트 됩니다.

### 2. 오프라인 푸시
상기 단계를 완료한 후 음성 또는 영상 통화를 걸거나 받을 수 있습니다. 그러나 `App이 백그라운드에 있거나` 또는 `APP이 닫힌 후`에도 사용자가 전화 초대를 받을 수 있도록 하려면 오프라인 푸시 기능도 구현해야 합니다. 자세한 내용은 [**오프라인 푸시(iOS)**](https://www.tencentcloud.com/document/product/647/51000)를 참고하십시오.

### 3. 플로팅 창 기능
플로팅 창 기능을 활성화하려면 TUICallKit 컴포넌트 초기화 시 다음 인터페이스를 호출하여 이 기능을 활성화할 수 있습니다.
 <dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] enableFloatWindow:YES];
:::
::: Swift
TUICallKit.createInstance().enableFloatWindow(true)
:::
</dx-codeblock>

### 4. 통화 상태 수신
만약 귀하의 업무에서 통화 시작, 종료, 통화 중 네트워크 품질 등 **통화 상태를 수신**하려면 다음 이벤트를 수신할 수 있습니다.
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallEngine createInstance] addObserver:self];

- (void)onCallBegin:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole {
  

}
- (void)onCallEnd:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole totalTime:(float)totalTime {
  

}
- (void)onUserNetworkQualityChanged:(NSArray<TUINetworkQualityInfo *> *)networkQualityList {
  

}
:::
::: Swift
TUICallEngine.createInstance().add(self)

public func onCallBegin(roomId: TUIRoomId, callMediaType: TUICallMediaType, callRole: TUICallRole) {
        
}
public func onCallEnd(roomId: TUIRoomId, callMediaType: TUICallMediaType, callRole: TUICallRole, totalTime: Float) {
        
}
public func onUserNetworkQualityChanged(networkQualityList: [TUINetworkQualityInfo]) {
        
}
:::
</dx-codeblock>

### 5. 사용자 지정 벨소리
수신 전화의 벨소리를 사용자 지정하려면 다음 인터페이스를 통해 설정할 수 있습니다.
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] setCallingBell:filePath];
:::
::: Swift
TUICallKit.createInstance().setCallingBell(filePath: filePath)
:::
</dx-codeblock>


## FAQ
### 1. ‘The package you purchased does not support this ability’라는 오류 메시지가 표시되면 어떻게 해야 합니까?

오류 메시지는 애플리케이션의 오디오/비디오 통화 기능 패키지가 만료되었거나 활성화되지 않았음을 나타냅니다. TUICallKit을 계속 사용하려면 [1단계](#step1)의 지침에 따라 음성/영상 통화 기능을 요청하거나 활성화할 수 있습니다.

### 2. 플랜은 어떻게 구매하나요?

자세한 내용은 [가격 개요](https://www.tencentcloud.com/document/product/647/50553)를 참고하십시오. 기타 궁금한 사항이 있으시면 페이지 우측의 프리세일 패키지 상담을 클릭하시거나 QQ그룹 **592465424**에 가입하여 상담 및 피드백 부탁드립니다.

>? 자세한 내용은 [FAQ (iOS)](https://www.tencentcloud.com/document/product/647/51023)를 참고하십시오.

## 교류 및 피드백

사용 중 제안이나 의견이 있으시면 colleenyu@tencent.com으로 연락주시기 바랍니다.
