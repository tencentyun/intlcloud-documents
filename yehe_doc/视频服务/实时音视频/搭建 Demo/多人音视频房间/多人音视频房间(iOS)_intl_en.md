## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC’s video call features, including screen sharing, beauty filters, and low-latency video call.

## Solution Strengths
- `TUIRoom` integrates various capabilities such as ultra-low-latency audio/video calling, screen sharing, and beauty filters, covering the common features of group audio/video room.
- It can be further developed as needed to quickly implement custom UI and layout, helping you quickly launch your business.
- It encapsulates the basic TRTC and IM SDKs to implement basic logic control and provides APIs for you to call features easily.

## Connection Guide
To quickly implement the group audio/video room feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `Module` module in the app and customize your own UI.

[](id:ui_step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTUIRoom` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.

[](id:ui_step2)
### Step 2. Download the application source code
Click [TUIRoom](https://github.com/tencentyun/TUIRoom) to clone or download the source code.

[](id:ui_step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `Example/Debug/GenerateTestUserSig.swift`.
3. Set the following parameters in `GenerateTestUserSig.swift`:
<ul style="margin:0"><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png" width="750" height="395"/>

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui_step4)
### Step 4. Run the project
Open `Example/DemoApp.xcworkspace` with Xcode (11.0 or above) and click **Run**.

[](id:ui_step5)
### Step 5. Modify the project source code
The `Source` folder in the source code contains the UI folder, which contains UI code. The table below lists the folders and the UI views they represent. You can refer to it when making UI changes.

| Folder | Description |
|:-------:|:--------|
| TUIRoomEnter | Implementation code for the `TUIRoom` entry. The `TUIRoomEntranceViewController` class is a public CocoaPods class. |
| TUIRoomMain | Implementation code for the `TUIRoom` main UI. This is a private CocoaPods class. |
| TUIRoomMemberList | Implementation code for the participant list view. This is a private CocoaPods class. |
| TUIRoomSet | Implementation code for the settings UI. This is a private CocoaPods class. |

## Tryout
>! You need at least two devices to try out the application.
### Entry page
Select **Create Room** or **Enter Room**.

### Room creation page
When user A creates a room, the room ID will be automatically generated. User A can click **Create Room** to access the main UI.


### Room entry page
User B enters the ID of the room created by user A and click **Join** to access the main UI.



### Main UI (user A)
<img src="https://qcloudimg.tencent-cloud.cn/raw/eebab2b82db719000f0dc376070a25e7.png" width=300px>


### Mic-on list
It displays all users in the current room. If a user enables the camera and mic, you can watch the video image and hear the voice of the user.

### Top toolbar
It implements features such as mic switch, front/rear camera switch, room information display, and room exit.

### Bottom toolbar
It implements features such as local mic/camera control, beauty filter control, user list, and settings.

### Beauty filter
Beauty filters and special effects can be displayed on the screen during live streaming.


### Settings window
Audio and video parameters can be set, and **screen sharing** can be enabled.


### Exiting a room
- **Anchor**: dismisses the room, so all users need to exit the room.
- **Non-anchor**: leaves the room.

## Customizing UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIRoom) contains `UI` and `Presenter` folders. The `Presenter` folder contains the reusable open-source component `TUIRoomCore`. You can find the component's APIs in `TUIRoomCore.h` and use them to customize your own UI.
![#600px](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:ui_step1)
### Step 1. Integrate the SDK
The group audio/video room component `TUIRoom` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project:

- **Method 1: adding dependencies via CocoaPods**
```
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC'
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
- **Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.
<table>
<thead><tr><th>SDK</th><th>Download Page</th><th>Integration Guide</th></tr></thead>
<tbody><tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">Integration Documentation</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">Integration Documentation</a></td>
</tr>
</tbody></table>

[](id:model_step2)
### Step 2. Configure permission requests
Configure camera and mic permission requests by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model_step3)
### Step 3. Import the `TUIRoom` component
**To import the component through CocoaPods**, follow the steps below:
1. Copy the `Source`, `Resources`, `TCBeautyKit`, and `TXAppBasic` folders and the `TUIRoom.podspec` file from the demo directory to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
```swift
# Local dependency library
def local
  pod 'TXAppBasic', :path => "../../TXAppBasic/"
  pod 'TCBeautyKit', :path => "../../TCBeautyKit/"
  pod 'TXLiteAVSDK_TRTC',:path => "../../../SDK/"
end

def pod_local(type)
  loadLocalPod('TUIRoom', type)
end

def loadLocalPod(name, type)
    pod "#{name}/#{type}", :path => "../"
end

target 'DemoApp' do
  local
  pod_local('TRTC')
end
```

[](id:model_step4)
### Step 4. Create an instance and log in
1. Call `TUILogin` in `TUICore` to log in as shown below:
```swift
TUILogin.initWithSdkAppID(Int32(SDKAPPID))
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)
TUILogin.login(userID, userSig: userSig, succ: {
    debugPrint("login success") 
}, fail: { (code, errorDes) in
   debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```
2. After logging in, call `TUIRoomCore` to create a room.
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    } else {
    }
})
```
4. Enter the main UI after successful creation.
```swift
let vc = TUIRoomMainViewController(roomId: roomId, isVideoOn: openCameraSwitch.isOn, isAudioOn: openMicSwitch.isOn)
TUIRoomCore.shareInstance().setDelegate(vc)
navigationController?.pushViewController(vc, animated: true)
```
![#600px](https://qcloudimg.tencent-cloud.cn/raw/8c3391905188089fecd17e23477d34ea.png)

[](id:model_step5)
### Step 5. Members enter the room
1. Members call `TUILogin` in `TUICore` to log in as shown below:
```swift
TUILogin.initWithSdkAppID(Int32(SDKAPPID))
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)
TUILogin.login(userID, userSig: userSig, succ: {
    debugPrint("login success") 
}, fail: { (code, errorDes) in
   debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```
2. After logging in, call `TUIRoomCrre` to enter a room.
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
	    debugPrint("enter room success") 
	} else {
	}
})
```
4. Enter the main UI after successful room entry.
```swift
let vc = TUIRoomMainViewController(roomId: roomId, isVideoOn: openCameraSwitch.isOn, isAudioOn: openMicSwitch.isOn)
TUIRoomCore.shareInstance().setDelegate(vc)
navigationController?.pushViewController(vc, animated: true)
```
![#600px](https://qcloudimg.tencent-cloud.cn/raw/ffbda4de381ea198bf808de7d823ab59.png)

[](id:model_step6)
### Step 6. Enable screen sharing.
1. Call `startScreenCapture` of `TUIRoomCore` to share the screen.
2. Other members in the room will receive the `onRemoteUserScreenVideoAvailable` event notification.

```swift
// Click the button to enable screen sharing.
if #available(iOS 12.0, *) {
    // Start screen sharing.
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

[](id:step)
### Step 7. Exit a room
- The **anchor** calls the `destoryRoom` API to dismiss the room and IM group chat and exit the TRTC room. Room members receive the `onDestroyRoom` callback message that notifies them of group dismissal and exit the TRTC room.
- A **member** calls the `leaveRoom` API to leave the room and IM group chat and exit the TRTC room. Other room members receive the `onRemoteUserLeave` callback message that notifies them of the member exiting the room.

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
