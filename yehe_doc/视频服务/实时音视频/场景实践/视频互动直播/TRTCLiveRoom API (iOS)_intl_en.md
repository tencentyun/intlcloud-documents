`TRTCLiveRoom` has the following features based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM):

- The anchor can create a live room to start live streaming, and the viewers can enter the room to watch the stream.
- The anchor can interact with viewers through video co-anchoring.
- Anchors in two rooms can compete and interact with each other through co-anchoring.
- Users can send various text and custom messages. Custom messages can be used to send on-screen comments, give likes, and give gifts.

`TRTCLiveRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Co-anchoring Live Streaming (iOS)](https://intl.cloud.tencent.com/document/product/647/36060).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency live streaming component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms during live streaming. In addition, the co-anchoring processes between different anchors are connected through IM messages.



<h2 id="TRTCLiveRoom">TRTCLiveRoom API Overview</h2>

### Basic SDK APIs

| API | Description |
| --------------------------------- | -------------- |
| [delegate](#delegate)             | Sets event callback.           |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Modifies personal information. |

### Room APIs

| API | Description |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates room (called by anchor). If the room does not exist, the system will automatically create a new room. |
| [destroyRoom](#destroyroom) | Terminates room (called by anchor). |
| [enterRoom](#enterroom) | Enters room (called by viewer). |
| [exitRoom](#exitroom) | Exits room (called by viewer). |
| [getRoomInfos](#getroominfos) | Gets room list details.                                     |
| [getAnchorList](#getanchorlist) | Gets the list of all anchors in room. This API will take effect only if it is called after `enterRoom()` succeeds. |
| [getAudienceList](#getaudiencelist) | Gets the information of all viewers in room. This API will take effect only if it is called after `enterRoom()` succeeds. |

### Push/Pull APIs

| API | Description |
| ----------------------------------------- | -------------------------------------------------- |
| [startCameraPreview](#startcamerapreview) | Enables the preview image of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [startPublish](#startpublish)             | Starts live streaming (push).                                |
| [stopPublish](#stoppublish)               | Stops live streaming (push).                                 |
| [startPlay](#startplay) | Plays back remote video image. This API can be called in common watch and co-anchoring scenarios. |
| [stopPlay](#stopplay)                     | Stops rendering remote video images.                             |

### Co-anchoring between the anchor and viewers

| API | Description |
| ----------------------------------------- | ------------------ |
| [requestJoinAnchor](#requestjoinanchor) | Requests co-anchoring (by viewer). |
| [responseJoinAnchor](#responsejoinanchor) | Processes co-anchoring request (by anchor). |
| [kickoutJoinAnchor](#kickoutjoinanchor) | Kicks out a co-anchoring viewer (by anchor). |

### Cross-Room anchor competition

| API | Description |
| --------------------------------- | ---------------------- |
| [requestRoomPK](#requestroompk) | Requests cross-room competition (by anchor). |
| [responseRoomPK](#responseroompk) | Responds to cross-room competition request (by anchor). |
| [quitRoomPK](#quitroompk)         | Quits cross-room competition. |

### Audio/Video control APIs

| API | Description |
| ----------------------------------------- | ------------------ |
| [switchCamera](#switchcamera)   | Switches between front and rear cameras.           |
| [setMirror](#setmirror)                   | Sets whether to enable mirroring display. |
| [muteLocalAudio](#mutelocalaudio) | Mutes local audio. |
| [muteRemoteAudio](#muteremoteaudio) | Mutes remote audio. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes all remote audios. |

### Background music and sound effect APIs

| API | Description |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets background music and sound effect management object [TXAudioEffectManager](#trtcaudioeffectmanagerapi). |

### Beauty filter APIs

| API | Description |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | Gets beauty filter management object [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager). |

### Message sending APIs

| API | Description |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts text message in room. This API is generally used for on-screen comment chat. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends custom text message. |

### Debugging APIs

| API | Description |
| --------------------------------------- | --------------------------- |
| [showVideoDebugLog](#showvideodebuglog) | Specifies whether to display debugging information on the UI. |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API Overview</h2>

### Common event callbacks

| API | Description |
| ------------------------- | ---------- |
| [onError](#onerror) | Callback for error. |
| [onWarning](#onwarning) | Callback for warning. |
| [onDebugLog](#ondebuglog) | Callback for log. |

### Room event callbacks

| API | Description |
| ------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy) | Callback for room termination. |
| [onRoomInfoChange](#onroominfochange) | Callback for live room information change. |

### Anchor/Viewer room entry/exit event callbacks

| API | Description |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter) | Notification of new anchor's room entry. |
| [onAnchorExit](#onanchorexit) | Notification of anchor's room exit. |
| [onAudienceEnter](#onaudienceenter) | Notification of viewer's room entry. |
| [onAudienceExit](#onaudienceexit) | Notification of viewer's room exit. |

### Anchor/Viewer co-anchoring event callbacks

| API | Description |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | Callback when the anchor receives a viewer's co-anchoring request. |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | Notification of being kicked out of co-anchoring received by co-anchoring viewer. |

### Anchor competition event callbacks

| API | Description |
| ----------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk) | Notification of cross-room competition request. |
| [onQuitRoomPK](#onquitroompk) | Notification of cross-room competition stop. |

### Message event callbacks

| API | Description |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | Receipt of text message.   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of custom message. |



## Basic SDK APIs

### delegate

This API is used to get the event callback of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060). You can use `TRTCLiveRoomDelegate` to get various status notifications of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060).

```objc
@property(nonatomic, weak)id<TRTCLiveRoomDelegate> delegate;
```

>?`delegate` is the delegation callback of `TRTCLiveRoom`.


### login

This API is used to log in.

```objc
/// This API is used to log in the component system
/// - Parameters:
///   - sdkAppID: you can view `SDKAppID` on the TRTC console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info".
///   - userID: ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_).
///   - userSig: Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
///   - config: global configuration information. Please initialize it during login as it cannot be modified after login. Use `isAttachedTUIKit` to specify whether to include `TUIKit` into the project.
///   - callback: callback for login. The `code` will be 0 if the operation succeeds.
/// - Note:
///   - userSig: You're advised to set the validity of `userSig` as seven days to avoid IM's failure in receiving and sending messages, failure in TRTC co-anchoring due to `UserSig` expiration.
- (void)loginWithSdkAppID:(int)sdkAppID
                  userID:(NSString *)userID
                 userSig:(NSString *)userSig
                  config:(TRTCLiveRoomConfig *)config
                callback:(Callback _Nullable)callback
