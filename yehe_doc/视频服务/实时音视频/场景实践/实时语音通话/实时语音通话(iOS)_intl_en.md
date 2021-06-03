## Demonstration


To quickly implement the audio call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCCalling` component and implement custom UI.

>! We previously provided the `TRTCAudioCall` component, which has been moved to the [component repository](https://github.com/tencentyun/LiteAVClassic). The `TRTCCalling` component uses IM signaling APIs and is not compatible with the old component.

[](id:ui)

## Using Demo UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestAudioCall`, and click **Create**.

>! This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.

[](id:ui.step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files
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
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)

### Step 4. Run the demo

Use Xcode (version 11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging the demo.

[](id:ui.step5)

### Step 5. Modify the demo source code

The source code folder `TRTCCallingDemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

| File or Folder | Feature Description |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  | Video call UI where calls can be answered or rejected. |
|  TRTCCallingAudioViewController.swift  | Audio call UI where calls can be answered or rejected. |
| TRTCCallingContactViewController.swift | UI for searching for contacts. |


[](id:model)

## Implementing Your Custom UI

The [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCCallingDemo) folder `TRTCCallingDemo` contains two subfolders: `ui` and `model`. The `model` folder contains the implemented reusable open-source component `TRTCCalling`. You can find the API functions provided by this component in the `TRTCCalling.h` file.
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

You can use the open-source component `TRTCCalling` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"></span>

### Step 1. Integrate SDKs

The call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project by following the steps below:

- **Method 1: implement dependency through the CocoaPods repository**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.
- **Method 2: implement dependency through the local files**
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

[](id:model.step2)

### Step 2. Configure permissions

Apply for camera and mic permissions by adding `Privacy - Camera Usage Description` and `Privacy - Microphone Usage Description` in the `info.plist` file.

[](id:model.step3)

### Step 3. Import the TRTCCalling component

Copy all the files in the following directory to your project:
```
iOS/TRTCSceneDemo/TXLiteAVDemo/TRTCCallingDemo/model 
```

[](id:model.step4)

### Step 4. Initialize and log in to the component

1. Set the push information.
```
[TRTCCalling shareInstance].imBusinessID = your business ID;
[TRTCCalling shareInstance].deviceToken =  deviceToken;
```
2. Call `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` to log in to the component. Enter the key parameters as shown below:
 <table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>sdkAppID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>user</td>
<td>ID of the current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></table>
<dx-codeblock>

```
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Audio call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Audio call login failed.");
}];
```

[](id:model.step5)
### Step 5. Make a one-to-one call

1. The caller can call the `call(userId, callType)` method in `TRTCCalling` and pass in the user ID as `userId` and `CallType_Audio` as `callType` to initiate an audio call request.
2. The receiver can call the `accept` method to answer the call or call the `reject` method to reject the call after receiving the `onInvited` event.
3. The caller receives the `onUserEnter` callback, which indicates that the receiver has joined the call.
```
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

<span id="model.step6"></span>
### Step 6. Make a group call

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

[](id:offline)
### Step 7. Answer a call offline

>?If your business is an online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, we recommend that you implement offline answering.

The IM SDK supports offline push, but you need to complete the corresponding settings to meet its availability standard.

1. Apply for an Apple push certificate. For detailed directions, please see [Obtaining Apple Push Notification Service Certificates](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Configure offline push on the backend and client. For detailed directions, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).
3. Set `param.busiId` in the `login` function to the corresponding certificate ID.

[](id:api)
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
