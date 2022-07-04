This document describes how to enter a TRTC room. Only after entering an audio/video room can a user subscribe to the audio/video streams of other users in the room or publish his or her own audio/video streams.
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

## Call Guide

[](id:step1)
### Step 1. Import the SDK and set the application permissions
Import the SDK as instructed in [iOS](https://intl.cloud.tencent.com/document/product/647/35092).

[](id:step2)
### Step 2. Create an SDK instance and set an event listener
Call the initialization API to create a TRTC object instance.
<dx-codeblock>
::: Android java
// Create an SDK instance in singleton mode and set an event listener
// Create trtc instance(singleton) and set up event listeners
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(this);
:::
::: iOS&Mac ObjC
// Create an SDK instance in singleton mode and set an event listener
// Create trtc instance(singleton) and set up event listeners
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
:::
::: Windows C++
// Create an SDK instance in singleton mode and set an event listener
// Create trtc instance (singleton) and set up event listeners
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);
:::
</dx-codeblock>

[](id:step3)
### Step 3. Listen for SDK events
You can use the `setListener` API to set callbacks and listen for errors, warnings, traffic statistics, and network quality information as well as various audio/video events during SDK operations.
<dx-codeblock>
::: Android
You can make your business class inherit **TRTCCloudListener**, reload the `onError` function, and use the **setListener** API to pass in the `this` pointer to the SDK, so as to listen for callback events from the SDK in the current class.
```java
// Listen for SDK events, and print logs for error messages such as "Current application is not authorized to use the camera"
// Listen to the "onError" event, and print logs for errors such as "Camera is not authorized"
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(this);

@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    if (errCode == TXLiteAVCode.ERR_CAMERA_NOT_AUTHORIZED) {
        Log.d(TAG, "Current application is not authorized to use the camera");
    }
}
```
:::
::: iOS&Mac ObjC
You can make your business class inherit **TRTCCloudDelegate**, reload the `onError` function, and use the **delegate** attribute of `TRTCCloud` to pass in the `this` pointer to the SDK, so as to listen for callback events from the SDK in the current class.
```ObjectiveC
// Listen for SDK events, and print logs for error messages such as "Current application is not authorized to use the camera"
// Listen to the "onError" event, and print logs for errors such as "Camera is not authorized"
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;

- (void)onError:(TXLiteAVError)errCode
         errMsg:(nullable NSString *)errMsg
        extInfo:(nullable NSDictionary *)extInfo{
    if (ERR_CAMERA_NOT_AUTHORIZED == errCode) {
        NSString *errorInfo = @"Current application is not authorized to use the camera:";
        errorInfo = [errorInfo stringByAppendingString errMsg];
        [self toastTip:errorInfo];
    }
}
```
:::
::: Windows C++
You can make your business class inherit **ITRTCCloudCallback**, reload the `onError` function, and use the **addCallback** API to pass in the `this` pointer to the SDK, so as to listen for callback events from the SDK in the current class.
```C++
// Listen for SDK events, and print logs for error messages such as "Current application is not authorized to use the camera"
// Listen to the "onError" event, and print logs for errors such as "Camera is not authorized"
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);

// Reload the `onError` function
void onError(TXLiteAVError errCode, const char* errMsg, void* extraInfo) {
    if (errCode == ERR_CAMERA_NOT_AUTHORIZED) {
        printf("Current application is not authorized to use the camera");
    }
}
```
:::
</dx-codeblock>

[](id:step4)
### Step 4. Prepare the room entry parameter `TRTCParams`
When calling the `enterRoom` API, you need to enter two key parameters: `TRTCParams` and `TRTCAppScene`.

#### Parameter 1: TRTCAppScene
This parameter is used to specify whether your application scenario is **live streaming** or **real-time call**.
- **Real-time call:**
Real-time call includes `TRTCAppSceneVideoCall` (video call) and `TRTCAppSceneAudioCall` (audio call). This mode is suitable for one-to-one audio/video calls or online meetings for up to 300 attendees.

- **Live streaming:**
Live streaming includes `TRTCAppSceneLIVE` (video live streaming) and `TRTCAppSceneVoiceChatRoom` (audio live streaming). This mode is suitable for live streaming to up to 100,000 users. However, it requires you to specify the **role** field in the `TRTCParams` parameter for users in the room: **anchor** or **audience**.

