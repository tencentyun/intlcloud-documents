## Use Cases
TRTC supports four room entry modes, among which video call (VideoCall) and audio call (VoiceCall) are classified as call mode, while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as [live streaming mode](https://intl.cloud.tencent.com/document/product/647/35107).
In call mode, there can be a maximum of 300 members in a single TRTC room, and up to 50 of them can speak at the same time. This service is suitable for various scenarios such as one-to-one video call, video conferencing with up to 300 attendees, online medical diagnosis, video interview, video customer service, and online werewolf.

## How It Works
The TRTC service consists of two types of server nodes: access servers and proxy servers:
- **Access server**
Backed by the highest-quality lines and high-performance servers, this type of nodes is ideal for processing end-to-end low-latency co-anchoring calls, but the fees per unit time are relatively high.
- **Proxy server**
With general lines and average-performance servers, this type of nodes is suitable for processing high-concurrence playback of pulled streams, and the fees per unit time are low.

In call mode, all users in the TRTC room will be assigned to access servers, which means that each user is an "anchor" and can speak at any time (up to 50 concurrent upstreams are supported), so it is suitable for scenarios such as online conferencing, but the number of members in a single room is limited to 300.


## Sample Code
You can log in to [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo) to get the sample code related to this document.


>If your access to GitHub is slow, you can directly download [TXLiteAVSDK_TRTC_iOS_latest.zip](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip).

## Directions
<span id="step1"> </span>
### Step 1. Integrate the SDK
You can integrate the **TRTC SDK** into your project in the following ways:
#### Method 1. Use CocoaPods for integration
1. Install **CocoaPods**. For detailed directions, please see [Getting Started](https://guides.cocoapods.org/using/getting-started.html).
2. Open the `Podfile` file in the root directory of your current project and add the following content:
>If there is no `Podfile` file in the directory, run the `pod init` command to create one and then add the following content:
>
```
target 'Your Project' do
        pod 'TXLiteAVSDK_TRTC'
end
```
3. Run the following command to install the **TRTC SDK**.
```
pod install
```
A **xcworkspace** file will be generated in the root directory of the current project after the installation is successful.
4. Open the newly generated **xcworkspace** file.

#### Method 2. Download the ZIP package for manual integration
If you do not want to install the CocoaPods environment, or it has been installed but the access to CocoaPods repositories is slow, you can directly download the [ZIP package](https://intl.cloud.tencent.com/document/product/647/34615) and integrate the SDK into your project as instructed in [Quick Integration (iOS)](https://intl.cloud.tencent.com/document/product/647/35092).

<span id="step2"> </span>
### Step 2. Grant media device permissions
Add the permissions to request camera and mic access in the `Info.plist` file.

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | It describes the reason for requesting the camera permission; for example, camera access is required before video can be displayed in video chat |
| Privacy - Microphone Usage Description | It describes the reason for requesting the mic permission; for example, mic access is required before audio can be sent in chat |

<span id="step3"> </span>
### Step 3. Initialize an SDK instance and listen on the event callback

1. Call the [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35119) API to create a `TRTCCloud` instance.
```swift
// Create a `trtcCloud` instance
let trtcCloud: TRTCCloud = TRTCCloud.sharedInstance()
trtcCloud.delegate = self
```
2. Set the `delegate` attribute to register the event callback and listen on relevant events and error notifications.
```swift
// Error notifications should be listened on, captured, and sent to the user
func onError(_ errCode: TXLiteAVError, errMsg: String?, extInfo: [AnyHashable : Any]?) {
        if ERR_ROOM_ENTER_FAIL == errCode {
                toastTip("Failed to enter the room[\(errMsg ?? "")]")
                exitRoom()
        }
}
```

<span id="step4"> </span>
### Step 4. Assemble the room entry parameter `TRTCParams`
When calling the [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) API, you need to enter a key parameter [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams), which includes the following required fields:

| Parameter | Field Type | Description | Example |
|---------|---------|---------|---------|
| sdkAppId | Numeric | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app). | 1400000123 |
| userId | String | It can contain only letters (a–z and A–Z), digits (0–9), underscores, and hyphens. | test_user_001 |
| userSig | String | `userSig` can be calculated based on `userId`. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Numeric | Room IDs in string type are not supported by default, as they will lower the room entry speed. If you need to used string-type room IDs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. | 29834 |

> In TRTC, users with the same `userId` cannot be in the same room at the same time; otherwise, there will be a conflict.

<span id="step5"> </span>
### Step 5. Create and enter a room
1. Call [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) to enter the audio/video room specified by `roomId` in the `TRTCParams` parameter. If the room does not exist, the SDK will automatically create it with the `roomId` value as the room number.
2. Please set the appropriate **`appScene`** parameter according to the actual application scenario. An incorrect selection may lead to higher lagging rate or lower video definition than expected.
 - For video calls, please set `TRTCAppScene.videoCall`.
 - For audio calls, please set `TRTCAppScene.audioCall`.
3. After successful room entry, the SDK will call back the `onEnterRoom(result)` event. If `result` is greater than 0, the room entry succeeds, and the specific value indicates the time in milliseconds (ms) used for entering the room; if `result` is less than 0, the room entry fails, and the specific value indicates the error code of the failure.

```swift
func enterRoom() {
    let params = TRTCParams.init()
    params.sdkAppId = sdkappid
    params.userId   = userid
    params.userSig  = usersig
    params.roomId   = 908
    trtcCloud.enterRoom(params, appScene: TRTCAppScene.videoCall)
}

func onEnterRoom(_ result: Int) {
    if result > 0 {
        toastTip("Entered room successfully; the total time used is [\(result)] ms")
    } else {
        toastTip("Failed to enter the room; the error code is [\(result)]")
    }
}
```

> 
>- If the room entry fails, the SDK will also call back the `onError` event and return the parameters `errCode` ([error code](https://intl.cloud.tencent.com/document/product/647/35124)), `errMsg` (error message), and `extraInfo` (reserved parameter).
>- If you are already in a room, you must call `exitRoom()` to exit the current room first before entering the next room.

<span id="step6"> </span>
### Step 6. Subscribe to remote audio/video streams
The SDK supports both automatic subscription and manual subscription.

#### Automatic subscription mode (default)
In automatic subscription mode, after room entry, the SDK will automatically receive audio streams from other users in the room to achieve the best "instant broadcasting" effect:
1. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) event notification, and the SDK will automatically play back the audio of the remote user.
2. You can block the audio data of a specified `userId` through [muteRemoteAudio(userId, mute: true)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) or all remote users through [muteAllRemoteAudio(true)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14). After that, the SDK will no longer pull the audio data of the corresponding remote users.
3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) event notification; however, since the SDK has not received instructions on how to display the video data at this time, video data will not be processed automatically. You need to associate the video data of the remote user with the display `view` by calling the [startRemoteView(userId, view: view)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) method.
4. You can specify the display mode of the local video image through [setRemoteViewFillMode()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff):
 - `Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
 - `Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
5. You can block the video data of a specified `userId` through [stopRemoteView(userId)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066) or all remote users through [stopAllRemoteView()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b). After that, the SDK will no longer pull the video data of the corresponding remote users.

```swift
// Sample code: subscribe to (or unsubscribe from) the video image of the remote user based on the notification
func onUserVideoAvailable(_ userId: String, available: Bool) {
    let remoteView = remoteViewDic[userId] as! UIView
    if available {
        trtcCloud.startRemoteView(userId, view: remoteView)
        trtcCloud.setRemoteViewFillMode(userId, mode: TRTCVideoFillMode.fit)
    } else {
        trtcCloud.stopRemoteView(userId)
    }
}
```

> If you do not call `startRemoteView()` to subscribe to the video stream immediately after receiving the `onUserVideoAvailable()` event callback, the SDK will stop receiving remote video data within 5 seconds.

#### Manual subscription mode
You can specify the SDK to enter the manual subscription mode through the [setDefaultStreamRecvMode()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) API. In this mode, the SDK will not automatically receive audio/video data of other users in the room; instead, you need to manually trigger the receipt through API functions.

1. **Before room entry**, call the [setDefaultStreamRecvMode(false, video: false)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) API to set the SDK to manual subscription mode.
2. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) event notification. At this time, you need to manually subscribe to the user's audio data by calling [muteRemoteAudio(userId, mute: false)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2), and the SDK will decode and play back it after receiving it.
3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) event notification. At this time, you need to manually subscribe to the user's video data by calling [startRemoteView(userId, view: view)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49), and the SDK will decode and play back it after receiving it.

