## TUICallEngine APIs

`TUICallEngine` is an audio/video call component that **does not include UI elements**. If `TUICallKit` does not meet your requirements, you can use the APIs of `TUICallEngine` to customize your project.

## Overview

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](#createinstance)                            | Creates a `TUICallEngine` instance (singleton mode). |
| [destroyInstance](#destroyinstance)                          | Terminates a `TUICallEngine` instance (singleton mode). |
| [init](#init) | Authenticates the basic audio/video call capabilities.                                |
| [addObserver](#addobserver) | Registers an event listener.                                                |
| [removeObserver](#removeobserver) | Unregisters an event listener.                                                |
| [call](#call) | Makes a one-to-one call.                                               |
| [groupCall](#groupcall) | Makes a group call.                                                |
| [accept](#accept) | Accepts a call. |
| [reject](#reject) | Rejects a call. |
| [hangup](#hangup) | Ends a call.                                                    |
| [ignore](#ignore) | Ignores a call.                                                    |
| [inviteUser](#inviteuser) | Invites users to the current group call.                                |
| [joinInGroupCall](#joiningroupcall) | Joins a group call.                                    |
| [switchCallMediaType](#switchcallmediatype) | Changes the call type, for example, from video call to audio call.                    |
| [startRemoteView](#startremoteview) | Subscribes to the video stream of a remote user.                                      |
| [stopRemoteView](#stopremoteview) | Unsubscribes from the video stream of a remote user.                                     |
| [openCamera](#opencamera) | Turns the camera on.         |
| [closeCamera](#closecamera) | Turns the camera off.         |
| [switchCamera](#switchcamera) | Switches between the front and rear cameras. |
| [openMicrophone](#openmicrophone) | Turns the mic on.                                                  |
| [closeMicrophone](#closemicrophone) | Turns the mic off.                                                  |
| [selectAudioPlaybackDevice](#selectaudioplaybackdevice) | Selects the audio playback device (receiver or speaker).                             |
| [setSelfInfo](#setselfinfo) | Sets the alias and profile photo.                                        |
| [enableMultiDeviceAbility](#enablemultideviceability) | Sets whether to enable multi-device login for `TUICallEngine` (supported by the premium package). |

## Details

### createInstance

This API is used to create a `TUICallEngine` singleton.

```objectivec
- (TUICallEngine *)createInstance;
```

### destroyInstance

This API is used to terminate a `TUICallEngine` singleton.

```objectivec
- (void)destroyInstance;
```

### Init

This API is used to initialize `TUICallEngine`. Call it to authenticate the call service and perform other required actions before you call other APIs.

```objectivec
- (void)init:(NSString *)sdkAppID userId:(NSString *)userId userSig:(NSString *)userSig succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppID | int | You can view `SDKAppID` in [Application Management](https://console.cloud.tencent.com/trtc/app) > **Application Info** of the TRTC console. |
| userId | String | The ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). |
| userSig | String | Tencent Cloud's proprietary security signature. For how to calculate and use it, see [UserSig](https://www.tencentcloud.com/document/product/647/35166). |
| callback | TUIDefine.Callback | The initialization callback. `onSuccess` indicates initialization is successful.                        |

### addObserver

This API is used to register an event listener to listen for `TUICallObserver` events.

```objectivec
- (void)addObserver:(id<TUICallObserver>)observer;
```

### removeObserver

This API is used to unregister an event listener.

```objectivec
- (void)removeObserver:(id<TUICallObserver>)observer;
```

### call

This API is used to make a (one-to-one) call.

```objectivec
- (void)call:(TUIRoomId *)roomId userId:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

The parameters are described below:

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| userId        | NSString         | The target user ID.                                            |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |
| params        | TUICallParams    | An additional parameter. For example, you can use it to customize an offline notification.                   |

### groupCall

This API is used to make a group call. Note that you need to create an IM group before making a group call.

```objectivec
- (void)groupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId userIdList:(NSArray <NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType params:(TUICallParams *)params succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| groupId       | NSString                  | The group ID.                                          |
| userIdList    | NSArray          | The target user IDs.                                       |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |
| params        | TUICallParams    | An additional parameter. For example, you can use it to customize an offline notification.                   |

### accept

This API is used to accept a call. After receiving the `onCallReceived()` callback, you can call this API to accept the call.

```objectivec
- (void)accept:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### reject

This API is used to reject a call. After receiving the `onCallReceived()` callback, you can call this API to reject the call.

```objectivec
- (void)reject:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### ignore

This API is used to ignore a call. After receiving the `onCallReceived()`, you can call this API to ignore the call. The caller will receive the `onUserLineBusy` callback. If your project involves live streaming or conferencing, you can also use this API to implement the “in a meeting” or “on air” feature.

```objectivec
- (void)ignore:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### hangup

This API is used to end a call.

```objectivec
- (void)hangup:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### inviteUser

This API is used by a participant of a group call to invite users to the call.

```objectivec
- (void)inviteUser:(NSArray<NSString *> *)userIdList params:(TUICallParams *)params succ:(void(^)(NSArray <NSString *> *userIdList))succ fail:(TUICallFail)fail
```

| Parameter       | Type                            | Description  |
| ---------- | ------------- | ------------------------------------------ |
| userIdList    | NSArray          | The target user IDs.                 |
| params        | TUICallParams    | An additional parameter. For example, you can use it to customize an offline notification.                   |

### joinInGroupCall

This API is used by a group member to join the group’s call.

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| groupId       | NSString                  | The group ID.                                          |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |

### switchCallMediaType

This API is used to change the call type.

```objectivec
- (void)switchCallMediaType:(TUICallMediaType)newType;
```

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ---------------- | -------------------------------------- |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |

### startRemoteView

This API is used to set the view object to display a remote video.

```objectivec
- (void)startRemoteView:(NSString *)userId videoView:(TUIVideoView *)videoView onPlaying:(void(^)(NSString *userId))onPlaying onLoading:(void(^)(NSString *userId))onLoading onError:(void(^)(NSString *userId, int code, NSString *errMsg))onError;
```

| Parameter | Type | Description |
| --------- | ------------ | ----------------- |
| userId        | NSString                  | The target user ID.                                      |
| videoView | TUIVideoView | The view to be rendered.      |

### StopRemoteView

This API is used to unsubscribe from the video stream of a remote user.

```objectivec
- (void)stopRemoteView:(NSString *)userId;
```

| Parameter       | Type                            | Description  |
| ------ | -------- | ----------------- |
| userId        | NSString                  | The target user ID.                                      |

### openCamera

This API is used to turn the camera on.

```objectivec
- (void)openCamera:(TUICallCamera)camera videoView:(TUIVideoView *)videoView succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

| Parameter | Type | Description |
| --------- | ------------- | ---------------- |
| camera    | TUICallCamera | Whether to use the front or rear camera. |
| videoView | TUIVideoView | The view to be rendered.      |

### closeCamera

This API is used to turn the camera off.

```objectivec
- (void)closeCamera;
```

### switchCamera

This API is used to switch between the front and rear cameras.

```objectivec
- (void)switchCamera:(TUICallCamera)camera;
```

| Parameter | Type | Description |
| ------ | ------------- | ---------------- |
| camera    | TUICallCamera | Whether to use the front or rear camera. |

### openMicrophone

This API is used to turn the mic on.

```objectivec
- (void)openMicrophone:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### closeMicrophone

This API is used to turn the mic off.

```objectivec
- (void)closeMicrophone;
```

### selectAudioPlaybackDevice

This API is used to select the audio playback device (receiver or speaker). In call scenarios, you can use this API to turn on/off hands-free mode.

```objectivec
- (void)selectAudioPlaybackDevice:(TUIAudioPlaybackDevice)device;
```

| Parameter   |  Type  | Description                                                         |
| ------ | ---------------------- | ----------- |
| device | TUIAudioPlaybackDevice | The speaker or receiver. |

### setSelfInfo

This API is used to set the alias and profile photo. The alias cannot exceed 500 bytes, and the profile photo is specified by a URL.

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickName avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```

### enableMultiDeviceAbility

This API is used to set whether to enable multi-device login for `TUICallEngine` (supported by the premium package).

```objectivec
- (void)enableMultiDeviceAbility:(BOOL)enable succ:(TUICallSucc)succ fail:(TUICallFail)fail;
```