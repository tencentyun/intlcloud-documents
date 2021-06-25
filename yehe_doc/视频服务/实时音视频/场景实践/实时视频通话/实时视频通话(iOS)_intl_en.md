## Effect Demo
To quickly implement the video call feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCCalling` component and implement your custom UI.

>! Previously we offered `TRTCVideoCall` component, which was moved to the [Component Repository](https://github.com/tencentyun/LiteAVClassic). We now provide `TRTCCalling` component which uses IM signaling API and is not compatible with the previous version.

<span id="ui"> </span>

## Reusing Demo UI

<span id="ui.step1"></span>

### Step 1. Create an application

1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestVideoCall`, and click **Create Application**.

>! This feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.IM is a value-added service at the prices as detailed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<span id="ui.step2"></span>

### Step 2. Download the SDK and demo source code

1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to enter GitHub (or click **[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**), and download the relevant SDK and supporting demo source code.
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>

### Step 3. Configure demo project files

1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set the parameters in the `GenerateTestUserSig.h` file:
  - SDKAPPID: it is 0 by default. Please replace it with the real `SDKAppID`.
  - SECRETKEY: it is an empty string by default. Please replace it with the real key information.
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Log in to the Console to Manage the Application**.

>!
>- In this document, the `SECRETKEY` is configured in the client code to obtain `UserSig`. The `SECRETKEY` is easily decompiled and reverse cracked. If the `SECRETKEY` is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method only applies to locally running a demo project and commissioning features**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166#Server).

<span id="ui.step4"></span>

### Step 4. Run the demo

Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` source code project and click **Run** to debug the demo.

<span id="ui.step5"></span>

### Step 5. Modify the demo source code

The source code folder `TRTCCallingDemo` contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code:

|              File or Folder              | Description                                                 |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  | Video call homepage where calls can be answered or rejected. |
|  TRTCCallingAudioViewController.swift  | Audio call homepage where calls can be answered or rejected. |
| TRTCCallingContactViewController.swift | It is used to show the interface for searching for contacts.                               |


<span id="model"> </span>

## Implementing Custom UI

The `TRTCCallingDemo` folder in the [source code] contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCCalling`. You can find the API functions provided by this component in the `TRTCCalling.h` file.
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

You can use the open-source component `TRTCCalling` to implement your own UI, i.e., only reusing the `model` to implement your custom UI.

<span id="model.step1"> </span>

### Step 1. Integrate the SDK

The call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

- **Method 1. Implement dependency through the CocoaPods repository**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.
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

Apply for the camera and mic permissions by adding `Privacy - Camera Usage Description` and `Privacy - Microphone Usage Description` in the `info.plist` file.

<span id="model.step3"> </span>

### Step 3. Import the TRTCCalling component

Copy all files in the following directory to your project:
```
iOS/TRTCSceneDemo/TXLiteAVDemo/TRTCCallingDemo/model 
```

<span id="model.step4"> </span>

### Step 4. Initialize and log in to the component

1. Set push information.
```
[TRTCCalling shareInstance].imBusinessID = your business ID;
[TRTCCalling shareInstance].deviceToken =  deviceToken;
```
2. Call `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` to log in to the component. Enter key parameters as shown below:
<table>
<tr><th>Parameter Name</th><th>Description</th></tr>
<tr>
<td>sdkAppID</td>
<td>You can view the `SDKAPPID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr><tr>
<td>user</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_). </td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr></table>
<pre>
// Login
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Video call login success.");
} fail:^(int code, NSString *msg) {
        NSLog(@"Video call login failed.");
}];
</pre>

<span id="model.step5"> </span>

### Step 5. Implement one-to-one calls

1. Caller: call the `call(userId, callType)` method in `TRTCCalling` and pass in the user ID as `userId` and `CallType_Video` as `callType` to initiate a video call request.
2. Callee: if already logged in, the callee will receive the `onInvited()` callback. The caller can use the parameter `callType` to set the call type and the callee can use this parameter to initiate the call interface. If you want the callee to receive call requests even when logged out, please see [Offline Answering](#offline).
3. Callee: the callee can call the `accept()` function to answer the call and also call the `openCamera()` function to enable the local camera if this is a video call. And the callee can call `reject()` to reject the call.
4. After the audio/video channel between the caller and callee is established, they will receive the `onUserVideoAvailable()` callback, which indicates that they have received each other's image. At this point, they can call `startRemoteView()` to display the remote video image, and the remote audio will be played back by default.

```Objective-C
// 1. Listen on callback
[[TRTCCalling shareInstance] addDelegate:delegate];

// Answer/reject the call
// At this point, if user B also logs in to the IM system, user B will receive the `onInvited(A, null, false)` callback
// Call the TRTCCalling `accept` method/`reject()` method to accept/reject the call
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIdsv
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType {
    [[TRTCCalling shareInstance] accept];
}

// 2. View each other's image
// As user A enables the camera, user B will receive the `onUserVideoAvailable(A, true)` callback after answering the call
- (void)onUserVideoAvailable:(NSString *)uid available:(BOOL)available {
  if (available) {
    UIView* renderView =[[UIView alloc] init];
    [[TRTCCalling shareInstance] startRemoteView:uid view:renderView]; // They can see each other's image
  } else {
    [[TRTCCalling shareInstance] stopRemoteView:uid]; // Stops rendering the image
  }
}

// 3. Call the component’s other functions to initiate or hang up a call or to use other features
// Note: you can only call functions after login
// Initiate a video call
[[TRTCCalling shareInstance] call:@"Target user" type:CallType_Video];
// Hang up
[[TRTCCalling shareInstance] hangup];
// Reject
[[TRTCCalling shareInstance] reject];

```


<span id="model.step6"> </span>

### Step 6. Make a group call

1. Caller: to make a group video/audio call, the caller needs to call `groupCall()` function in `TRTCCalling`, pass in `userIdList` (user list, required) and `groupId` (IM group ID, optional) parameters. The `callType` is `CallType_Video`.
Callee: a callee can receive the request via the `onInvited()` callback. The parameter list is entered by the caller and the parameter `callType` is used to set the call type. Callee can use this parameter to initiate the call interface.
3. Callee: a callee can call the `accept()` method to answer the call or call the `reject()` method to reject the call after receiving the callback.
4. If a callee does not respond to the call for a certain period of time (30 seconds by default), this callee will receive the `onCallingTimeOut()` callback, and the caller will receive the `onNoResp()` callback. If multiple callees do not answer the call, the caller can call `hangup ()`, and each callee will receive the `onCallingCancel()` callback.
5. A user can call the`hangup()` method to leave the current group call.
6. If there is a user joining or leaving the call, other users will receive the `onUserEnter()` or `onUserLeave()` callback.

>?The `groupID` parameter in the `groupCall:type:groupID:` API is the group ID in the IM SDK. If this parameter is set, the call request will be sent through the group message system, which is simple and reliable. If this parameter is left empty, the `TRTCalling` component will send the message to users one by one.

```Objective-C
// Omitted content...
// Splice the list of users to be called
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// If the call is not initiated in an IM group, an empty string can be passed in for `groupId`;
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];

