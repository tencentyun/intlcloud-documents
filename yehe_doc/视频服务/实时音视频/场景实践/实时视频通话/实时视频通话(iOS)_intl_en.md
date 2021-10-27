## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the app we provide to try out the effect of real-time video call.



To quickly implement the video call feature, you can use the app we provide and adapt it to your needs. You can also use the `TUICalling` component and customize your own UI.

>! We previously provided the `TRTCVideoCall` component, which has been moved to the [component repository](https://github.com/tencentyun/LiteAVClassic). The `TUICalling` component uses IM signaling APIs and is not compatible with the old component.

[](id:ui)

## Using the Demo App's UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestVideoCall` and click **Create**.
3. Click **Next** to skip this step.

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the app source code
Clone or download the [TUICalling](https://github.com/tencentyun/TUICalling) source code.

[](id:ui.step3)
### Step 3. Configure app project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `TUICalling/Debug/GenerateTestUserSig.swift`.
3. Set parameters in `GenerateTestUserSig.swift`:
<ul style="margin:0"><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the demo app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo app

Open the source code project `TUICalling/TUICallingApp.xcworkspace` with Xcode (version 11.0 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo app's source code

The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code.

| File or Folder | Description |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  | The main view for video calls, where calls are answered/declined |
|  TRTCCallingAudioViewController.swift   | The main view for audio calls, where calls are answered/declined |


## Tryout
>! You need at least two devices to try out the demo app.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Enter the username to be called and tap **Search**.
3. Tap **Call** and choose to make a **video call** (**please make sure that the callee stays in the app; otherwise, the call may fail**).

### User B
1. Enter a username (**which must be unique**) and log in.
2. Go to the homepage and wait for the incoming call.


[](id:model)
## Customizing Your Own UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUICalling) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCCalling`. You can find the component's APIs in `TRTCCalling.h`.
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

You can use the open-source component `TRTCCalling` to customize your own UI. This means you will use the model of the demo but design the UI by yourself.

[](id:model.step1)
### Step 1. Integrate the SDK

The call component `TRTCCalling` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project by following the steps below:

- **Method 1: adding dependencies via CocoaPods**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC' 
:::
</dx-codeblock>
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
- **Method 2: Implement dependency through the local files**
If access to the CocoaPods repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.
<table>
<tr>
<th>SDK</th>
<th>Download Page</th>
<th>Integration Guide</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">Integration document</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
</tr>
</table>

[](id:model.step2)
### Step 2. Configure permission requests

Apply for the camera and mic permissions by adding `Privacy - Camera Usage Description` and `Privacy - Microphone Usage Description` in the `info.plist` file.

[](id:model.step3)
### Step 3. Import the `TUICalling` component
**To import the component through CocoaPods**, the specific steps are as follows:
1. Copy the `Source`, `Resources`, and `TXAppBasic` folders and the `TUICalling.podspec` file under the demo project directory to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
<dx-codeblock>
::: swift
 pod 'TXAppBasic', :path => "TXAppBasic/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUICalling', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Initialize and log in to the component

1. Set push information.
<dx-codeblock>
::: swift
 [TRTCCalling shareInstance].imBusinessID = your business ID;
 [TRTCCalling shareInstance].deviceToken =  deviceToken;
:::
</dx-codeblock>
>?  `imBusinessID` is generated after you upload an APNs certificate in the [IM console](https://console.cloud.tencent.com/im). Then, you can request a callback from Apple's backend through `AppDelegate` to return the corresponding `deviceToken` value. For detailed directions, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).
2. Call `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` to log in to the component. Enter key parameters as shown below:
<table>
<tr><th>Parameter</th><th>Description</th></tr>
<tr>
<td>sdkAppID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>user</td>
<td>ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></table>
<dx-codeblock>
::: Objective-C Objective-C
// Login
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Video call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Video call login failed.");
}];
:::
</dx-codeblock>


[](id:model.step5)
### Step 5. Make a one-to-one call

1. Caller: the caller can call the `call(userId, callType)` method in `TRTCCalling` and pass in the user ID as `userId` and call type as `callType` with the value `CallType_Video` to make a video call.
2. Callee: if already logged in, the callee will receive the `onInvited()` callback, where `callType` is the call type entered by the caller. You can start the corresponding UI according to this parameter. If you want the callee to receive call requests even when logged out, please see [Offline Answering](#offline).
3. Callee: the callee can call `accept()` to answer the call and `openCamera()` to turn the local camera on if the call is a video call. He or she can also call `reject()` to decline the call.
4. After communication is established between the caller and callee, they will both receive the `onUserAudioAvailable()` callback, which indicates that they have received each other's audio. Remote audio will be played back automatically by default.

<dx-codeblock>
::: Objective-C Objective-C
// 1. Listen on the callback
[[TRTCCalling shareInstance] addDelegate:delegate];

// Accept/Decline
// At this point, if user B also logs in to the IM system, user B will receive the `onInvited(A, null, false)` callback
// The `accept`/`reject` methods of `TRTCCalling` can be called to accept/decline the call
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
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
    [[TRTCCalling shareInstance] stopRemoteView:uid]; // Stop rendering the image
  }
}

// 3. Other functions of the component can be called to perform other operations such as making and ending a call
// Note: they can be called normally only after successful login
// Make a video call
[[TRTCCalling shareInstance] call:@"target user" type:CallType_Video];
// Hang up
[[TRTCCalling shareInstance] hangup];
// Decline
[[TRTCCalling shareInstance] reject];
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Make a group call

1. Caller: to initiate a group audio/video call, the caller needs to call the `groupCall()` function in `TRTCCalling` and pass in the required user list (`userIdList`), optional IM group ID (`groupId`), and `CallType_Video` as the call type (`callType`).
2. Callee: a callee can receive the request through the `onInvited()` callback, where the parameter list contains parameters entered by the caller, and the `callType` parameter is the call type. You can start the corresponding UI according to this parameter.
3. Callee: a callee can call the `accept()` method to answer the call or call the `reject()` method to decline the call after receiving the callback.
4. If a callee does not respond to the call for a certain period of time (30 seconds by default), this callee will receive the `onCallingTimeOut()` callback, and the caller will receive the `onNoResp()` callback. If multiple callees do not answer the call, the caller can call `hangup()`, and each callee will receive the `onCallingCancel()` callback.
5. A user can call the`hangup()` method to leave the current group call.
6. If there is a user joining or leaving the call, other users will receive the `onUserEnter()` or `onUserLeave()` callback.

>?The `groupID` parameter in the `groupCall:type:groupID:` API is the group ID in the IM SDK. If this parameter is set, the call request signaling message will be sent through the group ID, which is simple and reliable. If this parameter is left empty, the `TRTCalling` component will send the message to users one by one.

<dx-codeblock>
::: Objective-C Objective-C
// Omitted content...
// Splice the list of users to be called
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// If the call is not initiated in an IM group, an empty string can be passed in for `groupId`
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];

// Turn on the local camera
[[TRTCCalling shareInstance] openCamera:true view:renderView];
:::
</dx-codeblock>

[](id:offline)
### Step 7. Answer a call offline

>?If your business is online customer service or any other service that does not require the offline answering feature, you only need to complete [step 1](#model.step1) to [step 6](#model.step6) for integration. If your business is used for social networking, we recommend you implement offline answering.

The IM SDK supports offline push, but you need to complete the corresponding settings to meet its availability standard.

1. Apply for an Apple push certificate. For detailed directions, please see [Applying for Apple Push Certificate](https://intl.cloud.tencent.com/document/product/1047/34346).
2. Configure offline push on the backend and client. For detailed directions, please see [Offline Push (iOS)](https://intl.cloud.tencent.com/document/product/1047/34347).
3. Set `param.busiId` in the `login` function to the corresponding certificate ID.

[](id:api)

## Component APIs

The table below lists the APIs of the `TRTCCalling` component.

| API Function | Feature |
| --------------- | -------------------------------------------------------- |
| addDelegate | Sets the `TRTCCalling` callback, through which users can get status notifications |
| login | Logs in to IM. All other features can be used only after login |
| logout | Logs out of IM. Calls cannot be made after logout |
| call | Invites the user to the C2C call. The invited user will receive the `onInvited` callback |
| groupCall | Invites users to an IM group call. The invited users will receive the `onInvited` callback |
| accept | Answers a call |
| reject | Declines a call |
| hangup | Ends a call |
| startRemoteView | Renders the camera data of the remote user in the specified `UIView` |
| stopRemoteView | Stops rendering the camera data of the remote user |
| openCamera | Enables the camera and renders the camera data into the specified `TXCloudVideoView` |
| closeCamera | Disables the camera |
| switchCamera | Switches between the front and rear cameras |
| setMicMute | Specifies whether to mute the mic |
| setHandsFree | Specifies whether to enable the hands-free mode |