#### Parameter 2: TRTCParams
`TRTCParams` consists of many fields; however, you usually only need to pay attention to how to set the following fields:

| Parameter | Description | Remarks | Data Type | Sample Value |
|---------|---------|---------|---------|---------|
| SDKAppID | Application ID | You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>. If it doesn't exist, click **Create Application** to create an application. | Numeric | 1400000123 |
| userId | User ID | Username. It can contain only letters, digits, underscores, and hyphens. In TRTC, a user cannot use the same `userId` to enter the same room on two different devices at the same time. | String | `denny` or `123321`|
| userSig | Room entry signature | You can calculate `userSig` based on `SDKAppID` and `userId` as instructed in [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | String | eJyrVareCeYrSy1SslI... |
| roomId | Room ID | Room ID of the numeric type. To use a string-type room ID, use only the **strRoomId** field instead of the `roomId` field, as they cannot be used together. | Number | 29834 |
| strRoomId | Room ID | Room ID of the string type. Do not use `strRoomId` and `roomId` at the same time. `"123"` and `123` are considered different rooms by the TRTC backend. | String | 29834 |
| role | Role | There are two roles: anchor and audience. This field is required only when `TRTCAppScene` is set to the `TRTCAppSceneLIVE` or `TRTCAppSceneVoiceChatRoom` live streaming scenarios. | Enumeration | `TRTCRoleAnchor` or `TRTCRoleAudience`   |

>!
>- In TRTC, a user cannot use the same `userId` to enter the same room on two different devices at the same time; otherwise, there will be a conflict.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.


[](id:step5)
### Step 5. Enter the room (`enterRoom`)
After preparing the two parameters `TRTCAppScene` and `TRTCParams` described in step 4, you can call the `enterRoom` API to enter the room.

<dx-codeblock>
::: Android  Java
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(mTRTCCloudListener);

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
TRTCCloudDef.TRTCParams param = new TRTCCloudDef.TRTCParams();
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.userId = "denny";       // Replace with your own user ID  
params.roomId = 123321;        // Replace with your own room number
params.userSig = "xxx";        // Replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
mCloud.enterRoom(param, TRTCCloudDef.TRTC_APP_SCENE_LIVE);        
:::

::: iOS&Mac  objectivec
self.trtcCloud = [TRTCCloud sharedInstance];
self.trtcCloud.delegate = self;

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
TRTCParams *params = [[TRTCParams alloc] init];
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.roomId = 123321; // Replace with your own room number
params.userId = @"denny";   // Replace with your own userid  
params.userSig = @"xxx"; // Replace with your own userSig
params.role = TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
[self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
:::

::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
liteav::TRTCParams params;
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.userId = "denny";       // Replace with your own user ID  
params.roomId = 123321;        // Replace with your own room number
params.userSig = "xxx";        // Replace with your own userSig
params.role = liteav::TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
trtc_cloud_->enterRoom(params, liteav::TRTCAppSceneLIVE);        
:::
</dx-codeblock>

**Event callback**
If room entry succeeds, the SDK will call back the `onEnterRoom(result)` event. Here, `result` is a value greater than 0, indicating the time in milliseconds taken to enter the room.
If room entry fails, the SDK will also call back the `onEnterRoom(result)` event, but the value of `result` will be a negative number, indicating the error code for the room entry failure.
<dx-codeblock>
::: Android Java
// Listen for the `onEnterRoom` event of the SDK to get the room entry result
// Listen for the `onEnterRoom` event of the SDK and learn whether the room is successfully entered
@Override
public void onEnterRoom(long     result) {
    if (result > 0) {
        Log.d(TAG, "Enter room succeed");
    } else {
        Log.d(TAG, "Enter room failed");
    }
}
:::
::: iOS&Mac ObjC
// Listen for the `onEnterRoom` event of the SDK to get the room entry result
// Listen for the `onEnterRoom` event of the SDK and learn whether the room is successfully entered
- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"Enter room succeed!"];
    } else {
        [self toastTip:@"Enter room failed!"];
    }
}
:::
::: Windows C++
// Listen for the `onEnterRoom` event of the SDK to get the room entry result
// override to the onEnterRoom event of the SDK and learn whether the room is successfully entered
void onEnterRoom(int result) {
    if (result > 0) {
        printf("Enter room succeed");
    } else {
        printf("Enter room failed");
    }
}
:::
</dx-codeblock>
