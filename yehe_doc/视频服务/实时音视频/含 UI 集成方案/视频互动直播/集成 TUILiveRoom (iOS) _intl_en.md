## Overview

`TUILiveRoom` is an open-source video live streaming scenario UI component. After integrating it into your project, you can enable your application to support interactive video live streaming simply by writing a few lines of code. It provides source code for Android, iOS, and mini program platforms. Its basic features are as shown below:

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)
## Integration

[](id:model.step1)
### Step 1. Import the `TUILiveRoom` component

**To import the component using CocoaPods**, follow the steps below:
1. Create a `TUILiveRoom` folder in the same directory as `Podfile` in your project.
2. Go to the component's [GitHub page](https://github.com/tencentyun/TUILiveRoom), clone or download the code, and copy the `Source`, `Resources`, `TUIBeauty`, `TUIAudioEffect`, `TUIBarrage`, `TUIGift`, and `TXAppBasic` folders and the `TUILiveRoom.podspec` file in [**TUILiveRoom/iOS/**](https://github.com/tencentyun/TUILiveRoom/tree/main/iOS) to the `TUILiveRoom` folder in your project.
3. Add the following dependencies to your `Podfile` and run `pod install` to import the component.
```
# :path => "The relative path of `TUILiveRoom.podspec`"
pod 'TUILiveRoom', :path => "./TUILiveRoom/TUILiveRoom.podspec", :subspecs => ["TRTC"]
# :path => "The relative path of `TXAppBasic.podspec`"
pod 'TXAppBasic', :path => "./TUILiveRoom/TXAppBasic/"
# :path => "The relative path of `TUIBeauty.podspec`"
pod 'TUIBeauty', :path => "./TUILiveRoom/TUIBeauty/"
# :path => "The relative path of `TUIBeauty.podspec`"
pod 'TUIAudioEffect', :path => "./TUILiveRoom/TUIAudioEffect/"
# :path => "The relative path of `TUIBeauty.podspec`"
pod 'TUIBarrage', :path => "./TUILiveRoom/TUIBarrage/"
# :path => "The relative path of `TUIBeauty.podspec`"
pod 'TUIGift', :path => "./TUILiveRoom/TUIGift/"
```

>! 
>- The `Source` and `Resources` folders and the `TUILiveRoom.podspec` file must be in the same directory.
>- `TXAppBasic.podspec` is in the `TXAppBasic` folder.

[](id:model.step2)
### Step 2. Configure permissions

Your app needs mic and camera permissions to implement audio/video communication. Add the two items below to `Info.plist` of your app. Their content is what users see in the mic and camera access pop-up windows.

```
<key>NSCameraUsageDescription</key>
<string>RoomApp needs to access your camera to capture video.</string>
<key>NSMicrophoneUsageDescription</key>
<string>RoomApp needs to access your mic to capture audio.</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/9395aca2af5433c9a63ffb4ba9ff9888.png)

[](id:model.step3)
### Step 3. Initialize and log in to the component

<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUILiveRoom;
@import TUICore;

// 1. Log in to the component
[TUILogin login:@"Your SDKAppID" userID:@"Your UserID" userSig:@"Your UserSig" succ:^{
        
} fail:^(int code, NSString *msg) {
        
}];
// 2. Initialize the `TUILiveRoom` instance
TUILiveRoom *mLiveRoom = [TUILiveRoom sharedInstance];
```
:::
::: Swift  Swift
import TUILiveRoom
import TUICore

