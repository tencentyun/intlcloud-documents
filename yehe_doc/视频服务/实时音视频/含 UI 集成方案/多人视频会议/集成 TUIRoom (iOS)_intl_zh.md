## 组件介绍
TUIRoom 是一个开源的音视频 UI 组件，通过在项目中集成 TUIRoom 组件，您只需要编写几行代码就可以为您的 App 添加屏幕分享、美颜、低延时视频通话等。TUIRoom 同时支持 [Android](https://intl.cloud.tencent.com/document/product/647/37283)、[Windows](https://intl.cloud.tencent.com/document/product/647/44071)，[Mac](https://intl.cloud.tencent.com/document/product/647/44071) 等平台，基本功能如下图所示：

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/0f07b6d570174f6fdc999eb67864f1f3.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9bdc61aa798c2c3926949d00a97302dc.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/37ef82ac97172967c037a523c5d09af3.png" width="250"></td>
</tr>
</tbody></table>


## 组件集成

### 步骤一：下载并导入 TUIRoom 组件
您可通过 **cocoapods 导入组件**，具体步骤如下：
>? 如果需要屏幕分享功能，您可以通过 [**官网链接**](https://intl.cloud.tencent.com/document/product/647/34615) 去下载TXLiteAVSDK_ReplayKitExt.framework，然后加入到自己工程中，在 target 中新建"Broadcast Upload Extension"，实现可以参考 [示例工程](https://github.com/tencentyun/TUIRoom/tree/main/iOS/Example/TXReplayKit_Screen)。

1. 单击进入 [Github](https://github.com/tencentyun/TUIRoom) ，选择克隆/下载代码，然后拷贝 iOS下的`Resources`、`SDK`、`Source`文件夹 和`TUIRoom.podspec`文件到您的工程。
2. 在您的 `Podfile` 文件中添加以下依赖。之后执行 `pod install` 命令，完成导入。
```swift
# TXLiteAVSDK
pod 'TXLiteAVSDK_TRTC'

# :path => "指向TXAppBasic.podspec所在目录的相对路径"
pod 'TXAppBasic', :path => "../SDK/TXAppBasic/"

# :path => "指向TCBeautyKit.podspec所在目录的相对路径"
pod 'TCBeautyKit', :path => "../SDK/TCBeautyKit/"

# :path => "指向TUIRoom.podspec所在目录的相对路径"
pod 'TUIRoom', :path => "../", :subspecs => ["TRTC"]
```

>!  `Source`、`Resources`文件夹 和 `TUIRoom.podspec` 文件必需在同一目录下。
>-  TXAppBasic.podspec 在 TXAppBasic 文件夹下。
>-  TCBeautyKit.podspec 在 TCBeautyKit 文件夹下。

### 步骤二：配置权限

使用音视频功能，需要授权麦克风和摄像头的使用权限。在 App 的 Info.plist 中添加以下两项，分别对应麦克风和摄像头在系统弹出授权对话框时的提示信息。
- **Privacy - Microphone Usage Description**，并填入麦克风使用目的提示语。
- **Privacy - Camera Usage Description**，并填入摄像头使用目的提示语。

![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### 步骤三：创建并登录组件
1.  调用 TUICore 中的 TUILogin 进行登录，请参考如下示例：
```swift
TUILogin.initWithSdkAppID(Int32("您的sdkAppID"))
TUILogin.login("您的userId", userSig: "您的userSig", succ: {
     debugPrint("login success")
}, fail: { code, errorDes in
     debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```

**参数说明**
- **SDKAppID**：**TRTC 应用 ID**，如果您未开通腾讯云 TRTC 服务，可进入 [腾讯云实时音视频控制台](https://console.cloud.tencent.com/trtc/app)，创建一个新的 TRTC 应用后，单击**应用信息**，SDKAppID 信息如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC 应用密钥** 和 SDKAppId 对应，进入 [TRTC 应用管理](https://console.cloud.tencent.com/trtc/app) 后，SecretKey 信息如上图所示。
- **userId**：当前用户的 ID，字符串类型，只允许包含英文字母（a-z 和 A-Z）、数字（0-9）、连词符（-）和下划线（\_）。建议结合业务实际账号体系自行设置。
- **userSig**：根据 SDKAppId、userId，Secretkey 等信息计算得到的安全保护签名，您可以单击 [这里](https://console.cloud.tencent.com/trtc/usersigtool) 直接在线生成一个调试的 UserSig，也可以参照我们的 [示例工程](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42) 自行计算，更多信息见 [如何计算及使用 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。

### 步骤四：实现多人音视频互动

1. **实现房主创建多人音视频互动房间  [TUIRoomCore#createRoom](https://intl.cloud.tencent.com/document/product/647/37282)**。
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    } else {
    }
})
```
2. **实现其他成员加入音视频房间  [TUIRoomCore#enterRoom](https://intl.cloud.tencent.com/document/product/647/37282)**。
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("enter room success") 
   } else {
   }
})
```
3. **实现离开房间** 
	- **主持人**调用  [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37282) 接口解散房间，解散 IM 群聊，退出 TRTC 房间，成员端会收到 onDestroyRoom 回调消息，通知群解散，退出 TRTC 房间。
	- **成员**调用  [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37282) 接口解散房间，退出 IM 群聊，退出 TRTC 房间，其他成员端会收到 onRemoteUserLeave 回调，通知有成员离开房间。
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
4. **实现屏幕分享  [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282)**。
	- 调用 TUIRoomCore 的 `startScreenCapture` 实现分享。
	- 房间中其他成员会收到 `onRemoteUserScreenVideoAvailable` 的事件通知。
```swift
// 按钮单击实现屏幕分享
if #available(iOS 12.0, *) {
    // 屏幕分享
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

## 常见问题
### CocoaPods 如何安装？

在终端窗口中输入如下命令（需要提前在 Mac 中安装 Ruby 环境）：
```
sudo gem install cocoapods
```

>? 如果有任何需要或者反馈，您可以联系：colleenyu@tencent.com。

