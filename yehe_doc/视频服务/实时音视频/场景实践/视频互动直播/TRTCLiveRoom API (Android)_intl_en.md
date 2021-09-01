`TRTCLiveRoom` has the following features based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM):
- The anchor can create a live room to start live streaming, and the viewers can enter the room to watch the stream.
- The anchor and viewers can interact through video co-anchoring.
- Anchors in two rooms can compete and interact with each other through co-anchoring.
- Users can send various text and custom messages. Custom messages can be used to send on-screen comments, give likes, and give gifts.

`TRTCLiveRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Co-anchoring Live Streaming (Android)](https://intl.cloud.tencent.com/document/product/647/36061).
- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency live streaming component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms during live streaming. In addition, the co-anchoring processes between different anchors are connected through IM messages.


<h2 id="TRTCLiveRoom">TRTCLiveRoom API Overview</h2>

### Basic SDK APIs

| API | Description |
|-----|-----|
| [sharedInstance](#sharedinstance) | Gets singleton object. |
| [destroySharedInstance](#destroysharedinstance) | Terminates singleton object. |
| [setDelegate](#setdelegate) | Sets event callback. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where the event callback is. |
| [login](#login) | Logs in. |
| [logout](#logout) | Logs out. |
| [setSelfProfile](#setselfprofile) | Modifies personal information. |

### Room APIs

| API | Description |
|-----|-----|
| [createRoom](#createroom) | Creates room (called by anchor). If the room does not exist, the system will automatically create a new room. |
| [destroyRoom](#destroyroom) | Terminates room (called by anchor). |
| [enterRoom](#enterroom) | Enters room (called by viewer). |
| [exitRoom](#exitroom) | Exits room (called by viewer). |
| [getRoomInfos](#getroominfos) | Gets room list details. |
| [getAnchorList](#getanchorlist) | Gets the list of all anchors in room. This API will take effect only if it is called after `enterRoom()` succeeds. |
| [getAudienceList](#getaudiencelist) | Gets the information of all viewers in room. This API will take effect only if it is called after `enterRoom()` succeeds. |

### Push/Pull APIs

| API | Description |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | Enables the preview image of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [startPublish](#startpublish) | Starts live streaming (push). |
| [stopPublish](#stoppublish) | Stops live streaming (push). |
| [startPlay](#startplay) | Plays back remote video image. This API can be called in common watch and co-anchoring scenarios. |
| [stopPlay](#stopplay) | Stops rendering remote video image. |

### Co-anchoring between anchor and viewer

| API | Description |
|-----|-----|
| [requestJoinAnchor](#requestjoinanchor) | Requests co-anchoring (by viewer). |
| [responseJoinAnchor](#responsejoinanchor) | Processes co-anchoring request (by anchor). |
| [kickoutJoinAnchor](#kickoutjoinanchor) | Kicks out co-anchoring viewer (by anchor). |

### Cross-Room anchor competition

| API | Description |
|-----|-----|
| [requestRoomPK](#requestroompk) | Requests cross-room competition (by anchor). |
| [responseRoomPK](#responseroompk) | Responds to cross-room competition request (by anchor). |
| [quitRoomPK](#quitroompk) | Exits cross-room competition. |

### Audio/Video control APIs

| API | Description |
|-----|-----|
| [switchCamera](#switchcamera) | Switches between front and rear cameras. |
| [setMirror](#setmirror) | Sets whether to enable mirroring display. |
| [muteLocalAudio](#mutelocalaudio) | Mutes local audio. |
| [muteRemoteAudio](#muteremoteaudio) | Mutes remote audio. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes all remote audios. |

### Background music and sound effect APIs

| API | Description |
|-----|-----|
| [getAudioEffectManager](#getaudioeffectmanager) | Gets background music and sound effect management object [TXAudioEffectManager](#trtcaudioeffectmanagerapi). |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets beauty filter management object [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager). |

### Message sending APIs

| API | Description |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts text message in room. This API is generally used for on-screen comment chat. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends custom text message. |

### Debugging APIs

| API | Description |
|-----|-----|
| [showVideoDebugLog](#showvideodebuglog) | Specifies whether to display debugging information on the UI. |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API Overview</h2>

### General event callbacks

| API | Description |
|-----|-----|
| [onError](#onerror) | Callback for error. |
| [onWarning](#onwarning) | Callback for warning. |
| [onDebugLog](#ondebuglog) | Callback for log. |

### Room event callbacks

| API | Description |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | Callback for room termination. |
| [onRoomInfoChange](#onroominfochange) | Callback for live room information change. |

### Anchor/Viewer room entry/exit event callbacks

| API | Description |
|-----|-----|
| [onAnchorEnter](#onanchorenter) | Notification of new anchor's room entry. |
| [onAnchorExit](#onanchorexit) | Notification of anchor's room exit. |
| [onAudienceEnter](#onaudienceenter) | Notification of viewer's room entry. |
| [onAudienceExit](#onaudienceexit) | Notification of viewer's room exit. |

### Anchor/Viewer co-anchoring event callbacks

| API | Description |
|-----|-----|
| [onRequestJoinAnchor](#onrequestjoinanchor) | Callback when the anchor receives a viewer's co-anchoring request. |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | Notification of being kicked out of co-anchoring received by co-anchoring viewer. |

### Anchor competition event callbacks

| API | Description |
|-----|-----|
| [onRequestRoomPK](#onrequestroompk) | Notification of cross-room competition request. |
| [onQuitRoomPK](#onquitroompk) | Notification of cross-room competition stop. |

### Message event callbacks

| API | Description |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | Receipt of text message. |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of custom message. |

## Basic SDK APIs

<span id="sharedInstance"></span>
### sharedInstance

This API is used to get the [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061) singleton object.
```java
 public static synchronized TRTCLiveRoom sharedInstance(Context context);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| context | Context | Android context, which will be converted to `ApplicationContext` for the system APIs to call. |

   

