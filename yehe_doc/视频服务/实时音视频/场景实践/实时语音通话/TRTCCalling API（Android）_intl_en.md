`TRTCCalling` is an open-source class based on two closed-source SDKs: Tencent Cloud Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one and group audio calls. For detailed instructions how to implement it, please see [Real-Time Audio Call (Android)](https://intl.cloud.tencent.com/document/product/647/36068).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.


<h2 id="TRTCCalling">`TRTCCalling` API Overview</h2>

### Basic SDK APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | Gets a singleton.                                       |
| [destroySharedInstance](#destroysharedinstance) | Destroys a singleton. |
| [addDelegate](#adddelegate)                     | Registers an event listener.                                   |
| [removeDelegate](#removedelegate)               | Unregisters an event listener.                                   |
| [destroy](#destroy)                             | Destroys an instance that is no longer needed.    |
| [login](#login)                                 | Logs in. All features can be used only after login. |
| [logout](#logout)                               | Logs out. No calls can be made after logout.         |


### Call operation APIs

| API                                             | Description                                                         |
| ----------------------- | -------------- |
| [call](#call)           | Makes a one-to-one call. |
| [groupCall](#groupcall) | Makes a group chat call. |
| [accept](#accept) | Accepts the current call. |
| [reject](#reject) | Declines the current call. |
| [hangup](#hangup) | Ends the current call. |

### Audio control APIs

| API                                             | Description                                                         |
| ----------------------------- | ------------------------------------------------ |
| [setMicMute](#setmicmute)     | Mutes the local mic.                                   |
| [setHandsFree](#sethandsfree) | Enables the hands-free mode.                                       |

<h2 id="TRTCCallingDelegate">`TRTCCallingDelegate` API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------- | ---------- |
| [onError](#onerror) | Callback for error. |

### Inviter callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------------- |
| [onReject](#onreject) | The call was declined. |
| [onNoResp](#onnoresp) | The invitee did not answer. |
| [onLineBusy](#onlinebusy) | The line is busy. |

### Invitee callback APIs

| API | Description |
| ------------------------------------- | -------------------- |
| [onInvited](#oninvited)               | An invitation was received.     |
| [onCallingCancel](#oncallingcancel) | The call was canceled. |
| [onCallingTimeOut](#oncallingtimeout) | The call timed out. |

### General callback APIs

| API | Description |
| ------------------------------------------------------------ | -------------------------- |
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | The group chat invitee list was updated.     |
| [onUserEnter](#onuserenter)                                  | A user joined the call.         |
| [onUserLeave](#onuserleave)                                  | A user left the call.         |
| [onUserAudioAvailable](#onuseraudioavailable) | Whether a user is sending audio |
| [onUserVoiceVolume](#onuservoicevolume)                      | Call volume of the user         |
| [onCallEnd](#oncallend)                                      | The call ended.             |

## Basic SDK APIs

### sharedInstance

This API is used to get a singleton of the `TRTCCalling` component.

```java
public static ITRTCCalling sharedInstance(Context context);
```

### destroySharedInstance

This API is used to destroy a singleton of the `TRTCCalling` component.

```java
public static void destroySharedInstance();
```

### destroy

This API is used to destroy an instance that is no longer needed.

```java
void destroy();
```

### addDelegate

This API is used to register callbacks for [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066) events. You can receive status notifications of [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066) via `TRTCCallingDelegate`.

```java
public abstract void addDelegate(TRTCCallingDelegate delegate);
```

>?`TRTCCallingDelegate` is the delegate callback of `TRTCCalling`.

### removeListener

This API is used to unregister event callbacks.

```java
void removeDelegate(TRTCCallingDelegate listener);
```

### login

This API is used to log in to the component.

```java
void login( int sdkAppId,
            final String userId, 
            String userSig, 
            final ActionCallBack callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | int | You can view the `SDKAppID` via **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC console. |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallBack | Callback for login. `onSuccess` indicates a login success. |

### logout

This API is used to log out of the component.

```java
void logout(final ActionCallBack callBack);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ------------------------------------ |
| callBack | ActionCallBack | Callback for logout. `onSuccess` indicates a logout success. |

## Call Operation APIs

### call

This API is used to make a one-to-one call. It can be called during a call to invite more users.

```java
void call(String userId, int type);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | -------------------------------- |
| userId | String | User ID of the callee |
| type | int | `1`: audio call; `2`: video call |

### groupCall

This API is used to make an IM group call. Invitees will receive the `onInvited()` callback. This API can be called in an ongoing call to invite other users, and existing users in the call will receive the `onGroupCallInviteeListUpdate()` callback.

```java
void groupCall(List<String> userIdList, int type, String groupId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------ | -------------------------------- |
| userIdList | List&lt;String&gt; | Invitee ID list. |
| type | int | `1`: audio call; `2`: video call |
| groupId | String | Group ID. |



### accept

This API is used to accept the current call. After receiving the `onInvited()` callback, the invitee can call this API to accept the call.

```java
void accept();
```



### reject

This API is used to decline the current call. After receiving the `onInvited()` callback, the invitee can call this API to decline the call.

```java
void reject();
```



### hangup

This API is used to end the current call.

```java
void hangup();
```


## Audio Control APIs

### setMicMute

This API is used to mute the local mic.

```java
void setMicMute(boolean isMute);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------- | ------------------------------------------- |
| isMute | boolean | `true`: mutes the mic; `false`: unmutes the mic. |

### setHandsFree

This API is used to enable the hands-free mode.

```java
void setHandsFree(boolean isHandsFree);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ------- | --------------------------------------- |
| isHandsFree | boolean | `true`: enables the hands-free mode; `false`: disables the hands-free mode. |

## `TRTCCallingDelegate` Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>?This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```java
void onError(int code, String msg);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------ | ---------- |
| code    | int    | Error code   |
| msg  | String | Error message |


## Inviter Callback APIs

### onReject

The call was declined.

```java
void onReject(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------------- |
| userId | String | User ID of the invitee who declined the call |

### onNoResp

The invitee did not answer.

```java
void onNoResp(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------- |
| userId | String | User ID of the invitee who did not answer |

### onLineBusy

The line is busy.

```java
void onLineBusy(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------------- |
| userId | String | User ID of the invitee whose line is busy |

## Invitee Callback APIs

### onInvited

A call invitation was received.

```java
void onInvited(String sponsor, List<String> userIdList, boolean isFromGroup, int callType);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ----------- | ------------------ | -------------------------------- |
| sponsor     | String             | User ID of the inviter                    |
| userIdList     | List&lt;String&gt; | IDs of other users invited         |
| isFromGroup | boolean          | Whether it is a group call               |
| callType | int | `1`: audio call; `2`: video call |

### onCallingCancel

The call was canceled. The invitee will receive this callback if the inviter cancels the invitation before he or she handles it.

```java
void onCallingCancel();
```



### onCallingTimeOut

The call timed out.

```java
void onCallingTimeout();
```

## General Callback APIs

### onGroupCallInviteeListUpdate

The group chat invitee list was updated.

```java
void onGroupCallInviteeListUpdate(List<String> userIdList);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------ | -------------- |
| userIdList | List&lt;String&gt; | Invitee ID list. |

### onUserEnter

A user joined the call.

```java
void onUserEnter(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------- |
| userId | String | ID of the user who joined the call |

### onUserLeave

A user left the call.

```java
void onUserLeave(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------- |
| userId | String | ID of the user who left the call |

### onUserAudioAvailable

Whether a user is sending audio.

```java
void onUserAudioAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------- | ------------------ |
| userId | String | User ID |
| available | boolean| Whether the user has available audio |


### onUserVoiceVolume

Call volume of a user.

```java
void onUserVoiceVolume(Map<String, Integer> volumeMap);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------------------- | ------------------------------------------------------------ |
| volumeMap | Map&lt;String, Integer&gt; | Volume table. The corresponding volume can be obtained by each `userid`. The volume ranges from 0 to 100. |

### onCallEnd

The call ended.

```java
void onCallEnd();
```

