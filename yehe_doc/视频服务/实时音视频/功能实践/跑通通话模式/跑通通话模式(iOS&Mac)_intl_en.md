## Use Cases
TRTC supports four room entry modes. Video call (`VideoCall`) and audio call (`AudioCall`) are the call modes, and interactive video streaming (`Live`) and interactive audio streaming (`VoiceChatRoom`) are the [live streaming modes](https://intl.cloud.tencent.com/document/product/647/35107).
The call modes allow a maximum of 300 users in each TRTC room, and up to 50 of them can speak at the same time. The call modes are suitable for scenarios such as one-to-one video calls, video conferencing with up to 300 participants, online medical consultation, remote interviews, video customer service, and online Werewolf playing.

## How It Works
TRTC services use two types of server nodes: access servers and proxy servers.
- **Access server**
This type of nodes use high-quality lines and high-performance servers and are better suited to drive low-latency end-to-end calls, but the unit cost is relatively high.
- **Proxy server**
This type of servers use mediocre lines and average-performance servers and are better suited to power high-concurrency stream pulling and playback. The unit cost is relatively low.

In the call modes, all users in a TRTC room are assigned to access servers and are in the role of “anchor”. This means the users can speak to each other at any point during the call (up to 50 users can send data at the same time). This makes the call modes suitable for use cases such as online conferencing, but the number of users in each room is capped at 300.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code
You can visit [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC) to obtain the sample code used in this document.
![](https://main.qcloudimg.com/raw/468128bcaf078183eed097f7ee5f9c21.png)

>?If your access to GitHub is slow, download the ZIP file [here](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip).

## Directions
[](id:step1)
### Step 1. Integrate the SDK
You can integrate the **TRTC SDK** into your project in the following ways:
#### Method 1: integrating through CocoaPods
1. Install **CocoaPods**. For detailed directions, please see [Getting Started](https://guides.cocoapods.org/using/getting-started.html).
2. Open the `Podfile` file in the root directory of your project and add the code below.
>? If you cannot find a `Podfile` file in the directory, run the `pod init` command to create one and add the code below.
>
```
target 'Your Project' do
        pod 'TXLiteAVSDK_TRTC'
end
```
3. Run the command below to install the **TRTC SDK**.
```
pod install
```
After successful installation, an **XCWORKSPACE** file will be generated in the root directory of your project.
4. Open the **XCWORKSPACE** file.

#### Method 2: manual integration
If you do not want to install CocoaPods, or your access to CocoaPods repositories is slow, you can download the [ZIP file](https://intl.cloud.tencent.com/document/product/647/34615) of the SDK and integrate it into your project as instructed in [SDK Quick Integration > iOS](https://intl.cloud.tencent.com/document/product/647/35092).

[](id:step2)
### Step 2. Add device permission requests
Add camera and mic permission requests in the `Info.plist` file.

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | The reason for requesting camera permission, for example, “camera access is required to capture video” |
| Privacy - Microphone Usage Description | The reason for requesting mic permission, for example, “mic access is required to capture audio” |

[](id:step3)
### Step 3. Initialize an SDK instance and configure event callbacks

1. Call [sharedInstance()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) to create a `TRTCCloud` instance.
```
// Create a TRTCCloud instance
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
```
2. Set the attributes of `delegate` to subscribe to event callbacks and listen for event and error notifications.
<dx-codeblock>
::: iOS object-c
// Error events must be listened for and captured, and error messages should be sent to users.
- (void)onError:(TXLiteAVError)errCode errMsg:(NSString *)errMsg extInfo:(NSDictionary *)extInfo {
    if (ERR_ROOM_ENTER_FAIL == errCode) {
        [self toastTip:@"Failed to enter room"];
        [self.trtcCloud exitRoom];
    }
}
:::
</dx-codeblock>

[](id:step4)
### Step 4. Assemble the room entry parameter `TRTCParams`
When calling the [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API, you need to pass in a key parameter [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams), which includes the following required fields:

| Parameter | Field Type | Description | Example |
|---------|---------|---------|---------|
| sdkAppId | Number | Application ID, which you can view in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>. |1400000123 |
| userId | String | Only letters (a-z and A-Z), digits (0-9), underscores, and hyphens are allowed. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Number | String-type room IDs tend to slow down the room entry process and are therefore not supported by the SDK by default. If you need to use string-type room IDs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). | 29834 |

>! In TRTC, users with the same `userId` cannot be in the same room at the same time as it will cause a conflict.

[](id:step5)
### Step 5. Create and enter a room
1. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) to enter the room specified by the `roomId` field in `TRTCParams`. If the room does not exist, the SDK will create a room whose room number is the value of `roomId`.
2. Set the **`appScene`** parameter according to your actual application scenario. Inappropriate `appScene` values may lead to increased lag or decreased clarity.
 - For video calls, set the parameter to `TRTCAppScene.videoCall`.
 - For audio calls, set the parameter to `TRTCAppScene.audioCall`.
3. You will receive the `onEnterRoom(result)` callback. If `result` is greater than 0, room entry succeeds, and the value of `result` indicates the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.

<dx-codeblock>
::: iOS object-c
- (void)enterRoom() {
    TRTCParams *params = [TRTCParams new];
    params.sdkAppId = SDKAppID;
    params.roomId = _roomId;
    params.userId = _userId;
    params.role = TRTCRoleAnchor;
    params.userSig = [GenerateTestUserSig genTestUserSig:params.userId];
    [self.trtcCloud enterRoom:params appScene:TRTCAppSceneVideoCall];
}

- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"Entered room successfully"];
    } else {
        [self toastTip:@"Failed to enter room"];
    }
}
:::
</dx-codeblock>