### destroySharedInstance

This API is used to terminate the [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061) singleton object.
>?After the instance is terminated, the externally cached `TRTCLiveRoom` instance cannot be used, and you need to call [sharedInstance](#sharedInstance) again to get a new instance.

```java
public static void destroySharedInstance();
```   

### setDelegate

This API is used to get the event callback of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061). You can use `TRTCLiveRoomDelegate` to get various status notifications of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061).
```java
public abstract void setDelegate(TRTCLiveRoomDelegate delegate);
```

>?`setDelegate` is the delegation callback of `TRTCLiveRoom`.   

### setDelegateHandler

This API is used to set the thread where the event callback is.
```java
public abstract void setDelegateHandler(Handler handler);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| handler | Handler | Notifies various status notification callbacks in `TRTCLiveRoom` through this handler. Please do not use this parameter together with `setDelegate`. |

   

### login

This API is used to log in.
```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
 TRTCLiveRoomDef.TRTCLiveRoomConfig config, 
 TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppId | int | You can view the `SDKAppID` in the TRTC Console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| userId | String | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| config | TRTCLiveRoomConfig | Global configuration information, which needs to be initialized during the login and cannot be modified after the login. <ul style="margin:0;"><li>`useCDNFirst` attribute: used to set the way how viewers will watch live streaming. `true` means that general viewers will watch live streaming over CDN, which is cheap but has a high latency. `false` means that general viewers will watch live streaming through the low latency scheme, the cost of which ranges between that of CDN and co-anchoring, but the delay can be controlled within 1 second. </li><li>`CDNPlayDomain` attribute: it will take effect only if `useCDNFirst` is set to `true`. It is used to specify the playback domain name for watching over CDN. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** in the LVB Console.</li></ul> |
| callback | ActionCallback | Callback for login. The `code` will be 0 if the operation succeeds. |

   

### logout

