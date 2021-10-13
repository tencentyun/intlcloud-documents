`TRTCLiveRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a room and start live streaming, or enter a room as audience.
- The anchor and audience in a room can co-anchor with each other.
- Anchors in two rooms can compete and interact with each other.
- All users can send text and custom messages. Custom messages can be used to send on-screen comments, give likes, and send gifts.

`TRTCLiveRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Interactive Live Video Streaming (iOS)](https://intl.cloud.tencent.com/document/product/647/36060).

- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615) is used as a low-latency live streaming component.
- IM SDK: The `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996) is used to implement chat rooms, and IM messages are used to facilitate the co-anchoring process.



<h2 id="TRTCLiveRoom">`TRTCLiveRoom` API Overview</h2>

### Basic SDK APIs

| API                                             | Description                                                         |
| --------------------------------- | -------------- |
| [delegate](#delegate)             | Sets event callbacks.           |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets the profile. |

### Room APIs

| API | Description |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates a room (called by anchor). If the room does not exist, the system will create the room automatically. |
| [destroyRoom](#destroyroom) | Terminates a room (called by anchor). |
| [enterRoom](#enterroom) | Enters a room (called by audience). |
| [exitRoom](#exitroom) | Exits a room (called by audience). |
| [getRoomInfos](#getroominfos)           | Gets room list details.                                     |
| [getAnchorList](#getanchorlist) | Gets the anchors and co-anchoring viewers in a room. This API works only if it is called after `enterRoom()`. |
| [getAudienceList](#getaudiencelist) | Gets the information of all audience in a room. This API works only if it is called after `enterRoom()`. |

### Stream pushing/pulling APIs

| API                                             | Description                                                         |
| ----------------------------------------- | -------------------------------------------------- |
| [startCameraPreview](#startcamerapreview) | Enables preview of the local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [startPublish](#startpublish)             | Starts live streaming (pushing streams).                                 |
| [stopPublish](#stoppublish)               | Stops live streaming (pushing streams).                                 |
| [startPlay](#startplay) | Plays a remote video. This API can be called in common playback and co-anchoring scenarios. |
| [stopPlay](#stopplay)                     | Stops rendering a remote video.                             |

### APIs for anchor-audience co-anchoring

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
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html#interfaceTXAudioEffectManager). |

### Beauty filter APIs

| API                                             | Description                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager). |

### Message sending APIs

| API                                     | Description                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

### Debugging APIs

| API                                             | Description                                                         |
| --------------------------------------- | --------------------------- |
| [showVideoDebugLog](#showvideodebuglog) | Specifies whether to display debugging information on the UI. |

<h2 id="TRTCLiveRoomDelegate">`TRTCLiveRoomDelegate` API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------- |
| [onError](#onerror) | Error |
| [onWarning](#onwarning) | Warning |
| [onDebugLog](#ondebuglog) | Log |

### Room event callback APIs

| API                                             | Description                                                         |
| ------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)     | The room was terminated.       |
| [onRoomInfoChange](#onroominfochange) | The room information changed. |

### Callback APIs for entry/exit of anchors/audience

| API                                             | Description                                                         |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter) | There is a new anchor/co-anchoring viewer in the room. |
| [onAnchorExit](#onanchorexit)       | An anchor/co-anchoring viewer quit competition/co-anchoring.   |
| [onAudienceEnter](#onaudienceenter) | A viewer entered the room.    |
| [onAudienceExit](#onaudienceexit) | A viewer left the room. |

### Callback APIs for anchor-audience co-anchoring events

| API                                             | Description                                                         |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | A co-anchoring request was received. |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | A user was removed from co-anchoring. |

### Callback APIs for anchor competition events

| API                                             | Description                                                         |
| ----------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk) | A cross-room competition request was received. |
| [onQuitRoomPK](#onquitroompk) | Cross-room competition ended. |

### Message event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | A text message was received.  |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | A custom message was received. |



## Basic SDK APIs

### delegate

This API is used to get callbacks for the events of [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060). You can use `TRTCLiveRoomDelegate` to get the callbacks.

```objc
@property(nonatomic, weak)id<TRTCLiveRoomDelegate> delegate;
```

>?`delegate` is the delegate callback of `TRTCLiveRoom`.


### login

This API is used to log in.

```objc
/// Log in to the component.
/// - Parameters:
///   - sdkAppID: You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console.
///   - userID: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_)
///   - userSig: Tencent Cloud's proprietary security signature. For how to get it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
///   - config: global configuration information, which should be initialized during login and cannot be modified afterward. Use `isAttachedTUIKit` to specify whether to import TUIKit into your project.
///   - callback: callback for login. The return code is `0` if login is successful.
/// - Note:
///   - You are advised to set the validity period of `userSig` to 7 days to avoid cases where message sending/receiving and co-anchoring fail due to expired `userSig`.
- (void)loginWithSdkAppID:(int)sdkAppID
                  userID:(NSString *)userID
                 userSig:(NSString *)userSig
                  config:(TRTCLiveRoomConfig *)config
                callback:(Callback _Nullable)callback
