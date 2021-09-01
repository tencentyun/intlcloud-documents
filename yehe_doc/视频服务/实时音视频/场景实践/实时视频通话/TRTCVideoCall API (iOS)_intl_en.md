`TRTCVideoCall` supports one-to-one and group video calls based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). It is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Call (iOS)](https://intl.cloud.tencent.com/document/product/647/36065).
- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.


<h2 id="TRTCVideoCall">TRTCVideoCall API Overview</h2>

### Basic SDK APIs

| API | Description |
|-----|-----|
| [shared](#shared) | Gets component singleton. |
| [delegate](#delegate) | Sets event callback. |
| [setup](#setup) | Performs the required initialization before all other features can be used. |
| [destroy](#destroy) | Terminates instance when it is no longer needed. |
| [login](#login) | Logs in. All other features can be used only after login. |
| [logout](#logout) | Logs out. Calls cannot be made after logout. |


### Call operation APIs

| API | Description |
|-----|-----|
| [call](#call) | Makes one-to-one call. |
| [groupCall](#groupcall) | Makes group chat call. |
| [accept](#accept) | Accepts the current call. |
| [reject](#reject) | Declines the current call. |
| [hangup](#hangup) | Ends the current call. |

### Push/Pull APIs
| API | Description |
|-----|-----|
| [startRemoteView](#startremoteview) | Renders the camera data of remote user in the specified `UIView`. |
| [stopRemoteView](#stopremoteview) | Stops rendering remote data. |

### Audio/Video control APIs

| API | Description |
|-----|-----|
| [openCamera](#opencamera) | Enables camera and renders data in the specified `UIView`. |
| [switchCamera](#switchcamera) | Switches between front and rear cameras. |
| [closeCamara](#closecamara) | Disables camera. |
| [setMicMute](#setmicmute) | Mutes remote audio. |
| [setHandsFree](#sethandsfree) | Sets hands-free mode. |

<h2 id="TRTCVideoCallDelegate">TRTCVideoCallDelegate API Overview</h2>

### General event callbacks

| API | Description |
|-----|-----|
| [onError](#onerror) | Callback for error. |

### Inviter callbacks

| API | Description |
|-----|-----|
| [onReject](#onreject) | Callback for declined call. |
| [onNoResp](#onnoresp) | Callback for no answer. |
| [onLineBusy](#onlinebusy) | Callback for busy line. |

### Invitee callbacks

| API | Description |
|-----|-----|
| [onInvited](#oninvited) | Callback for received call. |
| [onCallingCancel](#oncallingcancel) | Callback for current call cancellation. |
| [onCallingTimeOut](#oncallingtimeout) | Callback for current call timeout. |

### General callbacks

| API | Description |
|-----|-----|
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | Callback for group chat invitee list update. |
| [onUserEnter](#onuserenter) | Callback for user entering call. |
| [onUserLeave](#onuserleave) | Callback for user leaving call. |
| [onUserAudioAvailable](#onuseraudioavailable) | Callback for whether audio upstreaming is enabled. |
| [onUserVideoAvailable](#onuservideoavailable) | Callback for whether video upstreaming is enabled. |
| [onUserVoiceVolume](#onuservoicevolume) | Callback for user call volume level. |
| [onCallEnd](#oncallend) | Callback for call end. |

## Basic SDK APIs
### shared
`shared` is the component singleton of `TRTCVideoCall`.
```swift
@objc public static let shared = TRTCVideoCall()
```


### delegate

This API is used to get the event callback of [TRTCVideoCall](https://intl.cloud.tencent.com/document/product/647/36065). You can use `TRTCVideoCallDelegate` to get various status notifications of [TRTCVideoCall](https://intl.cloud.tencent.com/document/product/647/36065).
```swift
@objc public weak var delegate: TRTCVideoCallDelegate?
```

>?`delegate` is the delegation callback of `TRTCVideoCall`.

### setup

This API is used to perform the required initialization before all other features can be used.
```swift
@objc public func setup()
```
### destroy

This API is used to terminate the instance when it is no longer needed.
```swift
@objc func destroy()
```

### login

This API is used to log in to the component.
```swift
@objc func login(sdkAppID: UInt32,
                 user: String,
                 userSig: String,
                 success: @escaping (() -> Void),
                 failed: @escaping ((_ code: Int, _ message: String) -> Void))
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppID | UInt32 | You can view the `SDKAppID` in the TRTC Console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| user | String | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| success | (() -> Void) | Callback for login success. |
| failed | ((_ code: Int, _ message: String) -> Void) | Callback for login failure. |

### logout

This API is used to log out of the component.
```swift
@objc func logout(success: @escaping (() -> Void),
           failed: @escaping ((_ code: Int, _ message: String) -> Void))
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| success | (() -> Void) | Callback for logout success. |
| failed | ((_ code: Int, _ message: String) -> Void) | Callback for logout failure. |


## Call Operation APIs
### call

This API is used to make a one-to-one call. It can be called in an ongoing call to invite another user.

```swift
@objc func call(userID: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | Caller ID. |

### groupCall

This API is used to make an IM group call. Invitees will receive the `onInvited()` callback. This API can be called in an ongoing call to invite other users, and existing users in the call will receive the `onGroupCallInviteeListUpdate()` callback.
```swift
@objc func groupCall(userIDs: [String], groupID: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userIDs | [String] | Invitee ID list. |
| groupID | String | Group ID. |



### accept

This API is used to accept the current call. The invitee can call it to accept the call when receiving the `onInvited()` callback.
```swift
@objc func accept()
```



### reject

This API is used to decline the current call. The invitee can call it to decline the call when receiving the `onInvited()` callback.
```swift
@objc func reject()
```



### hangup

This API is used to end the current call. It can be called during an ongoing call to end it.

```swift
@objc func hangup()
```


## Push/Pull APIs
### startRemoteView

This API is used to render the camera data of remote user in the specified `UIView`.
```swift
@objc func startRemoteView(userId: String, view: UIView)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Remote user ID. |
| view | UIView | Control that carries the video image. |


### stopRemoteView

This API is used to stop rendering remote data.
```swift
@objc func stopRemoteView(userId: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Remote user ID. |

## Audio/Video Control APIs
### openCamera

This API is used to enable camera and render data in the specified `UIView`.
```swift
@objc func openCamera(frontCamera: Bool, view: UIView)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| frontCamera | Bool | true: enables front camera; false: enables rear camera. |
| view | UIView | Control that carries the video image. |

### switchCamera

This API is used to switch between front and rear cameras.
```swift
@objc func switchCamera(frontCamera: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| frontCamera | Bool | true: switches to front camera; false: switches to rear camera. |

### closeCamara

This API is used to disable the camera.
```swift
@objc func closeCamara()
```

### setMicMute

This API is used to mute the remote audio.
```swift
@objc func setMicMute(isMute: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMute | Bool | true: disables mic; false: enables mic. |

### setHandsFree

This API is used to mute the remote audio.
```swift
@objc func setHandsFree(isHandsFree: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isHandsFree | Bool | true: enables hands-free mode; false: disables hands-free mode. |

## TRTCVideoCallDelegate Event Callbacks

## General Event Callbacks
### onError

Callback for error.
>?The SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions.

```swift
@objc optional func onError(code: Int32, msg: String?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | Int | Error code. |
| msg | String? | Error message. |


## Inviter Callbacks
### onReject

Callback for declined call.
```swift
@objc optional func onReject(uid: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | ID of the user who declines the call. |

### onNoResp

Callback for no answer.
```swift
@objc optional func onNoResp(uid: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | ID of the user who does not answer. |

### onLineBusy

Callback for busy line.
```swift
@objc optional func onLineBusy(uid: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | ID of the user whose line is busy. |

## Invitee Callbacks
### onInvited

Callback for received call.
```swift
@objc optional func onInvited(sponsor: String, userIds: [String], isFromGroup: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sponsor | String | Caller ID. |
| userIds | [String] | Invitee ID list. |
| isFromGroup | Bool | Whether it is a group call invitation. |

### onCallingCancel

Callback for current call cancellation. The invitee will receive this callback if the invitee does not process the request and then the inviter cancels the request.
```swift
@objc optional func onCallingCancel()
```



### onCallingTimeOut

Callback for current call timeout.
```swift
@objc optional func onCallingTimeOut()
```

## General Callbacks
### onGroupCallInviteeListUpdate

Callback for group chat invitee list update.
```swift
@objc optional func onGroupCallInviteeListUpdate(userIds: [String])
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userIds | [String] | Invitee ID list. |

### onUserEnter

Callback for user entering call.
```swift
@objc optional func onUserEnter(uid: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | ID of the user who enters the call. |

### onUserLeave

Callback for user leaving call.
```swift
@objc optional func onUserLeave(uid: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | ID of the user who leaves the call. |

### onUserAudioAvailable

Callback for whether audio upstreaming is enabled.
```swift
@objc optional func onUserAudioAvailable(uid: String, available: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | In-call user ID. |
| available | Bool | Whether user audio is available. |

### onUserVideoAvailable

Callback for whether video upstreaming is enabled. After receiving the notification, the user can call `startRemoteView` to render the remote video image.
```swift
@objc optional func onUserVideoAvailable(uid: String, available: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | In-call user ID. |
| available | Bool | Whether user video is available. |


### onUserVoiceVolume

Callback for user call volume level.
```swift
@objc optional func onUserVoiceVolume(uid: String, volume: UInt32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| uid | String | In-call user ID. |
| volume | UInt32 | Volume level of the speaking user. Value range: 0–100. |

### onCallEnd

Callback for call end.
```swift
@objc optional func onCallEnd()
```
