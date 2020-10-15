## Effect Demo

To quickly implement the video/audio call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCCalling` component and implement your custom UI.

>! We previously provided the `TRTCAudioCall` component, which has been moved to the [component repository](https://github.com/tencentyun/LiteAVClassic). The `TRTCCalling` component uses IM signaling APIs and is not compatible with the old component.

<span id="ui"> </span>

## Reusing the Demo UI

<span id="ui.step1"></span>

### Step 1: Create an application

1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestVideoCall`, and click **Create Application**.

>! This feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.IM is a value-added service at the prices as detailed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<span id="ui.step2"></span>

### Step 2: Download the SDK and demo source code

1. Hover over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to be redirected to GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**), and download the relevant SDK and supporting demo source code.
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC console and click **Downloaded and Next**. Then, you will be able to see the `SDKAppID` and key information.

<span id="ui.step3"></span>

### Step 3: Configure the demo project files

1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
	- SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.
	- SECRETKEY: it is an empty string by default. Please replace it with your real key information.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. Return to the TRTC console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>!
>- The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166#Server).

<span id="ui.step4"></span>

### Step 4: Run the demo

Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>

### Step 5: Modify the demo source code

The source code folder `TRTCCallingDemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

| File or Folder | Feature Description |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  | Video call homepage where calls can be answered or rejected. |
|  TRTCCallingAudioViewController.swift  | Audio call homepage where calls can be answered or rejected. |
| TRTCCallingContactViewController.swift | UI for searching for contacts. |


<span id="model"> </span>

## Implementing Your Custom UI

The [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCCallingDemo) folder `TRTCCallingDemo` contains two subfolders: `ui` and `model`. The `model` folder contains the implemented reusable open-source component `TRTCCalling`. You can find the API functions provided by this component in the `TRTCCalling.h` file.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

You can use the open-source component `TRTCCalling` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"> </span>

### Step 1: Integrate the SDKs

The call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project by following the steps below:

- **Method 1: Implement dependency through the CocoaPods repository**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.
- **Method 2: Implement dependency through the local files**
  If access to the CocoaPods repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.
<table>
<tr><th>SDK</th><th>Download Page</th><th>Integration Guide</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration documentation</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration documentation</a></td>
</tr></table>

<span id="model.step2"> </span>

### Step 2: Configure the permissions

Apply for the camera and mic permissions by adding `Privacy - Camera Usage Description` and `Privacy - Microphone Usage Description` in the `info.plist` file.

<span id="model.step3"> </span>

### Step 3: Import the TRTCCalling component

Copy all files in the following directory to your project:
```
iOS/TRTCSceneDemo/TXLiteAVDemo/TRTCCallingDemo/model 
```

<span id="model.step4"> </span>

### Step 4: Initialize and log in to the component

1. Set the push information.
```
[TRTCCalling shareInstance].imBusinessID = your business ID;
[TRTCCalling shareInstance].deviceToken =  deviceToken;
```
2. Call `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` to log in to the component. Enter the key parameters as shown below:
 <table>
<tr><th>Parameter Name</th><th>Description</th></tr>
<tr>
<td>sdkAppID</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>user</td>
<td>ID of the current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></table>
<pre>
// Login
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Audio call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Audio call login failed.");
}];
</pre>

<span id="model.step5"> </span>
### Step 5: Make a one-to-one call

1. The caller can call the `call(userId, callType)` method in `TRTCCalling` and pass in the user ID as `userId` and `CallType_Audio` as `callType` to initiate an audio call request.
2. The receiver can call the `accept` method to answer the call or call the `reject` method to reject the call after receiving the `onInvited` event.
3. The receiver receives the `onUserEnter` callback, which indicates that the receiver has joined the call.

```Objective-C
// 1. Listen on the callback
[[TRTCCalling shareInstance] addDelegate:delegate];

// Answer/Reject
// At this point, if user B also logs in to the IM system, user B will receive the `onInvited(A, null, false)` callback
// The `accept`/`reject` methods of `TRTCCalling` can be called to answer/reject the call
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType {
    [[TRTCCalling shareInstance] accept];
}

// 2. Other functions of the component can be called to perform other operations such as making and ending a call
// Note: they can be called normally only after successful login
// Make a video call
[[TRTCCalling shareInstance] call:@"target user" type:CallType_Audio];
// Hang up
[[TRTCCalling shareInstance] hangup];
// Reject
[[TRTCCalling shareInstance] reject];

```

<span id="model.step6"> </span>

### Step 6: Make a group call

1. Caller: to initiate a group audio call, the caller needs to call the `groupCall()` function in `TRTCCalling` and pass in the required user list (`userIdList`), the optional IM group ID (`groupId`), and `CallType_Audio` as the call type (`callType`).
2. Receiver: a receiver can receive the request through the `onInvited()` callback.
3. Receiver: a receiver can call the `accept()` method to answer the call or call the `reject()` method to reject the call after receiving the callback.
4. If a receiver does not respond to the call for a certain period of time (30 seconds by default), this receiver will receive the `onCallingTimeOut()` callback, and the caller will receive the `onNoResp(String userId)` callback. If multiple receivers do not answer the call, the caller can call `hangup()`, and each receiver will receive the `onCallingCancel()` callback.
5. A user can call the`hangup()` method to leave the current group call.
6. If there is a user joining or leaving the call, other users will receive the `onUserEnter()` or `onUserLeave()` callback.

```Objective-C
// Omitted content...
// Splice the list of users to be called
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// If the call is not initiated in an IM group, an empty string can be passed in for `groupId`
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];
```

>?You can implement corresponding UI prompts through a series of listening callbacks, such as `onReject`, `onCancel`, and other events.
><span id="offline"> </span>

### Step 7: Answer a call offline

>?If your business is an online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, we recommend that you implement offline answering.

The IM SDK supports offline push, but you need to complete the corresponding settings to meet its availability standard.

1. Apply for an Apple push certificate. For detailed directions, please see [Obtaining Apple Push Notification Service Certificates](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Configure offline push on the backend and on the client.
3. Set `param.busiId` in the `login` function to the corresponding certificate ID.

<span id="api"> </span>

## Component API List

Below is the list of `TRTCCalling` component APIs:

| API Function | Feature |
| --------------- | -------------------------------------------------------- |
| addDelegate | Sets the `TRTCCalling` callback, through which users can get status notifications |
| login | Logs in to IM. All other features can be used only after login |
| logout | Logs out of IM. Calls cannot be made after logout |
| call | Invites the user to the C2C call. The invited user will receive the `onInvited` callback |
| groupCall | Invites users to an IM group call. The invited users will receive the `onInvited` callback |
| accept | Answers the call as a receiver |
| reject | Rejects the call as a receiver |
| hangup | Ends the call |
| startRemoteView | Renders the camera data of the remote user in the specified `UIView` |
| stopRemoteView | Stops rendering the camera data of the remote user |
| openCamera | Enables the camera and renders the camera data into the specified `TXCloudVideoView` |
| closeCamera | Disables the camera |
| switchCamera | Switches between the front and rear cameras |
| setMicMute | Specifies whether to mute the mic |
| setHandsFree | Specifies whether to enable the hands-free mode |
