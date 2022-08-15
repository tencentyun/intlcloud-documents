## 컴포넌트 개요

TUILiveRoom은 오픈 소스 비디오 라이브 스트리밍 시나리오 UI 컴포넌트입니다. 프로젝트에 통합한 후 몇 줄의 코드 작성만으로 App이 ‘인터랙티브 비디오 라이브 스트리밍’ 시나리오를 추가할 수 있습니다. Android, iOS 및 미니프로그램 플랫폼용 소스 코드를 제공합니다. 기본 기능은 다음과 같습니다.

>?TUIKit 시리즈 컴포넌트는 Tencent Cloud의 두 가지 기본 PaaS 서비스, 즉 [Tencent Real-Time Communication](https://intl.cloud.tencent.com/document/product/647/35078) 및 [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/35448)을 사용합니다. TRTC를 활성화하면 IM과 IM SDK 평가판(100 DAU만 지원)이 자동으로 활성화됩니다. IM 과금 내역은 [요금 안내](https://intl.cloud.tencent.com/document/product/1047/34350)를 참고하십시오.

<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)
## 컴포넌트 통합

[](id:model.step1)
### 1단계: TUILiveRoom 컴포넌트 가져오기

**cocoapods를 통해 컴포넌트를 가져오려면** 다음 단계를 따르십시오.
1. 프로젝트의 `Podfile`과 같은 수준에 `TUILiveRoom` 폴더를 만듭니다.
2. 클릭하여 [**Github/TUILiveRoom**](https://github.com/tencentyun/TUILiveRoom)으로 이동하고 클론/다운로드 코드를 선택한 다음 [**TUILiveRoom/iOS/**](https://github.com/tencentyun/TUILiveRoom/tree/main/iOS) 디렉터리에 `Source`, `Resources`, `TUIBeauty`, `TUIAudioEffect`, `TUIBarrage`, `TUIGift`, `TXAppBasic` 폴더 및 `TUILiveRoom.podspec` 파일을 `1단계`에서 생성한 TUILiveRoom 폴더에 복사합니다.
3. Podfile에 다음 종속성을 추가하고 `pod install`을 실행하여 가져오기를 완료합니다.
```
# :path => "TUILiveRoom.podspec의 상대 경로를 가리킵니다."
pod 'TUILiveRoom', :path => "./TUILiveRoom/TUILiveRoom.podspec", :subspecs => ["TRTC"]
# :path => "TXAppBasic.podspec의 상대 경로를 가리킵니다."
pod 'TXAppBasic', :path => "./TUILiveRoom/TXAppBasic/"
# :path => "TUIBeauty.podspec의 상대 경로를 가리킵니다."
pod 'TUIBeauty', :path => "./TUILiveRoom/TUIBeauty/"
# :path => "TUIAudioEffect.podspec의 상대 경로를 가리킵니다."
pod 'TUIAudioEffect', :path => "./TUILiveRoom/TUIAudioEffect/"
# :path => "TUIBarrage.podspec의 상대 경로를 가리킵니다."
pod 'TUIBarrage', :path => "./TUILiveRoom/TUIBarrage/"
# :path => "TUIGift.podspec의 상대 경로를 가리킵니다."
pod 'TUIGift', :path => "./TUILiveRoom/TUIGift/"
```

>! 
>- `Source` 및 `Resources` 폴더와 `TUILiveRoom.podspec` 파일은 동일한 디렉터리에 있어야 합니다.
>- TXAppBasic.podspec은 TXAppBasic 폴더에 있습니다.

[](id:model.step2)
### 2단계: 권한 설정

오디오/비디오 기능을 사용하려면 마이크 및 카메라 권한을 부여해야 합니다. App의 Info.plist에 아래 두 항목을 추가합니다. 해당 콘텐츠는 사용자가 마이크 및 카메라 액세스 팝업 창에서 보는 것입니다.

```
<key>NSCameraUsageDescription</key>
<string>RoomApp은 이미지가 포함된 비디오를 촬영하려면 카메라에 액세스해야 합니다.</string>
<key>NSMicrophoneUsageDescription</key>
<string>RoomApp은 오디오가 포함된 비디오를 녹화하려면 마이크에 액세스해야 함</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/9395aca2af5433c9a63ffb4ba9ff9888.png)

[](id:model.step3)
### 3단계: 컴포넌트 초기화 및 로그인

<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUILiveRoom;
@import TUICore;

// 1. 컴포넌트에 로그인
[TUILogin login:@"사용자 SDKAppID" userID:@"사용자 UserID" userSig:@"사용자 UserSig" succ:^{
        
} fail:^(int code, NSString *msg) {
        
}];
// 2. TUILiveRoom 인스턴스 초기화
TUILiveRoom *mLiveRoom = [TUILiveRoom sharedInstance];
```
:::
::: Swift Swift
import TUILiveRoom
import TUICore

// 1. 컴포넌트에 로그인
TUILogin.login("사용자 SDKAppID", userID: "사용자 UserID", userSig: "사용자 UserSig") {
        
} fail: { code, msg in
        
}
// 2. TUILiveRoom 인스턴스 초기화
let mLiveRoom = TUILiveRoom.sharedInstance
```
:::
</dx-codeblock>

**매개변수 설명**:
- **SDKAppID**: **TRTC 애플리케이션 ID**입니다. TRTC 서비스를 활성화하지 않은 경우 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에 로그인하여 TRTC 애플리케이션을 생성하고 **애플리케이션 정보**를 클릭합니다. SDKAppID는 아래와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: SDKAppID에 해당하는 **TRTC 애플리케이션 키**입니다. TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지로 이동한 후, SecretKey는 아래와 같습니다.
- **userId**: 문자열이며 최대 32바이트의 문자와 숫자를 포함할 수 있는 현재 사용자 ID입니다(특수 기호는 지원되지 않음). 실제 계정 시스템에 따라 사용자 정의할 수 있습니다.
- **userSig**: SDKAppId, UserID 및 Secretkey를 기반으로 계산된 보안 보호 서명입니다. [여기](https://console.cloud.tencent.com/trtc/usersigtool)를 클릭하여 디버깅 UserSig를 온라인으로 직접 생성하거나 [TUILiveRoom 데모 프로젝트](https://github.com/tencentyun/TUILiveRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42)를 참고하여 직접 계산할 수 있습니다. 자세한 내용은 [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)를 참고하십시오


[](id:model.step4)
### 4단계: 인터랙티브 비디오 라이브 룸 구현
1. **앵커 방송 시작**
<dx-codeblock>
:::  Objective-C Objc
[mLiveRoom createRoomWithRoomId:123 roomName:@"test room" coverUrl:@""];

:::
:::  Swift Swift
mLiveRoom.createRoom(roomId: 123, roomName: "test room", coverUrl:"")
:::
</dx-codeblock>
2. **시청자 시청**
<dx-codeblock>
:::  Objective-C Objc
[mLiveRoom enterRoomWithRoomId:123];

:::
:::  Swift Swift
mLiveRoom.createRoom(roomId: 123)
:::
</dx-codeblock>

3. **[TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37332#requestjoinanchor)를 통해 관객과 앵커가 함께 공동 앵커합니다.**
<dx-codeblock>
:::  Objective-C Objc
// 1.시청자가 공동 앵커 요청 발송
[TRTCLiveRoom shareInstance].delegate = self;
// @param mSelfUserId String 현재 사용자 id
NSString *mSelfUserId = @"1314";
[[TRTCLiveRoom shareInstance] requestJoinAnchor:[NSString stringWithFormat:@"%@ 공동 앵커 요청", mSelfUserId] timeout:30 responseCallback:^(BOOL agreed, NSString * _Nullable reason) {
    if (agreed) {
        // 앵커가 요청 수락
      UIView *playView = [UIView new];
            [self.view addSubView:playView];
        // 시청자가 카메라를 켜고 스트림을 푸시 시작
      [[TRTCLiveRoom shareInstance] startCameraPreviewWithFrontCamera:YES view:playView callback:nil];
      [[TRTCLiveRoom shareInstance] startPublishWithStreamID:[NSString stringWithFormat:@"%@_stream", mSelfUserId] callback:nil];
    }            
}];

// 2.앵커가 공동 앵커 요청 수신
#pragma mark - TRTCLiveRoomDelegate
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onRequestJoinAnchor:(TRTCLiveUserInfo *)user reason:(NSString *)reason {
    // 공동 앵커 요청에 동의
    [[TRTCLiveRoom shareInstance] responseJoinAnchor:user.userId agree:YES reason:@"공동 앵커에 동의"];
}

- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onAnchorEnter:(NSString *)userID {
    // 앵커는 공동 앵커 시청자가 마이크를 켰다는 알림 수신
    UIView *playView = [UIView new];
    [self.view addSubview:playView];
    // 앵커가 시청자 화면 재생
    [[TRTCLiveRoom shareInstance] startPlayWithUserID:userID view:playView callback:nil];
}

:::
:::  Swift Swift
// 1.시청자가 공동 앵커 요청 발송
TRTCLiveRoom.shareInstance().delegate = self
let mSelfUserId = "1314"
TRTCLiveRoom.shareInstance().requestJoinAnchor(reason: mSelfUserId + "공동 앵커 요청", timeout: 30) {  [weak self] (agree, msg) in
    guard let self = self else { return }
  if agree {
        // 앵커가 요청 수락
        let playView = UIView()
        self.view.addSubView(playView)
        // 시청자가 카메라를 켜고 스트림을 푸시 시작
        TRTCLiveRoom.shareInstance().startCameraPreview(frontCamera: true, view: playView)
        TRTCLiveRoom.shareInstance().startPublish(streamID: mSelfUserId + "_stream")
  }
}

// 2.앵커가 공동 앵커 요청 수신
extension ViewController: TRTCLiveRoomDelegate {
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?) {
        // 공동 앵커 요청에 동의
        TRTCLiveRoom.shareInstance().responseRoomPK(userID: user.userId, agree: true, reason: "공동 앵커에 동의")
    }
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
        // 앵커는 공동 앵커 시청자가 마이크를 켰다는 알림 수신
        let playView = UIView()
        view.addSubview(playView)
        // 앵커가 시청자 화면 재생
        TRTCLiveRoom.shareInstance().startPlay(userID: userID, view: playView);
    }
}
:::
</dx-codeblock>

4. **앵커는 [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37332#requestroompk)를 통해 PK합니다.**
<dx-codeblock>
:::  Objective-C Objc
// 12345 방 생성
[[TUILiveRoom sharedInstance] createRoomWithRoomId:12345 roomName:@"roomA" coverUrl:@"roomA coverUrl"];
// 54321 방 생성
[[TUILiveRoom sharedInstance] createRoomWithRoomId:54321 roomName:@"roomB" coverUrl:@"roomB coverUrl"];

// 앵커 A
// 앵커 B에 PK 요청 보내기
[[TRTCLiveRoom shareInstance] requestRoomPKWithRoomID:543321 userID:@"roomB userId" timeout:30 responseCallback:^(BOOL agreed, NSString * _Nullable reason) {
    if (agreed) {
        // 사용자 B 수락
    } else {
        // 사용자 B 거절
    }
}];

// 앵커 B:
// 2.앵커 A의 요청 수신
#pragma mark - TRTCLiveRoomDelegate
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onRequestRoomPK:(TRTCLiveUserInfo *)user {
    // 3.앵커 A의 요청 수락
    [[TRTCLiveRoom shareInstance] responseRoomPKWithUserID:user.userId agree:YES reason:@""];
}

- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onAnchorEnter:(NSString *)userID {
    // 4.앵커 A 진입 알림 수신 및 앵커 A 영상 재생
    [[TRTCLiveRoom shareInstance] startPlayWithUserID:userID view:playAView callback:nil];
}

:::
:::  Swift Swift
// 12345 방 생성
TUILiveRoom.sharedInstance.createRoom(roomId: 12345, roomName: "roomA")
// 54321 방 생성
TUILiveRoom.sharedInstance.createRoom(roomId: 54321, roomName: "roomB")

// 앵커 A
// 앵커 B에 PK 요청 보내기
TRTCLiveRoom.shareInstance().requestRoomPK(roomID: 543321, userID: "roomB userId", timeout: 30) { [weak self] (agreed, msg) in
     guard let self = self else { return }
    if agreed {
        // 사용자 B 수락
    } else {
        // 사용자 B 거절
    }
}

// 앵커 B:
// 2.앵커 A의 요청 수신
extension ViewController: TRTCLiveRoomDelegate {
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo) {
        // 3.앵커 A의 요청 수락
        TRTCLiveRoom.shareInstance().responseRoomPK(userID: user.userId, agree: true, reason: "")
    }
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
        // 4.앵커 A 진입 알림 수신 및 앵커 A 영상 재생
        TRTCLiveRoom.shareInstance().startPlay(userID: userID, view: playAView);
    }
}
:::
</dx-codeblock>

## FAQ
요구 사항이나 피드백은 colleenyu@tencent.com으로 보내주시기 바랍니다.
