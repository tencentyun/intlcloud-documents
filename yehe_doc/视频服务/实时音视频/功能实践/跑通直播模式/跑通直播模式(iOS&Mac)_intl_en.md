## Use Cases
TRTC supports four room entry modes. Video call (`VideoCall`) and audio call (`VoiceCall`) are the [call modes](https://intl.cloud.tencent.com/document/product/647/35102), and interactive video streaming (`Live`) and interactive audio streaming (`VoiceChatRoom`) are the live streaming modes.
The live streaming modes allow a maximum of 100,000 concurrent users in each room with smooth mic on/off. Co-anchoring latency is kept below 300 ms and watch latency below 1,000 ms. The live streaming modes are suitable for use cases such as low-latency interactive live streaming, interactive classrooms for up to 100,000 participants, video dating, online education, remote training, and mega-scale conferencing.

## How It Works
TRTC services use two types of server nodes: access servers and proxy servers.
- **Access server**
This type of nodes use high-quality lines and high-performance servers and are better suited to drive low-latency end-to-end calls, but the unit cost is relatively high.
- **Proxy server**
This type of servers use mediocre lines and average-performance servers and are better suited to power high-concurrency stream pulling and playback. The unit cost is relatively low.

In the live streaming modes, TRTC has introduced the concept of "role". Users are either in the role of "anchor" or "audience". Anchors are assigned to access servers, and audience to proxy servers. Each room allows up to 100,000 users in the role of audience.
For audience to speak, they must switch the role (`switchRole`) to “anchor”. The switching process involves users being migrated from proxy servers to access servers. TRTC’s low-latency streaming and smooth mic on/off technologies help keep this process short.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code
You can visit [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC) to obtain the sample code used in this document.
![](https://main.qcloudimg.com/raw/91ba84ef5cee887717ba69e97d939fcd.png)

>?If your access to GitHub is slow, download the ZIP file [here](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip).


## Directions
[](id:step1)
### Step 1. Integrate the SDKs
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

1. Call the [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35119) API to create a `TRTCCloud` instance.
<dx-codeblock>
::: iOS object-c
// Create a `TRTCCloud` instance
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
:::
</dx-codeblock>
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

| Parameter | Type | Description | Example |
|---------|---------|---------|---------|
| sdkAppId | Number | Application ID, which you can view in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>. |1400000123 |
| userId | String | Only letters (a-z and A-Z), digits (0-9), underscores, and hyphens are allowed. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Number | Numeric room ID. For string-type room ID, use `strRoomId` in `TRTCParams`. | 29834 |

>! 
>-In TRTC, users with the same `userId` cannot be in the same room at the same time as it will cause a conflict.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.


[](id:step5)
### Step 5. Enable camera preview and mic capturing
1. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) to enable preview of the local camera. The SDK will ask for camera permission.
2. Call [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) to set the display mode of the local video image:
 - `Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
 - `Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
3. Call [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) to set the encoding parameters for the local video, which determine the [quality of your video](https://intl.cloud.tencent.com/document/product/647/35153) seen by other users in the room.
4. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) to turn the mic on. The SDK will ask for mic permission.

<dx-codeblock>
::: iOS object-c
// Sample code: publish the local audio/video stream
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];

// Set local video encoding parameters
TRTCVideoEncParam *encParams = [TRTCVideoEncParam new];
encParams.videoResolution = TRTCVideoResolution_640_360;
encParams.videoBitrate = 550;
encParams.videoFps = 15;
    
[self.trtcCloud setVideoEncoderParam:encParams];
:::
</dx-codeblock>

[](id:step6)
### Step 6. Sets beauty filters

1. Call [getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) to get the beauty filter management class [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager).
2. Call [setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a) to set the beauty filter style.
 - `Smooth`: smooth. This style features more obvious skin smoothing effect and is typically used by influencers.
 - `Nature`: natural. This style retains more facial details and is more natural.
 - `Pitu`: This style is supported only in the [Enterprise Edition](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise).
