## Effect Demo


To quickly implement the audio call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCAudioCall` component and implement custom UI.

<span id="ui"> </span>

## Reusing Demo UI

<span id="ui.step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestAudioCall`, and click **Create Application**.

> This feature uses two basic PaaS services of Tencent Cloud, namely, [Tencent Real-Time Communication (TRTC)](https://intl.cloud.tencent.com/document/product/647/35078) and [Instant Messaging (IM)](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to go to the GitHub website (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**) to download the SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage application.

>The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo
Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` source code project and click **Run** to debug the demo.

### Step 5. Modify the demo source code
The `TRTCAudioCallDemo` source code folder contains the `ui` and `model` subfolders, and the former stores UI code:

| File or Folder | Description |
|:-------:|:--------|
| AudioCallViewController.swift | It is used to show the main interface for audio calls, where calls are answered and rejected. | 
| AudioSelectContactViewController.swift | It is used to show the interface for selecting contacts. |
| AudioCallMainViewController.swift | It is used to show the interface of the contacts with whom you have had a call. Currently, you can only initiate calls. |
| AudioCallViewController+Data.swift | It is used to render images and design the layout during a call. | 

<span id="model"> </span>
## Customizing UI
The `TRTCAudioCallDemo` source code folder contains the `ui` and `model` subfolders. The latter contains the `TRTCAudioCall` component, which is a reusable open source component already implemented by Tencent Cloud. You can view the component’s API functions in the `ITRTCAudioCallInterface.swift` file.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)
You can customize the UI by reusing the code and the open source `TRTCAudioCall` component in the `model` folder and implementing the code in the `ui` folder yourself.

<span id="model.step1"> </span>
### Step 1. Integrate the SDK
The `TRTCAudioCall` component depends on the TRTC SDK and IM SDK which you can integrate into the project by following the steps below.
- **Method 1: CocoaPods library dependencies**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>You can get the latest version numbers of both SDKs on the GitHub home pages of [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
>
- **Method 2: local dependencies**
If it takes long for your development environment to access the CocoaPods library, you can download the ZIP file and manually integrate it into your project as instructed in the Integration Documentation.
<table>
<tr>
<th>SDK</th>
<th>Download Address</th>
<th>Integration Guide</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration Documentation</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration Documentation</a></td>
</tr>
</table>

<span id="model.step2"> </span>
### Step 2. Configure permissions
Add "Privacy - Microphone Usage Description" to the `info.plist` file to apply for mic permissions.

<span id="model.step3"> </span>
### Step 3. Import the TRTCAudioCall component

Copy all files from the following directory into your project:
```
iOS/trtcScenesDemo/trtcScenes/TRTCAudioCallDemo/model
```

<span id="model.step4"> </span>
### Step 4. Initialize and log in to the component
1. Invoke `setup()` to initialize the component.
2. Invoke `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` and specify the key parameters as shown below to log in to the component:
 <table>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr>
<tr>
<td>user</td>
<td>The ID of the current user. It is a string, which contains only letters, digits, hyphens, and underscores.</td>
</tr>
<tr>
<td>userSig</td>
<td>A security signature designed by Tencent Cloud. For details about how to calculate it, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Generate UserSig</a>.</td>
</tr>
</table>
<pre>
// Initialize
TRTCAudioCall.shared.setup()
TRTCAudioCall.shared.login(sdkAppid, A, password, success, failed)
</pre>

<span id="model.step5"> </span>
### Step 5. Implement one-to-one audio calls
1. The requester invokes the `call()` method of `TRTCAudioCall` to initiate a audio call request.
2. The receiver receives the `onInvited()` event, and invokes the `accept()` method to answer the call or the `reject()` method to reject it.
3 The requester receives the `onUserEnter()` callback which indicates the receiver has answered the call.

```
// 1. Initialize
TRTCAudioCall.shared.setup()

// 2. Listen on callback
TRTCAudioCall.shared.delegate = self

// Answer/reject the call
// At this point, if B also logs in to the IM system, it will receive the onInvited(A, null, false) callback
// Invoke TRTCAudioCall.shared.accept to answer and TRTCAudioCall.shared.reject to reject
func onInvited(sponsor: String, userIds: [String], isFromGroup: Bool) {
	TRTCAudioCall.shared.accept()
}

// 3. Log in to the component, and you can invoke the component's other functions after successful login
TRTCAudioCall.shared.login(sdkAppID: sdkAppid, user: A, userSig: Sig, success: {
    // Call B
    TRTCAudioCall.shared.call(B)
}) { (code, error) in
            
}

// Hang up
TRTCAudioCall.shared.hangup()
// Terminate the instance
TRTCAudioCall.shared.destroy()
```

<span id="model.step6"> </span>
### Step 6. Implement multi-person audio calls
1. Requester: to start a multi-person audio call, the requester invokes the `groupCall()` function of `TRTCAudioCall`, and specifies the `userIdList` (user list, required) and `groupId` (group ID, optional) parameters.
2. Receiver: the receiver receives the call request via the `onInvited()` callback.
3. Receiver: after the callback is received, the receiver invokes the `accept()` method to answer the call or the `reject()` method to reject it.
4. If there is no response for a certain time (30s by default), the receiver will receive the `onCallingTimeOut()` callback and the requester the `onNoResp(String userId)` callback. When multiple receivers do not respond, the requester invokes `hangup()` and each receiver receives the `onCallingCancel()` callback.
5. Invoke the `hangup()` method to exit the multi-person call.
6. If a user joins or exits the call, other users will receive the `onUserEnter()` or `onUserLeave()` callbacks respectively.

>The `groupID` parameter in the `groupCall()` API refers to the group ID in IM SDK. If this parameter is used, the call request messages are broadcast through the group messaging system, which is easy and reliable; if it is not used, the `TRTCAudioCall` component will send the messages one by one.

```
// The preceding code is ignored here …
// Specify the list of users you want to call
var callList: [String] = []
callList.append("b")
callList.append("c")
callList.append("d")
// If you are not initiating a call in an IM group, the value of groupId can be an empty string
TRTCAudioCall.shared.groupCall(userIDs: callList, groupID: "#groupId#")
```

<span id="offline"> </span>
### Step 7. Implement receiving a call offline
>If your business focuses on the scenarios where there is no need to receive a call offline, such as online customer service, following [Step 1](#model.step1) through [Step 6](#model.step6) is enough; but if your business focuses on social interaction scenarios, we recommend that you implement the feature.

The IM SDK supports offline push notification, which you need to configure to use.

1. For details on how to apply for an Apple push notification service certificate, please see [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).
2. For details on how to configure offline push in the backend and client, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/zh/document/product/1047/34347).
3. Modify the value of `param.busiId` in the `login` function to the certificate ID.

<span id="api"> </span>
## Component APIs
The API functions of the `TRTCAudioCall` component are as follows:

| API Function | Description |
|---------|---------|
| setup | Performs the required initialization before all other features can be used. | 
| destroy | Terminates an instance. |
| setDelegate | Sets the callback proxy of `TRTCAudioCallDelegate`, which provides status notification for users. |
| login | Logs in to IM. All other features can be used only after login. |
| logout | Logs out of IM. Calls cannot be made after logout. |
| call | Invites user to C2C call. The invited user will receive the `onInvited` callback. |
| groupCall | Invites users to IM group call. The invited users will receive the `onInvited` callback. |
| accept | Answers call as callee. |
| reject | Rejects call as callee. |
| hangup | Hangs up the call. |
| setMicMute | Whether to mute the mic. |
| setHandsFree | Whether to enable the hands-free mode. |