>! 
>- If room entry fails, you will also receive the `onError` callback, which contains `errCode` ([error code](https://intl.cloud.tencent.com/document/product/647/35124)), `errMsg` (error message), and `extraInfo` (reserved parameter).
>- If you are already in a room, you must call `exitRoom` to exit the room before entering another room.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

[](id:step6)
### Step 6. Subscribe to remote audio/video streams
The SDK supports automatic subscription and manual subscription.

#### Automatic subscription (default)
In the automatic subscription mode, after room entry, the SDK will automatically pull audio streams from other users in the room. This enables instant streaming.
1. If other users in the room are sending audio data, you will receive the [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) notification, and the SDK will automatically play back the users’ audio.
2. Call [muteRemoteAudio(userId, mute: true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) to mute a specified user (`userId`), or [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) to mute all remote users. The SDK will stop pulling the audio data of the user(s).
3. If a remote user in the room is sending video data, you will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) notification, but since the SDK has not received instructions on how to display the video, it will not process the video data. You must call [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) to associate the remote user’s video data with `view`.
4. Call [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) to specify the display mode of a remote video.
 - `Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
 - `Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
5. Call [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066) to block the video data of a specified user (`userId`) or [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) to block the video data of all remote users. The SDK will stop pulling the video data of the user(s).

<dx-codeblock>
::: iOS object-c
// Sample code: subscribe to or unsubscribe from the video image of a remote user based on the notification received
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available {
    UIView* remoteView = remoteViewDic[userId];
    if (available) {
        [_trtcCloud startRemoteView:userId streamType:TRTCVideoStreamTypeSmall view:remoteView];
    } else {
        [_trtcCloud stopRemoteView:userId streamType:TRTCVideoStreamTypeSmall];
    }
}
:::
</dx-codeblock>

>? If you do not call `startRemoteView()` to subscribe to the video stream immediately after receiving the `onUserVideoAvailable()` event callback, the SDK will stop pulling the remote video within 5 seconds.

#### Manual subscription
You can call [setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) to switch the SDK to the manual subscription mode. In this mode, the SDK will not pull the data of other users in the room automatically. You have to start the process manually via APIs.

1. **Before you enter a room**, call the [setDefaultStreamRecvMode(false, video: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) API to switch the SDK to the manual subscription mode.
2. If other users in the room are sending audio data, you will receive the [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) notification, and you need to call [muteRemoteAudio(userId, mute: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) to manually subscribe to the users’ audio. The SDK will decode and play the audio data received.
3. If a remote user in the room is sending video data, you will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) notification, and you need to call [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) to manually subscribe to the user's video data. The SDK will decode and play the video data received.

[](id:step7)
### Step 7. Publish the local stream
1. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) to enable local mic capturing and encode and send the audio captured.
2. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) to enable local camera capturing and encode and send the video captured.
3. Call [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) to set the display mode of the local video:
 - `Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
 - `Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
4. Call [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) to set the encoding parameters for the local video, which determine the [quality of your video](https://intl.cloud.tencent.com/document/product/647/35153) seen by other users in the room.

<dx-codeblock>
::: iOS object-c
// Sample code: publish the local audio/video stream
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
:::
</dx-codeblock>

>! The SDK for macOS uses the default camera and mic. You can call [setCurrentCameraDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) and [setCurrentMicDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) to switch to a different camera and mic.

[](id:step8)
### Step 8. Exit the room

Call [exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) to exit the room. The SDK disables and releases devices such as cameras and mics during room exit. Therefore, room exit is not an instant process. It completes only after the [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) callback is received.

<dx-codeblock>
::: iOS object-c
// Please wait for the `onExitRoom` callback after calling the room exit API.
[self.trtcCloud exitRoom];

- (void)onExitRoom:(NSInteger)reason {
    NSLog(@"Exited room: reason: %ld", reason)
}
:::
</dx-codeblock>

>! If your application integrates multiple audio/video SDKs, please wait after you receive the `onExitRoom` callback to enable other SDKs; otherwise, the device busy error may occur.