3. Call [setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#af864d9466d5161e1926e47bae0e3f027) to set the skin smoothing strength (`5` is recommended).
4. Call [setWhitenessLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a199b265f6013e0cca0ff99f731d60ff4) to set the skin brightening strength (`5` is recommended).
5. Given the yellow tint of the iPhone camera, we recommended that you call [setFilter()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) to apply the skin brightening filter to your video. You can download the file for the filter [here](https://liteav.sdk.qcloud.com/doc/res/trtc/filter/filterPNG.zip).



[](id:step7)
### Step 7. Create a room and push streams
1. Set the `role` field in [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) to **`TRTCRoleType.anchor`** to take the role of “anchor”.
2. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d), specifying **`appScene`**, and a room whose ID is the value of the `roomId` field in `TRTCParams` will be created.
 - `TRTCAppScene.LIVE`: the interactive video streaming mode, which is used in the example of this document
 - `TRTCAppScene.voiceChatRoom`: the interactive audio streaming mode
3. After the room is created, start encoding and transferring audio/video data. The SDK will return the [onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) callback. If `result` is greater than 0, room entry succeeds, and the value indicates the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.

<dx-codeblock>
::: iOS object-c
- (void)enterRoom() {
    TRTCParams *params = [TRTCParams new];
    params.sdkAppId = SDKAppID;
    params.roomId = _roomId;
    params.userId = _userId;
    params.role = TRTCRoleAnchor;
    params.userSig = [GenerateTestUserSig genTestUserSig:params.userId];
    [self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
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

[](id:step8)
### Step 8. Enter the room as audience
1. Set the `role` field in [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) to **`TRTCRoleType.audience`** to take the role of “audience”.
2. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) to enter the room whose ID is the value of the `roomId` field in `TRTCParams`, specifying **`appScene`**.
 - `TRTCAppScene.LIVE`: the interactive video streaming mode, which is used in the example of this document
 - `TRTCAppScene.voiceChatRoom`: the interactive audio streaming mode
3. Watch the anchor’s video:
 - If you know the anchor’s `userId`, call [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) with the anchor’s `userId` passed in to play the anchor's video.
 - If you do not know the anchor’s `userId`, find the anchor’s `userId` in the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) callback, which you will receive after room entry, and call [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) with the anchor’s `userId` passed in to play the anchor’s video.


[](id:step9)
### Step 9. Co-anchor
1. Call [switch(TRTCRoleType.TRTCRoleAnchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) to switch the role to “anchor” (`TRTCRoleType.TRTCRoleAnchor`).
2. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) to enable preview of the local image.
3. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) to enable mic capturing.

<dx-codeblock>
::: iOS object-c
// Sample code: start co-anchoring
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];

// Sample code: end co-anchoring
[self.trtcCloud switchRole:TRTCRoleAudience];
[self.trtcCloud stopLocalAudio];
[self.trtcCloud stopLocalPreview]
:::
</dx-codeblock>

[](id:step10)
### Step 10. Compete across rooms

Anchors from two rooms can compete with each other without exiting their current rooms.

1. Anchor A calls the [connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) API. The API uses parameters in JSON strings, so anchor A needs to pass the `roomId` and `userId` of anchor B in the format of `{"roomId": 978,"userId": "userB"}` to the API.
2. After the cross-room call is set up, anchor A will receive the [onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) callback, and all users in both rooms will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) and [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) callbacks.
 For example, after anchor A in room "001" uses `connectOtherRoom()` to call anchor B in room “002” successfully all users in room "001" will receive the `onUserVideoAvailable(B, available: true)` and `onUserAudioAvailable(B, available: true)` callbacks, and all users in room "002" will receive the `onUserVideoAvailable(A, available: true)` and `onUserAudioAvailable(A, available: true)` callbacks.
3. Users in both rooms can call [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) to play the video of the anchor in the other room, and audio will be played back automatically.

<dx-codeblock>
::: iOS object-c
// Sample code: cross-room competition
NSMutableDictionary * jsonDict = [[NSMutableDictionary alloc] init];
[jsonDict setObject:@([_otherRoomIdTextField.text intValue]) forKey:@"roomId"];
[jsonDict setObject:_otherUserIdTextField.text forKey:@"userId"];
NSData* jsonData = [NSJSONSerialization dataWithJSONObject:jsonDict options:NSJSONWritingPrettyPrinted error:nil];
NSString* jsonString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[self.trtcCloud connectOtherRoom:jsonString];
:::
</dx-codeblock>

[](id:step11)
### Step 11. Exit the room

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

>! If your application integrates multiple audio/video SDKs, please wait after you receive the `onExitRoom` callback to start other SDKs; otherwise, the device busy error may occur.

