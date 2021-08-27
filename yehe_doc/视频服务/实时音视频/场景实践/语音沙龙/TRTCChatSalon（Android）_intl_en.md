`TRTCChatSalon` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a chat salon and become a speaker, or enter a salon as a listener.
- The room owner can invite a listener to speak as well as remove a speaker.
- A listener can request to speak and become a speaker. A speaker can also become a listener.
- All users can send text and custom messages. Custom messages can be used to send on-screen comments, give likes, and send gifts.

`TRTCChatSalon` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Chat Salon (Android)](https://intl.cloud.tencent.com/document/product/647/39804).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647) is used as a low-latency audio chat component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the speaker list, and invitation signaling is used to send requests to speak or invite others to speak.

[](id:TRTCChatSalon)

## `TRTCChatSalon` API Overview

### Basic SDK APIs

| API | Description |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates singleton object. |
| [setDelegate](#setdelegate) | Sets event callback. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where the event callback is. |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets profile. |

### Room APIs

| API | Description |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates room (called by room owner). If the room does not exist, the system will automatically create a room. |
| [destroyRoom](#destroyroom) | Terminates room (called by room owner). |
| [enterRoom](#enterroom) | Enters room (called by listener). |
| [exitRoom](#exitroom) | Exits room (called by listener). |
| [getRoomInfoList](#getroominfolist) | Gets room list details.                                     |
| [getUserInfoList](#getuserinfolist) | Gets the user information of the specified `userId`. If the value is `null`, the information of all users in the room is obtained. |

### Mic APIs

| API                                             | Description                                                         |
| ----------------------- | ---------------------------------- |
| [enterSeat](#enterseat) | Becomes a speaker (called by room owner or listener). |
| [leaveSeat](#leaveseat) | Becomes a listener (called by speaker). |
| [pickSeat](#pickseat)   | Invites a listener to speak (called by room owner).                  |
| [kickSeat](#kickseat)   | Removes a speaker (called by room owner).                  |

### Local audio APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Enables mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [setAudioQuality](#setaudioquality)             | Sets audio quality.           |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker)                       | Turns the speaker on.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume.       |


### Remote audio APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | Mutes/Unmutes specified member. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all members. |

### Background music and sound effect APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa). |

### Message sending APIs

| API                                     | Description                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts text message in room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends custom text message. |

### Invitation signaling APIs

| API                                             | Description                                                         |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | Sends invitation. |
| [acceptInvitation](#acceptinvitation) | Accepts invitation.       |
| [rejectInvitation](#rejectinvitation) | Declines invitation.       |
| [cancelInvitation](#cancelinvitation) | Cancels invitation.       |

[](id:TRTCChatSalonDelegate)
## `TRTCChatSalonDelegate` API Overview

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------- |
| [onError](#onerror) | Error |
| [onWarning](#onwarning) | Warning |
| [onDebugLog](#ondebuglog) | Log |

### Room event callback APIs

| API                                             | Description                                                         |
| ----------------------------------------- | -------------------------- |
| [onRoomDestroy](#onroomdestroy) | Room termination |
| [onRoomInfoChange](#onroominfochange)     | Room information change |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Speaker list change callback APIs

| API                                                          | Description                                                         |
| ---------------------------------------------- | -------------------------------------- |
| [onAnchorEnterSeat](#onanchorenterseat) | Someone became a speaker after requesting or being invited by the room owner. |
| [onAnchorLeaveSeat](#onanchorleaveseat) | Someone became a listener or was moved to listeners by the room owner. |
| [onSeatMute](#onseatmute) | The room owner muted a speaker. |

### Callback APIs for room entry/exit by listeners

| API                                             | Description                                                         |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | A listener entered the room. |
| [onAudienceExit](#onaudienceexit) | A listener exited the room. |

### Message event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | Receipt of text message  |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of custom message |

### Signaling event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | Receipt of invitation |
| [onInviteeAccepted](#oninviteeaccepted)           | Invitation accepted by invitee   |
| [onInviteeRejected](#oninviteerejected)           |  Invitation declined by invitee   |
| [onInvitationCancelled](#oninvitationcancelled)   | Invitation canceled by inviter |

## Basic SDK APIs

### sharedInstance

This API is used to get a [TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804) singleton object.

```java
 public static synchronized TRTCChatSalon sharedInstance(Context context);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------- | ------- | ------------------------------------------------------------ |
| context | Context | Android context, which will be converted to `ApplicationContext` for the calling of system APIs |


### destroySharedInstance

This API is used to terminate a [TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804) singleton object.

>?After the instance is terminated, the externally cached `TRTCChatSalon` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```java
public static void destroySharedInstance();
```

### setDelegate
This API is used to set the event callbacks of [TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804). You can use `TRTCChatSalonDelegate` to get different status notifications of [TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/39804).

```java
public abstract void setDelegate(TRTCChatSalonDelegate delegate);
```

>?`setDelegate` is the delegate callback of `TRTCChatSalon`.   

### setDelegateHandler
This API is used to set the thread where the event callback is.

```java
public abstract void setDelegateHandler(Handler handler);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------- | ------- | ------------------------------------------------------------ |
| handler | Handler | Status notifications in `TRTCChatSalon` will be sent to the handler thread you specify. |

   

### login

This API is used to log in.

```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int | You can view the `SDKAppID` via **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC console. |
| userId | String | ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For more information on how to get it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The `code` will be 0 if login succeeds. |

   

### logout

This API is used to log out.

```java
public abstract void logout(TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | Callback for logout. The code is 0 if logout succeeds. |

   

### setSelfProfile

This API is used to set profile.

```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | -------------- | ----------------------------------- |
| userName | String | Nickname |
| `avatar` | `String` | Profile photo address |
| callback | ActionCallback | Callback for profile setting. The code is 0 if the operation succeeds. |

   


## Room APIs

### createRoom

This API is used to create a room (called by room owner).

```java
public abstract void createRoom(int roomId, TRTCChatSalonDef.RoomParam roomParam, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ------------------------------------------------------------ |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a chat salon room list. Currently, Tencent Cloud does not provide management services for chat salon room lists. Please manage the list by yourself. |
| roomParam | RoomParam | Room information, such as room name, speaker list information, and cover information |
| callback | ActionCallback | Callback for room creation result. The code is 0 if the operation succeeds.  |

The process of creating a chat salon and becoming a speaker is as follows: 

1. A user calls `createRoom` to create a chat salon, passing in room attributes (e.g., room ID and whether listeners require room owner’s consent to speak).
2. After creating the room, the user calls `enterSeat` to become a speaker.
3. The user receives an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

   

### destroyRoom

This API is used to terminate a room (called by room owner).

```java
public abstract void destroyRoom(TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room termination result. The code is 0 if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by listener).

```java
public abstract void enterRoom(int roomId, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| roomId | int | Room ID |
| callback | ActionCallback | Callback for room entry result. The code is 0 if the operation succeeds. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest chat salon list from your server. The list may contain the `roomId` and room information of multiple chat salons.
2. The user selects a chat salon, and calls `enterRoom` with the room ID passed in to enter.
3. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner’s consent is required for listeners to speak, etc.
4. The user receives an `onAnchorEnterSeat` notification that someone became a speaker.

### exitRoom()

This API is used to exit a room.

```java
public abstract void exitRoom(TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room exit result. The `code` is 0 if the operation succeeds. |

   

### getRoomInfoList

This API is used to get room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?If both the room list and room information are managed on your server, you can ignore this parameter.


```java
public abstract void getRoomInfoList(List<Integer> roomIdList, TRTCChatSalonCallback.RoomInfoCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | Room ID list |
| callback | RoomInfoCallback | Callback for room details |


### getUserInfoList

This API is used to get the user information of a specified `userId`.

```java
public abstract void getUserInfoList(List<String> userIdList, TRTCChatSalonCallback.UserListCallback userlistcallback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List | IDs of the users to query. If this parameter is `null`, the information of all users in the room is obtained. |
| userlistcallback | UserListCallback   | Callback for user details                                           |


## Mic APIs

### enterSeat

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onAnchorEnterSeat` notification.

```java
public abstract void enterSeat(TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the speaker list. In cases where listeners need the room owner’s consent to speak, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `enterSeat`.

### leaveSeat

This API is used to become a listener (called by speaker).

>?After a speaker becomes a listener, all members in the room will receive an `onAnchorLeaveSeat` notification..

```java
public abstract void leaveSeat(TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for operation |

### pickSeat

This API is used to invite a listener to speak (called by room owner).

>? After a listener becomes a speaker following the room owner's invitation, all members in the room will receive an `onAnchorEnterSeat` notification.

```java
public abstract void pickSeat(String userId, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ---------- |
| userID | String | User ID |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the speaker list. In cases where the room owner needs listeners’ consent to make them speakers, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `pickSeat`.


### kickSeat

This API is used to remove a speaker (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onAnchorLeaveSeat` notification.

```java
public abstract void kickSeat(String userId, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------------- |
| userId | String | User ID of the speaker to remove |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the speaker list.


## Local Audio APIs

### startMicrophone

This API is used to enable mic capturing.

```java
public abstract void startMicrophone();
```

### stopMicrophone

This API is used to stop mic capturing.

```java
public abstract void stopMicrophone();
```

### setAudioQuality

This API is used to set audio quality.

```java
public abstract void setAudioQuality(int quality);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int | Audio quality. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute the local audio.

```java
public abstract void muteLocalAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | Mutes/Unmutes. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to turn the speaker on.

```java
public abstract void setSpeaker(boolean useSpeaker);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | `true`: speaker; `false`: receiver |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```java
public abstract void setAudioCaptureVolume(int volume);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---- | ----------------------------- |
| volume | int | Capturing volume. Value range: 0-100 (default: 100) |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```java
public abstract void setAudioPlayoutVolume(int volume);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---- | ----------------------------- |
| volume | int | Playback volume. Value range: 0-100 (default: 100) |

### muteRemoteAudio

This API is used to mute/unmute a specified member.

```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | --------------------------------- |
| userId | String | Specified user ID |
| mute | boolean | `true`: mute; `false`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all members.

```java
public abstract void muteAllRemoteAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------- | --------------------------------- |
| mute | boolean | `true`: mute; `false`: unmute |

   

## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).

```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in the room, which is generally used for on-screen comments.

```java
public abstract void sendRoomTextMsg(String message, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| message | String | Text message |
| callback | ActionCallback | Callback for sending result |

   

### sendRoomCustomMsg

This API is used to send custom text messages.

```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------------------------------------------- |
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| callback | ActionCallback | Callback for sending result |

   

## Invitation Signaling APIs

### sendInvitation

This API is used to send an invitation.

```java
public abstract String sendInvitation(String cmd, String userId, String content, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ---------------- |
| cmd      | String         | Custom command of business |
| userId   | String         | Invitee’s user ID  |
| content  | String         | Invitation content     |
| callback | ActionCallback | Callback for sending result |

Returned value:

| Returned Value | Type | Description |
| -------- | ------ | --------------------- |
| inviteId | String | Invitation ID |

### acceptInvitation

This API is used to accept an invitation.

```java
public abstract void acceptInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for sending result |

### rejectInvitation

This API is used to decline an invitation.

```java
public abstract void rejectInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for sending result |


### cancelInvitation

This API is used to cancel an invitation.

```java
public abstract void cancelInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for sending result |

[](id:TRTCChatSalonDelegate)
## `TRTCChatSalonDelegate` Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```java
void onError(int code, String message);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Error message |


### onWarning

Callback for warning.

```java
void onWarning(int code, String message);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Warning message |

   

### onDebugLog

Callback for log.

```java
void onDebugLog(String message);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| message | String | Log information |

   


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the owner terminates the room, all users in the room will receive this callback.

```java
void onRoomDestroy(String roomId);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | --------- |
| roomId | String | Room ID |


### onRoomInfoChange

Callback for successful room entry. The information in `roomInfo` is passed in by the room owner during room creation.

```java
void onRoomInfoChange(TRTCChatSalonDef.RoomInfo roomInfo);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | Room information |

   

### onUserVolumeUpdate

Callback of the volume of each member in the room after the volume reminder is enabled.

```java
void onUserVolumeUpdate(String userId, int volume);

```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------------------------- |
| userId | String | User ID |
| volume | int | Volume. Value range: 0-100 |


## Speaker List Callback APIs

### onAnchorEnterSeat

Someone became a speaker after requesting or being invited by the room owner.

```java
void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo user);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | -------- | -------------------- |
| user | UserInfo | Details of the user who became a speaker |

### onAnchorLeaveSeat

A speaker became a listener or was moved to listeners by the room owner.

```java
void onAnchorLeaveSeat(TRTCChatSalonDef.UserInfo user);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | -------- | -------------------- |
| user | UserInfo | Details of the user who became a listener |


### onSeatMute

The room owner muted a speaker.

```java
void onSeatMute(String userId, boolean isMute);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------- | ---------------------------------- |
| userId | String | ID of the speaker who was muted |
| isMute | boolean | `true`: muted; `false`: unmuted |



## Callback APIs for Room Entry/Exit by Listener

### onAudienceEnter

A listener entered the room.

```java
void onAudienceEnter(TRTCChatSalonDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the user who entered the room |

### onAudienceExit

A listener exited the room.

```java
void onAudienceExit(TRTCChatSalonDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who exited the room |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.

```java
void onRecvRoomTextMsg(String message, TRTCChatSalonDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | ---------------- |
| message | String | Text message |
| userInfo | UserInfo | User information of sender |

   

### onRecvRoomCustomMsg

A custom message was received.

```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCChatSalonDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------- | -------------------------------------------------- |
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| userInfo | UserInfo | User information of sender                                   |

## Invitation Signaling Event Callbacks

### onReceiveNewInvitation

A new invitation was received.

```java
void onReceiveNewInvitation(String id, String inviter, String cmd, String content);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | -------- | ---------------------------------- |
| id      | String   | Invitation ID                          |
| inviter | String   | Inviter’s user ID                  |
| cmd     | String   | Custom command word specified by business |
| content | UserInfo | Content specified by business                   |

### onInviteeAccepted

The invitee accepted the invitation.

```java
void onInviteeAccepted(String id, String invitee);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ------------------- |
| id      | String | Invitation ID           |
| invitee | String | Invitee’s user ID |

### onInviteeRejected

The invitee declined the invitation.

```java
void onInviteeRejected(String id, String invitee);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ------------------- |
| id      | String | Invitation ID           |
| invitee | String | Invitee’s user ID |

### onInvitationCancelled

The inviter canceled the invitation.

```java
void onInvitationCancelled(String id, String inviter);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ----------------- |
| id      | String | Invitation ID         |
| inviter | String | Inviter’s user ID |

### onInvitationTimeout

The invitation timed out.

```java
void onInvitationTimeout(String id);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ----------------- |
| id      | String | Invitation ID         |
