## TUICallKit APIs

`TUICallKit` is an audio/video call component that **includes UI elements**. You can use its APIs to quickly implement an audio/video call application similar to WeChat. For directions on integration, see [Integrating TUICallKit](https://www.tencentcloud.com/document/product/647/50992).

## Overview

| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](#createinstance)                            | Creates a `TUICallKit` instance (singleton mode). |
| [setSelfInfo](#setselfinfo) | Sets the alias and profile photo.                                        |
| [call](#call) | Makes a one-to-one call.                                               |
| [groupCall](#groupcall) | Makes a group call.                                                |
| [joinInGroupCall](#joiningroupcall) | Joins a group call.         |
| [setCallingBell](#setcallingbell) | Sets the ringtone.               |
| [enableMuteMode](#enablemutemode) | Sets whether to turn on the mute mode. |
| [enableFloatWindow](#enablefloatwindow) | Sets whether to enable floating windows.              |

## Details

### createInstance

This API is used to create a `TUICallKit` singleton.

```objectivec
- (instancetype)createInstance;
```

### setSelfInfo

This API is used to set the alias and profile photo. The alias cannot exceed 500 bytes, and the profile photo is specified by a URL.

```objectivec
- (void)setSelfInfo:(NSString * _Nullable)nickname avatar:(NSString * _Nullable)avatar succ:(TUICallSucc)succ fail:(TUICallFail)fail
```

| Parameter     |  Type  | Description                                    |
| -------- | -------- | -------------- |
| nickName | NSString | The alias. |
| avatar   | NSString | The profile photo. |

### call

This API is used to make a (one-to-one) call.

```objectivec
- (void)call:(NSString *)userId callMediaType:(TUICallMediaType)callMediaType;
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ---------------- | -------------------------------------- |
| userId        | NSString                  | The target user ID.                                      |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |

### groupCall

This API is used to make a group call. Note that you need to create an IM group before making a group call.

```objectivec
- (void)groupCall:(NSString *)groupId userIdList:(NSArray<NSString *> *)userIdList callMediaType:(TUICallMediaType)callMediaType;
```

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ---------------- | -------------------------------------- |
| groupId       | String                  | The group ID.                                          |
| userIdList    | NSArray          | The target user IDs.                 |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |

### joinInGroupCall

This API is used to make a group call. Note that you need to create an IM group before making a group call.

```objectivec
- (void)joinInGroupCall:(TUIRoomId *)roomId groupId:(NSString *)groupId callMediaType:(TUICallMediaType)callMediaType;
```

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| groupId       | NSString                  | The group ID.                                          |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |

### setCallingBell

This API is used to set the ringtone. `filePath` must be an accessible local file URL.

The ringtone set is associated with the device and does not change with user.

To reset the ringtone, pass in an empty string for `filePath`.

```objectivec
- (void)setCallingBell:(NSString *)filePath;
```

### enableMuteMode

This API is used to set whether to turn on the mute mode.

```objc
- (void)enableMuteMode:(BOOL)enable;
```

### enableFloatWindow

This API is used to set whether to enable floating windows. The default value is `false`, and the floating window button in the top left corner of the call view is hidden. If it is set to `true`, the button will become visible.

```objc
- (void)enableFloatWindow:(BOOL)enable;
```