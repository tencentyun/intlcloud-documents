## Reusing Demo UI

<span id="ui.step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestVideoCall`, and click **Create Application**.

> This feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding card, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**), and download the relevant SDK and supporting demo source code.
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TRTCScenesDemo/debug/GenerateTestUserSig.h` file.
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  <ul><li>SDKAPPID: it is a placeholder by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is a placeholder by default. Please replace it with your real key information.</li></ul> 
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-Side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo
Use Xcode (v11.0 or above) to open the `trtcScenesDemo` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>
### Step 5. Modify the demo source code
The source code folder `trtcvideocalldemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

| File or Folder | Feature Description |
|:-------:|:--------|
| VideoCallViewController.swift | Video call homepage where calls can be answered or rejected. |
| VideoSelectContactViewController.swift| UI for selecting contacts. |
| VideoCallMainViewController.swift| UI for displaying historical contacts. |
| VideoCallViewController+Data.swift | Video image rendering and layout logic. |

<span id="model"> </span>
## Implementing Custom UI
The source code folder `TRTCVideoCallDemo` contains two subfolders: `ui` and `model`. The `model` folder contains the implemented reusable open-source component `TRTCVideoCall`. You can find the API functions provided by this component in the `ITRTCVideoCallInterface.swift` file.

You can use the open-source component `TRTCVideoCall` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"> </span>
### Step 1. Integrate SDKs
The video call component `TRTCVideoCall` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:
- **Method 1. Implement dependency through the CocoaPods repository**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.

- **Method 2. Implement dependency through local files**
If the access to the CocoaPods repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.
<table>
<tr>
<th>SDK</th>
<th>Download Page</th>
<th>Integration Guide</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration document</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
</tr>
</table>

<span id="model.step2"> </span>
### Step 2. Configure permissions
Apply for the camera and mic permissions by adding `Privacy - Camera Usage Description` and `Privacy - Microphone Usage Description` in the `info.plist` file.

<span id="model.step3"> </span>
### Step 3. Import the TRTCVideoCall component

Copy all files in the following directory to your project:
```
iOS/trtcScenesDemo/trtcScenes/TRTCVideoCallDemo/model 
```

<span id="model.step4"> </span>
### Step 4. Initialize and log in to the component
1. Call `setup()` to initialize the component.
2. Call `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` to log in to the component. Enter key parameters as shown below:
 <table>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppID</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr>
<tr>
<td>user</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For the calculation method, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr>
</table>
<pre>
// Initialize
TRTCVideoCall.shared.setup()
TRTCVideoCall.shared.login(sdkAppid, A, password, success, failed)
</pre>


