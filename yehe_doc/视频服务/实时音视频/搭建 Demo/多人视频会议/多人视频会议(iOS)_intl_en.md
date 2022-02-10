## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC’s video conferencing features, including screen sharing, beauty filters, and low-latency conferencing.




To quickly enable the video conferencing feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `TUIMeeting` component and customize your own UI.

## Using the App’s UI
[](id:ui_step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestMeetingRoom` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.

[](id:ui_step2)
### Step 2. Download the application source code
Clone or download the [TUIMeeting](https://github.com/tencentyun/TUIMeeting) source code.

[](id:ui_step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `TUIMeeting/Debug/GenerateTestUserSig.swift`.
3. Set the following parameters in `GenerateTestUserSig.swift`:
<ul style="margin:0"><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui_step4)
### Step 4. Run the project
Open the source code project `TUIMeeting/TUIMeetingApp.xcworkspace` with Xcode (version 11.0 or above) and click **Run**.

[](id:ui_step5)
### Step 5. Modify the project source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
| TRTCMeetingNewViewController.swift | Implementation code for the conference creation view. This is a public CocoaPods class. |
| SegmentVC | Implementation code for the settings view |
| TRTCBroadcastExtensionLauncher.swift | Implementation code for the screen recording popup window. This is a private CocoaPods class. |
| TRTCMeetingMainViewController.swift | Implementation code for the room view. This is a private CocoaPods class. |
| TRTCMeetingMemberViewController.swift | Implementation code for the participant list view. This is a private CocoaPods class. |
| TRTCMeetingMoreViewController.swift | Implementation code for the settings view. This is a public CocoaPods class. |


## Tryout
>! You need at least two devices to try out the application.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Enter the conference ID and tap **Join**.
3. Type a subject for the conference and tap **Let’s go**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the ID of the conference created by user A and tap **Join**.

[](id:model)
## Customizing UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIMeeting) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCMeeting`. You can find the component's APIs in `TRTCMeeting.h` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


[](id:model.step1)
### Step 1. Integrate the SDKs
The video conferencing component `TUIMeeting` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

**Method 1: adding dependencies via CocoaPods**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC'
:::
</dx-codeblock>

>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).

**Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### Step 2. Configure permission requests
Configure camera and mic permission requests by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TUIMeeting` component
**To import the component through CocoaPods**, follow the steps below:
1. Copy the `Source`, `Resources`, `TCBeautyKit`, and `TXAppBasic` folders and the `TUIMeeting.podspec` file under the demo project directory to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
```swift
 pod 'TXAppBasic', :path => "TXAppBasic/"
 pod 'TCBeautyKit', :path => "TCBeautyKit/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUIMeeting', :path => "./", :subspecs => ["TRTC"] 
```

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCMeeting` component.
2. Call the `setDelegate` API to register event callbacks of the component.
3. Call the `login` API to log in to the component, and set the key parameters as described below.
<table> 
<tr>
<th>Parameter</th>
<th>Description</th>
</tr><tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr><tr>
<td>callback</td>
<td>Login callback. The code is `0` if login is successful.</td>
</tr>
</table>

```swift
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)

TRTCMeeting.sharedInstance().login(SDKAPPID, userId: userID, userSig: userSig, callback: { code, message in
    if code == 0 {
        // Logged in
    }
})
```

[](id:model.step5)
### Step 5. Create a conference as an anchor
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your username and profile photo as an anchor.
2. Call `setDelegate` and then `createMeeting` to create a conference room.
3. Call `startCameraPreview` to capture video and `startMicrophone` to capture audio.
4. To use beauty filters, you can add beauty filter buttons to the UI and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports face changing and stickers.

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```swift
// 1. Set your username and profile photo as an anchor
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. Create a room
trtcMeeting.createMeeting(roomId) { (code, msg) in
 if code == 0 {
   // Room created successfully
  let localPreviewView=getRenderView(userId: selfUserId)!
  TRTCMeeting.sharedInstance().startCameraPreview(true, view: localPreviewView)
  TRTCMeeting.sharedInstance().startMicrophone();
  
  // Use default beauty filter parameters
  beautyPannel.resetAndApplyValues()
  return;
 }
}
```

[](id:model.step6)
### Step 6. Join a conference as a participant
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your username and profile photo as a participant.
2. Call `enterMeeting`, passing in the conference room ID to enter the room.
3. Call `startCameraPreview` to capture video and `startMicrophone` to capture audio.
4. If another participant turns the camera on, you will receive the `onUserVideoAvailable` callback. Then, you can call `startRemoteView`, passing in the `userId` to play the participant’s video.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```swift
// 1. Set your username and profile photo as a participant
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. Implement the `enterMeeting` API
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("Failed to join the conference:" + msg!)
   }
}
```
```swift
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  // After receiving the callback, call `startRemoteView`, passing in the `userId` to play the participant’s stream
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
} else {
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
// Refresh the view
renderView?.refreshVideo(isVideoAvailable: available)
```

[](id:model.step7)
### Step 7. Share the screen
1. Call `startScreenCapture`, passing in encoding parameters and the floating window during screen recording to start screen sharing. For more information, please see [startScreenCapture:streamType:encParam:()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97).
2. Other participants in the room will receive the `onUserVideoAvailable` callback.

>!Screen sharing and camera capturing are mutually exclusive. Before enabling screen sharing, you need to call `stopCameraPreview` to disable camera capturing.

```swift
// 1. Click the button to enable screen sharing.
if #available(iOS 12.0, *) {
  // Camera capturing must be disabled before screen recording.
  self.setLocalVideo(isVideoAvailable: false)
  
  // Start screen sharing.
  let params = TRTCVideoEncParam()
  params.videoResolution = TRTCVideoResolution._1280_720
  params.videoFps = 10
  params.videoBitrate = 1800
  TRTCMeeting.sharedInstance().startScreenCapture(params)
  TRTCBroadcastExtensionLauncher.launch()
} else {
  self.view.makeToast("The system version is below 12.0. Please upgrade.")
}     
```

[](id:model.step8)
### Step 8. Implement text chat and muting notifications
- Call `sendRoomTextMsg` to send common text messages. All users in the room will receive the `onRecvRoomTextMsg` callback.
IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
```swift
// Sender: send text messages
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}

// Recipient: listen for text messages
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint("Received a message \(String(describing: message)) from: \(String(describing: userInfo.userId))")
}
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, such as muting notifications and notifications about other meeting controls.
```swift
// Sender: customize CMD to distinguish a muting notification
// E.g., use "CMD_MUTE_AUDIO" to indicate muting notifications
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}

// Recipient: listen for custom messages
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint("Received a muting notification: \(String(describing: message)) from: \(String(describing: userInfo.userId))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```