// 1. Log in to the component
TUILogin.login("Your SDKAppID", userID: "Your UserID", userSig: "Your UserSig") {
        
} fail: { code, msg in
        
}
// 2. Initialize the `TUILiveRoom` instance
let mLiveRoom = TUILiveRoom.sharedInstance
```
:::
</dx-codeblock>

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated TRTC, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, click **Application Info**, and select the **Quick Start** tab to view its `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**. Each secret key corresponds to an `SDKAppID`. You can view your application’s secret key on the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- **UserId**: Current user ID, which is a custom string that can contain up to 32 bytes of letters and digits (special characters are not supported).
- **UserSig**: Security signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to quickly generate a `UserSig` for testing or calculate it on your own by referring to our [TUILiveRoom demo project](https://github.com/tencentyun/TUILiveRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


[](id:model.step4)
### Step 4. Implement an interactive video live room
1. **The anchor starts streaming**.
<dx-codeblock>
:::  Objective-C Objc
[mLiveRoom createRoomWithRoomId:123 roomName:@"test room" coverUrl:@""];

:::
:::  Swift Swift
mLiveRoom.createRoom(roomId: 123, roomName: "test room", coverUrl:"")
:::
</dx-codeblock>
2. **The audience member watches**.
<dx-codeblock>
:::  Objective-C Objc
[mLiveRoom enterRoomWithRoomId:123];

:::
:::  Swift Swift
mLiveRoom.createRoom(roomId: 123)
:::
</dx-codeblock>

3. **The audience member and the anchor co-anchor together through [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37332#requestjoinanchor)**.
<dx-codeblock>
:::  Objective-C Objc
// 1. The audience member sends a co-anchoring request
[TRTCLiveRoom shareInstance].delegate = self;
// @param mSelfUserId String Current user ID
NSString *mSelfUserId = @"1314";
[[TRTCLiveRoom shareInstance] requestJoinAnchor:[NSString stringWithFormat:@"%@ requested to co-anchor", mSelfUserId] timeout:30 responseCallback:^(BOOL agreed, NSString * _Nullable reason) {
    if (agreed) {
        // The request is accepted by the anchor
      UIView *playView = [UIView new];
            [self.view addSubView:playView];
        // The audience member turns on the camera and starts pushing streams
      [[TRTCLiveRoom shareInstance] startCameraPreviewWithFrontCamera:YES view:playView callback:nil];
      [[TRTCLiveRoom shareInstance] startPublishWithStreamID:[NSString stringWithFormat:@"%@_stream", mSelfUserId] callback:nil];
    }            
}];

// 2. The anchor receives the co-anchoring request
#pragma mark - TRTCLiveRoomDelegate
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onRequestJoinAnchor:(TRTCLiveUserInfo *)user reason:(NSString *)reason {
    // The anchor accepts the co-anchoring request
    [[TRTCLiveRoom shareInstance] responseJoinAnchor:user.userId agree:YES reason:@"agreed to co-anchor"];
}

- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onAnchorEnter:(NSString *)userID {
    // The anchor receives a notification that the co-anchoring audience member has turned on the mic
    UIView *playView = [UIView new];
    [self.view addSubview:playView];
    // The anchor plays the audience member's video
    [[TRTCLiveRoom shareInstance] startPlayWithUserID:userID view:playView callback:nil];
}

:::
:::  Swift Swift
// 1. The audience member sends a co-anchoring request
TRTCLiveRoom.shareInstance().delegate = self
let mSelfUserId = "1314"
TRTCLiveRoom.shareInstance().requestJoinAnchor(reason: mSelfUserId + "requested to co-anchor", timeout: 30) {  [weak self] (agree, msg) in
    guard let self = self else { return }
  if agree {
        // The request is accepted by the anchor
        let playView = UIView()
        self.view.addSubView(playView)
        // The audience member turns on the camera and starts pushing streams
        TRTCLiveRoom.shareInstance().startCameraPreview(frontCamera: true, view: playView)
        TRTCLiveRoom.shareInstance().startPublish(streamID: mSelfUserId + "_stream")
  }
}

// 2. The anchor receives the co-anchoring request
extension ViewController: TRTCLiveRoomDelegate {
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?) {
        // The anchor accepts the co-anchoring request
        TRTCLiveRoom.shareInstance().responseRoomPK(userID: user.userId, agree: true, reason: "agreed to co-anchor")
    }
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
        // The anchor receives a notification that the co-anchoring audience member has turned on the mic
        let playView = UIView()
        view.addSubview(playView)
        // The anchor plays the audience member's video
        TRTCLiveRoom.shareInstance().startPlay(userID: userID, view: playView);
    }
}
:::
</dx-codeblock>

4. **Anchors from different rooms communicate with each other by calling [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37332#requestroompk)**.
<dx-codeblock>
:::  Objective-C Objc
// Create room 12345
[[TUILiveRoom sharedInstance] createRoomWithRoomId:12345 roomName:@"roomA" coverUrl:@"roomA coverUrl"];
// Create room 54321
[[TUILiveRoom sharedInstance] createRoomWithRoomId:54321 roomName:@"roomB" coverUrl:@"roomB coverUrl"];

// Host A
// Send a cross-room communication request to anchor B
[[TRTCLiveRoom shareInstance] requestRoomPKWithRoomID:543321 userID:@"roomB userId" timeout:30 responseCallback:^(BOOL agreed, NSString * _Nullable reason) {
    if (agreed) {
        // Anchor B accepts the request
    } else {
        // Anchor B rejects the request
    }
}];

// Anchor B:
// 2. Receive anchor A’s request
#pragma mark - TRTCLiveRoomDelegate
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onRequestRoomPK:(TRTCLiveUserInfo *)user {
    // 3. Accept anchor A's request
    [[TRTCLiveRoom shareInstance] responseRoomPKWithUserID:user.userId agree:YES reason:@""];
}

- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onAnchorEnter:(NSString *)userID {
    // 4. Receive a notification about anchor A’s entry and play anchor A's video
    [[TRTCLiveRoom shareInstance] startPlayWithUserID:userID view:playAView callback:nil];
}

:::
:::  Swift Swift
// Create room 12345
TUILiveRoom.sharedInstance.createRoom(roomId: 12345, roomName: "roomA")
// Create room 54321
TUILiveRoom.sharedInstance.createRoom(roomId: 54321, roomName: "roomB")

// Host A
// Send a cross-room communication request to anchor B
TRTCLiveRoom.shareInstance().requestRoomPK(roomID: 543321, userID: "roomB userId", timeout: 30) { [weak self] (agreed, msg) in
     guard let self = self else { return }
    if agreed {
        // Anchor B accepts the request
    } else {
        // Anchor B rejects the request
    }
}

// Anchor B:
// 2. Receive anchor A’s request
extension ViewController: TRTCLiveRoomDelegate {
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo) {
        // 3. Accept anchor A's request
        TRTCLiveRoom.shareInstance().responseRoomPK(userID: user.userId, agree: true, reason: "")
    }
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
        // 4. Receive a notification about anchor A’s entry and play anchor A's video
        TRTCLiveRoom.shareInstance().startPlay(userID: userID, view: playAView);
    }
}
:::
</dx-codeblock>

## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