<span id="model.step5"> </span>
### Step 5. Make an one-to-one video call
1. Caller: the caller can call the `call()` method in `TRTCVideoCall` to initiate a video call request.
2. Callee: if already logged in, the callee will receive the `onInvited()` callback. If you want the callee to receive call requests even when logged out, please see [Offline Answering](#model.offline).
3. Callee: to answer the call, the callee can call the `accept()` function and the `openCamera()` function to enable the local camera. The callee can also call `reject()` to reject the call.
4. After the audio/video channel between the caller and callee is established, they will both receive the `onUserVideoAvailable()` callback, which indicates that they have received each other's image. At this point, they can call `startRemoteView()` to display the remote video image, and the remote audio will be played back by default.

```
// 1. Initialize
TRTCVideoCall.shared.setup()

// 2. Listen on the callback
TRTCVideoCall.shared.delegate = self

// Answer/Reject the call
// At this point, if user B also logs in to the IM system, user B will receive the `onInvited(A, null, false)` callback
// `TRTCVideoCall.shared.accept`/`TRTCVideoCall.shared.reject` can be called to answer/reject the call
func onInvited(sponsor: String, userIds: [String], isFromGroup: Bool) {
	TRTCVideoCall.shared.accept()
}

// View each other's image
// As user A enables the camera, user B will receive the `onUserVideoAvailable(A, true)` callback after answering the call
func onUserVideoAvailable(uid: String, available: Bool) {
	if available {
		let renderView = UIView()
		TRTCVideoCall.shared.startRemoteView(userId: uid, view: renderView)// They can see each other's image
	} else {
		TRTCVideoCall.shared.stopRemoteView(userId: uid)
	}
}

// 3. Log in to the component. Only after successful login can functions of other features of the component be called
TRTCVideoCall.shared.login(sdkAppID: sdkAppid, user: A, userSig: Sig, success: {
    // Call user B
    TRTCVideoCall.shared.call(B)
	// Enable local camera
	TRTCVideoCall.shared.openCamera(frontCamera: true, view: localPreView)  
}) { (code, error) in
            
}

// Hang up
TRTCVideoCall.shared.hangup()
// Terminate the instance
TRTCVideoCall.shared.destroy()
```

<span id="model.step6"> </span>
### Step 6. Make a group video call
1. Caller: to initiate a group video call, the caller needs to call the `groupCall()` function in `TRTCVideoCall` and pass in the required user list (`userIdList`) and optional IM group ID (`groupId`).
2. Callee: a callee can receive the request through the `onInvited()` callback.
3. Callee: a callee can call the `accept()` method to answer the call or call the `reject()` method to reject the call after receiving the callback.
4. If a callee does not respond to the call for a certain period of time (30 seconds by default), this callee will receive the `onCallingTimeOut()` callback, and the caller will receive the `onNoResp(String userId)` callback. If multiple callees do not answer the call, the caller can call `hangup()`, and each callee will receive the `onCallingCancel()` callback.
5. A user can call the`hangup()` method to leave the current group call.
6. If there is a user joining or leaving the call, other users will receive the `onUserEnter()` or `onUserLeave()` callback.

>The `groupID` parameter in the `groupCall()` API is the group ID in the IM SDK. If this parameter is set, the call request will be broadcast through the group message system, which is simple and reliable. If this parameter is left empty, the `TRTCVideoCall` component will send the message to users one by one.

```
// Omitted content...
// Splice the list of users to be called
var callList: [String] = []
callList.append("b")
callList.append("c")
callList.append("d")
// If the call is not initiated in an IM group, an empty string can be passed in for `groupId`
TRTCVideoCall.shared.groupCall(userIDs: callList, groupID: "#groupId#")

// Enable local camera
TRTCVideoCall.shared.openCamera(frontCamera: true, view: localPreView)  
```

<span id="offline"> </span>
### Step 7. Answer a call offline
>If your business is online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, you are recommended to implement offline answering.

The IM SDK supports offline push, but you need to complete the corresponding settings to meet its availability standard.

1. Apply for an Apple push certificate. For detailed directions, please see [Applying for Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Configure offline push on the backend and client. For detailed directions, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).
3. Set `param.busiId` in the `login` function to the corresponding certificate ID.

<span id="api"> </span>
## Component APIs
Below is the list of `TRTCVideoCall` component APIs:

| API Function | Feature |
|---------|---------|
| setup | Performs the required initialization before all other features can be used |
| destroy | Terminates instance |
| setDelegate | Sets the `TRTCVideoCallDelegate` callback, through which users can get status notifications |
| login | Logs in to IM. All other features can be used only after login |
| logout | Logs out of IM. Calls cannot be made after logout |
| call | Invites user to C2C call. The invited user will receive the `onInvited` callback |
| groupCall | Invites users to IM group call. The invited users will receive the `onInvited` callback |
| accept | Answers call as callee |
| reject | Rejects call as callee |
| hangup | Ends call |
| startRemoteView | Renders the camera data of remote user in the specified `UIView` |
| stopRemoteView | Stops rendering the camera data of remote user |
| openCamera | Enables camera and renders data in the specified `TXCloudVideoView` |
| closeCamera | Disables camera |
| switchCamera | Switches between front and rear cameras |
| setMicMute | Specifies whether to mute the mic |
| setHandsFree | Specifies whether to enable the hands-free mode |
