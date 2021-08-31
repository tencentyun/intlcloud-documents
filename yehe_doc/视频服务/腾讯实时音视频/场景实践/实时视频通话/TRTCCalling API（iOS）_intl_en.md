`TRTCCalling` supports one-to-one and group video/audio calls based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). It is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [iOS](https://intl.cloud.tencent.com/document/product/647/36065).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.


<h2 id="TRTCCalling">TRTCCalling API Overview</h2>

### Basic SDK APIs

| API | Description |
| ------------------------------- | ------------------------------------------------ |
| [shareInstance](#shareinstance) | Gets component singleton. |
| [addDelegate](#adddelegate) | Sets event callback. |
| [login](#login) | Logs in. All other features can be used only after login. |
| [logout](#logout) | Logs out. Calls cannot be made after logout. |


### Call operation APIs

| API | Description |
| ----------------------- | -------------- |
| [call](#call)           | Makes one-to-one call. |
| [groupCall](#groupcall) | Makes group call. |
| [accept](#accept)       | Accepts the current call. |
| [reject](#reject)       | Declines the current call. |
| [hangup](#hangup)       | Ends the current call. |

### Push/Pull APIs

| API | Description |
| ----------------------------------- | -------------------------------------------- |
| [startRemoteView](#startremoteview) | Renders the camera data of remote user in the specified `UIView`. |
| [stopRemoteView](#stopremoteview)   | Stops rendering remote data.                                     |

### Audio/Video control APIs

| API | Description |
| ----------------------------- | -------------------------------------- |
| [openCamera](#opencamera) | Enables camera and renders data in the specified `UIView`. |
| [switchCamera](#switchcamera) | Switches between front and rear cameras.                                  |
| [closeCamara](#closecamara)   | Disables camera.                                     |
| [setMicMute](#setmicmute)     | Mutes local audio capturing.                                   |
| [setHandsFree](#sethandsfree) | Sets hands-free mode.                                       |

<h2 id="TRTCCallingDelegate">TRTCCallingDelegate API Overview</h2>

### General event callbacks

| API | Description |
| ------------------- | ---------- |
| [onError](#onerror) | Callback for error. |

### Inviter callbacks

| API | Description |
| ------------------------- | ---------------- |
| [onReject](#onreject)     | Callback for declined call. |
| [onNoResp](#onnoresp)     | Callback for no answer. |
| [onLineBusy](#onlinebusy) | Callback for busy line. |

### Invitee callbacks

| API | Description |
| ------------------------------------- | -------------------- |
| [onInvited](#oninvited)               | Callback for received call.     |
| [onCallingCancel](#oncallingcancel)   | Callback for current call cancellation. |
| [onCallingTimeOut](#oncallingtimeout) | Callback for current call timeout. |

### General callbacks

| API | Description |
| ------------------------------------------------------------ | -------------------------- |
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | Callback for group chat invitee list update.     |
| [onUserEnter](#onuserenter)                                  | Callback for user entering call.         |
| [onUserLeave](#onuserleave)                                  | Callback for user leaving call.         |
| [onUserAudioAvailable](#onuseraudioavailable)                | Callback for whether audio upstreaming is enabled. |
| [onUserVideoAvailable](#onuservideoavailable)                | Callback for whether video upstreaming is enabled. |
| [onUserVoiceVolume](#onuservoicevolume)                      | Callback for user call volume level.         |
| [onCallEnd](#oncallend)                                      | Callback for call end.             |

## Basic SDK APIs

### shareInstance

`shareInstance` is the component singleton of `TRTCCalling`.

```Objective-C
/// Singleton object
+ (TRTCCalling *)shareInstance;
```


### addDelegate

This API is used to get the event callback of [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36065). You can use `TRTCCallingDelegate` to get various status notifications of [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36065).

```Objective-C
/// Set `TRTCCallingDelegate` callback
/// @param delegate   Callback instance
- (void)addDelegate:(id<TRTCCallingDelegate>)delegate;
```

### login

This API is used to log in to the component.

```Objective-C
typedef void(^CallingActionCallback)(void);
typedef void(^ErrorCallback)(int code, NSString *des);

/// Login API
/// @param sdkAppID   SDK ID, which can be obtained in the Tencent Cloud Console
/// @param userID   User ID
/// @param userSig   User signature
/// @param success   Callback for success
/// @param failed   Callback for failure
- (void)login:(UInt32)sdkAppID
         user:(NSString *)userID
      userSig:(NSString *)userSig
      success:(CallingActionCallback)success
       failed:(ErrorCallback)failed
NS_SWIFT_NAME(login(sdkAppID:user:userSig:success:failed:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------------------- | ------------------------------------------------------------ |
| sdkAppID | UInt32 | You can view the `SDKAppID` in the TRTC Console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| user | String | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| success  | CallingActionCallback | Callback for login success. |
| failed   | ErrorCallback         | Callback for login failure. |

### logout

This API is used to log out of the component.

```Objective-C
/// Logout API
/// @param success   Callback for success
/// @param failed   Callback for failure
- (void)logout:(CallingActionCallback)success
        failed:(ErrorCallback)failed
NS_SWIFT_NAME(logout(success:failed:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | --------------------- | -------------- |
| success | CallingActionCallback | Callback for logout success. |
| failed  | ErrorCallback         | Callback for logout failure. |


## Call Operation APIs

### call

This API is used to make a one-to-one call. It can be called in an ongoing call to invite another user.

```Objective-C
/// One-to-one call initiation API
/// @param userID   Invitee ID
/// @param type   Call type: video/audio
- (void)call:(NSString *)userID
        type:(CallType)type
NS_SWIFT_NAME(call(userID:type:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | -------- | --------------------- |
| userID | String | Caller ID. |
| type   | CallType | Call type: video/audio. |

### groupCall

This API is used to make an IM group call. Invitees will receive the `onInvited` callback. This API can be called in an ongoing call to invite other users, and existing users in the call will receive the `onGroupCallInviteeListUpdate` callback.

```Objective-C
/// Initiate a multi-person call
/// @param userIDs   Invitee ID list
/// @param type   Call type: video/audio
/// @param groupID   Group ID, which is optional
- (void)groupCall:(NSArray *)userIDs
             type:(CallType)type
          groupID:(NSString * _Nullable)groupID
NS_SWIFT_NAME(groupCall(userIDs:type:groupID:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | -------- | --------------------- |
| userIDs | [String] | Invitee ID list. |
| type    | CallType | Call type: video/audio. |
| groupID | String | Group ID. |



### accept

This API is used to accept the current call. The invitee can call it to accept the call when receiving the `onInvited` callback.

```Objective-C
/// Accept the current call
- (void)accept;
```



### reject

This API is used to decline the current call. The invitee can call it to decline the call when receiving the `onInvited` callback.

```Objective-C
/// Decline the current call
- (void)reject;
```



### hangup

This API is used to end the current call. It can be called during an ongoing call to end it.

```Objective-C
/// End the call actively
- (void)hangup;
```


## Push/Pull APIs

### startRemoteView

This API is used to render the camera data of remote user in the specified `UIView`.

```Objective-C
/// Enable remote user video rendering
- (void)startRemoteView:(NSString *)userId view:(UIView *)view
NS_SWIFT_NAME(startRemoteView(userId:view:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------------- |
| userId | String | Remote user ID. |
| view | UIView | Control that carries the video image. |


### stopRemoteView

This API is used to stop rendering remote data.

```Objective-C
/// Disable remote user video rendering
- (void)stopRemoteView:(NSString *)userId
NS_SWIFT_NAME(stopRemoteView(userId:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------- |
| userId | String | Remote user ID. |

## Audio/Video Control APIs

### openCamera

This API is used to enable camera and render data in the specified `UIView`.

```Objective-C
/// Enable camera
- (void)openCamera:(BOOL)frontCamera view:(UIView *)view
NS_SWIFT_NAME(openCamera(frontCamera:view:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ------ | --------------------------------------------- |
| frontCamera | Bool | true: enables front camera; false: enables rear camera. |
| view | UIView | Control that carries the video image. |

### switchCamera

This API is used to switch between front and rear cameras.

```Objective-C
/// Switch camera
- (void)switchCamera:(BOOL)frontCamera;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ---- | ------------------------------------------------- |
| frontCamera | Bool | true: switches to front camera; false: switches to rear camera. |

### closeCamara

This API is used to disable the camera.

```Objective-C
/// Disable camera
- (void)closeCamara;
```

### setMicMute

This API is used to mute the local audio capturing.

```Objective-C
/// Mute
- (void)setMicMute:(BOOL)isMute;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------- |
| isMute | Bool | true: disables mic; false: enables mic. |

### setHandsFree

This API is used to enable the hands-free mode.

```Objective-C
/// Enable hands-free mode
- (void)setHandsFree:(BOOL)isHandsFree;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ---- | --------------------------------- |
| isHandsFree | Bool | true: enables hands-free mode; false: disables hands-free mode. |

## TRTCCallingDelegate Event Callback

## General Event Callbacks

### onError

Callback for error.

>?The SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions.

```Objective-C
/// An error occurred inside the SDK | SDK error
/// - Parameters:
///   - code: error code
///   - msg: error message
-(void)onError:(int)code msg:(NSString * _Nullable)msg
NS_SWIFT_NAME(onError(code:msg:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ---------- |
| code | Int | Error code. |
| msg | String? | Error message. |


## Inviter Callbacks

### onReject

Callback for declined call.

```Objective-C
/// Callback for call rejection - only the inviter will be notified; for other users, `onUserEnter` should be used |
/// reject callback only worked for Sponsor, others should use onUserEnter)
/// - Parameter uid: userid
-(void)onReject:(NSString *)uid
NS_SWIFT_NAME(onReject(uid:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------ | --------------- |
| uid | String | ID of the user who declines the call. |

### onNoResp

Callback for no answer.

```Objective-C
/// Callback for no answer - only the inviter will be notified; for other users, `onUserEnter` should be used |
/// no response callback only worked for Sponsor, others should use onUserEnter)
/// - Parameter uid: userid
-(void)onNoResp:(NSString *)uid
NS_SWIFT_NAME(onNoResp(uid:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------ | ----------------- |
| uid | String | ID of the user who does not answer. |

### onLineBusy

Callback for busy line.

```Objective-C
/// Callback for busy line - only the inviter will be notified; for other users, `onUserEnter` should be used |
/// linebusy callback only worked for Sponsor, others should use onUserEnter
/// - Parameter uid: userid
-(void)onLineBusy:(NSString *)uid
NS_SWIFT_NAME(onLineBusy(uid:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------ | --------------- |
| uid | String | ID of the user whose line is busy. |

## Invitee Callbacks

### onInvited

Callback for received call.

```Objective-C
/// Callback for received call | invitee callback
/// - Parameter userIds: invitee ID list (invited list)
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType
NS_SWIFT_NAME(onInvited(sponsor:userIds:isFromGroup:callType:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | -------- | --------------------- |
| sponsor | String | Caller ID. |
| userIds | [String] | Invitee ID list. |
| isFromGroup | Bool | Whether it is a group call invitation. |
| callType    | CallType | Call type: video/audio. |

### onCallingCancel

Callback for current call cancellation. The invitee will receive this callback if the invitee does not process the request and then the inviter cancels the request.

```Objective-C
/// Callback for current call cancellation | current call had been canceled callback
-(void)onCallingCancel:(NSString *)uid
NS_SWIFT_NAME(onCallingCancel(uid:));
```



### onCallingTimeOut

Callback for current call timeout.

```Objective-C
/// Callback for current call timeout | timeout callback
-(void)onCallingTimeOut;
```

## General Callbacks

### onGroupCallInviteeListUpdate

Callback for group chat invitee list update.

```Objective-C
/// Callback for group chat invitee list update | update current inviteeList in group calling
/// - Parameter userIds: invitee ID list | inviteeList
-(void)onGroupCallInviteeListUpdate:(NSArray *)userIds
NS_SWIFT_NAME(onGroupCallInviteeListUpdate(userIds:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | -------- | -------------- |
| userIds | [String] | Invitee ID list. |

### onUserEnter

Callback for user entering call.

```Objective-C
/// Callback for entering call | user enter room callback
/// - Parameter uid: userid
-(void)onUserEnter:(NSString *)uid
NS_SWIFT_NAME(onUserEnter(uid:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------ | ----------------- |
| uid | String | ID of the user who enters the call. |

### onUserLeave

Callback for user leaving call.

```Objective-C
/// Callback for leaving call | user leave room callback
/// - Parameter uid: userid
-(void)onUserLeave:(NSString *)uid
NS_SWIFT_NAME(onUserLeave(uid:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------ | ----------------- |
| uid | String | ID of the user who leaves the call. |

### onUserAudioAvailable

Callback for whether audio upstreaming is enabled.

```Objective-C
/// Callback for whether audio upstreaming is enabled | is user audio available callback
/// - Parameters:
///   - uid: user ID | userID
///   - available: whether it is available | available
-(void)onUserAudioAvailable:(NSString *)uid available:(BOOL)available
NS_SWIFT_NAME(onUserAudioAvailable(uid:available:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ------------------ |
| uid | String | In-call user ID. |
| available | Bool | Whether user audio is available. |

### onUserVideoAvailable

Callback for whether video upstreaming is enabled. After receiving the notification, the user can call `startRemoteView` to render the remote video image.

```Objective-C
/// Callback for whether video upstreaming is enabled | is user video available callback
/// - Parameters:
///   - uid: user ID | userID
///   - available: whether it is available | available
-(void)onUserVideoAvailable:(NSString *)uid available:(BOOL)available
NS_SWIFT_NAME(onUserVideoAvailable(uid:available:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ------------------ |
| uid | String | In-call user ID. |
| available | Bool | Whether user video is available. |


### onUserVoiceVolume

Callback for user call volume level.

```Objective-C
/// Callback for user volume level
/// - Parameter uid: user ID | userID
/// - Parameter volume: volume level of the speaking user. Value range: 0–100
-(void)onUserVoiceVolume:(NSString *)uid volume:(UInt32)volume
NS_SWIFT_NAME(onUserVoiceVolume(uid:volume:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------------- |
| uid | String | In-call user ID. |
| volume | UInt32 | Volume level of the speaking user. Value range: 0–100. |

### onCallEnd

Callback for call end.

```Objective-C
/// Callback for call end | end callback
-(void)onCallEnd;
```
