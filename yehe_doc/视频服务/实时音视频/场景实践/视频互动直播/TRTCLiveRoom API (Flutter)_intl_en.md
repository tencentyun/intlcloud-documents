`TRTCLiveRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a room and start live streaming, or enter a room as audience.
- The anchor and audience in a room can co-anchor with each other.
- Anchors in two rooms can compete and interact with each other.
- All users can send text and custom messages. Custom messages can be used to send on-screen comments, give likes, and send gifts.

`TRTCLiveRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Interactive Live Video Streaming (Flutter)](https://intl.cloud.tencent.com/document/product/647/41944).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) is used as the low-latency live streaming component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996) is used to implement chat rooms, and IM messages are used to facilitate the co-anchoring process between anchors.

[](id:TRTCLiveRoom)

## `TRTCLiveRoom` API Overview

### Basic SDK APIs

| API | Description |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets a singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [registerListener](#registerlistener)                     | Registers an event listener.                                   |
| [unRegisterListener](#unregisterlistener)     | Removes an event listener. |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets profile. |

### Room APIs

| API | Description |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates a room (called by anchor). If the room does not exist, the system will automatically create a room. |
| [destroyRoom](#destroyroom) | Closes a room (called by anchor). |
| [enterRoom](#enterroom) | Enters a room (called by audience). |
| [exitRoom](#exitroom) | Exits a room (called by audience). |
| [getRoomInfos](#getroominfos)           | Gets room list details.                                     |
| [getAnchorList](#getanchorlist) | Gets the anchor and co-anchors in a room. This API works only if it is called after `enterRoom()`. |
| [getRoomMemberList](#getroommemberlist) | Gets the list of all users in a room. This API works only if it is called after `enterRoom()`.      |

### Stream pushing/pulling APIs

| API                                             | Description                                                         |
| ----------------------------------------- | -------------------------------------------------- |
| [startCameraPreview](#startcamerapreview) | Enables preview of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [startPublish](#startpublish)             | Starts live streaming (pushing streams).                                 |
| [stopPublish](#stoppublish)               | Stops live streaming (pushing streams).                                 |
| [startPlay](#startplay) | Plays a remote video. This API can be called in common playback and co-anchoring scenarios. |
| [stopPlay](#stopplay)                     | Stops rendering a remote video.                             |

### APIs for co-anchoring between anchors and audience

| API                                             | Description                                                         |
| ----------------------------------------- | ------------------ |
| [requestJoinAnchor](#requestjoinanchor) | Requests co-anchoring (called by audience). |
| [responseJoinAnchor](#responsejoinanchor) | Responds to a co-anchoring request (called by anchor). |
| [kickoutJoinAnchor](#kickoutjoinanchor) | Removes a user from co-anchoring (called by anchor). |

### APIs for cross-room anchor competition

| API                                             | Description                                                         |
| --------------------------------- | ---------------------- |
| [requestRoomPK](#requestroompk) | Requests cross-room competition (called by anchor). |
| [responseRoomPK](#responseroompk) | Responds to a cross-room competition request (called by anchor). |
| [quitRoomPK](#quitroompk)         | Quits cross-room competition.          |

### Audio/Video APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ------------------ |
| [switchCamera](#switchcamera) | Switches between the front and rear cameras. |
| [setMirror](#setmirror)                   | Sets the mirror mode. |
| [muteLocalAudio](#mutelocalaudio) | Mutes/Unmutes the local user. |
| [muteRemoteAudio](#muteremoteaudio) | Mutes/Unmutes a remote user. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all remote users. |

### Background music and audio effect APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html). |

### Beauty filter APIs

| API                                             | Description                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html). |

### Message sending APIs

| API                                     | Description                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ----------------------------------- | ---------------------------------- |
| [onError](#onerror)                 | Error                         |
| [onWarning](#onwarning)             | Warning                         |
| [onKickedOffline](#onkickedoffline) | You were kicked offline because another user logged in to the account. |

### Room event callback APIs

| API                                             | Description                                                         |
| --------------------------------------------- | ---------------------------------------------------- |
| [onEnterRoom](#onenterroom)                   | You entered the room.                                       |
| [onUserVideoAvailable](#onuservideoavailable) | Whether a remote user has playable video in the primary stream (usually used for camera images) |
| [onRoomDestroy](#onroomdestroy)               | The room was closed.                                   |

### Callback APIs for anchors and audience

| API                                             | Description                                                         |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter) | An anchor entered the room. |
| [onAnchorExit](#onanchorexit)       | An anchor left the room.   |
| [onAudienceEnter](#onaudienceenter) | A viewer entered the room.    |
| [onAudienceExit](#onaudienceexit) | A viewer left the room. |

### Callback APIs for co-anchoring between anchors and audience

| API                                             | Description                                                         |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | A co-anchoring request was received. |
| [onAnchorAccepted](#onanchoraccepted)       | The co-anchoring request was accepted.       |
| [onAnchorRejected](#onanchorrejected)       | The co-anchoring request was rejected.       |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | A user was removed from co-anchoring. |

### Anchor competition callback APIs

| API                                             | Description                                                         |
| ------------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk) | A cross-room competition request was received. |
| [onRoomPKAccepted](#onroompkaccepted) | The cross-room competition request was accepted. |
| [onRoomPKRejected](#onroompkrejected) | The cross-room competition request was rejected. |
| [onQuitRoomPK](#onquitroompk) | The cross-room competition ended. |

### Message event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | Receipt of a text message  |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of a custom message |

## Basic SDK APIs

### sharedInstance

This API is used to get a [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) singleton object.

```java
 static Future<TRTCLiveRoom> sharedInstance()
```

### destroySharedInstance

This API is used to terminate a [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) singleton object.

>?After the instance is terminated, the externally cached `TRTCLiveRoom` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```java
static void destroySharedInstance()
```

### registerListener

This API is used to get the event callback of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944). You can use `TRTCLiveRoomDelegate` to get various status notifications of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944).

```java
void registerListener(VoiceListenerFunc func);
```

>?`registerListener` is the delegate callback of `TRTCLiveRoom`.   


### unRegisterListener

This API is used to remove the event listener.

```java
void unRegisterListener(VoiceListenerFunc func);
```


### login

This API is used to log in.

```java
Future<ActionCallback> login(
      int sdkAppId, String userId, String userSig, TRTCLiveRoomConfig config);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppId | int | You can view the `SDKAppID` via **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC console. |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For how to obtain it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| config | TRTCLiveRoomConfig | Global configuration information, which needs to be initialized during login and cannot be modified afterwards. <ul style="margin:0;"><li>`useCDNFirst`: specifies the way audience watch live streams. `true` means watching over CDNs, which is cost-efficient but has high latency. `false` means watching under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second. </li><li>`CDNPlayDomain`: specifies the domain name for CDN live streaming. It takes effect only if `useCDNFirst` is set to `true`. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** of the CSS console.</li></ul> |

### logout

This API is used to log out.

```java
Future<ActionCallback> logout();
```

### setSelfProfile

This API is used to set profile.

```java
Future<ActionCallback> setSelfProfile(String userName, String avatarURL);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ---------- |
| userName | String | Nickname |
| avatarURL | String | Profile photo address |

## Room APIs

### createRoom

This API is used to create a room (called by anchor).

```java
Future<ActionCallback> createRoom(int roomId, TRTCCreateRoomParam roomParam);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | --------- | ------------------------------------------------------------ |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomId` values can be aggregated into a live room list. Currently, Tencent Cloud does not provide list management services. Please manage the list on your own. |
| roomParam | RoomParam | Room information, such as room name and cover information. If both the room list and room information are managed on your server, you can ignore this parameter. |

The process of creating a room and starting live streaming as an anchor is as follows: 

1. A user calls `startCameraPreview()` to enable camera preview and set beauty filters. 
2. The user calls `createRoom()` to create a room, the result of which is returned via the `ActionCallback` callback.
3. The user calls `starPublish()` to push streams.

### destroyRoom

This API is used to close a room (called by anchor).

```java
Future<ActionCallback> destroyRoom();
```


### enterRoom

This API is used to enter a room (called by audience).

```java
Future<ActionCallback> enterRoom(int roomId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ---------- |
| roomId | int | Room ID |

The process of entering a room and starting playback as audience is as follows: 

1. A user gets the latest room list from your server. The list may contain `roomId` and other room information of multiple rooms.
2. The user selects a room and calls `enterRoom()` to enter the room.
3. The user calls `startPlay(userId)`, passing in the anchor's `userId` to start playback.
 - If the room list contains the anchor's `userId`, the user can call `startPlay(userId)` to start playback.
 - If the user does not have the anchor's `userId` before room entry, he or she can find it in the `onAnchorEnter(userId)` callback of `TRTCLiveRoomDelegate`, which is returned after room entry. The user can then call `startPlay(userId)` to start playback. 

### exitRoom

This API is used to leave a room.

```java
Future<ActionCallback> exitRoom();
```


### getRoomInfos

This API is used to get room list details, which are set by anchors via `roomInfo` when they call `createRoom()`.

>?You don't need this API if both the room list and room information are managed on your server.


```java
Future<RoomInfoCallback> getRoomInfos(List<String> roomIdList);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------ | ------------ |
| roomIdList | List&lt;String&gt; | Room ID list |

### getAnchorList

This API is used to get the anchor and co-anchors in a room. It takes effect only if it is called after `enterRoom()`.

```java
Future<UserListCallback> getAnchorList();
```

### getRoomMemberList

This API is used to get the information of all audience in the room. It takes effect only if it is called after `enterRoom()`.

```java
Future<UserListCallback> getRoomMemberList(int nextSeq)
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ------------------------------------------------------------ |
| nextSeq | int | Pulling-by-page flag. It is set to 0 when the information is pulled for the first time. If the callback succeeds and `nextSeq` is not 0, pagination is needed. The value of this field is passed in for the next pull until the value becomes 0. |

   

## Stream Pushing/Pulling APIs

### startCameraPreview

This API is used to enable local video preview.

```java
Future<void> startCameraPreview(bool isFrontCamera, int viewId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------- | ---- | ------------------------------------- |
| isFrontCamera | bool | `true`: turns the front camera on; `false`: turns the rear camera on. |
| viewId  | int  | Called back video view ID                 |

### stopCameraPreview

This API is used to stop local video capturing and preview.

```java
  Future<void> stopCameraPreview();
```

   

### startPublish

This API is used to start live streaming (pushing streams), which can be called in the following scenarios:
- An anchor starts live streaming.
- A viewer starts co-anchoring.

```java
Future<void> startPublish(String streamId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------- | ------------------------------------------------------------ |
| streamId | String? | The `streamId` used to bind live streaming CDNs. You need to specify the `streamId` of the anchor if you want audience to play the anchor's streams via live streaming CDNs. |


### stopPublish

This API is used to stop live streaming (pushing streams), which can be called in the following scenarios:
- An anchor ends live streaming.
- A viewer ends co-anchoring.


```java
Future<void> stopPublish();
```

### startPlay

This API is used to play a remote video. It can be called in common playback and co-anchoring scenarios.

```java
Future<void> startPlay(String userId, int viewId);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------------------ |
| userId | String | ID of the user whose video is to be played |
| viewId | int    | Called back video view ID |

- **Common playback:**
    - If the room list contains the anchor's `userId`, audience can call `startPlay(userId)` to play the anchor's video after `enterRoom()`.
    - If audience do not have the anchor's `userId` before room entry, they can find it in the `onAnchorEnter(userId)` callback of `TRTCLiveRoomDelegate`, which is returned after room entry. They can then call `startPlay(userId)` to play the anchor's video.

- **Co-anchoring:**
After co-anchoring is initiated, the anchor will receive the `onAnchorEnter(userId)` callback from `TRTCLiveRoomDelegate` and can call `startPlay(userId), passing in the `userId` returned by the callback to play co-anchoring video.

### stopPlay

This API is used to stop rendering remote video. It needs to be called when the `onAnchorExit()` callback is received.

```java
Future<void> stopPlay(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ---------------- |
| userId | String | ID of the remote user |

## APIs for Co-anchoring Between Anchor and Audience

### requestJoinAnchor

This API is used by audience to send a co-anchoring request.

```java
Future<ActionCallback> requestJoinAnchor();
```

The process of co-anchoring between anchor and audience is as follows:

1. A **viewer** calls `requestJoinAnchor()` to send a co-anchoring request to the anchor.
2. The **anchor** receives the `onRequestJoinAnchor()` callback of `TRTCLiveRoomDelegate`.
3. The **anchor** calls `responseJoinAnchor()` to accept or reject the co-anchoring request.
4. The **viewer** receives the `responseCallback` callback, which carries the anchor's response.
5. If the request is accepted, the **viewer** calls `startCameraPreview()` to enable local camera preview.
6. The **viewer** calls `startPublish()` to push streams.
7. After the viewer starts pushing streams, the **anchor** receives the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate`.
8. The **anchor** calls `startPlay()` to play the co-anchoring viewer's video.
9. If there are other viewers co-anchoring with the anchor in the room, the new co-anchoring **viewer** will receive the `onAnchorEnter()` callback and can call `startPlay()` to play other co-anchoring viewers' video.

   

### responseJoinAnchor

This API is used by anchors to respond to a co-anchoring request after receiving the `onRequestJoinAnchor()` callback of `TRTCLiveRoomDelegate`.

```java
Future<ActionCallback> responseJoinAnchor(String userId, boolean agreee);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------------------------- |
| userId | String  | User ID of the viewer                  |
| agree | bool | `true`: accepts; `false`: rejects. |


### kickoutJoinAnchor

This API is used by anchors to remove a user from co-anchoring. After this API is called, the removed user will receive the `onKickoutJoinAnchor()` callback of `TRTCLiveRoomDelegate`.

```java
Future<ActionCallback> kickoutJoinAnchor(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------------- |
| userId | String | ID of the co-anchoring user |


## APIs for Cross-Room Anchor Competition

### requestRoomPK

This API is used by anchors to request cross-room competition.

```java
Future<ActionCallback> requestRoomPK(int roomId, String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------------- |
| roomId | int | Room ID of the anchor to call |
| userId | String | User ID of the anchor to call |

Two anchors in different rooms can compete with each other. The process is as follows:

1. **Anchor A** calls `requestRoomPK()` to send a co-anchoring request to anchor B.
2. **Anchor B** receives the `onRequestRoomPK()` callback of `TRTCLiveRoomDelegate`.
3. **Anchor B** calls `responseRoomPK()` to respond to the competition request.
4. After accepting the request, **anchor B** waits for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and calls `startPlay()` to play anchor A's video.
5. **Anchor A** receives the `onRoomPKAccepted` or `onRoomPKRejected` callback.
6. If the request is accepted, **anchor A** waits for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and calls `startPlay()` to play anchor B's video.

   

### responseRoomPK

This API is used by anchors to respond to a cross-room competition request, after which the request sending anchor will receive the `responseCallback` callback, which carries the response passed in to `requestRoomPK`.

```java
Future<ActionCallback> responseRoomPK(String userId, boolean agree);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------------------------- |
| userId | String | User ID of the anchor sending the competition request |
| agree | bool | `true`: accepts; `false`: rejects. |


### quitRoomPK

This API is used to quit cross-room competition. If either anchor quits cross-room competition, the other anchor will receive the `onQuitRoomPk()` callback of `TRTCLiveRoomDelegate`.

```java
Future<ActionCallback> quitRoomPK();
```


## Audio/Video APIs

### switchCamera

This API is used to switch between the front and rear cameras.

```java
Future<void> switchCamera(boolean isFrontCamera);
```

### setMirror

This API is used to set the mirror mode.

```java
Future<void> setMirror(boolean isMirror);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ---- | --------------- |
| isMirror | bool | Enables/Disables mirroring. |

   

### muteLocalAudio

This API is used to mute or unmute the local user.

```java
Future<void> muteLocalAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ---- | --------------------------------- |
| mute | boolean | `true`: mute; `false`: unmute |

   

### muteRemoteAudio

This API is used to enable the hands-free mode.

```java
Future<void> muteRemoteAudio(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | --------------------------------- |
| userId | String | ID of the remote user |
| mute | boolean | `true`: mute; `false`: unmute |

   

### muteAllRemoteAudio

This API is used to mute or unmute all remote users.

```java
Future<void> muteAllRemoteAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ---- | --------------------------------- |
| mute | boolean | `true`: mute; `false`: unmute |

   

## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html).

```java
getAudioEffectManager();
```


## Beauty Filter APIs

### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html).

```java
getBeautyManager();
```

You can do the following using `TXBeautyManager`:

- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in a room, which is generally used for on-screen comments.

```java
Future<ActionCallback> sendRoomTextMsg(String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Text message |

### sendRoomCustomMsg

This API is used to send a custom text message.

```java
Future<ActionCallback> sendRoomCustomMsg(String cmd, String message);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | -------------------------------------------------- |
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |


## `TRTCLiveRoomDelegate` Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>?This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errMsg    | String | Error message |


### onWarning

Callback for warning.

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ------ | ---------- |
| warningCode | int | Warning code |
| warningMsg  | String     | Warning message |


### onKickedOffline

Callback for being kicked offline because another user logged in to the same account.




## Room Event Callback APIs

### onRoomDestroy

Callback for room closing. All users in the room will receive this callback after the anchor leaves the room.

### onEnterRoom

Callback for room entry by the local user.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------------- |
| result | int | If `result` is greater than 0, it indicates the time (ms) room entry took; if `result` is less than 0, it represents the error code for room entry. |

### onUserVideoAvailable

Callback for whether a remote user has playable video in the primary stream (usually used for camera images).

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------ | -------------- |
| userId    | String | User ID |
| available | boolean | Whether the user's video is enabled |

## Callback APIs for Anchors and Audience

### onAnchorEnter

Callback for a new anchor/co-anchoring viewer. Audience will receive this callback when there is a new anchor/co-anchoring viewer in the room and can call `startPlay()` of `TRTCLiveRoom` to play the video of the anchor/co-anchoring viewer.


The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---------- | ------ | --------------- |
| userId | String | User ID of the new anchor/co-anchoring viewer |
| userName | String | Username |
| userAvatar | String | Profile photo address |

### onAnchorExit

Callback for the quitting of a competing anchor/co-anchoring viewer. The anchor and co-anchoring viewers in a room will receive this callback after a competing anchor/co-anchoring viewer quits co-anchoring and can call `stopPlay()` of `TRTCLiveRoom` to stop playing the video of the competing anchor/co-anchoring viewer.

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---------- | ------ | -------------- |
| userId   | String | ID of the user who quitted co-anchoring  |
| userName | String | Username |
| userAvatar | String | Profile photo address |


### onAudienceEnter

Callback for room entry by a viewer.

```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------------------------- | ----------------------------------- |
| userInfo | TRTCLiveRoomDef.TRTCLiveUserInfo | Information of the viewer who enters the room, such as user ID, nickname, and profile photo. |


### onAudienceExit

Callback for room exit by a viewer.


The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---------- | ------ | -------------- |
| userId | String  | User ID of the viewer                  |
| userName | String | Username |
| userAvatar | String | Profile photo address |

### onRequestJoinAnchor

Callback for receiving a co-anchoring request from a viewer.


The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | ----------------- |
| userId | String | ID of the request sending user |
| userName | String | Username |
| userAvatar | String | Profile photo address |

### onAnchorAccepted

Callback for accepting a co-anchoring request.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------------- |
| userId | String | User ID of the anchor |


### onAnchorRejected

Callback for rejecting a co-anchoring request.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------------- |
| userId | String | User ID of the anchor |

### onKickoutJoinAnchor

Callback for being removed from co-anchoring. A co-anchoring viewer needs to call `stopPublish()` of `TRTCLiveRoom` to quit co-anchoring after receiving this callback.


## Anchor Competition Callback APIs

### onRequestRoomPK

Callback for receiving a cross-room competition request. If an anchor accepts the request after receiving this callback, he or she should wait for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and call `startPlay()` to play the other anchor's video.

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | ----------------- |
| userId | String | User ID of the request sending anchor |
| userName | String | Username |
| userAvatar | String | Profile photo address |

### onRoomPKAccepted

Callback for accepting a cross-room competition request.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------------- |
| userId | String | User ID of the anchor who accepted the request |

### onRoomPKRejected

Callback for rejecting a cross-room competition request.

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ----------------------- |
| userId | String | User ID of the anchor who rejected the request |


### onQuitRoomPK

Callback for ending cross-room competition.


## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.


The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Text message |


### onRecvRoomCustomMsg

A custom message was received.


The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | -------------------------------------------------- |
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |

