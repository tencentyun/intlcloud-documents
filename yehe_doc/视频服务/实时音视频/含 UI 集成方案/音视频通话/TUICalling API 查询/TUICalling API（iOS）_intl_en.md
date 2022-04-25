`TUICalling` is an open-source class based on two closed-source SDKs: Tencent Cloud Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one and group video calls. For detailed instructions how to implement it, see [Real-Time Video Call (iOS)](https://intl.cloud.tencent.com/document/product/647/36065).

- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.

## `TUICalling` API Overview

#### Basic SDK APIs

| API                                                          | Description                     |
| :----------------------------------------------------------- | :------------------------ |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/43139) | Gets a component singleton.                |
| [call](https://intl.cloud.tencent.com/document/product/647/43139) | Sends call invitations by user ID.            |
| [setCallingListener](https://intl.cloud.tencent.com/document/product/647/43139) | Sets the listener.              |
| [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43139) | Sets the ringtone (shorter than 30s recommended). |
| [enableMuteMode](https://intl.cloud.tencent.com/document/product/647/43139) | Enables/Disables the mute mode.              |
| [enableCustomViewRoute](https://intl.cloud.tencent.com/document/product/647/43139) | Enables/Disables the custom view.            |

## `TUICallingListener` API Overview

#### Event callbacks

| API                                                          | Description                            |
| :----------------------------------------------------------- | :------------------------------- |
| [shouldShowOnCallView](https://intl.cloud.tencent.com/document/product/647/43139) | Callback of whether the answering view is displayed when there is an incoming call.           |
| [onCallStart](https://intl.cloud.tencent.com/document/product/647/43139) | Callback for starting a call, which is triggered for both callers and callees. |
| [onCallEnd](https://intl.cloud.tencent.com/document/product/647/43139) | Callback for ending a call, which is triggered for both callers and callees.     |
| [onCallEvent](https://intl.cloud.tencent.com/document/product/647/43139) | Call event callback.                     |

## Type

#### Call type

| enum                | Description     |
| :------------------ | :------- |
| TUICallingTypeAudio | Audio call |
| TUICallingTypeVideo | Video call |

## Role

#### Role type

| enum                  | Description               |
| :-------------------- | :----------------- |
| TUICallingRoleCall    | Caller |
| TTUICallingRoleCalled | Callee |

## Event

#### Event type

| enum                       | Description         |
| :------------------------- | :----------- |
| TUICallingEventCallStart   | The call started.     |
| TUICallingEventCallSucceed | The call was connected successfully. |
| TUICallingEventCallEnd     | The call ended.     |
| TUICallingEventCallFailed  | The call failed.     |

## Basic SDK APIs

### sharedInstance

This API is used to get a singleton of the `TUICallingManager` component.


```objc
+ (instancetype)shareInstance;
```

### call

This API is used to send call invitations by user ID.


```objc
- (void)call:(NSArray<NSString *> *)userIDs type:(TUICallingType)type;
```

The parameters are described below:

| Parameter | Type | Description |
| :------ | :------------- | :------------------ |
| userIDs    | NSArray  | List of the user IDs of call participants.      |
| type | TUICallingType | Call type: audio/video |

### setCallingListener

This API is used to set the listener.

```objc
- (void)setCallingListener:(id<TUICallingListerner>)listener;
```

The parameters are described below:

| Parameter | Type | Description |
| :------- | :----------------- | :-------------------- |
| listener    | TUICallingListener  | Listener of the `TUIcalling` component. |

### setCallingBell

This API is used to set the ringtone (preferably shorter than 30s).

```objc
- (void)setCallingBell:(NSString *)filePath;
```

The parameters are described below:

| Parameter | Type | Description |
| :------- | :------- | :----------- |
| filePath    | NSString  | Path of the ringtone file.   |

### enableMuteMode

This API is used to enable/disable the mute mode.

```objc
- (void)enableMuteMode:(BOOL)enable;
```

The parameters are described below:

| Parameter | Type | Description |
| :----- | :--- | :--------------- |
| enable    | BOOL  | Whether to enable the mute mode.   |

### enableCustomViewRoute

This API is used to enable/disable custom views.
After enabling custom views, you will receive a `CallingViewController` instance in the callback for calling/being called, and can decide how to display the view by yourself.

>! The view must be displayed full screen; otherwise, an error may occur.

```objc
- (void)enableCustomViewRoute:(BOOL)enable;
```

The parameters are described below:

| Parameter | Type | Description |
| :----- | :--- | :----------------- |
| enable    | BOOL  | Whether to enable custom views.   |

## `TUICallingListener` Callback APIs

### shouldShowOnCallView

Callback of whether the answering view is displayed when there is an incoming call.

```objc
- (BOOL)shouldShowOnCallView;
```

The parameters are described below:

| Parameter | Type | Description |
| :----- | :--- | :------- |
| Return value    | BOOL  |  Whether the answering view is displayed.   |

### onCallStart

Callback for starting a call, which is triggered for both callers and callees.

```objc
 - (void)callStart:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController;
```

The parameters are described below:

| Parameter | Type | Description |
| :------------- | :--------------- | :---------------------- |
| userIDs    | NSArray  | List of the user IDs of call participants.      |
| type | TUICallingType | Call type: audio/video. |
| role           | TUICallingRole   | Role type: caller/callee. |
| viewController | UIViewController | Calling view controller  |

### onCallEnd

Callback for ending a call, which is triggered for both callers and callees. If `enableCustomViewRoute` is set to `NO`, this callback will not be triggered.

```objc
 - (void)callEnd:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(CGFloat)totalTime;
```

The parameters are described below:

| Parameter | Type | Description |
| :-------- | :------------- | :---------------------- |
| userIDs    | NSArray  | List of the user IDs of call participants.      |
| type | TUICallingType | Call type: audio/video |
| role      | TUICallingRole | Role type: caller/callee. |
| totalTime | CGFloat        | Call duration in seconds.      |

### onCallEvent

Call event callback, which is triggered for both callers and callees. If `enableCustomViewRoute` is set to `NO`, this callback will not be triggered.

```objc
- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(NSString *)message;
```

The parameters are described below:

| Parameter | Type | Description |
| :------ | :-------------- | :---------------------- |
| event   | TUICallingEvent | Call event type.          |
| type | TUICallingType | Call type: audio/video |
| role    | TUICallingRole  | Role type: caller/callee. |
| message | NSString        | Event description.          |