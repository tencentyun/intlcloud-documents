`TRTCLiveRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:
- A user can create a room and start live streaming, or enter a room as audience.
- The anchor and audience in a room can co-anchor with each other.
- Anchors in two rooms can compete and interact with each other.
- All users can send text and custom messages. Custom messages can be used to send on-screen comments, give likes, and send gifts.

`TRTCLiveRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Interactive Live Video Streaming (Android)](https://intl.cloud.tencent.com/document/product/647/36061).
- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) is used as a low-latency live streaming component.
- IM SDK: The `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996) is used to implement chat rooms, and IM messages are used to facilitate the co-anchoring process.

[](id:TRTCLiveRoom)
## `TRTCLiveRoom` API Overview

### Basic SDK APIs

| API | Description |
|-----|-----|
| [sharedInstance](#sharedinstance) | Gets a singleton object. |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where event callbacks are. |
| [login](#login) | Logs in. |
| [logout](#logout) | Logs out. |
| [setSelfProfile](#setselfprofile) | Sets the profile. |

### Room APIs

| API | Description |
|-----|-----|
| [createRoom](#createroom) | Creates a room (called by anchor). If the room does not exist, the system will create the room automatically. |
| [destroyRoom](#destroyroom) | Terminates a room (called by anchor). |
| [enterRoom](#enterroom) | Enters a room (called by audience). |
| [exitRoom](#exitroom) | Exits a room (called by audience). |
| [getRoomInfos](#getroominfos) | Gets room list details. |
| [getAnchorList](#getanchorlist) | Gets the anchors in a room. This API works only if it is called after `enterRoom()`. |
| [getAudienceList](#getaudiencelist) | Gets the information of all audience in a room. This API works only if it is called after `enterRoom()`. |

### Stream pushing/pulling APIs

| API | Description |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | Enables preview of the local video. |
| [stopCameraPreview](#stopcamerapreview) | Stops local video capturing and preview.|
| [startPublish](#startpublish) | Starts live streaming (pushing streams).|
| [stopPublish](#stoppublish) | Stops live streaming (pushing streams).|
| [startPlay](#startplay) | Plays a remote video. This API can be called in common playback and co-anchoring scenarios. |
| [stopPlay](#stopplay) | Stops rendering a remote video.|

### APIs for anchor-audience co-anchoring

| API | Description |
|-----|-----|
| [requestJoinAnchor](#requestjoinanchor) | Requests co-anchoring (called by audience).|
| [responseJoinAnchor](#responsejoinanchor) | Responds to a co-anchoring request (called by anchor).|
| [kickoutJoinAnchor](#kickoutjoinanchor) | Removes a user from co-anchoring (called by anchor).|

### APIs for cross-room anchor competition

| API | Description |
|-----|-----|
| [requestRoomPK](#requestroompk) | Requests cross-room competition (by anchor).|
| [responseRoomPK](#responseroompk) | Responds to a cross-room competition request (called by anchor).|
| [quitRoomPK](#quitroompk) | Quits cross-room competition.|

### Audio/Video APIs

| API | Description |
|-----|-----|
| [switchCamera](#switchcamera) | Switches between the front and rear cameras.|
| [setMirror](#setmirror) | Specifies whether to mirror video. |
| [muteLocalAudio](#mutelocalaudio) | Mutes/Unmutes the local user. |
| [muteRemoteAudio](#muteremoteaudio) | Mutes/Unmutes a remote user. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all remote users.|

### Background music and audio effect APIs

| API | Description |
|-----|-----|
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager). |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).|

### Message sending APIs

| API | Description |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

### Debugging APIs

| API | Description |
|-----|-----|
| [showVideoDebugLog](#showvideodebuglog) | Specifies whether to display debugging information on the UI. |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API Overview</h2>

### Common event callback APIs

| API | Description |
|-----|-----|
| [onError](#onerror) | Error|
| [onWarning](#onwarning) | Warning|
| [onDebugLog](#ondebuglog) | Log|

### Room event callback APIs

| API | Description |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | The room was terminated.|
| [onRoomInfoChange](#onroominfochange) | The room information changed. |

### Callback APIs for entry/exit of anchors/audience

| API | Description |
|-----|-----|
| [onAnchorEnter](#onanchorenter) | There is a new anchor in the room. |
| [onAnchorExit](#onanchorexit) | An anchor left the room.|
| [onAudienceEnter](#onaudienceenter) | A viewer entered the room.|
| [onAudienceExit](#onaudienceexit) | A viewer left the room.|

### Callback APIs for anchor-audience co-anchoring events

| API | Description |
|-----|-----|
| [onRequestJoinAnchor](#onrequestjoinanchor) | A co-anchoring request was received. |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | A user was removed from co-anchoring. |

### Callback APIs for anchor competition events

| API | Description |
|-----|-----|
| [onRequestRoomPK](#onrequestroompk) | A cross-room competition request was received.|
| [onQuitRoomPK](#onquitroompk) | Cross-room competition ended.|

### Message event callback APIs

| API | Description |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | A text message was received.|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | A custom message was received.|

## Basic SDK APIs

[](id:sharedInstance)
### sharedInstance

This API is used to get a [TRTCLiveRoom](https://cloud.tencent.com/document/product/647/43182) singleton object.
```java
 public static synchronized TRTCLiveRoom sharedInstance(Context context);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| context | Context | Android context, which will be converted to `ApplicationContext` for the calling of system APIs |

   

### destroySharedInstance

This API is used to terminate a [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061) singleton object.
>?After the instance is terminated, the externally cached `TRTCLiveRoom` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```java
public static void destroySharedInstance();
```

### setDelegate

This API is used to get callbacks for the events of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061). You can use `TRTCLiveRoomDelegate` to get the callbacks.
```java
public abstract void setDelegate(TRTCLiveRoomDelegate delegate);
```

>?`setDelegate` is the delegate callback of `TRTCLiveRoom`.   

### setDelegateHandler

This API is used to set the thread where event callbacks are.
```java
public abstract void setDelegateHandler(Handler handler);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| handler | Handler | Callbacks for the events of `TRTCLiveRoom` are returned via this handler. Do not use it together with `setDelegate`. |

   

### login

This API is used to log in.

<dx-codeblock>
::: java java
public abstract void login(int sdkAppId,
 String userId, String userSig,
 TRTCLiveRoomDef.TRTCLiveRoomConfig config, 
 TRTCLiveRoomCallback.ActionCallback callback);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppId | int | You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_) |
| userSig | String | Tencent Cloud's proprietary security signature. For how to obtain it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| config | TRTCLiveRoomConfig | Global configuration information, which needs to be initialized during login and cannot be modified afterward. <ul style="margin:0;"><li>`useCDNFirst`: specifies the way audience watch live streams. `true` means watching over CDNs, which is cost-efficient but has high latency. `false` means watching under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second. </li><li>`CDNPlayDomain`: specifies the domain name for CDN live streaming. It takes effect only if `useCDNFirst` is set to `true`. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** of the CSS console.</li></ul> |
| callback | ActionCallback | Callback for login. The code is `0` if login succeeds. |

   

### logout

This API is used to log out.
```java
public abstract void logout(TRTCLiveRoomCallback.ActionCallback callback);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for logout. The code is `0` if logout succeeds. |

   

### setSelfProfile

This API is used to set the profile.
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userName | String | Username |
| avatar | String | Profile photo URL |
| callback | ActionCallback | Callback for profile setting. The code is `0` if the operation succeeds. |

   


## Room APIs
### createRoom

This API is used to create a room (called by anchor).
```java
public abstract void createRoom(int roomId, TRTCLiveRoomDef.TRTCCreateRoomParam roomParam, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomId` values can be aggregated into a live room list. Currently, Tencent Cloud does not provide list management services. Please manage the list on your own. |
| roomParam | TRTCCreateRoomParam | Room information, such as room name and cover information. If both the room list and room information are managed on your server, you can ignore this parameter. |
| callback | ActionCallback | Callback for room creation. The code is `0` if the operation succeeds. |

The process of creating a room and starting live streaming as an anchor is as follows: 
1. A user calls `startCameraPreview()` to enable camera preview and set beauty filters. 
2. The user calls `createRoom()` to create a room, the result of which is returned via the `ActionCallback` callback.
3. The user calls `startPublish()` to push streams.

   

### destroyRoom

This API is used to terminate a room (called by anchor).
```java
public abstract void destroyRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for room termination. The code is `0` if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by audience).
```java
public abstract void enterRoom(int roomId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Room ID |
| callback | ActionCallback | Callback for room entry. The code is `0` if the operation succeeds. |


The process of entering a room and starting playback as audience is as follows: 
1. A user gets the latest room list from your server. The list may contain the `roomId` and other information of multiple rooms.
2. The user selects a room and calls `enterRoom()` to enter the room.
3. The user calls `startPlay(userId)`, passing in the anchor’s `userId` to start playback.
 - If the room list contains the anchor’s `userId`, the user can call `startPlay(userId)` to start playback.
 - If the user does not have the anchor's `userId` before room entry, he or she can find it in the `onAnchorEnter(userId)` callback of `TRTCLiveRoomDelegate`, which is returned after room entry, and can then call `startPlay(userId)` to start playback. 

   

### exitRoom

This API is used to leave a room.
```java
public abstract void exitRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for room exit. The code is `0` if the operation succeeds. |

   

### getRoomInfos

This API is used to get room list details, which are set by anchors via `roomInfo` when they call `createRoom()`.
>?You don’t need this API if both the room list and room information are managed on your server.


```java
public abstract void getRoomInfos(List<Integer> roomIdList, TRTCLiveRoomCallback.RoomInfoCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomIdList | List&lt;Integer&gt; | Room ID list |
| callback | RoomInfoCallback | Callback of room details |


### getAnchorList

This API is used to get the anchors in a room. It takes effect only if it is called after `enterRoom()`.
```java
public abstract void getAnchorList(TRTCLiveRoomCallback.UserListCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | UserListCallback | Callback of user details |

   

### getAudienceList

This API is used to get the information of all audience in a room. It takes effect only if it is called after `enterRoom()`.
```java
public abstract void getAudienceList(TRTCLiveRoomCallback.UserListCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | UserListCallback | Callback of user details |

   

## Stream Pushing/Pulling APIs
### startCameraPreview

This API is used to enable local video preview.
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isFront | boolean | `true`: front camera; `false`: rear camera |
| view | TXCloudVideoView | The control that loads video images |
| callback | ActionCallback | Callback for the operation|

   

### stopCameraPreview

This API is used to stop local video capturing and preview.
```java
public abstract void stopCameraPreview();
```

   

### startPublish

This API is used to start live streaming (pushing streams), which can be called in the following scenarios:
- An anchor starts live streaming.
- A viewer starts co-anchoring.


```java
public abstract void startPublish(String streamId, TRTCLiveRoomCallback.ActionCallback callback);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| streamId | String | The `streamId` used to bind live streaming CDNs. You need to set it to the `streamId` of the anchor if you want audience to play the anchor’s stream via live streaming CDNs.|
| callback | ActionCallback | Callback for the operation |


### stopPublish

This API is used to stop live streaming (push), which is suitable for the following scenarios:
- An anchor ends live streaming.
- A viewer ends co-anchoring.


```java
public abstract void stopPublish(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for the operation |



   

### startPlay

This API is used to play a remote video. It can be called in common playback and co-anchoring scenarios.
```java
public abstract void startPlay(String userId, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user whose video is to be played |
| view | TXCloudVideoView | The control that loads video images |
| callback | ActionCallback | Callback for the operation |

**Common playback scenario**
- If the room list contains anchors’ `userId`, after entering a room, a user can call `startPlay(userId)` to play the anchor's video.
- If a user does not have the anchor's `userId` before room entry, he or she can find it in the `onAnchorEnter(userId)` callback of `TRTCLiveRoomDelegate`, which is returned after room entry, and can then call `startPlay(userId)` to play the anchor’s video.

**Co-anchoring scenario**
After co-anchoring starts, the anchor will receive the `onAnchorEnter(userId)` callback from `TRTCLiveRoomDelegate` and can call `startPlay(userId)`, passing in the `userId` obtained from the callback to play the co-anchoring user’s video.

   

### stopPlay

This API is used to stop rendering a remote video. It needs to be called after the `onAnchorExit()` callback is received.
```java
public abstract void stopPlay(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the remote user |
| callback | ActionCallback | Callback for the operation |


## APIs for Anchor-Audience Co-anchoring
### requestJoinAnchor

This API is used to send a co-anchoring request (called by audience).
```java
public abstract void requestJoinAnchor(String reason, int timeout, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| reason | String | Reason for co-anchoring |
| timeout | int | Timeout period |
| callback | ActionCallback | Callback of the anchor’s response |


The process of co-anchoring between anchors and audience is as follows:
1. A **viewer** calls `requestJoinAnchor()` to send a co-anchoring request to the anchor.
2. The **anchor** receives the `onRequestJoinAnchor()` callback of `TRTCLiveRoomDelegate`.
3. The **anchor** calls `responseJoinAnchor()` to accept or reject the co-anchoring request.
4. The **viewer** receives the `responseCallback` callback, which carries the anchor’s response.
5. If the request is accepted, the **viewer** calls `startCameraPreview()` to enable local camera preview.
6. The **viewer** calls `startPublish()` to push streams.
7. After the viewer starts pushing streams, the **anchor** receives the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate`.
8. The **anchor** calls `startPlay()` to play the co-anchoring viewer’s video.
9. If there are other viewers co-anchoring with the anchor in the room, the new co-anchoring **viewer** will receive the `onAnchorEnter()` callback and can call `startPlay()` to play other co-anchoring viewers’ video.

   

### responseJoinAnchor

This API is used to respond to a co-anchoring request (called by anchor) after receiving the `onRequestJoinAnchor()` callback of `TRTCLiveRoomDelegate`.
```java
public abstract void responseJoinAnchor(String userId, boolean agree, String reason);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID of the viewer |
| agree | boolean | `true`: accept; `false`: reject |
| reason | String | Reason for accepting/rejecting the request |


### kickoutJoinAnchor

This API is used to remove a user from co-anchoring (called by anchor). The removed user will receive the `onKickoutJoinAnchor()` callback of `TRTCLiveRoomDelegate`.

```java
public abstract void kickoutJoinAnchor(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the co-anchoring user |
| callback | ActionCallback | Callback for the operation |



## APIs for Cross-Room Anchor Competition
### requestRoomPK

This API is used to request cross-room competition (called by anchor).
```java
public abstract void requestRoomPK(int roomId, String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Room ID of the anchor to call |
| userId | String | User ID of the anchor to call |
| callback | ActionCallback | Callback for requesting cross-room competition |

Anchors in different rooms can compete with each other. The process of starting cross-room competition between anchor A and anchor B is as follows:
1. **Anchor A** calls `requestRoomPK()` to send a competition request to anchor B.
2. **Anchor B** receives the `onRequestRoomPK()` callback of `TRTCLiveRoomDelegate`.
3. **Anchor B** calls `responseRoomPK()` to respond to the competition request.
4. If **anchor B** accepts the request, he or she would wait for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and call `startPlay()` to play anchor A's video.
5. **Anchor A** receives the `responseCallback` callback, which carries anchor B’s response.
6. If the request is accepted, **anchor A** waits for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and calls `startPlay()` to play anchor B’s video.

   

### responseRoomPK

This API is used to respond to a cross-room competition request (called by anchor), after which the request sending anchor will receive the `responseCallback` passed in to `requestRoomPK`.
```java
public abstract void responseRoomPK(String userId, boolean agree, String reason);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID of the request sending anchor |
| agree | boolean | `true`: accept; `false`: reject |
| reason | String | Reason for accepting/rejecting the request |


### quitRoomPK

This API is used to quit cross-room competition. If either anchor quits cross-room competition, the other anchor will receive the `onQuitRoomPk()` callback of `TRTCLiveRoomDelegate`.
```java
public abstract void quitRoomPK(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for the operation |


## Audio/Video APIs
### switchCamera

This API is used to switch between the front and rear cameras.
```java
public abstract void switchCamera();
```

   

### setMirror

This API is used to set the mirror mode.
```java
public abstract void setMirror(boolean isMirror);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMirror | boolean | Enable/Disable mirroring |

   

### muteLocalAudio

This API is used to mute or unmute the local user.
```java
public abstract void muteLocalAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | `true`: mute; `false`: unmute |

   

### muteRemoteAudio

This API is used to mute or unmute a remote user.
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the remote user |
| mute | boolean | `true`: mute; `false`: unmute |

   

### muteAllRemoteAudio

This API is used to mute or unmute all remote users.
```java
public abstract void muteAllRemoteAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | `true`: mute; `false`: unmute |

   

## Background Music and Audio Effect APIs
### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).
```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## Beauty Filter APIs
### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).
```java
public abstract TXBeautyManager getBeautyManager();
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
public abstract void sendRoomTextMsg(String message, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message |
| callback | ActionCallback | Callback for message sending |

   

### sendRoomCustomMsg

This API is used to send a custom text message.
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| callback | ActionCallback | Callback for message sending |

   

## Debugging APIs
### showVideoDebugLog

This API is used to specify whether to display debugging information on the UI.
```java
public abstract void showVideoDebugLog(boolean isShow);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isShow | boolean | Show/Hide debugging information |

   

## `TRTCLiveRoomDelegate` Event Callback APIs

## Common Event Callback APIs
### onError

Callback for error.
>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```java
void onError(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | int | Error code |
| message | String | Error message |


### onWarning

Callback for warning.
```java
void onWarning(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | int | Error code |
| message | String | Warning message |

   

### onDebugLog

Callback for log.
```java
void onDebugLog(String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Log information |

   


## Room Event Callback APIs
### onRoomDestroy

Callback for room termination. All users in a room will receive this callback after the anchor leaves the room.
```java
void onRoomDestroy(String roomId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | String | Room ID |



   

### onRoomInfoChange

Callback for change of room information. This callback is usually used to notify users of room status change in co-anchoring and anchor competition scenarios.
```java
void onRoomInfoChange(TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomInfo | TRTCLiveRoomInfo | Room information |

   


## Callback APIs for Entry/Exit of Anchors/Audience
### onAnchorEnter

Callback for a new anchor/co-anchoring viewer. Audience will receive this callback when there is a new anchor/co-anchoring viewer in the room and can call `startPlay()` of `TRTCLiveRoom` to play the video of the anchor/co-anchoring viewer.
```java
void onAnchorEnter(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID of the new anchor/co-anchoring viewer |


### onAnchorExit

Callback for the quitting of an anchor. The anchors (including co-anchoring viewers) in a room will receive this callback after an anchor/co-anchoring viewer quits competition/co-anchoring and can call `stopPlay()` of `TRTCLiveRoom` to stop playing the video of the anchor/co-anchoring viewer.
```java
void onAnchorExit(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user who quit |


### onAudienceEnter

Callback for room entry by a viewer.
```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the viewer who entered the room |

   

### onAudienceExit

Callback for room exit by a viewer.
```java
void onAudienceExit(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the viewer who left the room |

   


## Callback APIs for Anchor-Audience Co-anchoring Events
### onRequestJoinAnchor

Callback for receiving a co-anchoring request from a viewer.
```java
void onRequestJoinAnchor(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, String reason, int timeOut);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the viewer who requested co-anchoring |
| reason | String | Reason for co-anchoring |
| timeout | int | Timeout period for response from the anchor. If the anchor does not respond to the request within the period, it will be discarded automatically. |

   

### onKickoutJoinAnchor

Callback for being removed from co-anchoring. A co-anchoring viewer needs to call `stopPublish()` of `TRTCLiveRoom` to quit co-anchoring after receiving this callback.
```java
void onKickoutJoinAnchor();
```



## Callback APIs for Anchor Competition Events
### onRequestRoomPK

Callback for receiving a cross-room competition request. If an anchor accepts the request, he or she should wait for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and call `startPlay()` to play the other anchor’s video.
```java
void onRequestRoomPK(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, int timeout);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the anchor who requested cross-room competition |
| timeout | int | Timeout period for response from the anchor |


### onQuitRoomPK

Callback for ending cross-room competition.
```java
void onQuitRoomPK();
```

   


## Message Event Callback APIs
### onRecvRoomTextMsg

Callback for receiving a text message.
```java
void onRecvRoomTextMsg(String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message |
| userInfo | TRTCLiveUserInfo | Information of the sender |

   

### onRecvRoomCustomMsg

Callback for receiving a custom message.
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| userInfo | TRTCLiveUserInfo | Information of the sender |


[](id:TRTCAudioEffectManager)
## TRTCAudioEffectManager
### playBGM

This API is used to play back background music.
```java
void playBGM(String url, int loopTimes, int bgmVol, int micVol, TRTCCloud.BGMNotify notify);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| url | String | Path of the music file |
| loopTimes | int | Loop times |
| bgmVol | int | Volume of background music |
| micVol | int | Audio capturing volume |
| notify | TRTCCloud.BGMNotify | Playback notification |

   

### stopBGM

This API is used to stop background music playback.
```java
void stopBGM();
```

   

### pauseBGM

This API is used to pause background music playback.
```java
void pauseBGM();
```

   

### resumeBGM

This API is used to resume background music playback.
```java
void resumeBGM();
```

   

### setBGMVolume

This API is used to set the playback volume of background music.
```java
void setBGMVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume. Value range: 0-100. Default value: `100` |

   

### setBGMPosition

This API is used to set the background music playback progress.
```java
int setBGMPosition(int position);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| position | int | Playback progress of background music in milliseconds (ms) |

__Return code__

`0`: successful

   

### setMicVolume

This API is used to set the mic volume. It can be used to control the volume of the mic when background music is mixed.
```java
void setMicVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | Int | Volume. Value range: 0-100. Default value: `100` |

   

### setReverbType

This API is used to set the reverb effect.
```java
void setReverbType(int reverbType);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| reverbType | int | Reverb effect. For details, please see the definitions of [TRTC_REVERB_TYPE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a60ecba31f49f70780e623d24bcfa1a7d) in `TRTCCloudDef`. |

   

### setVoiceChangerType

This API is used to set the voice changing effect.
```java
void setVoiceChangerType(int type);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| type | int | Voice changing effect. For details, please see the definitions of [TRTC_VOICE_CHANGER_TYPE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a899e72b3e4a16288e6c2edfd779e3beb) in `TRTCCloudDef`. |

   

### playAudioEffect

This API is used to play an audio effect. For each audio effect, you need to assign an ID, which is used to start and stop the playback of an audio effect as well as set its playback volume. Supported formats include AAC, MP3, and M4A.
```java
void playAudioEffect(int effectId, String path, int count, boolean publish, int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Audio effect ID |
| path | String | Audio effect path |
| count | int | Loop times |
| publish | boolean | Whether to push the audio effect. `true`: push the effect to remote users; `false`: preview the effect locally only |
| volume | int | Volume. Value range: 0-100. Default value: `100` |

   

### pauseAudioEffect

This API is used to pause playing an audio effect.
```java
void pauseAudioEffect(int effectId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Audio effect ID |

   

### resumeAudioEffect

This API is used to resume playing an audio effect.
```java
void resumeAudioEffect(int effectId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Audio effect ID |

   

### stopAudioEffect

This API is used to stop playing an audio effect.
```java
void stopAudioEffect(int effectId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Audio effect ID |

   

### stopAllAudioEffects

This API is used to stop playing all audio effects.
```java
void stopAllAudioEffects();
```

   

### setAudioEffectVolume

This API is used to set the volume of an audio effect.
```java
void setAudioEffectVolume(int effectId, int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Audio effect ID |
| volume | int | Volume. Value range: 0-100. Default value: `100` |

   

### setAllAudioEffectsVolume

This API is used to set the volume of all audio effects.
```java
void setAllAudioEffectsVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume. Value range: 0-100. Default value: `100` |

   
