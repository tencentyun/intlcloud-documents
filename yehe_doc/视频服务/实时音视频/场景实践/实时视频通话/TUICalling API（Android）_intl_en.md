`TUICalling` is an open-source class based on two closed-source SDKs: Tencent Cloud Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one and group video calls. For detailed instructions how to implement it, see [Real-Time Video Call (Android)](https://intl.cloud.tencent.com/document/product/647/36066).

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
| AUDIO | Audio call |
| VIDEO | Video call |

## Role
[](id:Role)

#### Role type
| Enumerated Type                 | Description       |
| ------------------- | ---------- |
| CALL | Caller |
| CALLED | Callee |

## Event
[](id:Event)

#### Event type
| Enumerated Type                 | Description       |
| ------------------- | ---------- |
| CALL_START | The call started. |
| CALL_SUCCEED | The call was connected successfully. |
| CALL_END | The call ended. |
| CALL_FAILED | The call failed. |

## Basic SDK APIs

### sharedInstance
[](id:sharedInstance)

This API is used to get a singleton of the `TUICalling` component.

```java
public static TUICallingManager sharedInstance();
```

### call
[](id:call)

This API is used to send call invitations by user ID.

```java
void call(String[] userIDs, Type type);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | List of the user IDs of call participants      |
| type | TUICalling.Type | Call type: audio/video |

### receiveAPNSCalled
[](id:receiveAPNSCalled)

This API is used to answer a call.

```java
void receiveAPNSCalled(String[] userIDs, Type type);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | List of the user IDs of call participants      |
| type | TUICalling.Type | Call type: audio/video |

### setCallingListener
[](id:setCallingListener)

This API is used to set the listener.

```java
void setCallingListener(TUICallingListener listener);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| listener    | TUICallingListener  | Listener of the `TUIcalling` component   |

### setCallingBell
[](id:setCallingBell)

This API is used to set the ringtone (preferably shorter than 30s).

```java
void setCallingBell(String filePath);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| filePath | String | Path of the ringtone file |

### enableMuteMode
[](id:enableMuteMode)

This API is used to enable/disable the mute mode.

```java
void enableMuteMode(boolean enable);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| enable | boolean | Whether to enable the mute mode |

### enableCustomViewRoute
[](id:enableCustomViewRoute)

This API is used to enable/disable custom views.
After enabling custom views, you will receive a `CallingView` instance in the callback for calling/being called, and can decide how to display the view by yourself.
>! The view must be displayed full screen or in proportion to the screen size; otherwise, an error may occur.

```java
void enableCustomViewRoute(boolean enable);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| enable    | boolean  | Whether to enable custom views   |


## `TUICallingListener` Callback APIs

### shouldShowOnCallView
[](id:shouldShowOnCallView)

Callback of whether the answering view is displayed when there is an incoming call.

```java
boolean shouldShowOnCallView();
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| Return value    | boolean  |  Whether the answering view is displayed   |

### onCallStart
[](id:onCallStart)

Callback for starting calling, which is triggered for both callers and callees.

```java
 void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | List of the user IDs of call participants      |
| type | TUICalling.Type | Call type: audio/video |
| role | TUICalling.Role | Role type: caller/callee |
| tuiCallingView | View | Calling view. When `enableCustomViewRoute` is `false`, `view` is null. |

### onCallEnd
[](id:onCallEnd)

Callback for ending a call, which is triggered for both callers and callees.

```java
 void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | List of the user IDs of call participants      |
| type | TUICalling.Type | Call type: audio/video |
| role | TUICalling.Role | Role type: caller/callee |
| totalTime | long | Call duration (s) |

### onCallEvent
[](id:onCallEvent)

Call event callback.

```java
void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------- | ------------------ |
| event    | TUICalling.Event  | Call event type      |
| type | TUICalling.Type | Call type: audio/video |
| role | TUICalling.Role | Role type: caller/callee |
| message | String | Event description |




