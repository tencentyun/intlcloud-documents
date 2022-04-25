`TUICalling` is an open-source class based on two closed-source SDKs: Tencent Cloud Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one and group video calls. For detailed instructions how to implement it, see [Real-Time Video Call (Android)](https://intl.cloud.tencent.com/document/product/647/36066).

- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.

## `TUICalling` API Overview

#### Basic SDK APIs

| API                                                          | Description                     |
| :----------------------------------------------------------- | :------------------------ |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/43140) | Gets a component singleton.                  |
| [call](https://intl.cloud.tencent.com/document/product/647/43140) | Sends call invitations by user ID.               |
| [setCallingListener](https://intl.cloud.tencent.com/document/product/647/43140) | Sets the listener.              |
| [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140) | Sets the ringtone (shorter than 30s recommended). |
| [enableMuteMode](https://intl.cloud.tencent.com/document/product/647/43140) | Enables/Disables the mute mode.              |
| [enableCustomViewRoute](https://intl.cloud.tencent.com/document/product/647/43140) | Enables/Disables the custom view.            |

## `TUICallingListener` API Overview

#### Event callbacks

| API                                                          | Description                            |
| :----------------------------------------------------------- | :------------------------------- |
| [shouldShowOnCallView](https://intl.cloud.tencent.com/document/product/647/43140) | Callback of whether the answering view is displayed when there is an incoming call.           |
| [onCallStart](https://intl.cloud.tencent.com/document/product/647/43140) | Callback for starting a call, which is triggered for both callers and callees. |
| [onCallEnd](https://intl.cloud.tencent.com/document/product/647/43140) | Callback for ending a call, which is triggered for both callers and callees.     |
| [onCallEvent](https://intl.cloud.tencent.com/document/product/647/43140) | Call event callback.                     |

## Type

#### Call type

| enum  | Description     |
| :---- | :------- |
| AUDIO | Audio call |
| VIDEO | Video call |

## Role

#### Role type

| enum   | Description               |
| :----- | :----------------- |
| CALL   | Caller |
| CALLED | Callee |

## Event

#### Event type

| enum         | Description         |
| :----------- | :----------- |
| CALL_START   | The call started.     |
| CALL_SUCCEED | The call was connected successfully. |
| CALL_END     | The call ended.     |
| CALL_FAILED  | The call failed.     |

## Basic SDK APIs

### sharedInstance

This API is used to get a singleton of the `TUICalling` component.

```java
public static TUICallingImpl sharedInstance();
```

### call

This API is used to send call invitations by user ID.


```java
void call(String[] userIDs, Type type);
```

The parameters are described below:

| Parameter | Type | Description |
| :------ | :-------------- | :------------------ |
| userIDs    | String[]  | List of the user IDs of call participants.      |
| type | TUICalling.Type | Call type: audio/video. |

### setCallingListener
This API is used to set the listener.


```java
void setCallingListener(TUICallingListener listener);
```

The parameters are described below:

| Parameter | Type | Description |
| :------- | :----------------- | :-------------------- |
| listener    | TUICallingListener  | Listener of the `TUIcalling` component   |

### setCallingBell

This API is used to set the ringtone (preferably shorter than 30s).

```java
void setCallingBell(String filePath);
```



The parameters are described below:

| Parameter | Type | Description |
| :------- | :----- | :----------- |
| filePath | String | Path of the ringtone file |

### enableMuteMode

This API is used to enable/disable the mute mode.

```java
void enableMuteMode(boolean enable);
```

The parameters are described below:

| Parameter | Type | Description |
| :----- | :------ | :--------------- |
| enable | boolean | Whether to enable the mute mode |

### enableCustomViewRoute

This API is used to enable/disable custom views.
After enabling custom views, you will receive a `CallingView` instance in the callback for calling/being called, and can decide how to display the view by yourself.

>! The view must be displayed full screen or in proportion to the screen size; otherwise, an error may occur.

```java
void enableCustomViewRoute(boolean enable);
```

The parameters are described below:

| Parameter | Type | Description |
| :----- | :------ | :----------------- |
| enable    | boolean  | Whether to enable custom views   |

## `TUICallingListener` Callback APIs

### shouldShowOnCallView

Callback of whether the answering view is displayed when there is an incoming call.

```java
boolean shouldShowOnCallView();
```

The parameters are described below:

| Parameter | Type | Description |
| :----- | :------ | :------- |
| Return value    | boolean  |  Whether the answering view is displayed   |

### onCallStart

Callback for starting a call, which is triggered for both callers and callees.

```java
 void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView);
```

The parameters are described below:

| Parameter | Type | Description |
| :------------- | :-------------- | :----------------------------------------------------------- |
| userIDs    | String[]  | List of the user IDs of call participants.      |
| type | TUICalling.Type | Call type: audio/video. |
| role           | TUICalling.Role | Role type: caller/callee. |
| tuiCallingView | View            | Calling view. When `enableCustomViewRoute` is `false`, the view is null. |

### onCallEnd

Callback for ending a call, which is triggered for both callers and callees.

```java
 void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime);
```

The parameters are described below:

| Parameter | Type | Description |
| :-------- | :-------------- | :---------------------- |
| userIDs    | String[]  | List of the user IDs of call participants.      |
| type | TUICalling.Type | Call type: audio/video. |
| role      | TUICalling.Role | Role type: caller/callee. |
| totalTime | long            | Call duration in seconds.      |

### onCallEvent

Call event callback.

```java
void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message);
```

The parameters are described below:

| Parameter | Type | Description |
| :------ | :--------------- | :---------------------- |
| event   | TUICalling.Event | Call event type.            |
| type | TUICalling.Type | Call type: audio/video. |
| role    | TUICalling.Role  | Role type: caller/callee. |
| message | String           | Event description.          |