// Enable local camera
[[TRTCCalling shareInstance] openCamera:true view:renderView];
```

<span id="offline"> </span>

### Step 7. Answer a call offline

>?If your business is online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, you are recommended to implement offline answering.

The IM SDK supports offline push, but you need to complete the corresponding settings to meet its availability standard.

1. For details on how to apply for an Apple push notification service certificate, please see [Applying for an Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Configure offline push on the backend and client. For detailed directions, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).
3. Set `param.busiId` in the `login` function to the corresponding certificate ID.

<span id="api"> </span>

## Component APIs

Below is the list of `TRTCCalling` component APIs:

| API Fuction        | Description                                                 |
| --------------- | -------------------------------------------------------- |
| addDelegate     | Sets the callback proxy of `TRTCVideoCallDelegate`, which provides status notification for users |
| login           | Logs in to IM. All other features can be used only after login                |
| logout          | Logs out of IM. Calls cannot be made after logout                        |
| call            | Customized apps can integrate with the MLVB SDK provided by Tencent Cloud to implement the push function.
| groupCall       | Invites users to IM group call. The invited users will receive the `onInvited` callback          |
| accept          | Answers the call as a callee                                     |
| reject          | Rejects the call as a callee                                     |
| hangup          | Hangs up the call                                                 |
| startRemoteView | Renders the camera data of remote user in the specified `UIView`             |
| stopRemoteView  | Stops rendering the camera data for a remote user                         |
| openCamera      | Enables camera and renders data in the specified `TXCloudVideoView`           |
| closeCamera     | Disables the camera                                               |
| switchCamera    | Switches between front and rear cameras                                           |
| setMicMute      | Specifies whether to mute the mic                                             |
| setHandsFree    | Specifies whether to enable the hands-free mode                                             |
