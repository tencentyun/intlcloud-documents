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

```java
TUICallEngine createInstance(Context context)
```

### destroyInstance

This API is used to terminate a `TUICallEngine` singleton.

```java
void destroyInstance();
```

### Init

This API is used to initialize `TUICallEngine`. Call it to authenticate the call service and perform other required actions before you call other APIs.

```java
void init(int sdkAppId, String userId, String userSig, TUICommonDefine.Callback callback)
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| -------- | ------------------------ | ------------------------------------------------------------ |
| sdkAppId | int | You can view `SDKAppID` in [Application Management](https://console.cloud.tencent.com/trtc/app) > **Application Info** of the TRTC console. |
| userId | String | The ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). |
| userSig | String | Tencent Cloud's proprietary security signature. For how to calculate and use it, see [UserSig](https://www.tencentcloud.com/document/product/647/35166). |
| callback | TUICommonDefine.Callback | The initialization callback. `onSuccess` indicates initialization is successful.                        |

### addObserver

This API is used to register an event listener to listen for `TUICallObserver` events.

```java
void addObserver(TUICallObserver observer);
```

### removeObserver

This API is used to unregister an event listener.

```java
void removeObserver(TUICallObserver observer);
```

### call

This API is used to make a (one-to-one) call.

```java
void call(TUICommonDefine.RoomId roomId, String userId, TUICallDefine.MediaType callMediaType,
          TUICallDefine.CallParams params, TUICommonDefine.Callback callback);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------- | ------------------------ | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| userId        | String                   | The target user ID.                                            |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |
| params        | TUICallDefine.CallParams | An additional parameter. For example, you can use it to customize an offline notification.                   |

### groupCall

This API is used to make a group call. Note that you need to create an IM group before making a group call.

```java
void groupCall(TUICommonDefine.RoomId roomId, String groupId, List<String> userIdList,    
               TUICallDefine.MediaType callMediaType, TUICallDefine.CallParams params,                               
               TUICommonDefine.Callback callback);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------- | ------------------------ | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| groupId       | String                  | The group ID.                                          |
| userIdList    | List                     | The target user IDs.                                       |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |
| params        | TUICallDefine.CallParams | An additional parameter. For example, you can use it to customize an offline notification.                   |

### accept

This API is used to accept a call. After receiving the `onCallReceived()` callback, you can call this API to accept the call.

```java
void accept(TUICommonDefine.Callback callback);
```

### reject

This API is used to reject a call. After receiving the `onCallReceived()` callback, you can call this API to reject the call.

```java
void reject(TUICommonDefine.Callback callback);
```

### ignore

This API is used to ignore a call. After receiving the `onCallReceived()`, you can call this API to ignore the call. The caller will receive the `onUserLineBusy` callback.

Note: If your project involves live streaming or conferencing, you can also use this API to implement the “in a meeting” or “on air” feature.

```java
void ignore(TUICommonDefine.Callback callback);
```

### hangup

This API is used to end a call.

```java
void hangup(TUICommonDefine.Callback callback);
```

### inviteUser

This API is used to invite users to the current group call.

This API is called by a participant of a group call to invite new users.

```java
void inviteUser(List<String> userIdList, TUICallDefine.CallParams params, 
                TUICommonDefine.ValueCallback callback);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ---------- | ------------------------ | ------------------------------------------ |
| userIdList    | List                    | The target user IDs.                 |
| params        | TUICallDefine.CallParams | An additional parameter. For example, you can use it to customize an offline notification.                   |

### joinInGroupCall

This API is used to join a group call.

This API is called by a group member to join the group’s call.

```java
void joinInGroupCall(TUICommonDefine.RoomId roomId, String groupId, 
                     TUICallDefine.MediaType callMediaType, TUICommonDefine.Callback callback);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| groupId       | String                  | The group ID.                                          |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |

### switchCallMediaType

This API is used to change the call type.

```java
void switchCallMediaType(TUICallDefine.MediaType callMediaType);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ----------------------- | -------------------------------------- |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |

### startRemoteView

This API is used to subscribe to the video stream of a remote user. For it to work, make sure you call it after `setRenderView`.

```java
void startRemoteView(String userId, TUIVideoView videoView, TUICommonDefine.PlayCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------------ | ----------------- |
| userId        | String                  | The target user ID.                                      |
| videoView | TUIVideoView | The view to be rendered.      |

### stopRemoteView

This API is used to unsubscribe from the video stream of a remote user.

```java
void stopRemoteView(String userId);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ------ | ----------------- |
| userId        | String                  | The target user ID.                                      |

### openCamera

This API is used to turn the camera on.

```java
void openCamera(TUICommonDefine.Camera camera, TUIVideoView videoView, TUICommonDefine.Callback callback);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ---------------------- | ---------------- |
| camera    | TUICommonDefine.Camera | The front or rear camera. |
| videoView | TUIVideoView | The view to be rendered.      |

### closeCamera

This API is used to turn the camera off.

```java
void closeCamera();
```

### switchCamera

This API is used to switch between the front and rear cameras.

```java
void switchCamera(TUICommonDefine.Camera camera);
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---------------------- | ---------------- |
| camera    | TUICommonDefine.Camera | The front or rear camera. |

### openMicrophone

This API is used to turn the mic on.

```java
void openMicrophone(TUICommonDefine.Callback callback);
```

### closeMicrophone

This API is used to turn the mic off.

```java
void closeMicrophone();
```

### selectAudioPlaybackDevice

This API is used to select the audio playback device (receiver or speaker). In call scenarios, you can use this API to turn on/off hands-free mode.

```java
void selectAudioPlaybackDevice(TUICommonDefine.AudioPlaybackDevice device);
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ----------------------------------- | ----------- |
| device | TUICommonDefine.AudioPlaybackDevice | The speaker or receiver. |

### setSelfInfo

This API is used to set the alias and profile photo. The alias cannot exceed 500 bytes, and the profile photo is specified by a URL.

```java
void setSelfInfo(String nickname, String avatar, TUICommonDefine.Callback callback);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------ | ---------------------- |
| nickname | String | The alias.               |
| avatar   | String | The URL of the profile photo. |

### enableMultiDeviceAbility

This API is used to set whether to enable multi-device login for `TUICallEngine` (supported by the premium package).

```java
void enableMultiDeviceAbility(boolean enable, TUICommonDefine.Callback callback);
```