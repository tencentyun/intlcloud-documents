## Overview
`TUIRoom` is an open-source UI component for audio/video communication. With just a few lines of code changes, you can integrate it into your project to implement screen sharing, beauty filters, low-latency video calls, and other features. In addition to the iOS component, we also offer components for [Android](https://intl.cloud.tencent.com/document/product/647/37283), [Windows](https://intl.cloud.tencent.com/document/product/647/44071), [macOS](https://intl.cloud.tencent.com/document/product/647/44071), and more.

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2944bac3c5d348b06d2a11c439783b48.png"></td>
</tr>
</tbody></table>

## Integration

### Step 1. Import the `TUIRoom` component

**To import the component using CocoaPods**, follow the steps below:
1. Create a `TUIRoom` folder in the same directory as `Podfile` in your project.
2. Go to the component’s [GitHub page](https://github.com/tencentyun/TUIRoom), clone or download the code, and copy the `Source`, `Resources`, `TUIBeauty`, and `TXAppBasic` folders and the `TUIRoom.podspec` file in [TUIRoom/iOS/](https://github.com/tencentyun/TUIRoom/tree/main/iOS) to the `TUIRoom` folder in your project.
3. Add the following dependencies to your `Podfile` and run `pod install` to import the component.
```
# :path => "The relative path of `TUIRoom.podspec`"
pod 'TUIRoom', :path => "./TUIRoom/TUIRoom.podspec", :subspecs => ["TRTC"]
# :path => "The relative path of `TXAppBasic.podspec`"
pod 'TXAppBasic', :path => "./TUIRoom/TXAppBasic/"
# :path => "The relative path of `TUIBeauty.podspec`"
pod 'TUIBeauty', :path => "./TUIRoom/TUIBeauty/"
```

>! The `Source` and `Resources` folders and the `TUIRoom.podspec` file must be in the same directory.
>- `TXAppBasic.podspec` is in the `TXAppBasic` folder.
>- `TUIBeauty.podspec` is in the `TCBeautyKit` folder.

### Step 2. Configure permissions

Your app needs mic and camera permissions to implement audio/video communication. Add the two items below to `Info.plist` of your app. Their content is what users see in the mic and camera access pop-up windows.

```
<key>NSCameraUsageDescription</key>
<string>RoomApp needs to access your camera to capture video.</string>
<key>NSMicrophoneUsageDescription</key>
<string>RoomApp needs to access your mic to capture audio.</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/9395aca2af5433c9a63ffb4ba9ff9888.png)

### Step 3. Create and initialize an instance of the component

<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;
@import TUICore;

// 1. Log in to the component
[TUILogin login:@"Your SDKAppID" userID:@"Your UserID" userSig:@"Your UserSig" succ:^{
        
} fail:^(int code, NSString *msg) {
        
}];
// 2. Initialize the `TUIRoom` instance
TUIRoom *tuiRoom = [TUIRoom sharedInstance];
```
:::
::: Swift  Swift
import TUIRoom
import TUICore

// 1. Log in to the component
TUILogin.login("Your SDKAppID", userID: "Your UserID", userSig: "Your UserSig") {
        
} fail: { code, msg in
        
}

// 2. Initialize the `TUIRoom` instance
let tuiRoom = TUIRoom.sharedInstance
```
:::
</dx-codeblock>

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated TRTC, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, click **Application Info**, and select the **Quick Start** tab to view its `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**. Each secret key corresponds to an `SDKAppID`. You can view your application’s secret key on the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- **UserId**: Current user ID, which is a custom string that can contain up to 32 bytes of letters and digits (special characters are not supported).
- **UserSig**: Security signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to quickly generate a `UserSig` for testing or calculate it on your own by referring to our [TUIRoom demo project](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


### Step 4. Implement group audio/video communication
1. **Create a room**
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[tuiRoom createRoomWithRoomId:12345 speechMode:TUIRoomFreeSpeech isOpenCamera:YES isOpenMicrophone:YES];
:::
::: Swift  Swift
import TUIRoom

tuiRoom.createRoom(roomId: 12345, speechMode: .freeSpeech, isOpenCamera: true, isOpenMicrophone: true)
```
:::
</dx-codeblock>
2. **Join a room**
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[tuiRoom enterRoomWithRoomId:12345 isOpenCamera:YES isOpenMicrophone:YES]
:::
::: Swift  Swift
import TUIRoom

tuiRoom.enterRoom(roomId: 12345, isOpenCamera: true, isOpenMicrophone: true)
```
:::
</dx-codeblock>

### Step 5. Implement room management (optional)
1. **The room owner calls [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37284) to close the room**.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[[TUIRoomCore shareInstance] destroyRoom:^(NSInteger code, NSString * _Nonnull message) {
            
}];
```
:::
::: Swift  Swift
import TUIRoom

TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
    guard let self = self else { return }
    self.navigationController?.popViewController(animated: true)
}
```
:::
</dx-codeblock>
2. **A user in the room calls [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37284) to leave the room**.
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[[TUIRoomCore shareInstance] leaveRoom:^(NSInteger code, NSString * _Nonnull message) {
            
}];
```
:::
::: Swift  Swift
import TUIRoom

TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
    guard let self = self else { return }
    self.navigationController?.popViewController(animated: true)
}
```
:::
</dx-codeblock>

### Step 6. Implement screen sharing (optional)
Call [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282) to implement screen sharing. For detailed directions, see [Real-Time Screen Sharing (iOS)](https://intl.cloud.tencent.com/document/product/647/37338).
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

 // Start screen sharing
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


## FAQs

### How do I install CocoaPods?

Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```

>? If you have any requirements or feedback, contact colleenyu@tencent.com.

