`TRTCLiveRoom` has the following features based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM):
- The anchor can create a live room to start live streaming, and the viewers can enter the room to watch the stream.
- The anchor and viewers can interact through video co-anchoring.
- Anchors in two rooms can compete and interact with each other through co-anchoring.
- Users can send various text and custom messages. Custom messages can be used to send on-screen comments, give likes, and give gifts.

`TRTCLiveRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Co-anchoring Live Streaming (iOS)](https://intl.cloud.tencent.com/document/product/647/36060).
- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency live streaming component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms during live streaming. In addition, the co-anchoring processes between different anchors are connected through IM messages.



<h2 id="TRTCLiveRoom">TRTCLiveRoom API Overview</h2>

### Basic SDK APIs

| API | Description |
|-----|-----|
| [delegate](#delegate) | Sets event callback. |
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
| [getBeautyManager](#getbeautymanager) | Gets beauty filter management object [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager). |

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

<h2 id="trtcaudioeffectmanagerapi">TRTCAudioEffectManager API Overview</h2>

| API | Description |
|-----|-----|
| [playBgm](#playbgm) | Plays back background music. |
| [stopBgm](#stopbgm) | Stops background music. |
| [pauseBgm](#pausebgm) | Pauses background music. |
| [resumeBgm](#resumebgm) | Resumes background music. |
| [setBGMVolume](#setbgmvolume) | Sets background music volume level. It is used to control the background music volume level during playback. |
| [setBGMPosition](#setbgmposition) | Sets the background music playback progress. |
| [setMicVolume](#setmicvolume) | Sets mic volume level. It is used to adjust the mic volume level when background music is played back. |
| [setReverbType](#setreverbtype) | Sets reverb effect. |
| [setVoiceChangerType](#setvoicechangertype) | Sets voice changer type. |
| [playAudioEffect](#playaudioeffect) | Plays back sound effect. You need to assign an ID to each sound effect, through which you can start, stop, or set the volume level of the sound effect. AAC, MP3, and M4A formats are supported. |
| [pauseAudioEffect](#pauseaudioeffect) | Pauses sound effect. |
| [resumeAudioEffect](#resumeaudioeffect) | Resumes sound effect. |
| [stopAudioEffect](#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](#pauseaudioeffect) | Stops all sound effects. |
| [setAudioEffectVolume](#setaudioeffectvolume) | Sets sound effect volume level. |
| [setAllAudioEffectsVolume](#setallaudioeffectsvolume) | Sets the volume level of all sound effects. |

## Basic SDK APIs
### delegate

This API is used to get the event callback of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060). You can use `TRTCLiveRoomDelegate` to get various status notifications of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060).
```swift
@objc public weak var delegate: TRTCLiveRoomDelegate?
```

>?`delegate` is the delegation callback of `TRTCLiveRoom`.


### login

This API is used to log in.
```swift
@objc func login(sdkAppID: Int, userID: String, userSig: String, config: TRTCLiveRoomConfig, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppID | Int | You can view the `SDKAppID` in the TRTC Console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| userID | String | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| config | TRTCLiveRoomConfig | Global configuration information, which needs to be initialized during the login and cannot be modified after the login. <ul style="margin:0;"><li>`useCDNFirst` attribute: used to set the way how viewers will watch live streaming. `true` means that general viewers will watch live streaming over CDN, which is cheap but has a high latency. `false` means that general viewers will watch live streaming through the low latency scheme, the cost of which ranges between that of CDN and co-anchoring, but the delay can be controlled within 1 second. </li><li>`CDNPlayDomain` attribute: it will take effect only if `useCDNFirst` is set to `true`. It is used to specify the playback domain name for watching over CDN. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** in the LVB Console.</li></ul> |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for login. The `code` will be 0 if the operation succeeds.                                  |


### logout

This API is used to log out.
```swift
@objc func logout(_ callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String?) -> Void | Callback for logout. The `code` will be 0 if the operation succeeds. |


### setSelfProfile

This API is used to modify the personal information.
```swift
@objc func setSelfProfile(name: String, avatarURL: String?, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| name | String | Nickname. |
| avatarURL | String | Profile photo address. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for personal information setting. The `code` will be 0 if the operation succeeds. |


## Room APIs
### createRoom

This API is used to create a room (called by the anchor).

```swift
@objc func createRoom(roomID: UInt32, roomParam: TRTCCreateRoomParam, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomID | UInt32 | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated as a live room list. Currently, Tencent Cloud does not provide the live room list management service. Please manage your live room list on your own. |
| roomParam | TRTCCreateRoomParam | Room description information, such as room name and cover information. If both the room list and room information are managed by yourself, you can ignore this parameter. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room creation result. The `code` will be 0 if the operation succeeds.  |

Generally, the anchor starts live streaming in the following call process: 
1. The **anchor** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted. 
2. The **anchor** calls `createRoom()` to create a live room. No matter whether the room is successfully created, the result will be notified to the anchor through `callback`.
3. The **anchor** calls `starPublish()` to start push.

### destroyRoom

This API is used to terminate a room (called by the anchor). After creating a room, the anchor can call this API to terminate it.
```swift
@objc func destroyRoom(callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room termination result. The `code` will be 0 if the operation succeeds. |



### enterRoom

This API is used to enter a room (called by the viewer).
```swift
@objc func enterRoom(roomID: UInt32, callback: Callback?) 
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomID | UInt32 | Room ID. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room entry result. The `code` will be 0 if the operation succeeds.  |



Generally, the viewer can watch a live stream in the following call process: 
1. The **viewer** gets the latest live room list from your server. The list may contain `roomID` and room information of multiple live rooms.
2. The **viewer** selects a live room and calls `enterRoom()` to enter it.
3. The **viewer** calls `startPlay(userId)` and passes in the `userId` of the anchor to start playback.
 - If the live room list contains the `userId` of the anchor, the viewer can directly call `startPlay(userId)` to start playback.
 - If the viewer does not have the anchor's `userId` before entering the room, after entering the room, the viewer will receive the `onAnchorEnter(userId)` event callback in `TRTCLiveRoomDelegate`, which carries the anchor's `userId` information. Then, the viewer can call `startPlay(userId)` to start playback. 



### exitRoom

This API is used to exit a room.
```swift
@objc func exitRoom(callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room exit result. The `code` will be 0 if the operation succeeds. |

### getRoomInfos

This API is used to get the room list details set through `roomInfo` by the anchor during `createRoom()`.
>?If both the room list and room information are managed on your server, you can ignore this parameter.

```swift
@objc func getRoomInfos(roomIDs: [UInt32], callback: RoomInfoCallback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomIDs | [UInt32] | Room ID list. |
| callback | (_ code: Int, _ message: String?, _ roomList: [TRTCLiveRoomInfo]) -> Void | Callback for room details. |



### getAnchorList

This API is used to get the list of all anchors in the room. It will take effect only if it is called after `enterRoom()` succeeds.
```swift
@objc func getAnchorList(callback: UserListCallback?)
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | Callback for user details. |


### getAudienceList

This API is used to get the information of all viewers in the room. This API will take effect only if it is called after `enterRoom()` succeeds.
```swift
@objc func getAudienceList(callback: UserListCallback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | Callback for user details. |


## Push/Pull APIs
### startCameraPreview

This API is used to enable the preview image of local video.
```swift
@objc func startCameraPreview(frontCamera: Bool, view: UIView, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| frontCamera | Bool | true: front camera; false: rear camera. |
| view | UIView | Control that carries the video image. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |


### stopCameraPreview

This API is used to stop local video capturing and preview.
```swift
@objc func stopCameraPreview()
```


### startPublish

This API is used to start live streaming (push), which is suitable for the following scenarios:
- The anchor starts live streaming.
- The viewer starts co-anchoring.


```swift
@objc func startPublish(streamID: String?, callback: Callback?)
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| streamID | String | Binds the `streamId` of LVB CDN. If you want viewers to watch through LVB CDN, you need to specify the LVB `streamId` of the current anchor. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |


### stopPublish

This API is used to stop live streaming (push), which is suitable for the following scenarios:
- The anchor ends live streaming.
- The viewer ends co-anchoring.


```swift
@objc func stopPublish(callback: Callback?)
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |



### startPlay

This API is used to play back the remote video image. It can be called in general watch and co-anchoring scenarios.
```swift
@objc func startPlay(userID: String, view: UIView, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | ID of the user whose video image is to be played back. |
| view | UIView | `view` control that carries the video image. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |


**General watch scenario**
- If the live room list contains the `userId` of the anchor, the viewer can directly call `startPlay(userId)` to start playing back the anchor's video image after `enterRoom()` succeeds.
- If the viewer does not have the anchor's `userId` before entering the room, after entering the room, the viewer will receive the `onAnchorEnter(userId)` event callback in `TRTCLiveRoomDelegate`, which carries the anchor's `userId` information. Then, the viewer can call `startPlay(userId)` to start playing back the anchor's video image.

**Live streaming co-anchoring scenario**
After co-anchoring is initiated, the anchor will receive the `onAnchorEnter(userId)` callback from `TRTCLiveRoomDelegate`. Then, the anchor can play back the co-anchoring video image by calling `startPlay(userId)` with the `userId` in the callback.



### stopPlay

This API is used to stop rendering the remote video image. It needs to be called when the `onAnchorExit()` callback is received.
```swift
@objc func stopPlay(userID: String, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | Remote user information. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |




## Co-anchoring Between Anchor and Viewer
### requestJoinAnchor

This API is used by the viewer to request co-anchoring.
```swift
@objc func requestJoinAnchor(reason: String?, responseCallback: ResponseCallback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| reason | String? | Reason for co-anchoring. |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | Callback for anchor response. |

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
```swift
@objc func responseJoinAnchor(userID: String, agree: Bool, reason: String?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | Viewer ID. |
| agree | Bool | true: accepts; false: rejects. |
| reason | String? | Reason for accepting/rejecting co-anchoring. |


### kickoutJoinAnchor

This API is used by the anchor to kick out the co-anchoring viewer. After this API is called, the kicked out viewer will receive the `onKickoutJoinAnchor()` callback notification of `TRTCLiveRoomDelegate`.
```swift
@objc func kickoutJoinAnchor(userID: String, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | Co-anchoring viewer ID. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |



## Cross-Room Anchor Competition
### requestRoomPK

This API is used by the anchor to request cross-room competition.
```swift
@objc func requestRoomPK(roomID: UInt32, userID: String, responseCallback: ResponseCallback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomID | UInt32 | Room ID of the invited anchor. |
| userID | String | ID of the invited anchor. |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | Callback for cross-room competition request result. |

Anchors in different rooms can compete with each other. Anchor A and anchor B can start cross-room competition during live streaming in the following steps:
1. **Anchor A** calls `requestRoomPK()` to send a co-anchoring request to anchor B.
2. **Anchor B** receives the `onRequestRoomPK()` callback notification of `TRTCLiveRoomDelegate`.
3. **Anchor B** calls `responseRoomPK()` to decide whether to accept the competition request from anchor A.
4. If **anchor B** accepts the request of anchor A, anchor B will wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to display anchor A's video image.
5. **Anchor A** receives the `responseCallback` callback notification, which carries the processing result from anchor B.
6. If the request of **anchor A** is accepted, anchor A will wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to display anchor B's video image.


### responseRoomPK

This API is used by the anchor to respond to the cross-room competition request. After the anchor responds, the other anchor will receive the `responseCallback` callback passed in by `requestRoomPK`.
```swift
@objc func responseRoomPK(userID: String, agree: Bool, reason: String?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | ID of the anchor who initiates the competition request. |
| agree | Bool | true: accepts; false: rejects. |
| reason | String? | Reason for accepting/rejecting competition. |


### quitRoomPK

This API is used to exit cross-room competition. If either anchor exits cross-room competition, the other anchor will receive the `trtcLiveRoomOnQuitRoomPK()` callback notification of `TRTCLiveRoomDelegate`.

```swift
@objc func quitRoomPK(callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | (_ code: Int, _ message: String?) -> Void | Callback for operation. |


## Audio/Video Control APIs
### switchCamera

This API is used to switch between front and rear cameras.
```swift
@objc func switchCamera()
```


### setMirror

This API is used to set whether to enable mirroring display.
```swift
@objc func setMirror(_ isMirror: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMirror | Bool | Enables/Disables mirroring. |


### muteLocalAudio

This API is used to mute the local audio.
```swift
@objc func muteLocalAudio(_ isMuted: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMuted | Bool | true: mutes; false: unmutes. |

### muteRemoteAudio

This API is used to mute the remote audio.
```swift
@objc func muteRemoteAudio(userID: String, isMuted: Bool) 
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userID | String | Remote user ID. |
| isMuted | Bool | true: mutes; false: unmutes. |



### muteAllRemoteAudio

This API is used to mute all remote audios.
```swift
@objc func muteAllRemoteAudio(_ isMuted: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isMuted | Bool | true: mutes; false: unmutes. |


## Background Music and Sound Effect APIs
### getAudioEffectManager

This API is used to get the background music and sound effect management object [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66).
```swift
@objc func getAudioEffectManager() -> TXAudioEffectManager
```

## Beauty Filter APIs
### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager).
```swift
@objc func getBeautyManager() -> TXBeautyManager
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
```swift
@objc func sendRoomTextMsg(message: String, callback: Callback?) 
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for sending result. |


### sendRoomCustomMsg

This API is used to send a custom text message.
```swift
@objc func sendRoomCustomMsg(command: String, message: String, callback: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| command | String | Custom command word used to distinguish between different message types. |
| message | String | Text message. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for sending result. |


## Debugging APIs
### showVideoDebugLog

This API is used to specify whether to display debugging information on the UI.
```swift
@objc func showVideoDebugLog(_ isShow: Bool)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isShow | Bool | Enables/Disables the display of debugging information. |


## TRTCLiveRoomDelegate Event Callbacks

## General Event Callbacks
### onError

Callback for error.
>?The SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions.

```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onError code: Int, message: String?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| code | Int | Error code. |
| message | String? | Error message. |


### onWarning

Callback for warning.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onWarning code: Int, message: String?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| code | Int | Warning code (TRTCWarningCode). |
| message | String? | Warning message. |



### onDebugLog

Callback for log.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onDebugLog log: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| log | String | Log message. |


## Room Event Callbacks
### onRoomDestroy

Callback for room termination. When the anchor exits the room, all users in the room will receive this callback.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRoomDestroy roomID: String)
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| roomID | String | Room ID. |


### onRoomInfoChange

Callback for live room information change. It is usually used for notifications of room status changes during live streaming co-anchoring and cross-room competition.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRoomInfoChange info: TRTCLiveRoomInfo)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| info | TRTCLiveRoomInfo | Room information. |




## Anchor/Viewer Room Entry/Exit Event Callbacks
### onAnchorEnter

Notification of new anchor's room entry. After co-anchoring viewers and the anchor invited to cross-room competition enter the room, the viewers will receive the event of the new anchor's room entry. `startPlay()` of `TRTCLiveRoom` can be called to display the anchor's video image.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAnchorEnter userID: String)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| userID | String | ID of the new user who enters the room. |



### onAnchorExit

Notification of anchor's room exit. The anchor in the room and co-anchoring viewers will receive the room exit event of the new anchor. `stopPlay()` of `TRTCLiveRoom` can be called to disable the anchor's video image.

```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAnchorExit userID: String) 
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| userID | String | ID of the user who exits the room. |



### onAudienceEnter

Notification of viewer's room entry.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAudienceEnter user: TRTCLiveUserInfo)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user | TRTCLiveUserInfo | Information of the viewer who enters the room. |


### onAudienceExit

Notification of viewer's room exit.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAudienceExit user: TRTCLiveUserInfo) 
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user | TRTCLiveUserInfo | Information of the viewer who exits the room. |


## Anchor/Viewer Co-anchoring Event Callbacks
### onRequestJoinAnchor

Callback when the anchor receives the viewer's co-anchoring request.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user | TRTCLiveUserInfo | Information of the viewer who requests co-anchoring. |
| reason | String? | Reason for co-anchoring. |
| timeout | Double | Timeout period for processing request. |


### onKickoutJoinAnchor

Notification of being kicked out of co-anchoring received by co-anchoring viewer. If the co-anchoring viewer receives a message of being kicked out of co-anchoring by the anchor, the viewer needs to call `stopPublish()` of `TRTCLiveRoom` to exit co-anchoring.
```swift
@objc optional func trtcLiveRoomOnKickoutJoinAnchor(_ trtcLiveRoom: TRTCLiveRoomImpl)
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |



## Anchor Competition Event Callbacks
### onRequestRoomPK

Notification of cross-room competition request. If the anchor receives a competition request from the anchor of another room and accepts the competition, the anchor needs to wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to play back the stream of the inviting anchor.

```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) 
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user | TRTCLiveUserInfo | Information of the anchor who initiates cross-room co-anchoring. |
| timeout | Double | Timeout period for processing request. |


### onQuitRoomPK

Callback for cross-room competition stop.
```swift
 @objc optional func trtcLiveRoomOnQuitRoomPK(_ trtcLiveRoom: TRTCLiveRoomImpl)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |



## Message Event Callbacks
### onRecvRoomTextMsg

Receipt of text message.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| message | String | Text message. |
| user | TRTCLiveUserInfo | User information of sender. |



### onRecvRoomCustomMsg

Receipt of custom message.
```swift
@objc optional func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| command | String | Custom command word used to distinguish between different message types. |
| message | String | Text message. |
| user | TRTCLiveUserInfo | User information of sender. |


<span id="TRTCAudioEffectManager"></span>
## TRTCAudioEffectManager
### playBgm

This API is used to play back background music.
>?When `stopBgm` is called manually, `completion` will not be called back.


```swift
@objc func playBgm(_ url: String, progress:@escaping (_ progressMs: Int, _ duration: Int) -> Void, completion: Callback?)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| url | String | Path of background music file. |
| progress | (_ progressMs: Int, _ duration: Int) -> Void | Callback for progress. The current playback duration and total background music length in ms will be returned. |
| completion | (_ code: Int, _ message: String?) -> Void | Callback for background music stop. |




### stopBgm

This API is used to stop background music.
```swift
@objc func stopBgm()
```


### pauseBgm

This API is used to pause background music.
```swift
@objc func pauseBgm()
```


### resumeBgm

This API is used to resume background music.
```swift
@objc func resumeBgm()
```



### setBGMVolume

This API is used to set background music volume level. It is used to control the background music volume level during playback.
```swift
@objc func setBGMVolume(volume: Int)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | Int | Volume level. `100` indicates normal volume level. Value range: 0–100. Default value: 100. |



### setBGMPosition

This API is used to set the background music playback progress. A returned value of 0 indicates success.
```swift
@objc func setBGMPosition(pos: Int) -> Int
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| pos | Int | Background music playback progress in milliseconds. |


### setMicVolume

This API is used to set mic volume level. It is used to adjust the mic volume level when background music is played back.
```swift
@objc func setMicVolume(volume: Int)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | Int | Volume level. Value range: 0–100. Default value: 100. |


### setReverbType

This API is used to set reverb effect.
```swift
@objc func setReverbType(reverbType:TRTCReverbType)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| reverbType | TRTCReverbType | Reverb type. For more information, please see the definition of [TXReverbType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) in`TRTCCloudDef.h`. |


### setVoiceChangerType

This API is used to set voice changer type.
```swift
@objc func setVoiceChangerType(voiceChangerType:TRTCVoiceChangerType)
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| voiceChangerType | TXVoiceChangerType | Voice changer type. For more information, please see the definition of [TXVoiceChangerType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) in `TRTCCloudDef.h`. |



### playAudioEffect

This API is used to play back a sound effect. You need to assign an ID to each sound effect, through which you can start, stop, or set the volume level of the sound effect. AAC, MP3, and M4A formats are supported.
```swift
@objc func playAudioEffect(effectId: Int32, path: String, count: Int32, publish: Bool, volume: Int32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | Int32 | Sound effect ID. |
| path | String | Path of sound effect. |
| count | Int32 | Loop times. |
| publish | Bool | Whether to push. true: push to viewers; false: local preview. |
| volume | Int32 | Volume level. Value range: 0–100. Default value: 100. |


### pauseAudioEffect

This API is used to pause a sound effect.
```swift
@objc func pauseAudioEffect(effectId: Int32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | Int32 | Sound effect ID. |



### resumeAudioEffect

This API is used to resume a sound effect.
```swift
@objc func resumeAudioEffect(effectId: Int32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | Int32 | Sound effect ID. |


### stopAudioEffect

This API is used to stop a sound effect.
```swift
@objc func stopAudioEffect(effectId: Int32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | Int32 | Sound effect ID. |



### stopAllAudioEffects

This API is used to stop all sound effects.
```swift
@objc func stopAllAudioEffects()
```


### setAudioEffectVolume

This API is used to set sound effect volume level.
```swift
@objc func setAudioEffectVolume(effectId: Int32, volume: Int32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | Int32 | Sound effect ID. |
| volume | Int32 | Volume level. Value range: 0–100. Default value: 100. |


### setAllAudioEffectsVolume

This API is used to set the volume level of all sound effects.
```swift
@objc func setAllAudioEffectsVolume(volume: Int32)
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | Int32 | Volume level. Value range: 0–100. Default value: 100. |