<span id="step7"> </span>
### Step 7. Publish the local audio/video stream
1. Call [startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) to enable local mic capture and encode and send the captured audio.
2. Call [startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) to enable local camera capture and encode and send the captured video.
3. Call [setLocalViewFillMode()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) to set the display mode of the local video image:
 - `Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
 - `Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
4. Call [setVideoEncoderParam()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.

```swift
// Sample code: send local audio/video streams
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.fit)
trtcCloud.startLocalPreview(frontCamera, view: localView)
trtcCloud.startLocalAudio()
```

> The SDK for macOS will use the system-default camera and mic by default. You can call [setCurrentCameraDevice()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) and [setCurrentMicDevice()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) to select another camera and mic.

<span id="step8"> </span>
### Step 8. Exit the current room

Call the [exitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) method to exit the room. The SDK needs to disable and release hardware devices such as the camera and mic during room exit. Therefore, room exit is not completed as soon as the method is called. Only after the [onExitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) callback is received can the room exit be considered completed.

```swift
// Please wait for the `onExitRoom` event callback after calling the room exit method
trtcCloud.exitRoom()

func onExitRoom(_ reason: Int) {
    print("Exit room [\(roomId)]: reason[\(reason)]")
}
```

> If multiple audio/video SDKs are integrated into your application, please enable other SDKs only after receiving the `onExitRoom` callback; otherwise, hardware occupancy issues may occur.