This API is used to log out.
```java
public abstract void logout(TRTCLiveRoomCallback.ActionCallback callback);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for logout. The `code` will be 0 if the operation succeeds. |

   

### setSelfProfile

This API is used to modify the personal information.
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| name | String | Nickname. |
| avatarURL | String | Profile photo address. |
| callback | ActionCallback | Callback for personal information setting. The `code` will be 0 if the operation succeeds. |

   


## Room APIs
### createRoom

This API is used to create a room (called by the anchor).
```java
public abstract void createRoom(int roomId, TRTCLiveRoomDef.TRTCCreateRoomParam roomParam, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated as a live room list. Currently, Tencent Cloud does not provide the live room list management service. Please manage your live room list on your own. |
| roomParam | TRTCCreateRoomParam | Room description information, such as room name and cover information. If both the room list and room information are managed on your server, you can ignore this parameter. |
| callback | ActionCallback | Callback for room creation result. The `code` will be 0 if the operation succeeds.  |

Generally, the anchor starts live streaming in the following call process: 
1. The **anchor** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted. 
2. The **anchor** calls `createRoom()` to create a live room. No matter whether the room is successfully created, the result will be notified to the anchor through `ActionCallback`.
3. The **anchor** calls `starPublish()` to start push.

   

### destroyRoom

This API is used to terminate a room (called by the anchor). After creating a room, the anchor can call this API to terminate it.
```java
public abstract void destroyRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for room termination result. The `code` will be 0 if the operation succeeds. |
   

### enterRoom

This API is used to enter a room (called by the viewer).
```java
public abstract void enterRoom(int roomId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Room ID. |
| callback | ActionCallback | Callback for room entry result. The `code` will be 0 if the operation succeeds.  |


Generally, the viewer can watch a live stream in the following call process: 
1. The **viewer** gets the latest live room list from your server. The list may contain `roomID` and room information of multiple live rooms.
2. The **viewer** selects a live room and calls `enterRoom()` to enter it.
3. The **viewer** calls `startPlay(userId)` and passes in the `userId` of the anchor to start playback.
 - If the live room list contains the `userId` of the anchor, the viewer can directly call `startPlay(userId)` to start playback.
 - If the viewer does not have the anchor's `userId` before entering the room, after entering the room, the viewer will receive the `onAnchorEnter(userId)` event callback in `TRTCLiveRoomDelegate`, which carries the anchor's `userId` information. Then, the viewer can call `startPlay(userId)` to start playback. 

   

### exitRoom

This API is used to exit a room.
```java
public abstract void exitRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for room exit result. The `code` will be 0 if the operation succeeds. |

   

### getRoomInfos

This API is used to get the room list details set through `roomInfo` by the anchor during `createRoom()`.
>?If both the room list and room information are managed on your server, you can ignore this parameter.


```java
public abstract void getRoomInfos(List<Integer> roomIdList, TRTCLiveRoomCallback.RoomInfoCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomIdList | List&lt;Integer&gt; | Room ID list. |
| callback | RoomInfoCallback | Callback for room details. |
   

### getAnchorList

This API is used to get the list of all anchors in the room. It will take effect only if it is called after `enterRoom()` succeeds.
```java
public abstract void getAnchorList(TRTCLiveRoomCallback.UserListCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | UserListCallback | Callback for user details. |

   

### getAudienceList

This API is used to get the information of all viewers in the room. This API will take effect only if it is called after `enterRoom()` succeeds.
```java
public abstract void getAudienceList(TRTCLiveRoomCallback.UserListCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | UserListCallback | Callback for user details. |

   

## Push/Pull APIs
### startCameraPreview

This API is used to enable the preview image of local video.
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isFront | boolean | true: front camera; false: rear camera. |
| view | TXCloudVideoView | Control that carries the video image. |
| callback | ActionCallback | Callback for operation. |

   

### stopCameraPreview

This API is used to stop local video capturing and preview.
```java
public abstract void stopCameraPreview();
```

   

### startPublish

This API is used to start live streaming (push), which is suitable for the following scenarios:
- The anchor starts live streaming.
- The viewer starts co-anchoring.


```java
public abstract void startPublish(String streamId, TRTCLiveRoomCallback.ActionCallback callback);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| streamId | String | Binds the `streamId` of LVB CDN. If you want viewers to watch through LVB CDN, you need to specify the LVB `streamId` of the current anchor. |
| callback | ActionCallback | Callback for operation. |
   

### stopPublish

This API is used to stop live streaming (push), which is suitable for the following scenarios:
- The anchor ends live streaming.
- The viewer ends co-anchoring.


```java
public abstract void stopPublish(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for operation. |



   

### startPlay

This API is used to play back the remote video image. It can be called in general watch and co-anchoring scenarios.
```java
public abstract void startPlay(String userId, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user whose video image is to be played back. |
| view | TXCloudVideoView | `view` control that carries the video image. |
| callback | ActionCallback | Callback for operation. |

**General watch scenario**
- If the live room list contains the `userId` of the anchor, the viewer can directly call `startPlay(userId)` to start playing back the anchor's video image after `enterRoom()` succeeds.
- If the viewer does not have the anchor's `userId` before entering the room, after entering the room, the viewer will receive the `onAnchorEnter(userId)` event callback in `TRTCLiveRoomDelegate`, which carries the anchor's `userId` information. Then, the viewer can call `startPlay(userId)` to start playing back the anchor's video image.

**Live streaming co-anchoring scenario**
After co-anchoring is initiated, the anchor will receive the `onAnchorEnter(userId)` callback from `TRTCLiveRoomDelegate`. Then, the anchor can play back the co-anchoring video image by calling `startPlay(userId)` with the `userId` in the callback.

   

### stopPlay

This API is used to stop rendering the remote video image. It needs to be called when the `onAnchorExit()` callback is received.
```java
public abstract void stopPlay(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Remote user information. |
| callback | ActionCallback | Callback for operation. |
   

## Co-anchoring Between Anchor and Viewer
### requestJoinAnchor

This API is used by the viewer to request co-anchoring.
```java
public abstract void requestJoinAnchor(String reason, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| reason | String | Reason for co-anchoring. |
| responseCallback | ActionCallback | Callback for anchor response. |


The anchor and viewer start co-anchoring in the following steps:
1. The **viewer** calls `requestJoinAnchor()` to send a co-anchoring request to the anchor.
2. The **anchor** receives the `onRequestJoinAnchor()` callback notification of `TRTCLiveRoomDelegate`.
3. The **anchor** calls `responseJoinAnchor()` to determine whether to accept the co-anchoring request from the viewer.
4. The **viewer** receives the `responseCallback` callback notification, which carries the processing result of the anchor.
5. If the request of the **viewer** is accepted, `startCameraPreview()` will be called to enable the local camera.
6. The **viewer** calls `startPublish()` to formally enter the push status.
7. The **anchor** will receive the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` once the viewer enters the co-anchoring status.
8. The **anchor** can view the video image of the co-anchoring viewer simply by calling `startPlay()`.
9. If there are other viewers co-anchoring with the anchor in the live room, the new co-anchoring **viewer** will receive the `onAnchorEnter()` notification and can call `startPlay()` to play back the video images of other co-anchoring users.

   

### responseJoinAnchor

This API is used by the anchor to process the co-anchoring request. After receiving the `onRequestJoinAnchor()` callback of `TRTCLiveRoomDelegate`, the anchor needs to call this API to process the co-anchoring request of the viewer.
```java
public abstract void responseJoinAnchor(String userId, boolean agree, String reason);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Viewer ID. |
| agree | boolean | true: accepts; false: rejects. |
| reason | String | Reason for accepting/rejecting co-anchoring. |
   

### kickoutJoinAnchor

This API is used by the anchor to kick out the co-anchoring viewer. After this API is called, the kicked out viewer will receive the `onKickoutJoinAnchor()` callback notification of `TRTCLiveRoomDelegate`.

```java
public abstract void kickoutJoinAnchor(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Co-anchoring viewer ID. |
| callback | ActionCallback | Callback for operation. |
  


## Cross-Room Anchor Competition
### requestRoomPK

This API is used by the anchor to request cross-room competition.
```java
public abstract void requestRoomPK(int roomId, String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Room ID of the invited anchor. |
| userId | String | ID of the invited anchor. |
| responseCallback | ActionCallback | Callback for cross-room competition request result. |

Anchors in different rooms can compete with each other. Anchor A and anchor B can start cross-room competition during live streaming in the following steps:
1. **Anchor A** calls `requestRoomPK()` to send a co-anchoring request to anchor B.
2. **Anchor B** receives the `onRequestRoomPK()` callback notification of `TRTCLiveRoomDelegate`.
3. **Anchor B** calls `responseRoomPK()` to decide whether to accept the competition request from anchor A.
4. If **anchor B** accepts the request of anchor A, anchor B will wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to display anchor A's video image.
5. **Anchor A** receives the `responseCallback` callback notification, which carries the processing result from anchor B.
6. If the request of **anchor A** is accepted, anchor A will wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to display anchor B's video image.

   

### responseRoomPK

This API is used by the anchor to respond to the cross-room competition request. After the anchor responds, the other anchor will receive the `responseCallback` callback passed in by `requestRoomPK`.
```java
public abstract void responseRoomPK(String userId, boolean agree, String reason);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the anchor who initiates the competition request. |
| agree | boolean | true: accepts; false: rejects. |
| reason | String |  Reason for accepting/rejecting competition. |
   

### quitRoomPK

This API is used to exit cross-room competition. If either anchor exits cross-room competition, the other anchor will receive the `onQuitRoomPk()` callback notification of `TRTCLiveRoomDelegate`.
```java
public abstract void quitRoomPK(TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for operation. |
   

## Audio/Video Control APIs
### switchCamera

This API is used to switch between front and rear cameras.
```java
public abstract void switchCamera();
```

   

### setMirror

This API is used to set whether to enable mirroring display.
```java
public abstract void setMirror(boolean isMirror);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMirror | boolean | Enables/Disables mirroring. |

   

### muteLocalAudio

This API is used to mute the local audio.
```java
public abstract void muteLocalAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | true: mutes; false: unmutes. |

   

### muteRemoteAudio

This API is used to mute the remote audio.
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | Remote user ID. |
| mute | boolean | true: mutes; false: unmutes. |

   

### muteAllRemoteAudio

This API is used to mute all remote audios.
```java
public abstract void muteAllRemoteAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | true: mutes; false: unmutes. |

   

## Background Music and Sound Effect APIs
### getAudioEffectManager

This API is used to get the background music and sound effect management object [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).
```java
public abstract TXAudioEffectManager getAudioEffectManager();
```
   

## Beauty Filter APIs
### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).
```java
public abstract TXBeautyManager getBeautyManager();
```

You can use the following features with beauty filter management:
- Set beauty effects such as "beauty filter style", "brightening", "rosy skin", "eye enlarging", "face slimming", "chin slimming", "chin lengthening or shortening", "face shortening", "nose narrowing", "eye brightening", "teeth whitening", "eye bag removal", "wrinkle removal", and "smile line removal".
- Adjust the "hairline", "eye distance", "eye corners", "mouth shape", "nose wing", "nose position", "lip thickness", and "face shape".
- Set animated effects such as facial pendants (materials).
- Add makeup effects.
- Recognize gestures.


## Message Sending APIs
### sendRoomTextMsg

This API is used to broadcast a text message in the room, which is generally used for on-screen comment chat.
```java
public abstract void sendRoomTextMsg(String message, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message. |
| callback | ActionCallback | Callback for sending result. |

   

### sendRoomCustomMsg

This API is used to send a custom text message.
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCLiveRoomCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| cmd | String | Custom command word used to distinguish between different message types. |
| message | String | Text message. |
| callback | ActionCallback | Callback for sending result. |

   

## Debugging APIs
### showVideoDebugLog

This API is used to specify whether to display debugging information on the UI.
```java
public abstract void showVideoDebugLog(boolean isShow);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isShow | boolean | Enables/Disables the display of debugging information. |

   

## TRTCLiveRoomDelegate Event Callbacks

## General Event Callbacks
### onError

Callback for error.
>?The SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions.

```java
void onError(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | int | Error code. |
| message | String | Error message. |
   

### onWarning

Callback for warning.
```java
void onWarning(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | int | Error code. |
| message | String | Warning message. |

   

### onDebugLog

Callback for log.
```java
void onDebugLog(String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Log message. |

   


## Room Event Callbacks
### onRoomDestroy

Callback for room termination. When the anchor exits the room, all users in the room will receive this callback.
```java
void onRoomDestroy(String roomId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | String | Room ID. |



   

### onRoomInfoChange

Callback for live room information change. It is usually used for notifications of room status changes during live streaming co-anchoring and cross-room competition.
```java
void onRoomInfoChange(TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomInfo | TRTCLiveRoomInfo | Room information. |

   


## Anchor/Viewer Room Entry/Exit Event Callbacks
### onAnchorEnter

Notification of new anchor's room entry. After co-anchoring viewers and the anchor invited to cross-room competition enter the room, the viewers will receive the event of the new anchor's room entry. `startPlay()` of `TRTCLiveRoom` can be called to display the anchor's video image.
```java
void onAnchorEnter(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the new anchor who enters the room. |
   

### onAnchorExit

Notification of anchor's room exit. The anchor in the room and co-anchoring viewers will receive the room exit event of the new anchor. `stopPlay()` of `TRTCLiveRoom` can be called to disable the anchor's video image.
```java
void onAnchorExit(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user who exits the room. |
   

### onAudienceEnter

Notification of viewer's room entry.
```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the viewer who enters the room. |

   

### onAudienceExit

Notification of viewer's room exit.
```java
void onAudienceExit(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the viewer who exits the room. |

   


## Anchor/Viewer Co-anchoring Event Callbacks
### onRequestJoinAnchor

Callback when the anchor receives the viewer's co-anchoring request.
```java
void onRequestJoinAnchor(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, String reason, int timeOut);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the viewer who requests co-anchoring. |
| reason | String | Reason for co-anchoring. |
| timeout | int | Timeout period for processing request. If a request is not processed by the upper layer after the timeout period elapses, it will be discarded automatically. |

   

### onKickoutJoinAnchor

Notification of being kicked out of co-anchoring received by co-anchoring viewer. If the co-anchoring viewer receives a message of being kicked out of co-anchoring by the anchor, the viewer needs to call `stopPublish()` of `TRTCLiveRoom` to exit co-anchoring.
```java
void onKickoutJoinAnchor();
```
  


## Anchor Competition Event Callbacks
### onRequestRoomPK

Notification of cross-room competition request. If the anchor receives a competition request from the anchor of another room and accepts the competition, the anchor needs to wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to play back the stream of the inviting anchor.
```java
void onRequestRoomPK(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, int timeout);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | Information of the anchor who initiates cross-room co-anchoring. |
| timeout | int | Timeout period for processing request. |
   

### onQuitRoomPK

Callback for cross-room competition stop.
```java
void onQuitRoomPK();
```

   


## Message Event Callbacks
### onRecvRoomTextMsg

Receipt of text message.
```java
void onRecvRoomTextMsg(String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message. |
| user | TRTCLiveUserInfo | User information of sender. |

   

### onRecvRoomCustomMsg

Receipt of custom message.
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| command | String | Custom command word used to distinguish between different message types. |
| message | String | Text message. |
| user | TRTCLiveUserInfo | User information of sender. |

   
<span id="TRTCAudioEffectManager"></span>
## TRTCAudioEffectManager
### playBGM

This API is used to play back background music.
```java
void playBGM(String url, int loopTimes, int bgmVol, int micVol, TRTCCloud.BGMNotify notify);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| url | String | Path of background music file. |
| loopTimes | int | Loop times. |
| bgmVol | int | Volume level of background music. |
| micVol | int | Capturing volume level. |
| notify | TRTCCloud.BGMNotify | Playback notification. |

   

### stopBGM

This API is used to stop background music.
```java
void stopBGM();
```

   

### pauseBGM

This API is used to pause background music.
```java
void pauseBGM();
```

   

### resumeBGM

This API is used to resume background music.
```java
void resumeBGM();
```

   

### setBGMVolume

This API is used to set background music volume level. It is used to control the background music volume level during playback.
```java
void setBGMVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. `100` indicates normal volume level. Value range: 0–100. Default value: 100. |

   

### setBGMPosition

This API is used to set the background music playback progress.
```java
int setBGMPosition(int position);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| position | int | Background music playback progress in milliseconds (ms). |

__Response__

0: success.

   

### setMicVolume

This API is used to set mic volume level. It is used to adjust the mic volume level when background music is played back.
```java
void setMicVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | Int | Volume level. Value range: 0–100. Default value: 100. |

   

### setReverbType

This API is used to set reverb effect.
```java
void setReverbType(int reverbType);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| reverbType | int | Reverb type. For more information, please see the definition of [TRTC_REVERB_TYPE](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a60ecba31f49f70780e623d24bcfa1a7d) in `TRTCCloudDef`. |

   

### setVoiceChangerType

This API is used to set voice changer type.
```java
void setVoiceChangerType(int type);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| type | int | Voice changer type. For more information, please see the definition of [TRTC_VOICE_CHANGER_TYPE](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a899e72b3e4a16288e6c2edfd779e3beb) in `TRTCCloudDef`. |

   

### playAudioEffect

This API is used to play back a sound effect. You need to assign an ID to each sound effect, through which you can start, stop, or set the volume level of the sound effect. AAC, MP3, and M4A formats are supported.
```java
void playAudioEffect(int effectId, String path, int count, boolean publish, int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |
| path | String | Path of sound effect. |
| count | int | Loop times. |
| publish | boolean | Whether to push. true: push to viewers; false: local preview. |
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

   

### pauseAudioEffect

This API is used to pause a sound effect.
```java
void pauseAudioEffect(int effectId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |

   

### resumeAudioEffect

This API is used to resume a sound effect.
```java
void resumeAudioEffect(int effectId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |

   

### stopAudioEffect

This API is used to stop a sound effect.
```java
void stopAudioEffect(int effectId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |

   

### stopAllAudioEffects

This API is used to stop all sound effects.
```java
void stopAllAudioEffects();
```

   

### setAudioEffectVolume

This API is used to set sound effect volume level.
```java
void setAudioEffectVolume(int effectId, int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

   

### setAllAudioEffectsVolume

This API is used to set the volume level of all sound effects.
```java
void setAllAudioEffectsVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

   
