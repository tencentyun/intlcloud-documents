## TUICallKit APIs

`TUICallKit` is an audio/video call component that **includes UI elements**. You can use its APIs to quickly implement an audio/video call application similar to WeChat. For directions on integration, see [Integrating TUICallKit](https://www.tencentcloud.com/document/product/647/50991).

## API Overview

| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](#createinstance)                            | Creates a `TUICallKit` instance (singleton mode). |
| [setSelfInfo](#setselfinfo) | Sets the alias and profile photo.                  |
| [call](#call) | Makes a one-to-one call.                       |
| [groupCall](#groupcall) | Makes a group call.                        |
| [joinInGroupCall](#joiningroupcall) | Joins a group call.         |
| [setCallingBell](#setcallingbell) | Sets the ringtone.               |
| [enableMuteMode](#enablemutemode) | Sets whether to turn on the mute mode. |
| [enableFloatWindow](#enablefloatwindow) | Sets whether to enable floating windows.              |

## Details

### createInstance

This API is used to create a `TUICallKit` singleton.

```java
TUICallKit createInstance(Context context)
```

### setSelfInfo

This API is used to set the alias and profile photo. The alias cannot exceed 500 bytes, and the profile photo is specified by a URL.

```java
void setSelfInfo(String nickname, String avatar, TUICommonDefine.Callback callback)
```

The parameters are described below:

| Parameter     |  Type  | Description                                    |
| -------- | ------ | -------------- |
| nickname | String | The alias. |
| avatar   | String | The profile photo. |

### call

This API is used to make a (one-to-one) call.

```java
 void call(String userId, TUICallDefine.MediaType callMediaType)
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ----------------------- | -------------------------------------- |
| userId        | String                  | The target user ID.                                      |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio. |

### groupCall

This API is used to join a group call.

>! Before making a group call, you need to create an IM group first.

```java
void groupCall(String groupId, List<String> userIdList, TUICallDefine.MediaType callMediaType) {
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ----------------------- | -------------------------------------- |
| groupId       | String                  | The group ID.                    |
| userIdList    | List                    | The target user IDs.                 |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio. |

### joinInGroupCall

This API is used to join a group call.

>! Before making a group call, you need to create an IM group first.

```java
void joinInGroupCall(TUICommonDefine.RoomId roomId, String groupId, TUICallDefine.MediaType callMediaType, TUICommonDefine.Callback callback);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| groupId       | String                  | The group ID.                                          |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |

### setCallingBell

This API is used to set the ringtone. `filePath` must be an accessible local file URL.

The ringtone set is associated with the device and does not change with user.

To reset the ringtone, pass in an empty string for `filePath`.

```java
void setCallingBell(String filePath);
```

### enableMuteMode

This API is used to set whether to turn on the mute mode.

```java
void enableMuteMode(boolean enable);
```

### enableFloatWindow

This API is used to set whether to enable floating windows.

The default value is `false`, and the floating window button in the top left corner of the call view is hidden. If it is set to `true`, the button will become visible.

```java
void enableFloatWindow(boolean enable);
```