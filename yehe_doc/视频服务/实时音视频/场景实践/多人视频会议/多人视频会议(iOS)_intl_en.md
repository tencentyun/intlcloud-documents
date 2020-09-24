## Effect Demo
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo to try out the video conferencing capabilities of TRTC, such as screen sharing, beauty filters, and low-latency conferencing.

To quickly implement the video conferencing feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCMeeting` component and implement custom UI.

## Reusing Demo UI

### Step 1. Create an application

1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestMeetingRoom`, and click **Create Application**.

>? This feature uses two basic PaaS services, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.IM is a value-added service at the prices as detailed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**), and download the relevant SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-Side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo
Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging the demo.

### Step 5. Modify the demo source code
The ``trtcmeetingdemo`` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The following table lists the files or folders and the corresponding UIs for easy adjustment:

| File or Folder | Feature Description |
|:-------:|:--------|
| SegmentVC | Implementation code for settings UI. |
| TRTCBroadcastExtensionLauncher.swift | Implementation code for screen recording popup UI. |
| TRTCMeetingNewViewController | Implementation code for video meeting creation UI. |
| TRTCMeetingMainViewController | Implementation code for video room UI. |
| TRTCMeetingMemberViewController | Implementation code for member list UI. |
| TRTCMeetingMoreViewController | Implementation code for settings UI. |


<span id="model"> </span>
## Implementing Custom UI

The `trtcmeetingdemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCMeetingDemo) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCMeeting`. You can find the API functions provided by this component in the `TRTCMeeting.h` file and use the corresponding API to implement your own custom UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


<span id="model.step1"> </span>
### Step 1. Integrate SDKs
The video conferencing component `TRTCMeeting` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

**Method 1. Implement dependency through the CocoaPods repository**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.

**Method 2. Implement dependency through local files**
If the access to the CocoaPods repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### Step 2. Configure permissions
Apply for the camera and mic permissions by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in the `info.plist` file.

<span id="model.step3"> </span>
### Step 3. Import the TRTCMeeting component
Copy all files in the `iOS/LiteAVDemo/TXLiteAVDemo/TRTCMeetingDemo/model` directory to your project.

<span id="model.step4"> </span>
### Step 4. Create and log in to the component
1. Call the `sharedInstance` API to create an instance object of the `TRTCMeeting` component.
2. Call the `setDelegate` function to register the event notification of the component.
3. Call the `login` function to log in to the component. Enter key parameters as shown below:
<table> 
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The `code` will be 0 if login is successful.</td>
</tr>
</table>

```swift
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)

TRTCMeeting.sharedInstance().login(SDKAPPID, userId: userID, userSig: userSig, callback: { code, message in
    if code == 0 {
        // Logged in successfully
    }
})
```

<span id="model.step5"> </span>
### Step 5. Create a meeting
1. The chairperson can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The chairperson can call `setDelegate` to make an event call of `createMeeting` to create a meeting room.
3. The chairperson can call `startCameraPreview` to capture video image or call `startMicrophone` to capture sound.
4. If the chairperson requires beauty filters, the beauty filter adjusting buttons can be configured on the UI for setting beauty filters through `getBeautyManager`.
>Face changing and sticker pendant features are not supported for SDKs in editions other than the Enterprise Edition.
>

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```swift
// 1. The anchor sets the nickname and profile photo
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. The anchor creates a room
trtcMeeting.createMeeting(roomId) { (code, msg) in
 if code == 0 {
   // Created room successfully
  let localPreviewView=getRenderView(userId: selfUserId)!
  TRTCMeeting.sharedInstance().startCameraPreview(true, view: localPreviewView)
  TRTCMeeting.sharedInstance().startMicrophone();
  
  // Use default beauty filter parameters
  beautyPannel.resetAndApplyValues()
  return;
 }
}
```

<span id="model.step6"> </span>
### Step 6. The participant joins the meeting
1. The participant can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The participant can call `enterMeeting` and pass in the meeting room number to enter the meeting room.
3. The participant can call `startCameraPreview` to capture video image and call `startMicrophone` to capture sound.
4. If another participant enables the camera, the participant will receive the `onUserVideoAvailable` event. At this time, the participant can call `startRemoteView` and pass in the `userId` to start playback.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```swift
// 1. The participant sets the nickname and profile photo
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. Implement the `enterMeeting` function
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("Failed to join the meeting:" + msg!)
   }
}
```

```swift
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  // The callback is received. Call `startRemoteView` and pass in `userId` to start playback
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
} else {
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
// Refresh the current page
renderView?.refreshVideo(isVideoAvailable: available)
```

<span id="model.step7"> </span>
### Step 7. Share the screen
1. Call `startScreenCapture`, pass in the encoding parameters and the floating window in the screen sharing process to implement the screen sharing feature. For more information, please see [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97).
2. Other participants in the meeting will receive the `onUserVideoAvailable` event notification.

>!Screen sharing and camera capture are mutually exclusive. If you need to enable screen sharing, please call `stopCameraPreview` to disable camera capture first.

```swift
// 1. Click the button to implement screen sharing
if #available(iOS 12.0, *) {
  // Camera capture must be disabled before screen recording
  self.setLocalVideo(isVideoAvailable: false)
  
  // Share the screen
  let params = TRTCVideoEncParam()
  params.videoResolution = TRTCVideoResolution._1280_720
  params.videoFps = 10
  params.videoBitrate = 1800
  TRTCMeeting.sharedInstance().startScreenCapture(params)
  TRTCBroadcastExtensionLauncher.launch()
} else {
  self.view.makeToast("The system version is below 12.0. Please upgrade the system")
}     
```

<span id="model.step8"> </span>
### Step 8. Implement text chat and messaging mute
- `sendRoomTextMsg` can be used to send general text messages, and all anchors and viewers in the room can receive the `onRecvRoomTextMsg` callback.
The backend of IM has default sensitive word filtering rules, and text messages that are considered to contain any sensitive words will not be forwarded by the cloud.

```swift
// Sender: sends text messages
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}

// Receiver: listens on text messages
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint("A message from :\(String(describing: userInfo.userId)) is received\(String(describing: message))")
}
```

- `sendRoomCustomMsg` can be used to send custom (signaling) messages, and all chairpersons and participants in the room can receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, such as meeting controls like mute.

```swift
// Sender: mute notifications can be identified by custom `CMD`
// eg:"CMD_MUTE_AUDIO" indicates a mute notification
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}

// Receiver: listens on custom messages
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint("A mute notification from :\(String(describing: userInfo.userId)) is received:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```

