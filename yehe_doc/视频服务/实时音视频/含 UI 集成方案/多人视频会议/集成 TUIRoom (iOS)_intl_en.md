## Component Overview
`TUIRoom` is an open-source audio/video UI component. After integrating it into your project, you can add features such as screen sharing, beauty filter, and low-latency video call to your application simply by writing a few lines of code. It also supports the [Android](https://intl.cloud.tencent.com/document/product/647/37283), [Windows](https://intl.cloud.tencent.com/document/product/647/44071), and [macOS](https://intl.cloud.tencent.com/document/product/647/44071) platforms. Its basic features are as shown below:

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/0f07b6d570174f6fdc999eb67864f1f3.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9bdc61aa798c2c3926949d00a97302dc.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/37ef82ac97172967c037a523c5d09af3.png" width="250"></td>
</tr>
</tbody></table>


## Component Integration

### Step 1. Download and import the `TUIRoom` component
**To import the component through CocoaPods**, follow the steps below:
>? To implement the screen sharing feature, download `TXLiteAVSDK_ReplayKitExt.framework` [**here**](https://intl.cloud.tencent.com/document/product/647/34615), add it to your project, and create the "Broadcast Upload Extension" target. You can refer to the [demo project](https://github.com/tencentyun/TUIRoom/tree/main/iOS/Example/TXReplayKit_Screen) for implementation.

1. Go to [GitHub](https://github.com/tencentyun/TUIRoom), clone or download the code, and copy the `Resources`, `SDK`, and `Source` folders and the `TUIRoom.podspec` file in the `iOS` directory to your project.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
```swift
# TXLiteAVSDK
pod 'TXLiteAVSDK_TRTC'

# :path => "Points to the relative path of the directory of `TXAppBasic.podspec`"
pod 'TXAppBasic', :path => "../SDK/TXAppBasic/"

# :path => "Points to the relative path of the directory of `TCBeautyKit.podspec`"
pod 'TCBeautyKit', :path => "../SDK/TCBeautyKit/"

# :path => "Points to the relative path of the directory of `TUIRoom.podspec`"
pod 'TUIRoom', :path => "../", :subspecs => ["TRTC"]
```

>! The `Source` and `Resources` folders and the `TUIRoom.podspec` file must be in the same directory.
>- `TXAppBasic.podspec` is in the `TXAppBasic` folder.
>- `TCBeautyKit.podspec` is in the `TCBeautyKit` folder.

### Step 2. Configure permissions

To use the audio/video features, you need to grant mic and camera permissions. Add the two items below to `Info.plist` of your application. Their content is what users see in the mic and camera access pop-up windows.
- **Privacy - Microphone Usage Description**, plus a statement specifying why mic access is needed
- **Privacy - Camera Usage Description**, plus a statement specifying why camera access is needed

![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### Step 3. Create and log in to the component
1. Call `TUILogin` in `TUICore` to log in as shown below:
```swift
TUILogin.initWithSdkAppID(Int32("Your sdkAppID"))
TUILogin.login("Your userId", userSig: "Your userSig", succ: {
     debugPrint("login success")
}, fail: { code, errorDes in
     debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```

**Parameter description**
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**, which corresponds to `SDKAppID`. On the [Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online or calculate it on your own by referring to the [demo project](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Implement group audio/video interaction

1. **The room owner creates a group audio/video interaction room through [TUIRoomCore#createRoom](https://intl.cloud.tencent.com/document/product/647/37282)**.
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    } else {
    }
})
```
2. **Other users enter the audio/video room through [TUIRoomCore#enterRoom](https://intl.cloud.tencent.com/document/product/647/37282)**.
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("enter room success") 
   } else {
   }
})
```
3. **Implement room exit**. 
	- The **anchor** calls the [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37282) API to dismiss the room and IM group chat and exit the TRTC room. Room members receive the `onDestroyRoom` callback message that notifies them of group dismissal and exit the TRTC room.
	- A **member** calls the [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37282) API to leave the room and IM group chat and exit the TRTC room. Other room members receive the `onRemoteUserLeave` callback message that notifies them of the room exit by the member.
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
4. **Implement screen sharing through [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282)**.
	- Call `startScreenCapture` of `TUIRoomCore` to share the screen.
	- Other members in the room will receive the `onRemoteUserScreenVideoAvailable` event notification.
```swift
// Click the button to enable screen sharing
if #available(iOS 12.0, *) {
    // Start screen sharing
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

## FAQs
### How do I install CocoaPods?

Enter the following command in a terminal window (you need to install Ruby on your Mac first):
```
sudo gem install cocoapods
```

>? If you have any requirements or feedback, contact colleenyu@tencent.com.