NS_SWIFT_NAME(login(sdkAppID:userID:userSig:config:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| sdkAppId | Int | You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| userID | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_) |
| userSig | String | Tencent Cloud's proprietary security signature. For how to obtain it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| config | TRTCLiveRoomConfig | Global configuration information, which needs to be initialized during login and cannot be modified afterward. <ul style="margin:0;"><li>`useCDNFirst`: specifies the way audience watch live streams. `true` means watching over CDNs, which is cost-efficient but has high latency. `false` means watching under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second. </li><li>`CDNPlayDomain`: specifies the domain name for CDN live streaming. It takes effect only if `useCDNFirst` is set to `true`. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** of the CSS console.</li></ul> |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for login. The code is `0` if login is successful.                                  |


### logout

This API is used to log out.

```objc
// Log out
/// - Parameter callback:  callback for logout. The code is `0` if logout is successful.
- (void)logout:(Callback _Nullable)callback
NS_SWIFT_NAME(logout(_:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | --------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for logout. The code is `0` if logout is successful. |


### setSelfProfile

This API is used to set the profile.

```objc
/// Set user profiles. The information will be stored in Tencent Cloud IM.
/// - Parameters:
///   - name: username
///   - avatarURL: profile picture URL
///   - callback: callback for setting user profiles. The code is `0` if the operation is successful.
- (void)setSelfProfileWithName:(NSString *)name
                     avatarURL:(NSString * _Nullable)avatarURL
                      callback:(Callback _Nullable)callback
NS_SWIFT_NAME(setSelfProfile(name:avatarURL:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ----------------------------------------- | ----------------------------------- |
| name      | String                                    | Username                              |
| avatarURL | String                                    | Profile picture URL                          |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for setting user profiles. The code is `0` if the operation is successful. |


## Room APIs

### createRoom

This API is used to create a room (called by anchor).

```objc
/// Create a room (called by anchor.) If the room does not exist, the system will create the room automatically.
/// The process of creating a room and starting live streaming as an anchor is as follows:
/// 1. A user calls `startCameraPreview()` to enable camera preview and set beauty filters.
/// 2. The user calls `createRoom()` to create a room, the result of which is returned via a callback.
/// 3. The user calls `starPublish()` to push streams.
/// - Parameters:
///   - roomID: room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a live room list. Currently, Tencent Cloud does not provide list management services. Please manage the list on your own.
///   - roomParam: room information, such as room name and cover information. If both the room list and room information are managed by yourself, you can ignore this parameter.
///   - callback: callback for room entry. The code is `0` if room entry is successful.
/// - Note:
///   - This API is called by an anchor to start live streaming. An anchor can create a room he or she created before.
- (void)createRoomWithRoomID:(UInt32)roomID
                   roomParam:(TRTCCreateRoomParam *)roomParam
                    callback:(Callback _Nullable)callback
NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ----------------------------------------- | ------------------------------------------------------------ |
| roomID | UInt32 | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a live room list. Currently, Tencent Cloud does not provide list management services. Please manage the list on your own. |
| roomParam | TRTCCreateRoomParam | Room information, such as room name and cover information. If both the room list and room information are managed by yourself, you can ignore this parameter. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room creation. The code is `0` if the operation is successful.  |

The process of creating a room and starting live streaming as an anchor is as follows: 

1. A user calls `startCameraPreview()` to enable camera preview and set beauty filters. 
2. The user calls `createRoom()` to create a room, the result of which is returned via a callback.
3. The user calls `starPublish()` to push streams.

### destroyRoom

This API is used to terminate a room (called by anchor).

```objc
/// Terminate a room (called by anchor)
/// After creating a room, an anchor can call this API to terminate it.
/// - parameter callback: callback for room termination. The code is `0` if the operation is successful.
/// - Note:
///   - After creating a room, an anchor can call this API to terminate it
- (void)destroyRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(destroyRoom(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room termination. The code is `0` if the operation is successful. |



### enterRoom

This API is used to enter a room (called by audience).

```objc
/// Enter a room (called by audience)
/// The process of entering a room and starting playback as audience is as follows:
/// 1. A user gets the latest room list from your server. The list may contain the `roomID` and other information of multiple rooms.
/// 2. The user selects a room and call `enterRoom()` to enter the room.
/// 3. If the room list managed by your server contains the `userID` of the anchor of each room, after entering the room, the user can call `startPlay(userID)` to play the anchor’s video.
/// If the room list contains `roomID` only, upon room entry, the user will receive the `onAnchorEnter(userID)` callback from `TRTCLiveRoomDelegate`.
/// The user can then call `startPlay(userID)`, passing in the `userID` obtained from the callback, to play the anchor’s video.
/// - Parameters:
///   - roomID: room ID
///   - useCDNFirst: whether to play streams via CDNs whenever possible
///   - cdnDomain: CDN domain name
///   - callback:  callback for room entry. The code is `0` if room entry is successful.
/// - Note:
///   - This API is called by audience to enter a room.
///   - An anchor cannot use this API to enter a room he or she created, but must use createRoom instead.
- (void)enterRoomWithRoomID:(UInt32)roomID
                useCDNFirst:(BOOL)useCDNFirst
                  cdnDomain:(NSString * _Nullable)cdnDomain
                   callback:(Callback)callback
NS_SWIFT_NAME(enterRoom(roomID:useCDNFirst:cdnDomain:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------------------------------- |
| roomID   | UInt32                                    | Room ID                            |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room entry. The code is `0` if the operation is successful. |



The process of entering a room and starting playback as audience is as follows: 

1. A user gets the latest room list from your server. The list may contain the `roomID` and other information of multiple rooms.
2. The user selects a room and calls `enterRoom()` to enter the room.
3. The user calls `startPlay(userID)`, passing in the anchor’s `userID` to start playback.
 - If the room list contains anchors’ `userID`, the user can call `startPlay(userID)` to start playback.
 - If the user does not have the anchor's `userID` before room entry, he or she can find it in the `onAnchorEnter(userID)` callback of `TRTCLiveRoomDelegate`, which is returned after room entry, and can then call `startPlay(userID)` to start playback. 



### exitRoom

This API is used to leave a room.

```objc
/// Leave a room (called by audience)
/// - Parameter callback: callback for room exit. The code is `0` if the operation is successful.
/// - Note:
///   - This API is called by audience to leave a room.
///   - An anchor cannot use this API to leave a room.

- (void)exitRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(exitRoom(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for room exit. The code is `0` if the operation is successful. |

### getRoomInfos

This API is used to get room list details, which are set by anchors via `roomInfo` when they call `createRoom()`.
>?You don’t need this API if both the room list and room information are managed on your server.

```objc
/// Get room details
/// The information is provided by anchors via the `roomInfo` parameter when they call `createRoom()`. You don’t need this API if both the room list and room information are managed by yourself.
/// - Parameter roomIDs: list of room IDs
/// - Parameter callback: callback of room details
- (void)getRoomInfosWithRoomIDs:(NSArray<NSNumber *> *)roomIDs
                       callback:(RoomInfoCallback _Nullable)callback
NS_SWIFT_NAME(getRoomInfos(roomIDs:callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ------------------ |
| roomIDs  | [UInt32]                                                       | List of room IDs       |
| callback | (_ code: Int, _ message: String?, _ roomList: [TRTCLiveRoomInfo]) -> Void | Callback of room details |



### getAnchorList

This API is used to get the anchors and co-anchoring viewers in a room. It takes effect only if it is called after `enterRoom()`.

```objc
/// Get the anchors and co-anchoring viewers in a room. This API takes effect only if it is called after `enterRoom()`.
/// - Parameter callback: callback of user details
- (void)getAnchorList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAnchorList(callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | Callback of user details |


### getAudienceList

This API is used to get the information of all audience in a room. It takes effect only if it is called after `enterRoom()`.

```objc
/// Get the information of all audience in a room. This API takes effect only if it is called after `enterRoom()`.
/// - Parameter callback: callback of user details
- (void)getAudienceList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAudienceList(callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | Callback of user details |


## Stream Pushing/Pulling APIs

### startCameraPreview

This API is used to enable local video preview.

```objc
/// Enable local video preview
/// - Parameters:
///   - frontCamera: `true`: front camera; `false`: rear camera
///   - view: the control that loads video images
///   - callback: callback for the operation
- (void)startCameraPreviewWithFrontCamera:(BOOL)frontCamera
                                     view:(UIView *)view
                                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startCameraPreview(frontCamera:view:callback:));

```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ----------------------------------------- | ------------------------------------- |
| frontCamera | Bool                                      | `true`: front camera; `false`: rear camera |
| view        | UIView                                    | The control that loads video images                  |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation                                  |


### stopCameraPreview

This API is used to stop local video capturing and preview.

```objc
/// Stop local video capturing and preview
- (void)stopCameraPreview;

```


### startPublish

This API is used to start live streaming (pushing streams), which can be called in the following scenarios:

- An anchor starts live streaming.
- A viewer starts co-anchoring.


```objc
/// Start live streaming (pushing streams). This API can be called in the following scenarios:
/// 1. An anchor starts live streaming.
/// 2. A viewer starts co-anchoring.
/// - Parameters:
///   - streamID: the `streamID` used to bind live streaming CDNs. You need to set it to the `streamID` of the anchor if you want audience to play the anchor’s stream via CDNs.
///   - callback: callback for the operation
- (void)startPublishWithStreamID:(NSString *)streamID
                        callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPublish(streamID:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| streamID | String | The `streamID` used to bind live streaming CDNs. You need to set it to the `streamID` of the anchor if you want audience to play the anchor’s stream via CDNs. |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation                                  |


### stopPublish

This API is used to stop live streaming (pushing streams), which can be called in the following scenarios:

- An anchor ends live streaming.
- A viewer ends co-anchoring.

```objc
/// Stop live streaming (pushing streams). This API can be called in the following scenarios:
/// 1. An anchor ends live streaming.
/// 2. A viewer ends co-anchoring.
/// - Parameter callback: callback for the operation
- (void)stopPublish:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPublish(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation |



### startPlay

This API is used to play a remote video. It can be called in common playback and co-anchoring scenarios.

```objc
/// Play a remote video. This API can be called in common playback and co-anchoring scenarios.
/// Common playback scenario
/// 1. If the room list managed by your server contains the `userID` of the anchor of each room, after entering a room, a user can call `startPlay(userID)` to play the anchor’s video.
/// 2. If the room list contains `roomID` only, upon room entry, a user will receive the `onAnchorEnter(userID)` callback from `TRTCLiveRoomDelegate`.
/// The user can then call `startPlay(userID)`, passing in the `userID` obtained from the callback, to play the anchor’s video.
/// Co-anchoring scenario
/// After co-anchoring starts, the anchor will receive the `onAnchorEnter(userID)` callback from `TRTCLiveRoomDelegate` and can call `startPlay(userID)`, passing in the `userID` obtained from the callback to play the co-anchoring user’s video.
/// - Parameters:
///   - userID: ID of the user whose video is to be played
///   - view: the control that loads video images
///   - callback: callback for the operation
- (void)startPlayWithUserID:(NSString *)userID
                       view:(UIView *)view
                   callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPlay(userID:view:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | -------------------------- |
| userID   | String                                    | ID of the user whose video is to be played        |
| view     | UIView                                    | The control that loads video images |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation                                  |


**Common playback scenario**

- If the room list contains anchors’ `userID`, after entering a room, a user can call `startPlay(userID)` to play the anchor's video.
- If a user does not have the anchor's `userID` before room entry, he or she can find it in the `onAnchorEnter(userID)` callback of `TRTCLiveRoomDelegate`, which is returned after room entry, and can then call `startPlay(userID)` to play the anchor’s video.

**Co-anchoring scenario**
After co-anchoring starts, the anchor will receive the `onAnchorEnter(userID)` callback from `TRTCLiveRoomDelegate` and can call `startPlay(userID), passing in the `userID` obtained from the callback to play the co-anchoring user’s video.



### stopPlay

This API is used to stop rendering a remote video. It needs to be called after the `onAnchorExit()` callback is received.

```objc
/// Stop rendering a remote video
/// - Parameters:
///   - userID: ID of the remote user
///   - callback: callback for the operation
/// - Note:
///   - Call this API after receiving the `onAnchorExit` callback.
- (void)stopPlayWithUserID:(NSString *)userID
                  callback:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPlay(userID:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ---------------- |
| userID   | String                                    | ID of the remote user |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation                                  |




## APIs for Anchor-Audience Co-anchoring

### requestJoinAnchor

This API is used to send a co-anchoring request (called by audience).

```objc
/// Send a co-anchoring request
/// - Parameters:
///   - reason: reason for co-anchoring
///   - responseCallback: callback of the response
/// - Note: After a viewer sends a co-anchoring request, the anchor will receive the `onRequestJoinAnchor` callback.
- (void)requestJoinAnchor:(NSString *)reason
                  timeout:(double)timeout
         responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestJoinAnchor(reason:timeout:responseCallback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------------------------------- | -------------- |
| reason   | String                                                       | Reason for co-anchoring       |
| timeout | long | Timeout period for the co-anchoring request |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | Callback of the anchor’s response |

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

```objc
/// Respond to a co-anchoring request
/// - Parameters:
///   - user: user ID of the viewer
///   - agree: `true`: accept; `false`: reject
///   - reason: reason for accepting/rejecting the request
/// - Note: After the anchor responds to the request, the viewer will receive the `responseCallback` passed in to `requestJoinAnchor`.
- (void)responseJoinAnchor:(NSString *)userID
                     agree:(BOOL)agree
                    reason:(NSString *)reason
NS_SWIFT_NAME(responseJoinAnchor(userID:agree:reason:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------- | ------------------------- |
| userID | String  | User ID of the viewer                  |
| agree | Bool | `true`: accept; `false`: reject |
| reason | String? | Reason for accepting/rejecting the request |


### kickoutJoinAnchor

This API is used to remove a user from co-anchoring (called by anchor). The removed user will receive the `onKickoutJoinAnchor()` callback of `TRTCLiveRoomDelegate`.

```objc
/// Remove a user from co-anchoring
/// - Parameters:
///   - userID: ID of the user to remove from co-anchoring
///   - callback: callback for the operation
/// - Note: After the anchor calls this API to remove a user from co-anchoring, the user will receive the `trtcLiveRoomOnKickoutJoinAnchor()` callback.
- (void)kickoutJoinAnchor:(NSString *)userID
                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(kickoutJoinAnchor(userID:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ------------- |
| userID   | String                                    | ID of the user to remove from co-anchoring |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation                                  |



## APIs for Cross-Room Anchor Competition

### requestRoomPK

This API is used to request cross-room competition (called by anchor).

```objc
/// Request cross-room competition
/// - Parameters:
///   - roomID: room ID of the anchor to invite
///   - userID: user ID of the anchor to invite
///   - responseCallback: callback of the response
/// - Note: After a cross-room competition request is sent, the invited anchor will receive the `onRequestRoomPK` callback.
- (void)requestRoomPKWithRoomID:(UInt32)roomID
                         userID:(NSString *)userID
               responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestRoomPK(roomID:userID:responseCallback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------------------------------- | ------------------------ |
| roomID           | UInt32                                      | room ID of the anchor to invite          |
| userID           | String                                      | user ID of the anchor to invite          |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | Callback of the response |

Anchors in different rooms can compete with each other. The process of starting cross-room competition between anchor A and anchor B is as follows:

1. **Anchor A** calls `requestRoomPK()` to send a co-anchoring request to anchor B.
2. **Anchor B** receives the `onRequestRoomPK()` callback of `TRTCLiveRoomDelegate`.
3. **Anchor B** calls `responseRoomPK()` to respond to the competition request.
4. If **anchor B** accepts the request, he or she would wait for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and call `startPlay()` to play anchor A's video.
5. **Anchor A** receives the `responseCallback` callback, which carries anchor B’s response.
6. If the request is accepted, **anchor A** waits for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and calls `startPlay()` to play anchor B’s video.


### responseRoomPK

This API is used to respond to a cross-room competition request (called by anchor), after which the request sending anchor will receive the `responseCallback` passed in to `requestRoomPK`.

```objc
/// Respond to a cross-room competition request
/// Respond to a competition request from another anchor
/// - Parameters:
///   - user: user ID of the request sending anchor
///   - agree: `true`: accept; `false`: reject
///   - reason: reason for accepting/rejecting the request
/// - Note: After the anchor responds to the request, the request sending anchor will receive the `responseCallback` passed in to `requestRoomPK`.
- (void)responseRoomPKWithUserID:(NSString *)userID
                           agree:(BOOL)agree
                          reason:(NSString *)reason
NS_SWIFT_NAME(responseRoomPK(userID:agree:reason:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------- | ------------------------- |
| userID | String  | User ID of the request sending anchor   |
| agree | Bool | `true`: accept; `false`: reject |
| reason | String? | Reason for accepting/rejecting the request |


### quitRoomPK

This API is used to quit cross-room competition. If either anchor quits cross-room competition, the other anchor will receive the `trtcLiveRoomOnQuitRoomPK()` callback of `TRTCLiveRoomDelegate`.

```objc
/// Quit cross-room competition
/// - Parameter callback: callback for quitting cross-room competition
// - Note: If either anchor quits cross-room competition, the other anchor will receive the `trtcLiveRoomOnQuitRoomPK` callback.
- (void)quitRoomPK:(Callback _Nullable)callback
NS_SWIFT_NAME(quitRoomPK(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for the operation |


## Audio/Video APIs

### switchCamera

This API is used to switch between the front and rear cameras.

```objc
/// Switch between the front and rear cameras
- (void)switchCamera;
```


### setMirror

This API is used to set the mirror mode.

```objc
/// Specify whether to mirror video
/// - Parameter isMirror: enable/disable mirroring
- (void)setMirror:(BOOL)isMirror
NS_SWIFT_NAME(setMirror(isMirror:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | ---- | --------------- |
| isMirror | Bool | Enable/Disable mirroring |


### muteLocalAudio

This API is used to mute or unmute the local user.

```objc
/// Mute or unmute the local user
/// - Parameter isMuted: `true`: mute; `false`: unmute
- (void)muteLocalAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteLocalAudio(isMuted:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | `true`: mute; `false`: unmute |

### muteRemoteAudio

This API is used to mute or unmute a remote user.

```objc
/// Mute or unmute a remote user
/// - Parameters:
///   - userID: ID of the remote user
///   - isMuted: `true`: mute; `false`: unmute
- (void)muteRemoteAudioWithUserID:(NSString *)userID isMuted:(BOOL)isMuted
NS_SWIFT_NAME(muteRemoteAudio(userID:isMuted:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | --------------------------------- |
| userID | String | ID of the remote user |
| isMuted | Bool | `true`: mute; `false`: unmute |



### muteAllRemoteAudio

This API is used to mute or unmute all remote users.

```objc
/// Mute or unmute all remote users
/// - Parameter isMuted: `true`: mute; `false`: unmute
- (void)muteAllRemoteAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteAllRemoteAudio(_:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | `true`: mute; `false`: unmute |

### setAudioQuality

This API is used to set audio quality.

```objc
/// Set audio quality. Valid values: `1` (low), `2` (average), `3` (high)
/// - Parameter quality: audio quality
- (void)setAudioQuality:(NSInteger)quality
NS_SWIFT_NAME(setAudioiQuality(quality:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | --------- | ---------------------------- |
| quality | NSInteger | `1`: speech; `2`: standard; `3`: music |

## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66).

```objc
/// Get the audio effect management object
- (TXAudioEffectManager *)getAudioEffectManager;
```

## Beauty Filter APIs

### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager).

```objc
/* Get the beauty filter management object TXBeautyManager
*
* You can do the following using TXBeautyManager:
* - Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
* - Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
* - Apply animated effects such as face widgets (materials).
* - Add makeup effects.
* - Recognize gestures.
*/
- (TXBeautyManager *)getBeautyManager;
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

```objc
/// Send a text message that can be seen by all users in a room
/// - Parameters:
///   - message: text message
///   - callback: callback for message sending
- (void)sendRoomTextMsg:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------------------------------- | -------------- |
| message | String | Text message |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for message sending |


### sendRoomCustomMsg

This API is used to send a custom text message.

```objc
/// Send a custom message
/// - Parameters:
///   - command: custom command word used to distinguish between different message types
///   - message: text message
///   - callback: callback for message sending
- (void)sendRoomCustomMsgWithCommand:(NSString *)command message:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomCustomMsg(command:message:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ----------------------------------------- | -------------------------------------------------- |
| command  | String                                                       | Custom command word used to distinguish between different message types |
| message  | String                                                       | Custom text message    |
| callback | (_ code: Int, _ message: String?) -> Void | Callback for message sending  |


## Debugging APIs

### showVideoDebugLog

This API is used to specify whether to display debugging information on the UI.

```objc
/// Specify whether to display debugging information on the UI
/// - Parameter isShow: show/hide debugging information
- (void)showVideoDebugLog:(BOOL)isShow
NS_SWIFT_NAME(showVideoDebugLog(_:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---- | -------------------------- |
| isShow | Bool | Show/Hide debugging information |


## `TRTCLiveRoomDelegate` Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
             onError:(NSInteger)code
             message:(NSString  *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onError:message:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| code         | Int              | Error code                     |
| message      | String?          | Error message                   |


### onWarning

Callback for warning.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
           onWarning:(NSInteger)code
             message:(NSString *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onWarning:message:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| code         | Int              | TRTCWarningCode     |
| message      | String?          | Warning message                   |



### onDebugLog

Callback for log.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
          onDebugLog:(NSString *)log
NS_SWIFT_NAME(trtcLiveRoom(_:onDebugLog:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| log          | String           | Log information                   |


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. All users in a room will receive this callback after the anchor leaves the room.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onRoomDestroy:(NSString *)roomID
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomDestroy:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| roomID       | String           | room ID                    |


### onRoomInfoChange

Callback for change of room information. This callback is usually used to notify users of room status change in co-anchoring and anchor competition scenarios.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
    onRoomInfoChange:(TRTCLiveRoomInfo *)info
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomInfoChange:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| info         | TRTCLiveRoomInfo | room information                   |




## Callback APIs for Entry/Exit of Anchors/Audience

### onAnchorEnter

Callback for a new anchor/co-anchoring viewer. Audience will receive this callback when there is a new anchor/co-anchoring viewer in the room and can call `startPlay()` of `TRTCLiveRoom` to play the video of the anchor/co-anchoring viewer.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onAnchorEnter:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorEnter:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| userID       | String           | User ID of the new anchor/co-anchoring viewer              |



### onAnchorExit

Callback for the quitting of an anchor/co-anchoring viewer. The anchors and co-anchoring viewers in a room will receive this callback after an anchor/co-anchoring viewer quits competition/co-anchoring and can call `stopPlay()` of `TRTCLiveRoom` to stop playing the video of the anchor/co-anchoring viewer.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
        onAnchorExit:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorExit:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| userID       | String           | User ID of the anchor/co-anchoring viewer                |



### onAudienceEnter

Callback for room entry by a viewer.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onAudienceEnter:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceEnter:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| user         | TRTCLiveUserInfo | Information of the user who entered the room               |


### onAudienceExit

Callback for room exit by a viewer.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
      onAudienceExit:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceExit:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| user         | TRTCLiveUserInfo | Information of the user who left the room               |


## Callback APIs Audience-Anchor Co-anchoring Events

### onRequestJoinAnchor

Callback for receiving a co-anchoring request from a viewer.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
 onRequestJoinAnchor:(TRTCLiveUserInfo *)user
             reason:(NSString * _Nullable)reason
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestJoinAnchor:reason:timeout:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| user         | TRTCLiveUserInfo | Information of the user who requested co-anchoring           |
| reason       | String?          | Reason for co-anchoring               |
| timeout      | Double           | Timeout period for response from the anchor         |


### onKickoutJoinAnchor

Callback for being removed from co-anchoring. After receiving this callback, a co-anchoring viewer needs to call `stopPublish()` of `TRTCLiveRoom` to quit co-anchoring.

```objc
- (void)trtcLiveRoomOnKickoutJoinAnchor:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnKickoutJoinAnchor(_:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |



## Callback APIs for Anchor Competition Events

### onRequestRoomPK

Callback for receiving a cross-room competition request. If an anchor accepts the request, he or she should wait for the `onAnchorEnter()` callback of `TRTCLiveRoomDelegate` and call `startPlay()` to play the other anchor’s video.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onRequestRoomPK:(TRTCLiveUserInfo *)user
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestRoomPK:timeout:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| user         | TRTCLiveUserInfo | Information of the anchor who requested competition     |
| timeout      | Double           | Timeout period for response from the anchor         |


### onQuitRoomPK

Callback for ending cross-room competition.

```objc
 - (void)trtcLiveRoomOnQuitRoomPK:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnQuitRoomPK(_:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |



## Message Event Callback APIs

### onRecvRoomTextMsg

Callback for receiving a text message.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
   onRecvRoomTextMsg:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomTextMsg:fromUser:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| message      | String           | Text message                   |
| user         | TRTCLiveUserInfo | Information of the sender             |



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

| Parameter    | Type   | Description                                                                                                                    |
| ------------ | ---------------- | -------------------------------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | Current `TRTCLiveRoom` component instance |
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| user         | TRTCLiveUserInfo | Information of the sender                                   |
