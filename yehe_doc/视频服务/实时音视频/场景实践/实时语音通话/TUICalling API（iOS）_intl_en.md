`TUICalling` is an open-source class based on two closed-source SDKs: Tencent Cloud Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one and group audio calls. For detailed instructions how to implement it, see [Real-Time Audio Call (iOS)](https://intl.cloud.tencent.com/document/product/647/36067).

- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.


## `TUICalling` API Overview
[](id:TUICalling)

#### Basic SDK APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | Gets a singleton.                                       |
| [call](#call) | Sends call invitations by user ID.                                   |
| [receiveAPNSCalled](#receiveAPNSCalled)                     | Answers a call.                                    |
| [setCallingListener](#setCallingListener)               | Sets the listener.                                   |
| [setCallingBell](#setCallingBell)                             | Sets the ringtone (preferably shorter than 30s).   |
| [enableMuteMode](#enableMuteMode)                                 | Enables/Disables the mute mode. |
| [enableCustomViewRoute](#enableCustomViewRoute)                               | Enables/Disables custom views.        |


## `TUICallingListener` API Overview
[](id:TUICallingListener)

#### Event callbacks

| API                                             | Description                                                         |
| ------------------- | ---------- |
| [shouldShowOnCallView](#shouldShowOnCallView) | Callback of whether the answering view is displayed when there is an incoming call |
| [onCallStart](#onCallStart) | Callback for starting calling. This callback is triggered for both callers and callees. |
| [onCallEnd](#onCallEnd) | Callback for ending a call. This callback is triggered for both callers and callees. |
| [onCallEvent](#onCallEvent) | Call event callback |

## Type
[](id:Type)

#### Call type
| Enumerated Type                 | Description       |
| ------------------- | ---------- |
| TUICallingTypeAudio | Audio call |
| TUICallingTypeVideo | Video call |

## Role
[](id:Role)

#### Role type
| Enumerated Type                 | Description       |
| ------------------- | ---------- |
| TUICallingRoleCall | Caller |
| TTUICallingRoleCalled | Callee |

## Event
[](id:Event)

#### Event type
| Enumerated Type                 | Description       |
| ------------------- | ---------- |
| TUICallingEventCallStart | The call started. |
| TUICallingEventCallSucceed | The call was connected successfully. |
| TUICallingEventCallEnd | The call ended. |
| TUICallingEventCallFailed | The call failed. |

## Basic SDK APIs

### sharedInstance
[](id:sharedInstance)

This API is used to get a singleton of the `TUICallingManager` component.

```objc
+ (instancetype)shareInstance;
```

### call
[](id:call)

This API is used to send call invitations by user ID.

```objc
- (void)call:(NSArray<NSString *> *)userIDs type:(TUICallingType)type;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | List of the user IDs of call participants      |
| type | TUICallingType | Call type: audio/video |

### receiveAPNSCalled
[](id:receiveAPNSCalled)

This API is used to answer a call.

```objc
- (void)receiveAPNSCalled:(NSArray<NSString *> *)userIDs type:(TUICallingType)type;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | List of the user IDs of call participants      |
| type | TUICallingType | Call type: audio/video |

### setCallingListener
[](id:setCallingListener)

This API is used to set the listener.

```objc
- (void)setCallingListener:(id<TUICallingListerner>)listener;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| listener    | TUICallingListener  | Listener of the `TUIcalling` component   |

### setCallingBell
[](id:setCallingBell)

This API is used to set the ringtone (preferably shorter than 30s).

```objc
- (void)setCallingBell:(NSString *)filePath;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| filePath    | NSString  | Path of the ringtone file   |

### enableMuteMode
[](id:enableMuteMode)

This API is used to enable/disable the mute mode.

```objc
- (void)enableMuteMode:(BOOL)enable;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| enable    | BOOL  | Whether to enable the mute mode   |

### enableCustomViewRoute
[](id:enableCustomViewRoute)

This API is used to enable/disable custom views.
After enabling custom views, you will receive a `CallingViewController` instance in the callback for calling/being called, and can decide how to display the view by yourself.
>! The view must be displayed full screen; otherwise, an error may occur.

```objc
- (void)enableCustomViewRoute:(BOOL)enable;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| enable    | BOOL  | Whether to enable custom views   |


## `TUICallingListener` Callback APIs

### shouldShowOnCallView
[](id:shouldShowOnCallView)

Callback of whether the answering view is displayed when there is an incoming call.

```objc
- (BOOL)shouldShowOnCallView;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| Return value    | BOOL  |  Whether the answering view is displayed   |

### onCallStart
[](id:onCallStart)

Callback for starting calling, which is triggered for both callers and callees.

```objc
 - (void)callStart:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | List of the user IDs of call participants      |
| type | TUICallingType | Call type: audio/video |
| role | TUICallingRole | Role type: caller/callee |
| viewController | UIViewController | Calling view controller  |

### onCallEnd
[](id:onCallEnd)

Callback for ending a call, which is triggered for both callers and callees. If `enableCustomViewRoute` is set to `NO`, this callback will not be triggered.

```objc
 - (void)callEnd:(NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(CGFloat)totalTime;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | NSArray  | List of the user IDs of call participants      |
| type | TUICallingType | Call type: audio/video |
| role | TUICallingRole | Role type: caller/callee |
| totalTime | CGFloat | Call duration (s) |

### onCallEvent
[](id:onCallEvent)

Call event callback, which is triggered for both callers and callees. If `enableCustomViewRoute` is set to `NO`, this callback will not be triggered.

```objc
- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(NSString *)message;
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| event    | TUICallingEvent  | Call event type      |
| type | TUICallingType | Call type: audio/video |
| role | TUICallingRole | Role type: caller/callee |
| message | NSString | Event description |




