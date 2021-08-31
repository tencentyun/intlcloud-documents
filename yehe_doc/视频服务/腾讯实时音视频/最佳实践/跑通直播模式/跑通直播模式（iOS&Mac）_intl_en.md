## Use Cases
TRTC supports four room entry modes, among which video call (VideoCall) and audio call (VoiceCall) are classified as [call mode](https://intl.cloud.tencent.com/document/product/647/35102), while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as live streaming mode.
TRTC in live streaming mode supports a maximum of 100,000 online users in one single room with a co-anchoring latency of below 300 ms and a watch latency of below 1,000 ms and enables users to mic on/off smoothly. This mode is suitable for such application scenarios as low-latency interactive live streaming, interactive classroom for up to 100,000 participants, video dating, online education, remote training, and large-scale conferencing.

## How It Works
The TRTC service consists of two types of server nodes: access servers and proxy servers:
- **Access server**
Backed by the highest-quality lines and high-performance servers, this type of nodes is ideal for processing end-to-end low-latency co-anchoring calls, but the fees per unit time are relatively high.
- **Proxy server**
With general lines and average-performance servers, this type of nodes is suitable for processing high-concurrence playback of pulled streams, and the fees per unit time are low.

In live streaming mode, TRTC uses the concept of "role". Specifically, users are divided into two roles, namely, "anchors" and "viewers". "Anchors" will be allocated to access servers, while "viewers" to proxy servers. A room can accommodate up to 100,000 viewers.
If a "user" wants to mic on, the role needs to be switched (switchRole) to "anchor" for the user to speak. During role switch, the user is also migrated from a proxy server to an access server. Thanks to its proprietary low-latency watch and smooth mic-on/off technologies, TRTC can get the whole switch done in a blink.



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
### Step 5. The anchor enables camera preview and mic capture
1. The anchor can call [startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) to enable the preview of local camera, and the SDK will request the system camera access.
2. The anchor can call [setLocalViewFillMode()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) to set the display mode of the local video image:
 - `Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
 - `Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
3. The anchor can call [setVideoEncoderParam()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.
4. The anchor can call [startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) to enable the mic, and the SDK will request the system mic access.

```swift
// Sample code: send local audio/video streams
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.fit)
trtcCloud.startLocalPreview(frontCamera, view: localView)
// Set local video encoding parameter
let encParams = TRTCVideoEncParam.init()
encParams.videoResolution = TRTCVideoResolution._960_540
encParams.videoBitrate    = 1200
encParams.videoFps        = 15
trtcCloud.setVideoEncoderParam(encParams)
trtcCloud.startLocalAudio()
```

<span id="step6"> </span>
### Step 6. The anchor sets beauty filters

1. The anchor can call [getBeautyManager()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) to get the beauty filter setting API [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager).
2. The anchor can call [setBeautyStyle()](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a) to set the beauty filter style.
 - Smooth: smooth style, which has more obvious skin smoothing effect, similar to the selfie style of internet influencers.
 - Nature: natural style, which retains more facial details and seems more natural subjectively.
 - Pitu: it is supported only for the [Enterprise Edition](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise).
3. The anchor can call [setBeautyLevel()](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#af864d9466d5161e1926e47bae0e3f027) to set the skin smoothing level (level 5 is generally okay).
4. The anchor can call [setWhitenessLevel()](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#a199b265f6013e0cca0ff99f731d60ff4) to set the skin brightening level (level 5 is generally okay).
5. As the tone of iPhone cameras is a little bit yellowish, it is recommended to call [setFilter()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) to add the skin brightening effect. The corresponding filter file can be downloaded [here](https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/filter/filterPNG.zip).

<span id="step7"> </span>
### Step 7. The anchor creates a room and starts push
1. The anchor sets the `role` field in [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) to **`TRTCRoleType.anchor`**, which indicates that the current user role is anchor.
2. The anchor can call [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) to create an audio/video room whose ID is the `roomId` field value in the `TRTCParams` parameter and specify the **`appScene`** parameter:
 - TRTCAppScene.LIVE: interactive live video streaming mode, which is used as an example in this document.
 - TRTCAppScene.voiceChatRoom: interactive live audio streaming mode.
3. After a room is successfully created, the anchor starts encoding and transferring audio/video data. At the same time, the SDK will call back the [onEnterRoom(result)](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) event. If `result` is greater than 0, the room entry succeeds, and the specific value indicates the time in milliseconds (ms) used for entering the room; if `result` is less than 0, the room entry fails, and the specific value indicates the error code of the failure.

```swift
func enterRoom() {
    let params = TRTCParams.init()
    params.sdkAppId = sdkappid
    params.userId   = userid
    params.userSig  = usersig
    params.roomId   = 908
    trtcCloud.enterRoom(params, appScene: TRTCAppScene.LIVE)
}

func onEnterRoom(_ result: Int) {
    if result > 0 {
        toastTip("Entered room successfully; the total time used is [\(result)] ms")
    } else {
        toastTip("Failed to enter the room; the error code is [\(result)]")
    }
}
```

<span id="step8"> </span>
### Step 8. The viewer enters the room to watch the live stream
1. The viewer sets the field `role` in [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) to **`TRTCRoleType.audience`**, which indicates that the current user role is viewer.
2. The viewer can call [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) to enter the audio/video room whose ID is the `roomId` field value in the `TRTCParams` parameter and specify the **`appScene`** parameter:
 - TRTCAppScene.LIVE: interactive live video streaming mode, which is used as an example in this document.
 - TRTCAppScene.voiceChatRoom: interactive live audio streaming mode.
3. View the anchor's video image:
 - If the viewer knows the anchor's `userId` in advance, the viewer can use it to call [startRemoteView(userId, view: view)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) after successfully entering the room so as to display the anchor's video image.
 - If the viewer does not know the anchor's `userId`, the viewer will receive the [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) event notification after successfully entering the room. The viewer can use the anchor's `userId` obtained from the callback to call [startRemoteView(userId, view: view)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) so as to display the anchor's video image.


<span id="step9"> </span>
### Step 9. The viewer co-anchors with the anchor
1. The viewer can call [switch(TRTCRoleType.anchor)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) to switch the role to anchor (TRTCRoleType.anchor).
2. The viewer can call [startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) to enable the local image.
3. The viewer can call [startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) to enable mic capture:

```swift
// Sample code: the viewer mics on
trtcCloud.switch(TRTCRoleType.anchor)
trtcCloud.startLocalAudio()
trtcCloud.startLocalPreview(frontCamera, view: localView)

// Sample code: the viewer mics off
trtcCloud.switch(TRTCRoleType.audience)
trtcCloud.stopLocalAudio()
trtcCloud.stopLocalPreview()
```


<span id="step10"> </span>
### Step 10. Anchors compete across rooms (cross-room co-anchoring)

In TRTC, two anchors in different rooms can use the "cross-room call" feature to engage in "cross-room co-anchoring" without the need to exit their current rooms.

1. Anchor A calls the [connectOtherRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) API. Currently, the API parameters are in JSON format, and `roomId` and `userId` of anchor B need to be spliced into a parameter in the format of `{"roomId": "978","userId": "userB"}` and then passed in to the API function.
2. After the cross-room call is successfully made, anchor A will receive the [onConnectOtherRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) event callback. At the same time, all users in both rooms will receive the [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) and [onUserAudioAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) event callbacks.
 For example, when anchor A in room "001" uses `connectOtherRoom()` to successfully call anchor B in room "002", all users in room "001" will receive the `onUserVideoAvailable(B, available: true)` and `onUserAudioAvailable(B, available: true)` callbacks of anchor B, and all users in room "002" will receive the `onUserVideoAvailable(A, available: true)` and `onUserAudioAvailable(A, available: true)` callbacks of anchor A.
3. Users in both rooms can call [startRemoteView(userId, view: view)](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) to display the video image of the anchor in the other room, and audio will be automatically played back.

```swift
// Sample code: cross-room co-anchoring
let jsonDict = [ "roomId" : "978", "userId" : "userB" ]
guard let jsonData = try? JSONSerialization.data(withJSONObject: jsonDict,
                 options: JSONSerialization.WritingOptions.prettyPrinted) else {
    fatalError("JSONSerialization failed")
}
let jsonString = String.init(data: jsonData, encoding: String.Encoding.utf8)
trtcCloud.connectOtherRoom(jsonString)
```

<span id="step11"> </span>
### Step 11. Exit the current room

Call the [exitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) method to exit the room. The SDK needs to disable and release hardware devices such as the camera and mic during room exit. Therefore, room exit is not completed as soon as the method is called. Only after the [onExitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) callback is received can the room exit be considered completed.

```swift
// Please wait for the `onExitRoom` event callback after calling the room exit method
trtcCloud.exitRoom()

func onExitRoom(_ reason: Int) {
    print("Exit room [\(roomId)]: reason[\(reason)]")
}
```

> If multiple audio/video SDKs are integrated into your application, please enable other SDKs only after receiving the `onExitRoom` callback; otherwise, hardware occupancy issues may occur.

