__Feature__

MLVB mic connect live room

>! The backend API supports up to 100 concurrent requests per second. If you need higher concurrency capability, please [contact us](https://intl.cloud.tencent.com/contact-us) for processing in advance.

__Introduction__

Based on Tencent Cloud's PaaS services Cloud Streaming Services (CSS), Video on Demand (VOD), and Instant Messaging (IM), MLVBLiveRoom provides the following features:

- A host can create a live room to start live streaming, and viewers can enter the room to watch the stream.
- The host and viewers can interact with each other through video mic connect.
- Hosts in two rooms can compete and interact with each other through mic connect.
- Each live room has a chat room that supports an unlimited number of members. In chat rooms, users can send various text and custom messages. Custom messages can be used to send on-screen comments, give likes, and give gifts.


MLVBLiveRoom is an open-source class depending on two closed-source Tencent Cloud SDKs:

- LiteAVSDK: the TXLivePush and TXLivePlayer components of the LiteAVSDK are used for publishing and playback respectively.
- IM SDK: the `AVChatRoom` feature of the IM SDK is used to implement chat rooms during live streaming. In addition, the mic connect processes between different hosts are implemented through IM messages.




## Basic SDK APIs

### delegate

This API is used to get the event callbacks of MLVBLiveRoom. You can use `MLVBLiveRoomDelegate` to get various status notifications of MLVBLiveRoom.

```
@property (nonatomic, weak) id< MLVBLiveRoomDelegate > delegate
```

>?The SDK uses the main queue for callback by default. To customize a callback thread, use `delegateQueue`.

***

### delegateQueue

This API is used to set the GCD queue that drives the callback function.

```
@property (nonatomic, copy) dispatch_queue_t delegateQueue
```

***

### sharedInstance

This API is used to get MLVBLiveRoom singleton objects.

```
+ (instancetype)sharedInstance
```

__Response__

MLVBLiveRoom instance

>?You can call `destroySharedInstance` of the MLVBLiveRoom to terminate singleton objects.

***

### destorySharedInstance

This API is used to terminate MLVBLiveRoom singleton objects.

```
+ (void)destorySharedInstance
```

>?After the instance is terminated, the externally cached MLVBLiveRoom instance cannot be used, and you need to call sharedInstance again to get a new instance.

***

### loginWithInfo

This API is used for login.

```
- (void)loginWithInfo:(MLVBLoginInfo *)loginInfo completion:(void(^)(int errCode, NSString *errMsg))completion 
```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------- |
| loginInfo  | MLVBLoginInfo *                        | Login information     |
| completion | void(^)(int errCode, NSString *errMsg) | Login result callback |

***

### logout

This API is used for logout.

```
- (void)logout
```

***

### setSelfProfile

This API is used to modify profile.

```
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL completion:(void(^)(int code, NSString *msg))completion 
```

__Parameters__

| Parameter | Type | Description |
| --------- | ---------- | ---------- |
| userName  | NSString * | Nickname     |
| avatarURL | NSString * | Profile photo address |

***


## Room APIs

### getRoomList

This API is used to get a room list.

```
- (void)getRoomList:(int)index count:(int)count completion:(void(^)(int errCode, NSString *errMsg, NSArray< MLVBRoomInfo * > *roomInfoArray))completion 
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---------- | ------------------------------------------------------------ | --------------------------- |
| index      | int                                                          | Room index starting value, which is 0 |
| count      | int                                                          | Number of rooms to be returned    |
| completion | void(^)(int errCode, NSString *errMsg, NSArray< MLVBRoomInfo * > *roomInfoArray) | Callback of the result of getting the room list    |

__Introduction__

This API supports room list pagination. You can use the `index` and `count` parameters to specify the room list pagination logic:

- index = 0 & count = 10: to obtain the 10 rooms on the first page
- index = 11 & count = 10: to obtain the 10 rooms on the second page

***

### getAudienceList

This API is used to get the list of viewers in a room.

```
- (void)getAudienceList:(NSString *)roomID completion:(void(^)(int errCode, NSString *errMsg, NSArray< MLVBAudienceInfo * > *audienceInfoArray))completion 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---------- | ------------------------------------------------------------ | ------------------------ |
| roomID     | NSString *                                                   | Room ID               |
| completion | void(^)(int errCode, NSString *errMsg, NSArray< MLVBAudienceInfo * > *audienceInfoArray) | Callback of the result of getting the viewer list |

__Introduction__

When viewers enter a room, the backend adds their information to the viewer list of the room. You can call this API to get the viewer list.

>?A viewer list can contain up to 30 viewers. This list length is sufficient for common UI display. A longer list not only wastes storage space but also slows down the return of the list.

***

### createRoom

This API is used to create a room (called by a host).

```
- (void)createRoom:(NSString *)roomID roomInfo:(NSString *)roomInfo completion:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---------- | -------------------------------------- | ------------------------------------------------------------ |
| roomID     | NSString *                             | Room ID. It is recommended that you use the user IDs of hosts as room IDs, eliminating the need for mapping on the backend. This parameter can be left empty, and in that case, the backend will generate a room ID instead. |
| roomInfo   | NSString *                             | Room information, for example, the room name. This parameter is optional and can be in JSON format. |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the room creation result                                         |

__Introduction__

Generally, a host can start live streaming in the following call process: 

1. The host calls `startLocalPreview` to enable camera preview, during which the host can adjust beauty filter parameters. 
2. The host calls `createRoom` to create a live room. Regardless of whether the room is created successfully, the result will be notified to the host through `completion`.

***

### enterRoom

This API is used to enter a room (called by a viewer).

```
- (void)enterRoom:(NSString *)roomID view:(UIView *)view completion:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------------- |
| roomID     | NSString *                                                   | Room ID               |
| view       | UIView *                               | Control that carries the video image |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the room entry result  |

__Introduction__

The general process for a viewer to watch a live stream is as follows: 

1. The viewer calls `getRoomList` to refresh the latest live room list and gets the room list through `completion`. 
2. The viewer selects a live room and calls `enterRoom` to enter the live room.

***

### exitRoom

This API is used to exit a room.

```
- (void)exitRoom:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------------- |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the room exit result  |

***

### setCustomInfo

This API is used to set extended fields for the current room.

```
- (void)setCustomInfo:(MLVBCustomFieldOp)op key:(NSString *)key value:(id)value completion:(void(^)(int errCode, NSString *custom))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | ----------------------------------- |
| op         | MLVBCustomFieldOp                      | Operation                          |
| key        | NSString *                             | Custom key                          |
| value      | id                                     | The value can be of the NSNumber or NSString type. |
| completion | void(^)(int errCode, NSString *custom) | Callback of operation completion                    |

__Introduction__

MLVB provides the following operation APIs for users to set extended fields such as **number of likes** and **whether mic connect is in process** as required:

- SET: set. `value` can be an integer or a string. This API is suitable for extended fields such as **whether mic connect is in process**.
- INC: increase. `value` must be an integer. This API is suitable for extended fields such as **number of likes** and **popularity**.
- DEC: decrease. `value` must be an integer. This API is suitable for extended fields such as **number of likes** and **popularity**.

>?When `op` is `MLVBCustomFieldOpInc` or `MLVBCustomFieldOpDec`, `value` must be an integer.

***

### getCustomInfo

This API is used to get the extended fields of the current room.

```
- (void)getCustomInfo:(void(^)(int errCode, NSString *errMsg, NSDictionary *customInfo))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ------------------------------------------------------------ | ------------------ |
| completion | void(^)(int errCode, NSString *errMsg, NSDictionary *customInfo) | Callback of the result of getting extended field values |

***


## Mic Connect Between a Host and a Viewer

### requestJoinAnchor

This API is used by a viewer to request mic connect.

```
- (void)requestJoinAnchor:(NSString *)reason completion:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------- |
| reason     | NSString *                             | Reason for mic connect     |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the host response |

__Introduction__

The mic connect process between a host and a viewer is as follows:

1. The viewer calls `requestJoinAnchor` to send a mic connect request to the host.
2. The host receives the `MLVBLiveRoomDelegate onRequestJoinAnchor` callback notification.
3. The host calls `responseJoinAnchor` to specify whether to accept the mic connect request from the viewer.
4. The viewer receives a callback notification passed in by `requestJoinAnchor` and gets to know whether the request is accepted.
5. If the request is accepted, the viewer calls `startLocalPreview` to enable the local camera. If the application has not obtained the camera and microphone permissions, a permission prompt will be displayed on the UI.
6. The viewer calls `joinAnchor` to officially enter the mic connect status.
7. Once the viewer enters the mic connect status, the host receives the `MLVBLiveRoomDelegate onAnchorEnter` callback notification.
8. The host calls `startRemoteView` to view the video image of the mic connect viewer.
9. If there are other mic connect viewers in the live room of the host, the new mic connect viewer will receive the `MLVBLiveRoomDelegate onAnchorJoin` callback notification and can call `startRemoteView` to display the video images of the other mic connect viewers.

***

### responseJoinAnchor

This API is used by a host to process mic connect requests.

```
- (void)responseJoinAnchor:(NSString *)userID agree:(BOOL)agree reason:(NSString *)reason 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ---------- | ------------------------- |
| userID | NSString * | Viewer ID                 |
| agree  | BOOL       | `YES`: accept; `NO`: reject     |
| reason | NSString * | Reason for accepting or rejecting a mic connect request |

__Introduction__

After receiving the `MLVBLiveRoomDelegate onRequestJoinAnchor` callback notification, a host needs to call this API to process the mic connect request of the viewer.

***

### joinAnchor

This API is used by a viewer to enter the mic connect status.

```
- (void)joinAnchor:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------------- |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the result of entering the mic connect status |

__Introduction__

Once a viewer enters the mic connect status, the host and other mic connect viewers in the host's live room will receive the `MLVBLiveRoomDelegate onAnchorEnter` callback notification.

***

### quitJoinAnchor

This API is used by a viewer to exit mic connect.

```
- (void)quitJoinAnchor:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------------- |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the result of exiting mic connect |

__Introduction__

Once a viewer exits mic connect, the host and other mic connect viewers in the host's live room will receive the `MLVBLiveRoomDelegate onAnchorExit` callback notification.

***

### kickoutJoinAnchor

This API is used by a host to kick out a mic connect viewer.

```
- (void)kickoutJoinAnchor:(NSString *)userID 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ---------- | --------------- |
| userID | NSString * | ID of the mic connect viewer |

__Introduction__

After a host calls this API to kick out a mic connect viewer, the kicked out viewer will receive the `MLVBLiveRoomDelegate onKickoutJoinAnchor` callback notification.

***


## Cross-Room Host Competition

### requestRoomPK

This API is used by a host to request for cross-room competition.

```
- (void)requestRoomPK:(NSString *)userID completion:(void(^)(int errCode, NSString *errMsg, NSString *streamUrl))completion 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---------- | ----------------------------------------------------------- | ------------------------ |
| userID     | NSString *                                                  | ID of the invited host          |
| completion | void(^)(int errCode, NSString *errMsg, NSString *streamUrl) | Callback of the result of the cross-room host competition request |

__Introduction__

Hosts in different rooms can compete with each other. The process for host A and host B to start cross-room competition during live streaming is as follows:

1. Host A calls `requestRoomPK` to send a competition request to host B.
2. Host B receives the `MLVBLiveRoomDelegate onRequestRoomPK` callback notification.
3. Host B calls `responseRoomPK` to specify whether to accept the competition request from host A.
4. If host B accepts the request of host A, host B calls `startRemoteView ` to display the video image of host A.
5. Host A receives the `completion` callback notification and gets to know whether the request is accepted by host B.
6. If the request of host A is accepted, host A calls `startRemoteView` to display the video image of host B.

***

### responseRoomPK

This API is used by a host to respond to a cross-room competition request.

```
- (void)responseRoomPK:(MLVBAnchorInfo *)anchor agree:(BOOL)agree reason:(NSString *)reason 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ---------------- | -------------------------- |
| anchor | MLVBAnchorInfo * | ID of the host who initiates the competition request       |
| agree  | BOOL       | `YES`: agree; `NO`: reject     |
| reason | NSString *       | Reason for accepting or rejecting the competition request |

__Introduction__

Once the invited host responds to the cross-room competition request, the inviting host will receive the `MLVBLiveRoomDelegate onRequestRoomPK` callback notification.

***

### quitRoomPK

This API is used to exit cross-room competition.

```
- (void)quitRoomPK:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | ------------------------ |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the result of exiting cross-room competition |

__Introduction__

If either host exits cross-room competition, the other host will receive the `MLVBLiveRoomDelegate onQuitRoomPK` callback notification.

***


## Video APIs

### startLocalPreview

This API is used to enable the preview image of the local video.

```
- (void)startLocalPreview:(BOOL)frontCamera view:(UIView *)view 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ----------- | -------- | --------------------------------- |
| frontCamera | BOOL | `YES`: front camera; `NO`: rear camera |
| view    | UIView * | Control that carries the video image                  |

***

### stopLocalPreview

This API is used to stop local video capturing and preview.

```
- (void)stopLocalPreview

```

***

### startRemoteView

This API is used to start rendering remote video images.

```
- (void)startRemoteView:(MLVBAnchorInfo *)anchorInfo view:(UIView *)view onPlayBegin:(IPlayBegin)onPlayBegin onPlayError:(IPlayError)onPlayError playEvent:(IPlayEventBlock)onPlayEvent 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ---------------- | -------------------- |
| anchorInfo  | MLVBAnchorInfo * | Information of the remote user     |
| view        | UIView *         | Control that carries the video image |
| onPlayBegin | IPlayBegin       | Callback of player start     |
| onPlayError | IPlayError       | Callback of a playback error       |
| onPlayEvent | IPlayEventBlock  | Callback of other playback events   |

>?Call this API upon `onUserVideoAvailable` callback.

***

### stopRemoteView

This API is used to stop rendering remote video images.

```
- (void)stopRemoteView:(MLVBAnchorInfo *)anchor 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ---------------- | ------------ |
| anchor | MLVBAnchorInfo * | Information of the remote user |

***

### setMirror

This API is used to set the mirror effect on the viewer side.

```
- (void)setMirror:(BOOL)isMirror 

```

__Parameters__

| Parameter | Type | Description |
| -------- | ---- | ----------------------------------------------------------- |
| isMirror | BOOL | `YES`: mirrored images are displayed on the player side. `NO`: non-mirrored images are displayed on the player side. |

__Introduction__

Since the front camera captures images from the viewing angle of the phone, there is no problem in showing the captured images directly to viewers. However, if the captured images are displayed directly to the host as well, the host will have the weird experience totally opposite to that when the host is looking in the mirror. Therefore, the SDK enables the mirror effect for the preview image of the local camera by default so that the host will feel like looking in the mirror during live streaming.
The `setMirror` API affects only the mirror effect on the viewer side. To enable the images seen at the viewer side to be consistent with those at the host side, enable the mirror effect. To enable the viewer side to see normal, unprocessed images (for example, when the host plays guitar), disable the mirror effect.

>?The `setMirror` API is available only when the front camera is used. **The API is unavailable when the rear camera is used.**

***


## Audio APIs

### muteLocalAudio

This API is used to specify whether to mute local audio.

```
- (void)muteLocalAudio:(BOOL)mute 

```

__Parameters__

| Parameter | Type | Description |
| ---- | ---- | --------------------- |
| mute | BOOL | `YES`: mute; `NO`: unmute |

***

### muteRemoteAudio

This API is used to specify whether to mute a specified user.

```
- (void)muteRemoteAudio:(NSString *)userID mute:(BOOL)mute 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ---------- | ----------------------- |
| userID | NSString * | ID of the specified user |
| mute | BOOL | `YES`: mute; `NO`: unmute |

***

### muteAllRemoteAudio

This API is used to specify whether to mute all remote users.

```
- (void)muteAllRemoteAudio:(BOOL)mute 

```

__Parameters__

| Parameter | Type | Description |
| ---- | ---- | ----------------------- |
| mute | BOOL | `YES`: mute; `NO`: unmute |

***


## Camera APIs

### switchCamera

This API is used to switch between the front and rear cameras.

```
- (void)switchCamera

```

***

### setCameraMuteImage

This API is used to set the picture to display when the host blocks the camera.

```
- (void)setCameraMuteImage:(UIImage *)image 

```

__Parameters__

| Parameter | Type | Description |
| ----- | --------- | ---------- |
| image | UIImage * | Picture |

__Introduction__

When the host blocks the camera, or the camera cannot be used because the application is switched to the background, we need to display a picture to viewers saying like "the host has left temporarily and will come back soon".

***

### setZoom

This API is used to adjust the focal length.

```
- (void)setZoom:(CGFloat)distance 

```

__Parameters__

| Parameter | Type | Description |
| -------- | ------- | --------------------------- |
| distance | CGFloat | Focal length. Value range: 1-5. |

>?The value `1` indicates the furthest view (normal lens), and `5` indicates the nearest view (enlarging lens). The maximum value is recommended to be `5`. If the maximum value is greater than 5, the video image will become blurry.

***

### enableTorch

This API is used to enable or disable flashlight.

```
- (BOOL)enableTorch:(BOOL)bEnable 

```

__Parameters__

| Parameter | Type | Description |
| ------- | ---- | --------------------- |
| bEnable | BOOL | `YES`: enable; `NO`: disable |

__Response__

`YES`: successful; `NO`: failed

***

### setFocusPosition

This API is used to set the manual focus area.

```
- (void)setFocusPosition:(CGPoint)touchPoint 

```

__Introduction__

The SDK uses the auto focus feature of the camera by default. You can also use the `touchFocus` option of TXLivePushConfig to disable the auto focus feature and enable manual focus. After manual focus is enabled, the host needs to tap a certain area on the camera preview image to manually adjust the camera focus.

***


## Beauty Filter APIs

### getBeautyManager

This API is used to get the beauty filter management object TXBeautyManager.

```
- (TXBeautyManager *)getBeautyManager 

```

>With TXBeautyManager, you can use the following features:
>
>- Set beauty effects such as the beauty filter style, skin whitening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening or shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
>- Adjust the hairline, eye spacing, eye corners, mouth shape, nose wings, nose position, lip thickness, and face shape.
>- Set animated effects such as face widgets (materials).
>- Add makeup effects.
>- Recognize gestures.

***

### setFilter

This API is used to specify the material filter effect.

```
- (void)setFilter:(UIImage *)image 

```

__Parameters__

| Parameter | Type | Description |
| ----- | --------- | ---------------------------- |
| image | UIImage * | Specified material, which is an image from the color lookup table |

>?The filter material must be in PNG format. The JPG format is not allowed. Note: you need to use Photoshop to change the format of a picture because in Windows, changing the file name extension does not change the format of the picture.

***

### setSpecialRatio

This API is used to set the strength of a filter.

```
- (void)setSpecialRatio:(float)specialValue 

```

__Parameters__

| Parameter | Type | Description |
| ------------ | ----- | ----------------------------------------- |
| specialValue | float | Value range: 0-1. The larger the value, the more obvious the effect. Default value: `0.5` |

***

### setGreenScreenFile

This API is used to set the green screen effect for videos. It works only in the Enterprise Edition.

```
- (void)setGreenScreenFile:(NSURL *)file 

```

__Parameters__

| Parameter | Type | Description |
| ---- | ------- | ------------------------------------------ |
| file | NSURL * | Path to the video file, which can be in MP4 format. nil: disable the effect. |

>?The green screen feature here is not intelligent keying. It requires that a green screen exists behind the recorded person or object for further chroma keying.

***

## Message Sending APIs

### sendRoomTextMsg

This API is used to send text messages.

```
- (void)sendRoomTextMsg:(NSString *)message completion:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | -------------------------------------- | -------------- |
| message    | NSString *                             | Text message     |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the message sending result |

***

### sendRoomCustomMsg

This API is used to send custom text messages.

```
- (void)sendRoomCustomMsg:(NSString *)cmd msg:(NSString *)message completion:(void(^)(int errCode, NSString *errMsg))completion 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---------- | -------------------------------------- | -------------------------------------------------- |
| cmd        | NSString *                             | Custom command word used to distinguish between different message types |
| message    | NSString *                             | Text message                                         |
| completion | void(^)(int errCode, NSString *errMsg) | Callback of the message sending result                                     |

***


## Background Music Mixing APIs

### playBGM

This API is used to play background music.

```
- (BOOL)playBGM:(NSString *)path 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---------- | ------------------------------------------------------------ |
| path | NSString * | Path to the music file. The path must be under the `document` directory corresponding to `app`. Otherwise, reading the file will fail. |

__Response__

`YES`: successful; `NO`: failed

***

### playBGM

This API is used to play background music. (This is an advanced API.)

```
- (BOOL)playBGM:(NSString *)path withBeginNotify:(void(^)(NSInteger errCode))beginNotify withProgressNotify:(void(^)(NSInteger progressMS, NSInteger durationMS))progressNotify andCompleteNotify:(void(^)(NSInteger errCode))completeNotify 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| path           | NSString *                                          | Path to the music file. The path must be under the `document` directory corresponding to `app`. Otherwise, reading the file will fail. |
| beginNotify    | void(^)(NSInteger errCode)                          | Callback notification of the start of music playback                                     |
| progressNotify | void(^)(NSInteger progressMS, NSInteger durationMS) | Notification of the progress of music playback, in milliseconds |
| completeNotify | void(^)(NSInteger errCode)                          | Callback notification of the stop of music playback                                      |

__Response__

`YES`: successful; `NO`: failed

***

### stopBGM

This API is used to stop background music playback.

```
- (BOOL)stopBGM

```

***

### pauseBGM

This API is used to pause background music playback.

```
- (BOOL)pauseBGM

```

***

### resumeBGM

This API is used to resume background music playback.

```
- (BOOL)resumeBGM

```

***

### getMusicDuration

This API is used to get the total length of the background music file, in milliseconds.

```
- (int)getMusicDuration:(NSString *)path 

```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---------- | ------------------------------------------------------------ |
| path | NSString * | Path to the music file. If `path` is `nil`, the length of the music file being played back will be returned. |

__Response__

If this API is successfully called, the length of the music file will be returned, in milliseconds. Otherwise, `-1` will be returned.

***

### setMicVolume

This API is used to set the microphone volume when background music is being played.

```
- (BOOL)setMicVolume:(float)volume 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ----- | --------------------------------------------- |
| volume | float | Volume. `1.0` indicates a normal volume. Recommended value range: 0.0-2.0. |

***

### setBGMVolume

This API is used to set the background music volume when background music is being played.

```
- (BOOL)setBGMVolume:(float)volume 

```

__Parameters__

| Parameter | Type | Description |
| ------ | ----- | -------------------------------------------- |
| volume | float | Volume. 1.0 indicates a normal volume. Recommended value range: 0.0-2.0. |

***

### setBGMPitch

This API is used to adjust the pitch of background music.

```
- (BOOL)setBGMPitch:(float)pitch 

```

__Parameters__

| Parameter | Type | Description |
| ----- | ----- | ---------------------------------------------- |
| pitch | float | Pitch. Default value: 0.0f. Value range: -1 to 1. |

__Response__

`YES`: successful; `NO`: failed

***

### setReverbType

This API is used to set the reverb effect.

```
- (BOOL)setReverbType:(TXReverbType)reverbType 

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ------------ | ---------------------------------------------------------- |
| reverbType | TXReverbType | Reverb type. For more information, please see the definition of `TXReverbType` in `TXLiveSDKTypeDef.h`. |

__Response__

`YES`: successful; `NO`: failed

***

### setVoiceChangerType

This API is used to set the voice changing type.

```
- (BOOL)setVoiceChangerType:(TXVoiceChangerType)voiceChangerType 
```

__Parameters__

| Parameter | Type | Description |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| voiceChangerType | TXVoiceChangerType | Voice changing type. For more information, please see the definition of `voiceChangerType` in `TXLiveSDKTypeDef.h`. |

__Response__

`YES`: successful; `NO`: failed

***


## Debugging APIs

### showVideoDebugLog

This API is used to specify whether to display a floating view to show playback or publishing status statistics and event messages over the rendering view.

```
- (void)showVideoDebugLog:(BOOL)isShow 
```

***