NS_SWIFT_NAME(login(sdkAppID:userID:userSig:config:callback:));
```

The parameters are as detailed below:

| Parameter      | Type                                      | Description                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| sdkAppID | Int | You can view the `SDKAppID` in the TRTC Console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| userID | String | ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| config | TRTCLiveRoomConfig | Global configuration information, which needs to be initialized during the login and cannot be modified after the login.<ul style="margin:0;"><li>`useCDNFirst` attribute: used to set the way how viewers will watch live streaming. `true` means that general viewers will watch live streaming over CDN, which is cheap but has a high latency. `false` means that general viewers will watch live streaming through the low latency scheme, the cost of which ranges between that of CDN and co-anchoring, but the delay can be controlled within 1 second. </li><li>`CDNPlayDomain` attribute: it will take effect only if `useCDNFirst` is set to `true`. It is used to specify the playback domain name for watching over CDN. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** in the LVB Console.</li></ul> |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for login. The `code` will be 0 if the operation succeeds.                                  |


### logout

This API is used to log out.

```objc
// Logs out.
/// - Parameter callback: Callback for logout. The `code` will be 0 if the operation succeeds.
- (void)logout:(Callback _Nullable)callback
NS_SWIFT_NAME(logout(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | --------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for logout. The `code` will be 0 if the operation succeeds. |


### setSelfProfile

This API is used to modify personal information.

```objc
/// This API is used to set user information, which will be stored in IM.
/// - Parameters:
///   - name: user name.
///   - avatarURL: URL of user profile photo.
///   - callback: Callback for personal information setting. The `code` will be 0 if the operation succeeds.
- (void)setSelfProfileWithName:(NSString *)name
                     avatarURL:(NSString * _Nullable)avatarURL
                      callback:(Callback _Nullable)callback
NS_SWIFT_NAME(setSelfProfile(name:avatarURL:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ----------------------------------------- | ----------------------------------- |
| name      | String                                    | Nickname.                              |
| `avatar` | `String` | User profile photo URL. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for personal information setting. The `code` will be 0 if the operation succeeds. |


## Room APIs

### createRoom

This API is used to create a room (called by the anchor).

```objc
/// This API is used to create a room (called by anchor). If the room does not exist, the system will automatically create a new room.
/// Generally, the anchor starts live streaming in the following call process:
/// 1. The **anchor** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted.
/// 2. The **anchor** calls `createRoom()` to create a live room. No matter whether the room is successfully created, the result will be notified to the anchor through `callback`.
/// 3. The **anchor** calls `starPublish()` to start push.
/// - Parameters:
///   - roomID: Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated as a live room list. Currently, Tencent Cloud does not provide the live room list management service. Please manage your live room list on your own.
///   - roomParam: TRTCCreateRoomParam | Room description information, such as room name and cover information. If both the room list and room information are managed by yourself, you can ignore this parameter.
///   - callback:  Callback for room entry result. The `code` will be 0 if the operation succeeds.
/// - Note:
///   - The anchor will call this function when starting a live stream. The anchor can create a room with a used Room ID.
- (void)createRoomWithRoomID:(UInt32)roomID
                   roomParam:(TRTCCreateRoomParam *)roomParam
                    callback:(Callback _Nullable)callback
NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ----------------------------------------- | ------------------------------------------------------------ |
| roomID | UInt32 | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated as a live room list. Currently, Tencent Cloud does not provide the live room list management service. Please manage your live room list on your own. |
| roomParam | TRTCCreateRoomParam | Room description information, such as room name and cover information. If both the room list and room information are managed by yourself, you can ignore this parameter. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room creation result. The `code` will be 0 if the operation succeeds.  |

Generally, the anchor starts live streaming in the following call process: 

1. The **anchor** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted. 
2. The **anchor** calls `createRoom()` to create a live room. No matter whether the room is successfully created, the result will be notified to the anchor through `callback`.
3. The **anchor** calls `starPublish()` to start push.

### destroyRoom

This API is used to terminate a room (called by the anchor). After creating a room, the anchor can call this API to terminate it.

```objc
/// This API is used to terminate a room (called by the anchor).
/// After creating a room, the anchor can call this API to terminate it.
/// - Parameter callback: callback for room termination result. The `code` will be 0 if the operation succeeds.
/// - Note:
///   - After creating a room, the anchor can call this API to terminate it.
- (void)destroyRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(destroyRoom(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room termination result. The `code` will be 0 if the operation succeeds. |



### enterRoom

This API is used to enter a room (called by the viewer).

```objc
/// This API is used to enter a room (called by the viewer).
/// Generally, the viewer can watch a live stream in the following call process:
/// 1. The **viewer** gets the latest live room list from your server. The list contains `roomID` and room information of multiple live rooms.
/// 2. The **viewer** selects a live room and calls `enterRoom()` to enter it.
/// 3. If `userID` of every anchor is included in the room list managed by the **viewer's** server, the viewer can directly call `startPlay(userID)` to start playing back an anchor's video image after `enterRoom()` succeeds.
/// It doesn't matter if the room list only contains `roomid`. The viewer will receive the `onAnchorEnter(userID)` event callback in `TRTCLiveRoomDelegate`.
/// Then, the viewer can play back an anchor's video image by using the `userID` in the callback to call `startPlay(userID)`.
/// - Parameters:
///   - roomID: room ID.
///   - useCDNFirst: whether to use CDN for playback preferably.
///   - cdnDomain: CDN domain name.
///   - callback: callback for room entry result. The `code` will be 0 if the operation succeeds.
/// - Note:
///   - This API is called by viewers when they are entering a live streaming room.
///   - Anchors cannot use this API to enter rooms created by themselves. They should use `createRoom`.
- (void)enterRoomWithRoomID:(UInt32)roomID
                useCDNFirst:(BOOL)useCDNFirst
                  cdnDomain:(NSString * _Nullable)cdnDomain
                   callback:(Callback)callback
NS_SWIFT_NAME(enterRoom(roomID:useCDNFirst:cdnDomain:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------------------------------- |
| roomID   | UInt32                                    | room ID.                            |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room entry result. The `code` will be 0 if the operation succeeds.  |



Generally, the viewer can watch a live stream in the following call process: 

1. The **viewer** gets the latest live room list from your server. The list may contain `roomID` and room information of multiple live rooms.
2. The **viewer** selects a live room and calls `enterRoom()` to enter it.
3. The **viewer** calls `startPlay(userID)` and passes in the `userID` of the anchor to start playback.
 - If the live room list contains the `userID` of the anchor, the viewer can directly call `startPlay(userID)` to start playback.
 - If the viewer does not have the anchor's `userID` before entering the room, after entering the room the viewer will receive the `onAnchorEnter(userID)` event callback in `TRTCLiveRoomDelegate`, which carries the anchor's `userID` information. Then, the viewer can call `startPlay(userID)` to start playback. 



### exitRoom

This API is used to exit a room.

```objc
/// This API is used to exit a room (called by the viewer).
/// - Parameter callback: Callback for room exit result. The `code` will be 0 if the operation succeeds.
/// - Note:
///   - Viewers can call this API to exit a live streaming room.
///   - Anchors cannot call this API to exit a room.

- (void)exitRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(exitRoom(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room exit result. The `code` will be 0 if the operation succeeds. |

### getRoomInfos

This API is used to get the room list details set through `roomInfo` by the anchor during `createRoom()`.
>?If both the room list and room information are managed on your server, you can ignore this parameter.

```objc
/// This API is used to get the room list details.
/// `roomInfo` is set by the anchor when using `createRoom()` to create room. If both the room list and room information are managed on your server, you can ignore this parameter.
/// - Parameter roomIDs: Room ID list.
/// - Parameter callback: callback for room details. 
- (void)getRoomInfosWithRoomIDs:(NSArray<NSNumber *> *)roomIDs
                       callback:(RoomInfoCallback _Nullable)callback
NS_SWIFT_NAME(getRoomInfos(roomIDs:callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ------------------ |
| roomIDs  | [UInt32]                                                     | Room ID list.       |
| callback | (_ code: Int, _ message: String?, _ roomList: [TRTCLiveRoomInfo]) -> Void | Callback for room details. |



### getAnchorList

This API is used to get the list of all anchors in the room. It will take effect only if it is called after `enterRoom()` succeeds.

```objc
/// This API is used to get the list of all anchors in the room. It will take effect only if it is called after `enterRoom()` succeeds.
/// - Parameter callback: callback for user details
- (void)getAnchorList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAnchorList(callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | Callback for user details. |


### getAudienceList

This API is used to get the information of all viewers in the room. This API will take effect only if it is called after `enterRoom()` succeeds.

```objc
/// This API is used to get the information of all viewers in the room. This API will take effect only if it is called after `enterRoom()` succeeds.
/// - Parameter callback: callback for user details.
- (void)getAudienceList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAudienceList(callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | Callback for user details. |


## Push/Pull APIs

### startCameraPreview

This API is used to enable preview of the local video image.

```objc
/// This API is used to enable preview of the local video image.
/// - Parameters:
///   - frontCamera: true: front camera; false: rear camera.
///   - view: the control that carries the video image.
///   - callback: operation callback.
- (void)startCameraPreviewWithFrontCamera:(BOOL)frontCamera
                                     view:(UIView *)view
                                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startCameraPreview(frontCamera:view:callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ----------------------------------------- | ------------------------------------- |
| frontCamera | Bool                                      | true: front camera; false: rear camera. |
| view        | UIView                                    | The control that carries the video image.                  |
| callback    | (_ code: Int, _ message: String?) -> Void | Operation callback.                         |


### stopCameraPreview

This API is used to stop local video capture and preview.

```objc
/// This API is used to stop local video capture and preview.
- (void)stopCameraPreview;

```


### startPublish

This API is used to start live streaming (push), which is suitable for the following scenarios:

- The anchor starts live streaming.
- The viewer starts co-anchoring.


```objc
/// This API is used to start live streaming (push), which is suitable for the following scenarios:
/// 1. The anchor starts live streaming.
/// 2. The viewer starts co-anchoring.
/// - Parameters:
///   - streamID: binds the `streamId` of LVB CDN. If you want viewers to watch through LVB CDN, you need to specify the LVB `streamId` of the current anchor.
///   - callback: operation callback.
- (void)startPublishWithStreamID:(NSString *)streamID
                        callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPublish(streamID:callback:));
```

The parameters are as detailed below:

| Parameter      | Type                                      | Description                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| streamID | String | Binds the `streamID` of LVB CDN. If you want viewers to watch through LVB CDN, you need to specify the LVB `streamID` of the current anchor. |
| callback | (_ code: Int, _ message: String?) -> Void | Operation callback.                                                   |


### stopPublish

This API is used to stop live streaming (push), which is suitable for the following scenarios:

- The anchor ends live streaming.
- The viewer ends co-anchoring.

```objc
/// This API is used to stop live streaming (push), which is suitable for the following scenarios:
/// 1. The anchor ends live streaming.
/// 2. The viewer ends co-anchoring.
/// - Parameter callback: operation callback.
- (void)stopPublish:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPublish(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | Operation callback.  |



### startPlay

This API is used to play back the remote video image. It can be called in common viewing and co-anchoring scenarios.

```objc
/// This API is used to play back the remote video image. It can be called in common viewing and co-anchoring scenarios.
/// **General watch scenario**
/// 1. If `userID` of every anchor is included in the room list managed by the viewer's server, the viewer can directly call `startPlay(userID)` to start playing back an anchor's video image after `enterRoom()` succeeds.
/// 2. It doesn't matter if the room list only contains `roomid`. The viewer will receive the `onAnchorEnter(userID)` event callback in `TRTCLiveRoomDelegate`.
/// Then, the viewer can play back the anchor's video image by using the `userID` in the callback to call `startPlay(userID)`.
/// **Live streaming co-anchoring scenario**
After the co-anchoring is initiated, the anchor will receive the `onAnchorEnter(userID)` callback from `TRTCLiveRoomDelegate`. Then, the anchor can play back the co-anchoring video image by using the `userID` in the callback to call `startPlay(userID)`.
/// - Parameters:
///   - userID: user ID of the viewer.
///   - view: the control that carries the video image.
///   - callback: operation callback.
- (void)startPlayWithUserID:(NSString *)userID
                       view:(UIView *)view
                   callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPlay(userID:view:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | -------------------------- |
| userID   | String                                    | User ID of the viewer.        |
| view     | UIView                                    | the control that carries the video image. |
| callback    | (_ code: Int, _ message: String?) -> Void | Operation callback.                            |


**General watch scenario**

- If the live room list contains the `userID` of the anchor, the viewer can directly call `startPlay(userID)` to start playing back the anchor's video image after `enterRoom()` succeeds.
- If the viewer does not have the anchor's `userID` before entering the room, after entering the room, the viewer will receive the `onAnchorEnter(userID)` event callback in `TRTCLiveRoomDelegate`, which carries the anchor's `userID` information. Then, the viewer can call `startPlay(userID)` to start playing back the anchor's video image.

**Live streaming co-anchoring scenario**
After the co-anchoring is initiated, the anchor will receive the `onAnchorEnter(userID)` callback from `TRTCLiveRoomDelegate`. Then, the anchor can play back the co-anchoring video image by using the `userID` in the callback to call `startPlay(userID)`.



### stopPlay

This API is used to stop rendering the remote video image. It needs to be called when the `onAnchorExit()` callback is received.

```objc
This API is used to stop rendering remote video image.
/// - Parameters:
///   - userID: ID of the remote user.
///   - callback: operation callback.
/// - Note:
///   - This API will be called when `onAnchorExit` callback is received.
- (void)stopPlayWithUserID:(NSString *)userID
                  callback:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPlay(userID:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ---------------- |
| userID   | String                                    | ID of the remote user. |
| callback    | (_ code: Int, _ message: String?) -> Void | Operation callback.                            |




## Co-anchoring Between the Anchor and Viewers

### requestJoinAnchor

This API is used by the viewer to request co-anchoring.

```objc
/// This API is used by the viewer to request co-anchoring.
/// - Parameters:
///   - reason: reason for requesting co-anchoring.
///   - responseCallback: callback of the co-anchoring request.
/// - Note: after a viewer initiates the co-anchoring request, the anchor will receive `onRequestJoinAnchor` callback.
- (void)requestJoinAnchor:(NSString *)reason
                  timeout:(double)timeout
         responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestJoinAnchor(reason:timeout:responseCallback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------------------------------- | -------------- |
| reason           | String?                                     | reason for the co-anchoring.     |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | Callback for the anchor response. |

The anchor and viewers start co-anchoring in the following steps:

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

```objc
/// The anchor use this API to respond to the viewer's request for co-anchoring.
/// - Parameters:
///   - user: ID of the viewer.
///   - agree: true: accepts; false: rejects.
///   - reason: reasons for accepting/rejecting co-anchoring.
/// - Note: after the anchor responds, the viewer will receive `responseCallback` passed in by `requestJoinAnchor`.
- (void)responseJoinAnchor:(NSString *)userID
                     agree:(BOOL)agree
                    reason:(NSString *)reason
NS_SWIFT_NAME(responseJoinAnchor(userID:agree:reason:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | ------------------------- |
| userID | String | ID of the viewer. |
| agree | Bool | true: accepts; false: rejects. |
| reason | String? | Reason for accepting/rejecting co-anchoring. |


### kickoutJoinAnchor

This API is used by the anchor to kick out co-anchoring viewers. After this API is called, the kicked out viewer will receive the `onKickoutJoinAnchor()` callback notification of `TRTCLiveRoomDelegate`.

```objc
/// This API is used by the anchor to kick out co-anchoring viewers.
/// - Parameters:
///   - userID: ID of the co-anchoring viewer.
///   - callback: operation callback.
After this API is called, the kicked out viewer will receive the callback notification of `trtcLiveRoomOnKickoutJoinAnchor()`.
- (void)kickoutJoinAnchor:(NSString *)userID
                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(kickoutJoinAnchor(userID:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------- |
| userID   | String                                    | ID of the co-anchoring viewer. |
| callback    | (_ code: Int, _ message: String?) -> Void | Operation callback.                            |



## Cross-Room Anchor Competition

### requestRoomPK

This API is used by the anchor to request cross-room competition.

```objc
/// This API is used by the anchor to request cross-room competition.
/// - Parameters:
///   - roomID: room ID of the invited anchor.
///   - userID: user ID of the invited anchor. 
///   - responseCallback: result callback of the cross-room competition request.
/// - Note: After the request is initiated, the invited anchor will receive the `onRequestRoomPK` callback.
- (void)requestRoomPKWithRoomID:(UInt32)roomID
                         userID:(NSString *)userID
               responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestRoomPK(roomID:userID:responseCallback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------------------------------- | ------------------------ |
| roomID           | UInt32                                      | Room ID of the invited anchor.          |
| userID           | String                                      | User ID of the invited anchor.         |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | Result callback of the cross-room competition request. |

Anchors in different rooms can compete with each other. Anchor A and anchor B can start cross-room competition during live streaming in the following steps:

1. **Anchor A** calls `requestRoomPK()` to send a co-anchoring request to anchor B.
2. **Anchor B** receives the `onRequestRoomPK()` callback notification of `TRTCLiveRoomDelegate`.
3. **Anchor B** calls `responseRoomPK()` to decide whether to accept the competition request from anchor A.
4. If **anchor B** accepts the request of anchor A, anchor B will wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to display anchor A's video image.
5. **Anchor A** receives the `responseCallback` callback notification, which carries the processing result from anchor B.
6. If the request of **anchor A** is accepted, anchor A will wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to display anchor B's video image.


### responseRoomPK

This API is used by the anchor to respond to the cross-room competition request. After the anchor responds, the other anchor will receive the `responseCallback` callback passed in by `requestRoomPK`.

```objc
/// This API is used to respond to a cross-room competition request.
/// This anchor can respond to cross-room competition requests from anchors of other rooms.
/// - Parameters:
///   - user: ID of the anchor who initiates the competition request.
///   - agree: true: accepts; false: rejects.
///   - reason: reason for accepting/rejecting the competition.
/// - Note: after the anchor responds, the other anchor will receive the `responseCallback` callback passed in by `requestRoomPK`.
- (void)responseRoomPKWithUserID:(NSString *)userID
                           agree:(BOOL)agree
                          reason:(NSString *)reason
NS_SWIFT_NAME(responseRoomPK(userID:agree:reason:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | ------------------------- |
| userID | String | ID of the anchor who initiates the competition request. |
| agree | Bool | true: accepts; false: rejects. |
| reason | String? | Reason for accepting/rejecting the competition. |


### quitRoomPK

This API is used to exit cross-room competition. If either anchor exits cross-room competition, the other anchor will receive the `trtcLiveRoomOnQuitRoomPK()` callback notification of `TRTCLiveRoomDelegate`.

```objc
/// This API is used to quit the cross-room competition.
/// - Parameter callback: result callback of quitting the cross-room competition.
// - Note: if either anchor exits cross-room competition, the other anchor will receive the callback notification of `trtcLiveRoomOnQuitRoomPK`.
- (void)quitRoomPK:(Callback _Nullable)callback
NS_SWIFT_NAME(quitRoomPK(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ---------- |
| callback    | (_ code: Int, _ message: String?) -> Void | Operation callback.                            |


## Audio/Video Control APIs

### switchCamera

This API is used to switch between front and rear cameras.

```objc
/// This API is used to switch between front and rear cameras.
- (void)switchCamera;
```


### setMirror

This API is used to set whether to enable mirroring display.

```objc
/// This API is used to set whether to enable mirroring display.
/// - Parameter isMirror: enables/disables mirroring.
- (void)setMirror:(BOOL)isMirror
NS_SWIFT_NAME(setMirror(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ---- | --------------- |
| isMirror | Bool | Enables/Disables mirroring. |


### muteLocalAudio

This API is used to mute the local audio.

```objc
/// This API is used to mute the local audio.
/// - Parameter isMuted: true: mutes; false: unmutes. |
- (void)muteLocalAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteLocalAudio(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | true: mutes; false: unmutes. |

### muteRemoteAudio

This API is used to mute the remote audio.

```objc
/// This API is used to mute the remote audio.
/// - Parameters:
///   - userID: ID of the remote user.
///   - isMuted: true: mutes; false: unmutes. |
- (void)muteRemoteAudioWithUserID:(NSString *)userID isMuted:(BOOL)isMuted
NS_SWIFT_NAME(muteRemoteAudio(userID:isMuted:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------------------------------- |
| userID | String | ID of the remote user. |
| isMuted | Bool | true: mutes; false: unmutes. |



### muteAllRemoteAudio

This API is used to mute all remote audios.

```objc
/// This API is used to mute all remote audios.
/// - Parameter isMuted: true: mutes; false: unmutes. |
- (void)muteAllRemoteAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteAllRemoteAudio(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | true: mutes; false: unmutes. |

### setAudioQuality

This API is used to set the audio quality.

```objc
/// This API is used to set audio quality. Valid values: 1, 2, and 3, which represent low, middle, and high quality respectively.
/// - Parameter quality: audio quality.
- (void)setAudioQuality:(NSInteger)quality
NS_SWIFT_NAME(setAudioiQuality(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | --------- | ---------------------------- |
| quality | NSInteger | 1: audio; 2: standard; 3: music. |

## Background Music and Sound Effect APIs

### getAudioEffectManager

This API is used to get the background music and sound effect management object [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66).

```objc
/// This API is used to get the sound effect management object.
- (TXAudioEffectManager *)getAudioEffectManager;
```

## Beauty Filter APIs

### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__ios.html#interfaceTXBeautyManager).

```objc
/* Gets beauty filter management object `TXBeautyManager`.
*
* You can use the following features of beauty filter management:
* - Set the following beauty effects: whitening, ruddy, big eyes, slim face, V-shaped face, small chin, small face, small nose, bright eyes, white teeth, removing eye bags, removing wrinkles, and removing laugh lines.
* - Adjust the hairline, eye spacing, eye corners, mouth shape, nose wings, nose position, lip thickness, and face shape.
* - Set animated effects such as face widgets (materials).
* - Add makeup effects.
* - Recognize gestures.
*/
- (TXBeautyManager *)getBeautyManager;
```

You can use the following features of beauty filter management:

- Set the following beauty effects: whitening, ruddy, big eyes, slim face, V-shaped face, small chin, small face, small nose, bright eyes, white teeth, removing eye bags, removing wrinkles, and removing laugh lines.
- Adjust the hairline, eye spacing, eye corners, mouth shape, nose wings, nose position, lip thickness, and face shape.
- Set animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.



## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in the room, which is generally used for on-screen comment chat.

```objc
/// This API is used to send text messages visible to all members in the room.
/// - Parameters:
///   - message: text message.
///   - callback: callback for the sending result.
- (void)sendRoomTextMsg:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | -------------- |
| message | String | Text message. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the sending result. |


### sendRoomCustomMsg

This API is used to send a custom text message.

```objc
/// This API is used to send a custom text message.
/// - Parameters:
///   - command: custom command word used to distinguish between different message types. |
///   - message: text message.
///   - callback: callback for the sending result.
- (void)sendRoomCustomMsgWithCommand:(NSString *)cmd message:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | -------------------------------------------------- |
| command  | String                                    | Custom command word used to distinguish between different message types. |
| message  | String                                    | Text message.                                         |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the sending result.  |


## Debugging APIs

### showVideoDebugLog

This API is used to specify whether to display debugging information on the UI.

```objc
/// This API is used to specify whether to display debugging information on the UI.
/// - Parameter isShow: enables/disables the display of debugging information.
- (void)showVideoDebugLog:(BOOL)isShow
NS_SWIFT_NAME(showVideoDebugLog(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------- |
| isShow | Bool | Enables/Disables the display of debugging information. |


## TRTCLiveRoomDelegate Event Callbacks

## Common Event Callbacks

### onError

Error callback.

>?The SDK encountered an irrecoverable error which must be listened on. Corresponding UI reminders should be displayed as needed.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
             onError:(NSInteger)code
             message:(NSString  *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onError:message:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| code | Int | Error code. |
| message | String? | Error message. |


### onWarning

Callback for warnings.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
           onWarning:(NSInteger)code
             message:(NSString *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onWarning:message:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| code         | Int              | Error code `TRTCWarningCode`.    |
| message      | String?          | Warning message.                   |



### onDebugLog

Callback for log.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
          onDebugLog:(NSString *)log
NS_SWIFT_NAME(trtcLiveRoom(_:onDebugLog:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| log          | String           | Log information.                   |


## Room Event Callbacks

### onRoomDestroy

Callback for room termination. When the anchor exits the room, all users in the room will receive this callback.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onRoomDestroy:(NSString *)roomID
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomDestroy:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| roomID       | String           | Room ID.                    |


### onRoomInfoChange

Callback for live room information change. It is usually used for notifications of room status changes during live streaming co-anchoring and cross-room competition.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
    onRoomInfoChange:(TRTCLiveRoomInfo *)info
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomInfoChange:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| info         | TRTCLiveRoomInfo | Room information.                   |




## Anchor/Viewer Room Entry/Exit Event Callbacks

### onAnchorEnter

Notification of new anchor's room entry. After co-anchoring viewers and the anchor invited to cross-room competition enter the room, the viewers will receive the event of the new anchor's room entry. `startPlay()` of `TRTCLiveRoom` can be called to display the anchor's video image.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onAnchorEnter:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorEnter:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| userID | String | ID of the user who newly enters the room. |



### onAnchorExit

Notification of the anchor's room exit. The anchor in the room and co-anchoring viewers will receive the room exit event of the new anchor. `stopPlay()` of `TRTCLiveRoom` can be called to disable the anchor's video image.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
        onAnchorExit:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorExit:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| userID | String | ID of the user who exits the room. |



### onAudienceEnter

Notification of viewer's room entry.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onAudienceEnter:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceEnter:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user         | TRTCLiveUserInfo | Information of the user who enters the room.               |


### onAudienceExit

Notification of viewer's room exit.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
      onAudienceExit:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceExit:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user         | TRTCLiveUserInfo | Information of the user who exits the room.                |


## Anchor/Viewer Co-anchoring Event Callbacks

### onRequestJoinAnchor

Callback when the anchor receives a viewer's co-anchoring request.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
 onRequestJoinAnchor:(TRTCLiveUserInfo *)user
             reason:(NSString * _Nullable)reason
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestJoinAnchor:reason:timeout:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| userInfo | TRTCLiveUserInfo | Information of the viewer who requests co-anchoring. |
| reason       | String?          | Reason for co-anchoring.                |
| timeout      | Double           | Timeout period for processing a request.         |


### onKickoutJoinAnchor

Notification of being kicked out of co-anchoring received by a co-anchoring viewer. If the co-anchoring viewer receives such notification, the viewer needs to call `stopPublish()` of `TRTCLiveRoom` to exit co-anchoring.

```objc
- (void)trtcLiveRoomOnKickoutJoinAnchor:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnKickoutJoinAnchor(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |



## Anchor Competition Event Callbacks

### onRequestRoomPK

Notification of cross-room competition request. If an anchor receives a competition request from an anchor of another room and accepts the competition, the anchor needs to wait for the `onAnchorEnter()` notification of `TRTCLiveRoomDelegate` and call `startPlay()` to play back the stream of the inviting anchor.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onRequestRoomPK:(TRTCLiveUserInfo *)user
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestRoomPK:timeout:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| user | TRTCLiveUserInfo | Information of the anchor who initiates cross-room co-anchoring. |
| timeout      | Double           | Timeout period for processing request.        |


### onQuitRoomPK

Callback for cross-room competition stop.

```objc
 - (void)trtcLiveRoomOnQuitRoomPK:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnQuitRoomPK(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |



## Message Event Callbacks

### onRecvRoomTextMsg

Callback for receiving a text message.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
   onRecvRoomTextMsg:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomTextMsg:fromUser:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| message | String | Text message. |
| user         | TRTCLiveUserInfo | User information of the sender.             |



### onRecvRoomCustomMsg

Callback for receiving a custom message.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
onRecvRoomCustomMsgWithCommand:(NSString *)command
             message:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomCustomMsg:message:fromUser:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | ---------------- | -------------------------------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance. |
| command | String | Custom command word used to distinguish between different message types. |
| message | String | Text message. |
| user         | TRTCLiveUserInfo | User information of the sender.                                   |
