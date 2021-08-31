`TRTCVideoCall` supports one-to-one and group video calls based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). It is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Call (Android)](https://intl.cloud.tencent.com/document/product/647/36066).
- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.


<h2 id="TRTCVideoCall">TRTCVideoCall API Overview</h2>

### Basic SDK APIs

| API | Description |
|-----|-----|
| [sharedInstance](#sharedinstance) | Gets component singleton. |
| [destroySharedInstance](#destroysharedinstance) | Terminates component singleton. |
| [addListener](#addlistener) | Adds event callback. |
| [removeListener](#removelistener) | Removes callback. |
| [init](#init) | Performs the required initialization before all other features can be used. |
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
| [startRemoteView](#startremoteview) | Renders the camera data of remote user in the specified `TXCloudVideoView`. |
| [stopRemoteView](#stopremoteview) | Stops rendering remote data. |

### Audio/Video control APIs

| API | Description |
|-----|-----|
| [openCamera](#opencamera) | Enables camera and renders data in the specified `TXCloudVideoView`. |
| [switchCamera](#switchcamera) | Switches between front and rear cameras. |
| [closeCamara](#closecamara) | Disables camera. |
| [setMicMute](#setmicmute) | Mutes remote audio. |
| [setHandsFree](#sethandsfree) | Sets hands-free mode. |

<h2 id="TRTCVideoCallListener">TRTCVideoCallListener API Overview</h2>

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
### sharedInstance
`sharedInstance` is the component singleton of `TRTCVideoCall`.
```java
public static ITRTCVideoCall sharedInstance(Context context);
```

### destroySharedInstance
This API is used to terminate the component singleton.
```java
public static void destroySharedInstance();
```

### init

This API is used to perform the required initialization before all other features can be used.
```java
void init();
```

### destroy

This API is used to terminate the instance when it is no longer needed.
```java
void destroy();
```

### addListener

This API is used to get the event callback of [TRTCVideoCall](https://intl.cloud.tencent.com/document/product/647/36066). You can use `TRTCVideoCallListener` to get various status notifications of [TRTCVideoCall](https://intl.cloud.tencent.com/document/product/647/36066).
```java
void addListener(TRTCVideoCallListener listener);
```

>?`TRTCVideoCallListener` is the delegation callback of `TRTCVideoCall`.

### removeListener

This API is used to remove the callback.
```java
void removeListener(TRTCVideoCallListener listener);
```

### login

This API is used to log in to the component.
```java
void login( int sdkAppId,
            final String userId, 
            String userSign, 
            final ActionCallBack callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppID | UInt32 | You can view the `SDKAppID` in the TRTC Console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| user | String | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallBack | Callback for login. `onSuccess` indicates a login success. |

### logout

This API is used to log out of the component.
```java
void logout(final ActionCallBack callBack);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callBack | ActionCallBack | Callback for logout. `onSuccess` indicates a logout success. |

## Call Operation APIs
### call

This API is used to make a one-to-one call. It can be called in an ongoing call to invite another user.

```java
void call(String userId, int type);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Caller ID. |
| type | int | 1: audio call; 2: video call. |

### groupCall

This API is used to make an IM group call. Invitees will receive the `onInvited()` callback. This API can be called in an ongoing call to invite other users, and existing users in the call will receive the `onGroupCallInviteeListUpdate()` callback.
```java
void groupCall(List<String> userIdList, int type, String groupId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userIdList | List<String> | Invitee ID list. |
| type | int | 1: audio call; 2: video call. |
| groupId | String | Group ID. |



### accept

This API is used to accept the current call. The invitee can call it to accept the call when receiving the `onInvited()` callback.
```java
void accept();
```



### reject

This API is used to decline the current call. The invitee can call it to decline the call when receiving the `onInvited()` callback.
```java
void reject();
```



### hangup

This API is used to end the current call. It can be called during an ongoing call to end it.

```java
void hangup();
```


## Push/Pull APIs
### startRemoteView

This API is used to render the camera data of remote user in the specified `TXCloudVideoView`.
```java
void startRemoteView(String userId, TXCloudVideoView txCloudVideoView);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Remote user ID. |
| view | TXCloudVideoView | Control that carries the video image. |


### stopRemoteView

This API is used to stop rendering remote data.
```java
void stopRemoteView(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Remote user ID. |

## Audio/Video Control APIs
### openCamera

This API is used to enable camera and render data in the specified `TXCloudVideoView`.
```java
void openCamera(boolean isFrontCamera, TXCloudVideoView txCloudVideoView);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isFrontCamera | boolean | true: enables front camera; false: enables rear camera. |
| view | TXCloudVideoView | Control that carries the video image. |

### switchCamera

This API is used to switch between front and rear cameras.
```java
void switchCamera(boolean isFrontCamera);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isFrontCamera | boolean | true: switches to front camera; false: switches to rear camera. |

### closeCamara

This API is used to disable the camera.
```java
void closeCamera();
```

### setMicMute

This API is used to mute the remote audio.
```java
void setMicMute(boolean isMute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMute | boolean | true: disables mic; false: enables mic. |

### setHandsFree

This API is used to mute the remote audio.
```java
void setHandsFree(boolean isHandsFree);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isHandsFree | boolean | true: enables hands-free mode; false: disables hands-free mode. |

## TRTCVideoCallListener Event Callbacks

## General Event Callbacks
### onError

Callback for error.
>?The SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions.

```java
void onError(int code, String msg);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | int | Error code. |
| msg | String | Error message. |


## Inviter Callbacks
### onReject

Callback for declined call.
```java
void onReject(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user who declines the call. |

### onNoResp

Callback for no answer.
```java
void onNoResp(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user who does not answer. |

### onLineBusy

Callback for busy line.
```java
void onLineBusy(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user whose line is busy. |

## Invitee Callbacks
### onInvited

Callback for received call.
```java
void onInvited(String sponsor, List<String> userIdList, boolean isFromGroup, int callType);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sponsor | String | Caller ID. |
| userIds | List<String> | List of invitee IDs except the local user. |
| isFromGroup | boolean | Whether it is a group call invitation. |
| type | int | 1: audio call; 2: video call. |

### onCallingCancel

Callback for current call cancellation. The invitee will receive this callback if the invitee does not process the request and then the inviter cancels the request.
```java
void onCallingCancel();
```



### onCallingTimeOut

Callback for current call timeout.
```java
void onCallingTimeout();
```

## General Callbacks
### onGroupCallInviteeListUpdate

Callback for group chat invitee list update.
```java
void onGroupCallInviteeListUpdate(List<String> userIdList);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userIdList | List<String> | Invitee ID list. |

### onUserEnter

Callback for user entering call.
```java
void onUserEnter(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user who enters the call. |

### onUserLeave

Callback for user leaving call.
```java
void onUserLeave(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user who leaves the call. |

### onUserAudioAvailable

Callback for whether audio upstreaming is enabled.
```java
void onUserAudioAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | In-call user ID. |
| available | boolean | Whether user audio is available. |

### onUserVideoAvailable

Callback for whether video upstreaming is enabled. After receiving the notification, the user can call `startRemoteView` to render the remote video image.
```java
void onUserVideoAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | In-call user ID. |
| available | boolean | Whether user video is available. |


### onUserVoiceVolume

Callback for user call volume level.
```java
void onUserVoiceVolume(Map<String, Integer> volumeMap);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volumeMap | Map<String, Integer> | Volume level table. The corresponding volume level can be obtained by each `userid`. The volume level ranges from 0 to 100. |

### onCallEnd

Callback for call end.
```java
void onCallEnd();
```
