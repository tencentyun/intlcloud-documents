`TRTCChatSalon` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a chat salon and become a speaker, or enter a salon as a listener.
- The room owner can allow a listener to become a speaker as well as remove a speaker.
- A listener can request to speak and become a speaker. A speaker can also become a listener.
- All users can send text messages.

`TRTCChatSalon` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Chat Salon (Flutter)](https://intl.cloud.tencent.com/document/product/647/39805).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio chat component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the speaker list, and invitation signaling is used to send requests to speak or invite others to speak.

<span id="TRTCChatSalon"></span>

## TRTCChatSalon API Overview

### Basic SDK APIs

| API | Description |
| ----------------------------------------------- | -------------- |
| [sharedInstance](#sharedinstance) | Gets singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates singleton object. |
| [registerListener](#registerlistener)           | Sets event listener. |
| [unRegisterListener](#unregisterlistener)       | Terminates event listener. |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile)               | Sets profile. |

### Room APIs

| API | Description |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates room (called by room owner). If the room does not exist, the system will automatically create one. |
| [destroyRoom](#destroyroom) | Terminates room (called by room owner). |
| [enterRoom](#enterroom) | Enters room (called by listener). |
| [exitRoom](#exitroom) | Exits room (called by listener). |
| [getRoomInfoList](#getroominfolist) | Gets room list details.                                     |
| [getRoomMemberList](#getroommemberlist) | Gets the information of all users in room. |
| [getArchorInfoList](#getarchorInfolist) | Gets the list of speakers in room. |
| [getUserInfoList](#getuserinfolist)     | Gets the user information of a specified `userId`. |

### Mic APIs

| API | Description |
| --------------------- | ----------------------------------- |
| [enterMic](#entermic) | Becomes a speaker.                          |
| [leaveMic](#leavemic) | Becomes a listener.                          |
| [muteMic](#mutemic)   | Mutes/Unmutes a speaker (called by room owner). |
| [kickMic](#kickmic)   | Removes a speaker (called by room owner). |

### Local audio APIs

| API | Description |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Enables mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker)                       | Turns on speaker.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume.       |


### Remote audio APIs

| API | Description |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | Mutes/Unmutes specified member. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all members. |

### Background music and sound effect APIs

| API | Description |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets background music and sound effect management object [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa). |

### Message sending APIs

| API | Description |
| ----------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts text message in room. This API is generally used for on-screen comments. |

### Signaling APIs for requesting to speak

| API | Description |
| ------------------------------- | -------------- |
| [raiseHand](#raisehand)         | A listener requests to speak. |
| [agreeToSpeak](#agreetospeak)   | The room owner approves the request. |
| [refuseToSpeak](#refusetospeak) | The room owner declines the request. |

<span id="TRTCChatSalonDelegate"></span>
## TRTCChatSalonDelegate API Overview

### Common event callback APIs

| API | Description |
| ----------------------------------- | ---------- |
| [onError](#onerror)                 | Error |
| [onWarning](#onwarning)             | Warning |
| [onKickedOffline](#onkickedoffline) | Warning |

### Room event callback APIs

| API | Description |
| ----------------------------------------- | ------------------------ |
| [onRoomDestroy](#onroomdestroy) | Room termination |
| [onAnchorListChange](#onanchorlistchange) | Speaker list change |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Speaker list change callback APIs

| API | Description |
| ------------------------------------- | ------------------------------------- |
| [onAnchorEnterMic](#onanchorentermic) | Someone became a speaker after requesting or being invited by the room owner. |
| [onAnchorLeaveMic](#onanchorleavemic) | Someone became a listener or was moved to listeners by the room owner. |
| [onMicMute](#onmicmute)               | The room owner muted a speaker. |

### Callback APIs for room entry/exit by listeners

| API | Description |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | A listener entered the room. |
| [onAudienceExit](#onaudienceexit) | A listener exited the room. |

### Message event callback APIs

| API | Description |
| --------------------------------------- | -------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | Receipt of text message   |

### Mic-on Request Signaling Event Callback APIs

| API | Description |
| -------------------------------------- | ---------------------------------------- |
| [onRaiseHand](#onraisehand) | A listener raised hand to request to speak. |
| [onAgreeToSpeak](#onagreetospeak)   | The room owner approved the listener's request. |
| [onRefuseToSpeak](#onrefusetospeak)    | The room owner declined the listener's request. |

## Basic SDK APIs

### sharedInstance

This API is used to get a `TRTCChatSalon` singleton object.

```dart
 static Future<TRTCChatSalon> sharedInstance()
```


### destroySharedInstance

This API is used to terminate a `TRTCChatSalon` singleton object.

>?After the instance is terminated, the externally cached `TRTCChatSalon` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```dart
static void destroySharedInstance()
```

### registerListener

This API is used to set an event listener.

```
void registerListener(VoiceListenerFunc func)
```

>?`setDelegate` is the delegate callback of `TRTCChatSalon`.   

### unRegisterListener

This API is used to remove the component event listener.

```dart
void unRegisterListener(VoiceListenerFunc func)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ----------------- | --------------------------------------------------------- |
| func | VoiceListenerFunc | Various status notifications in `TRTCChatSalon` will be sent to the function you specify. |


### login

This API is used to log in.

```dart
Future<ActionCallback> login(int sdkAppId, String userId, String userSig)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------ | ------------------------------------------------------------ |
| sdkAppId | int | You can view the `SDKAppID` via **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC console. |
| userId | String | ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig  | String | Tencent Cloud's proprietary security signature. To get one, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |


### logout

This API is used to log out.

```dart
Future<ActionCallback> logout()
```

### setSelfProfile

This API is used to set profile.

```dart
Future<ActionCallback> setSelfProfile(String userName, String avatarURL)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ---------- |
| userName | String | Nickname |
| avatarURL | String | Profile photo address |

## Room APIs

### createRoom

This API is used to create a room.

```
Future<ActionCallback> createRoom(int roomId, RoomParam roomParam)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | --------- | ------------------------------------------------------------ |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated as a chat salon room list. Currently, Tencent Cloud does not provide the chat salon room list management service. Please manage the list on your own. |
| roomParam | RoomParam | Room information, such as room name and cover information. |

The process of creating a salon and becoming a speaker is as follows: 

1. A user calls `createRoom` to create a chat salon, passing in room attributes such as room ID.
2. The user will also receive an `onAnchorEnterMic` notification that someone became a speaker, and mic capturing will be enabled automatically.

### destroyRoom

This API is used to terminate a room (called by room owner).

```dart
Future<ActionCallback> destroyRoom()
```


### enterRoom

This API is used to enter a room (called by listener).

```dart
Future<ActionCallback> enterRoom(int roomId)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ---------- |
| roomId | int | Room ID. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest chat salon list from your server. The list may contain `roomId` and room information of multiple chat salons.
2. The user selects a chat salon and calls `enterRoom` with the room ID passed in to enter the room.
3. After entering the room, the user can call `getArchorInfoList` to get the speaker list and call `getRoomMemberList` to get the list of all users in the room. The listener list can be obtained by subtracting the speaker list from the user list.
4. The user will also receive an `onAnchorEnterMic` notification that someone became a speaker.

### exitRoom

This API is used to exit a room.

```dart
Future<ActionCallback> exitRoom()
```

### getRoomInfoList

This API is used to get the room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?You don’t need this API if both the room list and room information are managed on your server.


```dart
Future<RoomInfoCallback> getRoomInfoList(List<String> roomIdList)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------- | ------------ |
| roomIdList | List&lt;Integer&gt; | Room ID list |


### getRoomMemberList

This API is used to get the list of all members in the room.

>?In an IM live chat group, only the list of the last 31 members can be pulled by default.


```dart
Future<MemberListCallback> getRoomMemberList(double nextSeq)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------------------------------------------------ |
| nextSeq | double | Pulling-by-page flag. It is set to 0 when the information is pulled for the first time. If the callback succeeds and `nextSeq` is not 0, pagination is needed. The value of this parameter is passed in for the next pull until the value becomes 0. |

### getArchorInfoList

This API is used to get the list of speakers in the room.

```dart
Future<UserListCallback> getArchorInfoList()
```


### getUserInfoList

This API is used to get the user information of a specified `userId`.

```dart
Future<UserListCallback> getUserInfoList(List<String> userIdList)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------ | ------------------------------------------------------------ |
| userIdList | List&lt;String&gt; | List of the user IDs to obtain. If this parameter is `null`, the information of all users in the room is obtained. |


## Mic APIs

### enterMic

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onAnchorEnterSeat` notification.

```
Future<ActionCallback> enterMic();
```

Calling this API will immediately modify the speaker list. A listener needs to call `raiseHand` first to send a request to the room owner and call this API after receiving `onAgreeToSpeak`.

### leaveMic

This API is used to become a listener.

>?After a speaker becomes a listener, all members in the room will receive an `onAnchorLeaveMic` notification.

```dart
Future<ActionCallback> leaveMic()
```

### muteMic

This API is used to mute/unmute a speaker (called by room owner).

>? After the speaker status is changed, all members in the room will receive `onAnchorListChange` and `onMicMute` notifications.

```dart
Future<ActionCallback> muteMic(bool mute)
```

### kickMic

This API is used to remove a listener (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onAnchorLeaveMic` notification.

```dart
Future<ActionCallback> kickMic(String userId)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------------- |
| userId | String | ID of the speaker to remove |

Calling this API will immediately modify the speaker list.


## Local Audio APIs

### startMicrophone

This API is used to enable mic capturing.

```dart
void startMicrophone(int quality)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int | Audio quality. For more information, please see [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |

### stopMicrophone

This API is used to stop mic capturing.

```dart
void stopMicrophone()
```

### muteLocalAudio

This API is used to mute/unmute local audio.

```dart
void muteLocalAudio(bool mute)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | Mutes/Unmutes. For more information, please see [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |


### setSpeaker

This API is used to turn on the speaker.

```dart
void setSpeaker(bool useSpeaker)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | `true`: speaker; `false`: receiver |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```dart
void setAudioCaptureVolume(int volume)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ----------------------------- |
| volume | int | Capture volume level. Value range: 0-100 (default value: 100) |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```dart
void setAudioPlayoutVolume(int volume)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ----------------------------- |
| volume | int | Playback volume. Value range: 0-100 (default value: 100) |

### muteRemoteAudio

This API is used to mute/unmute a specified member.

```dart
void muteRemoteAudio(String userId, bool mute)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | --------------------------------- |
| userId | String | Specified user ID |
| mute | boolean | `true`: mute; `false`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all members.

```dart
void muteAllRemoteAudio(bool mute)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | --------------------------------- |
| mute | boolean | `true`: mute; `false`: unmute |


## Background Music and Sound Effect APIs

### getAudioEffectManager

This API is used to get the background music and sound effect management object [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).

```dart
TXAudioEffectManager getAudioEffectManager()
```


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in the room, which is generally used for on-screen comment chat.

```dart
Future<ActionCallback> sendRoomTextMsg(String message)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Text message |

   

## Mic-on Request Signaling APIs

### raiseHand

This API is used by a listener to request to speak.

```dart
void raiseHand()
```

### agreeToSpeak

This API is used by the room owner to approve a request to speak.

```dart
Future<ActionCallback> agreeToSpeak(String userId)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------- |
| userId | String | User ID |

### refuseToSpeak

This API is used by the room owner to decline a request to speak.

```dart
Future<ActionCallback> refuseToSpeak(String userId)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------- |
| userId | String | User ID |


## TRTCChatSalonDelegate Event Callback

## Common Event Callback APIs

### onError

Callback for error.

>? This callback indicates that the SDK encounters an irrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending on the situation.


The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | -------------------------------------------------------- |
| errCode | int | Error code |
| errMsg | String | Error message |
| extraInfo | String | Extended field. Certain error codes may carry extra information for troubleshooting. |

### onWarning

Callback for warning.

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ------ | -------------------------------------------------------- |
| warningCode | int | Warning code |
| warningMsg  | String     | Warning information                                                   |
| extraInfo | String | Extended field. Certain error codes may carry extra information for troubleshooting. |


### onKickedOffline

Another user logged in using the same account, and the current user was forced offline.


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the room owner terminates the room, all users in the room will receive this callback.

### onAnchorListChange

The speaker list changed.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ---------- |
| userId | String | User ID |
| mute | bool | Mute status |


### onUserVolumeUpdate

Volume notifications sent to all members after the volume reminder is enabled.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------------------- |
| userId | String | User ID |
| volume | int | Volume. Value range: 0-100 |


## Speaker List Callback APIs


### onAnchorEnterMic

A user became a speaker.

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | -------------------- |
| userId     | String | ID of the user who became a speaker       |
| userName   | String | User nickname          |
| userAvatar | String | Profile photo address           |
| mute       | bool   | Speaker status. Default value: unmuted |

### onAnchorLeaveMic

A speaker became a listener.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------- |
| userId | String | ID of the user who became a listener |

### onMicMute

Whether the room owner muted a speaker.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------- |
| userId | String | ID of the user to mute |
| mute   | bool   | Speaker status     |


## Callback APIs for Room Entry/Exit by Listeners

### onAudienceEnter

A listener entered the room.


The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | -------------- |
| userId | String | ID of the user who entered the room |
| userName   | String | User nickname     |
| userAvatar | String | Profile photo address |

### onAudienceExit

A listener exited the room.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------- |
| userId | String | ID of the user who exited the room |


## Message Event Callback APIs

### onRecvRoomTextMsg

Receipt of text message.

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | ---------------- |
| message | String | Text message |
| sendId     | String | Sender’s user ID   |
| userAvatar | String | Sender’s profile photo |
| userName   | String | Sender’s nickname |


## Raise-Hand Signaling Event Callback APIs

### onRaiseHand

A request to speak was received.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------------ |
| userId | String | ID of the user who raised hand |


### onAgreeToSpeak

The room owner approved the request.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------- |
| userId | String | Room owner's user ID |

### onRefuseToSpeak

The room owner rejected the request.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | -------------- |
| userId | String | Room owner's user ID |
