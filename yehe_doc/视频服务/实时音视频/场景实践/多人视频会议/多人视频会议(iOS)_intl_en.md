## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s video conferencing features, including screen sharing, beauty filters, and low-latency conferencing.

To quickly enable the video conferencing feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCMeeting` component and customize your own UI.

## Using the Demo UI
[](id:ui_step1)
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestMeetingRoom`, and click **Create**.

>?The video conferencing feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.

[](id:ui_step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui_step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set parameters in `GenerateTestUserSig.h` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo.
Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging.

### Step 5. Modify the demo source code.
The `trtcmeetingdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Use |
|:-------:|:--------|
| SegmentVC | Implementation code for the settings view |
| TRTCBroadcastExtensionLauncher.swift | Implementation code for the screen recording popup window |
| TRTCMeetingNewViewController | Implementation code for the meeting creation view |
| TRTCMeetingMainViewController | Implementation code for the room view |
| TRTCMeetingMemberViewController | Implementation code for the member list view |
| TRTCMeetingMoreViewController | Implementation code for the settings view |


[](id:model)
## Implementing A Custom UI

The `trtcmeetingdemo` folder in the [source code] contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCMeeting`. You can find the component’s API functions in `TRTCMeeting.h` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


[](id:model.step1)
### Step 1. Integrate the SDKs.
The video conferencing component `TRTCMeeting` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

**Method 1: adding dependencies via CocoaPods**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).

**Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP packages of the SDKs and manually integrate them into your project as instructed in the documents below.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### Step 2. Configure permission requests.
Configure camera and mic permission requests by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TRTCMeeting` component.
Copy all the files in `iOS/LiteAVDemo/TXLiteAVDemo/TRTCMeetingDemo/model` to your project.

<span id="model.step4"></span>
### Step 4. Create a component instance and log in.
1. Call the `sharedInstance` API to create an instance of the `TRTCMeeting` component.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
<table> 
<tr>
<th>Parameter</th>
<th>Note</th>
</tr><tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr><tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>

```swift
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)

TRTCMeeting.sharedInstance().login(SDKAPPID, userId: userID, userSig: userSig, callback: { code, message in
    if code == 0 {
        //Login successful
    }
})
```

[](id:model.step5)
### Step 5. Create a meeting as a host.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as a host.
2. Call `setDelegate` to create a meeting room via `createMeeting`.
3. Call `startCameraPreview` to capture video image and `startMicrophone` to capture sound.
4. To use beauty filters, you can add beauty filter buttons to the UI and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports face changing and stickers.

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```
// 1. The host sets his or her nickname and profile photo.
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. The host creates a room
trtcMeeting.createMeeting(roomId) { (code, msg) in
 if code == 0 {
   //Room created
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
### Step 6. Join a meeting as an attendee.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as an attendee.
2. Call `enterMeeting` and pass in the meeting room ID to enter the room.
3. Call `startCameraPreview` to capture video image and `startMicrophone` to capture sound.
4. If another attendee turns on the camera, you will receive the `onUserVideoAvailable` notification, and can call `startRemoteView` and pass in the `userId` to play the attendee’s video.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```
// 1. The attendee sets his or her nickname and profile photo
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. The `enterMeeting` function is implemented.
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("Failed to join the meeting:" + msg!)
   }
}
```

```
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  // The attendee receives a callback, calls `startRemoteView` and passes in the `userId` to start playback.
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
} else {
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
// The page is refreshed.
renderView?.refreshVideo(isVideoAvailable: available)
```

[](id:model.step7)
### Step 7. Share the screen.
1. Call `startScreenCapture`, pass in the encoding parameters and floating window to start screen sharing. For more information, see [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97).
2. Other attendees in the room will receive the `onUserVideoAvailable` event notification.

>!Screen sharing and camera capturing are mutually exclusive. Before enabling screen sharing, you need to call `stopCameraPreview` to disable camera capturing.

```
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
### Step 8. Implement text chat and muting notifications.
- Call `sendRoomTextMsg` to send text messages, and all hosts and attendees in the room will receive the `onRecvRoomTextMsg` callback.
IM has its default content moderation rules. Text messages that contain blocked terms will not be forwarded by the cloud.
```
// Sender: send text messages
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}
// Recipient: listen for text messages
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint("Received a message \(String(describing: message)) from: \(String(describing: userInfo.userId))")
}
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages, and all hosts and attendees in the room will receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, such as muting notifications and notifications about other meeting controls.
```
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

