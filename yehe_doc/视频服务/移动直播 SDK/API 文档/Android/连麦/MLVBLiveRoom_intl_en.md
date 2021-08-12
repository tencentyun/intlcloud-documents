__Feature__

MLVB mic connect live room

>! The backend API supports up to 100 concurrent requests per second. If you need higher concurrency capability, please [contact us](https://intl.cloud.tencent.com/contact-us) for processing in advance.

__Introduction__
    
Based on Tencent Cloud's PaaS services Live Video Broadcast (LVB), Video on Demand (VOD), and Instant Messaging (IM), MLVBLiveRoom provides the following features:

- A host can create a live room to start live streaming, and viewers can enter the room to watch the stream.
- Hosts and viewers can interact with each other through video mic connect.
- Hosts in two rooms can compete and interact with each other through mic connect.
- Each live room has a chat room that supports an unlimited number of members. In chat rooms, users can send various text and custom messages. Custom messages can be used to send on-screen comments, give likes, and give gifts.


MLVBLiveRoom is an open-source class depending on two closed-source Tencent Cloud SDKs:

- LiteAVSDK: the TXLivePusher and TXLivePlayer components of the LiteAVSDK are used for publishing and playback respectively.
- IM SDK: the `AVChatRoom` feature of the IM SDK is used to implement chat rooms during live streaming. In addition, the mic connect processes between different hosts are implemented through IM messages.



## Basic SDK APIs

### sharedInstance

This API is used to get [MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41673) singleton objects.

```
MLVBLiveRoom sharedInstance(Context context)
```

__Parameters__

| Parameter | Type | Description |
| ------- | ------- | ------------------------------------------------------------ |
| context | Context | Android context, which will be converted to `ApplicationContext` for the system APIs to call. |

__Response__

[MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41673) instance

>?You can call [MLVBLiveRoom#destroySharedInstance()](https://intl.cloud.tencent.com/document/product/1071/41673#destroysharedinstance) to terminate singleton objects.

***

### destroySharedInstance

This API is used to terminate [MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41673) singleton objects.

```
void destroySharedInstance()
```

>?After the instance is terminated, the externally cached [MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41673) instance cannot be used, and you need to call [MLVBLiveRoom#sharedInstance(Context)](https://intl.cloud.tencent.com/document/product/1071/41673#sharedinstance) again to get a new instance.

***

### setListener

This API is used to set callback.

```
abstract void setListener(IMLVBLiveRoomListener listener)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ---------- |
| listener | [IMLVBLiveRoomListener](https://intl.cloud.tencent.com/document/product/1071/41674) | Callback API |

__Introduction__

You can call [IMLVBLiveRoomListener](https://intl.cloud.tencent.com/document/product/1071/41674) to get various status notifications of [MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41673).

>?The SDK uses the main queue for callback by default. To customize a callback thread, use [MLVBLiveRoom#setListenerHandler(Handler)](https://intl.cloud.tencent.com/document/product/1071/41673#setlistenerhandler).

***

### setListenerHandler

This API is used to set the thread that drives callback.

```
abstract void setListenerHandler(Handler listenerHandler)
```

__Parameters__

| Parameter | Type | Description |
| --------------- | ------- | ------ |
| listenerHandler | Handler | Thread |

***

### login

This API is used to log in.

```
abstract void login(final LoginInfo loginInfo, final IMLVBLiveRoomListener.LoginCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| --------- | ------------------------------------------------------------ | -------------- |
| loginInfo | final LoginInfo                                              | Login information     |
| callback  | [final IMLVBLiveRoomListener.LoginCallback](https://intl.cloud.tencent.com/document/product/1071/41674#logincallback) | Login result callback |

***

### logout

This API is used to log out.

```
abstract void logout()
```

***

### setSelfProfile

This API is used to set profile.

```
abstract void setSelfProfile(String userName, String avatarURL)
```

__Parameters__

| Parameter | Type | Description |
| --------- | ------ | ---------- |
| userName | String | Nickname |
| avatarURL | String | Profile photo address |

***


## Room APIs

### getRoomList

This API is used to get the room list.

```
abstract void getRoomList(int index, int count, final IMLVBLiveRoomListener.GetRoomListCallback callback)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------------------------------------------------------------ | --------------------------- |
| index      | int                                                          | Room index starting value, which is 0 |
| count      | int                                                          | Number of rooms to be returned    |
| callback | [final IMLVBLiveRoomListener.GetRoomListCallback](https://intl.cloud.tencent.com/document/product/1071/41674#getroomlistcallback) | Callback of the room list getting result    |

__Introduction__

This API supports room list pagination. You can use the `index` and `count` parameters to specify the room list pagination logic:

- index = 0 & count = 10: to obtain the 10 rooms on the first page
- index = 11 & count = 10: to obtain the 10 rooms on the second page

***

### getAudienceList

This API is used to get the list of viewers in a room.

```
abstract void getAudienceList(IMLVBLiveRoomListener.GetAudienceListCallback callback)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------------------------------------------------------------ | ------------------------ |
| callback | [IMLVBLiveRoomListener.GetAudienceListCallback](https://intl.cloud.tencent.com/document/product/1071/41674#getaudiencelistcallback) | Callback of the room list getting result |

__Introduction__

When viewers enter a room, the backend adds their information to the viewer list of the room. You can call this API to get the viewer list.

>?A viewer list can contain up to 30 viewers. This list length is sufficient for common UI display. Longer lists not only waste storage space but also slow down the return of lists.

***

### createRoom

This API is used to create a room (called by a host).

```
abstract void createRoom(final String roomID, final String roomInfo, final IMLVBLiveRoomListener.CreateRoomCallback callback)
```

__Parameters__

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| roomID     | final String                             | Room ID. It is recommended that you use the user IDs of hosts as room IDs, eliminating the need for mapping on the backend. This parameter can be left empty, and in that case, the backend will generate a room ID instead. |
| roomInfo   | final String                            | Room information, for example, the room name. This parameter is optional and can be in JSON format. |
| callback | [final IMLVBLiveRoomListener.CreateRoomCallback](https://intl.cloud.tencent.com/document/product/1071/41674#createroomcallback) | Callback of the room creation result                                         |

__Introduction__

Generally, a host can start live streaming in the following call process: 

1. The host calls [startLocalPreview()](https://intl.cloud.tencent.com/document/product/1071/41673#startlocalpreview) to enable camera preview, during which the host can adjust beauty filter parameters. 
2. The host calls `createRoom` to create a live room. No matter whether the room is created successfully, the result will be notified to the host through [IMLVBLiveRoomListener.CreateRoomCallback](https://intl.cloud.tencent.com/document/product/1071/41674#createroomcallback).

***

### enterRoom

This API is used to enter a room (called by a viewer).

```
abstract void enterRoom(final String roomID, final TXCloudVideoView view, final IMLVBLiveRoomListener.EnterRoomCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | -------------------- |
| roomID   | final String                                                 | Room ID           |
| view     | final TXCloudVideoView                                       | Control that carries the video image |
| callback | [final IMLVBLiveRoomListener.EnterRoomCallback](https://intl.cloud.tencent.com/document/product/1071/41674#enterroomcallback) | Callback of the room entry result |

__Introduction__

The general process for a viewer to watch a live stream is as follows: 

1. The viewer calls [getRoomList()](https://intl.cloud.tencent.com/document/product/1071/41673#getroomlist) to refresh the latest live room list and gets the room list through [IMLVBLiveRoomListener.GetRoomListCallback](https://intl.cloud.tencent.com/document/product/1071/41674#getroomlistcallback). 
2. The viewer selects a live room and calls [enterRoom()](https://intl.cloud.tencent.com/document/product/1071/41673#enterroom) to enter the live room.

***

### exitRoom()

This API is used to exit a room.

```
abstract void exitRoom(IMLVBLiveRoomListener.ExitRoomCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | -------------------- |
| callback | [IMLVBLiveRoomListener.ExitRoomCallback](https://intl.cloud.tencent.com/document/product/1071/41674#exitroomcallback) | Callback of the room exit result |

***

### setCustomInfo

This API is used to set custom information.

```
abstract void setCustomInfo(final MLVBCommonDef.CustomFieldOp op, final String key, final Object value, final IMLVBLiveRoomListener.SetCustomInfoCallback callback)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------------------------------------------------------------ | -------------------------------------------------- |
| op       | final MLVBCommonDef.CustomFieldOp                            | Operation. For more information, please see `MLVBCommonDef.CustomFieldOp`. |
| key      | final String                                                 | Custom key                                         |
| value    | final Object                                                 | Value                                             |
| callback | [final IMLVBLiveRoomListener.SetCustomInfoCallback](https://intl.cloud.tencent.com/document/product/1071/41674#setcustominfocallback) | Callback of the completion of custom message setting                         |

__Introduction__

Sometimes you may need to generate certain additional information for a room. Such information can be cached to the server by using this API.

>?
>
>- When `op` is `MLVBCommonDef.CustomFieldOp#SET`, `value` can be a string or an integer.
>- When `op` is `MLVBCommonDef.CustomFieldOp#INC`, `value` must be an integer.
>- When `op` is `MLVBCommonDef.CustomFieldOp#DEC`, `value` must be an integer.

***

### getCustomInfo

This API is used to get custom information.

```
abstract void getCustomInfo(final IMLVBLiveRoomListener.GetCustomInfoCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | -------------------- |
| callback | [final IMLVBLiveRoomListener.GetCustomInfoCallback](https://intl.cloud.tencent.com/document/product/1071/41674#getcustominfocallback) | Callback of the custom information getting result |

***


## Mic Connect Between a Host and a Viewer

### requestJoinAnchor

This API is used by a viewer to request mic connect.

```
abstract void requestJoinAnchor(String reason, IMLVBLiveRoomListener.RequestJoinAnchorCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | ---------------- |
| reason   | String                                                       | Reason for mic connect       |
| callback | [IMLVBLiveRoomListener.RequestJoinAnchorCallback](https://intl.cloud.tencent.com/document/product/1071/41674#requestjoinanchorcallback) | Callback of the mic connect request result |

__Introduction__

The process for mic connect between a host and a viewer is as follows:

1. The viewer calls [requestJoinAnchor()](https://intl.cloud.tencent.com/document/product/1071/41673#requestjoinanchor) to send a mic connect request to the host.
2. The host receives the [IMLVBLiveRoomListener#onRequestJoinAnchor(AnchorInfo, String)](https://intl.cloud.tencent.com/document/product/1071/41674#onrequestjoinanchor) callback notification.
3. The host calls [responseJoinAnchor()](https://intl.cloud.tencent.com/document/product/1071/41673#responsejoinanchor) to specify whether to accept the mic connect request from the viewer.
4. The viewer receives a [IMLVBLiveRoomListener.RequestJoinAnchorCallback](https://intl.cloud.tencent.com/document/product/1071/41674#requestjoinanchorcallback) callback notification and gets to know whether the request is accepted.
5. If the request is accepted, the viewer calls [startLocalPreview()](https://intl.cloud.tencent.com/document/product/1071/41673#startlocalpreview) to enable the local camera. If the application has not obtained the camera and mic permissions, a permission prompt will be displayed on the UI.
6. The viewer calls [joinAnchor()](https://intl.cloud.tencent.com/document/product/1071/41673#joinanchor) to officially enter the mic connect status.
7. Once the viewer enters the mic connect status, the host receives the [IMLVBLiveRoomListener#onAnchorEnter(AnchorInfo)](https://intl.cloud.tencent.com/document/product/1071/41674#onanchorenter) notification.
8. The host calls [startRemoteView()](https://intl.cloud.tencent.com/document/product/1071/41673#startremoteview) to view the video image of the mic connect viewer.
9. If there are other mic connect viewers in the live room of the host, the new mic connect viewer will receive the `onAnchorJoin()` callback notification and can call `startRemoteView` to display the video images of the other mic connect viewers.

***

### responseJoinAnchor

This API is used by a host to process mic connect requests.

```
abstract int responseJoinAnchor(String userID, boolean agree, String reason)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------- | ------------------------- |
| userID | String  | Viewer ID                  |
| agree | boolean | `true`: accept; `false`: reject |
| reason | String | Reason for accepting or rejecting a mic connect request |

__Response__

0: successful. Other values: failed.

__Introduction__

After receiving the [IMLVBLiveRoomListener#onRequestJoinAnchor(AnchorInfo, String)](https://intl.cloud.tencent.com/document/product/1071/41674#onrequestjoinanchor) callback notification, a host needs to call this API to process the mic connect request of the viewer.

***

### joinAnchor

This API is used by a viewer to enter the mic connect status.

```
abstract void joinAnchor(final IMLVBLiveRoomListener.JoinAnchorCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | -------------------- |
| callback | [final IMLVBLiveRoomListener.JoinAnchorCallback](https://intl.cloud.tencent.com/document/product/1071/41674#joinanchorcallback) | Callback of the result of entering the mic connect status |

__Introduction__

Once a viewer enters the mic connect status, the host and other mic connect viewers in the host's live room will receive the [IMLVBLiveRoomListener#onAnchorEnter(AnchorInfo)](https://intl.cloud.tencent.com/document/product/1071/41674#onanchorenter) callback notification.

***

### quitJoinAnchor

This API is used by a viewer to exit mic connect.

```
abstract void quitJoinAnchor(final IMLVBLiveRoomListener.QuitAnchorCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | -------------------- |
| callback | [final IMLVBLiveRoomListener.QuitAnchorCallback](https://intl.cloud.tencent.com/document/product/1071/41674#quitanchorcallback) | Callback of the result of exiting mic connect |

__Introduction__

Once a viewer exits mic connect, the host and other mic connect viewers in the host's live room will receive the [IMLVBLiveRoomListener#onAnchorExit(AnchorInfo)](https://intl.cloud.tencent.com/document/product/1071/41674#onanchorexit) callback notification.

***

### kickoutJoinAnchor

This API is used by a host to kick out a mic connect viewer.

```
abstract void kickoutJoinAnchor(String userID)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------ | ------------- |
| userID | String | ID of the mic connect viewer |

__Introduction__

After a host calls this API to kick out a mic connect viewer, the kicked out viewer will receive the [IMLVBLiveRoomListener#onKickoutJoinAnchor()](https://intl.cloud.tencent.com/document/product/1071/41674#onkickoutjoinanchor) callback notification.

***


## Cross-Room Host Competition

### requestRoomPK

This API is used by a host to request for cross-room competition.

```
abstract void requestRoomPK(String userID, final IMLVBLiveRoomListener.RequestRoomPKCallback callback)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------------------------------------------------------------ | ------------------------ |
| userID   | String                                                       | ID of the invited host          |
| callback | [final IMLVBLiveRoomListener.RequestRoomPKCallback](https://intl.cloud.tencent.com/document/product/1071/41674#requestroompkcallback) | Callback of the result of the cross-room host competition request |

__Introduction__

Hosts in different rooms can compete with each other. The process for host A and host B to start cross-room competition during live streaming is as follows:

1. Host A calls [requestRoomPK()](https://intl.cloud.tencent.com/document/product/1071/41673#requestroompk) to send a competition request to host B.
2. Host B receives the [IMLVBLiveRoomListener#onRequestRoomPK(AnchorInfo)](https://intl.cloud.tencent.com/document/product/1071/41674#onrequestroompk) callback notification.
3. Host B calls [responseRoomPK()](https://intl.cloud.tencent.com/document/product/1071/41673#responseroompk) to specify whether to accept the competition request from host A.
4. If host B accepts the request of host A, host B calls [startRemoteView()](https://intl.cloud.tencent.com/document/product/1071/41673#startremoteview) to display the video image of host A.
5. Host A receives the [IMLVBLiveRoomListener.RequestRoomPKCallback](https://intl.cloud.tencent.com/document/product/1071/41674#requestroompkcallback) callback notification and gets to know whether the request is accepted.
6. If the request of host A is accepted, host A calls [startRemoteView()](https://intl.cloud.tencent.com/document/product/1071/41673#startremoteview) to display the video image of host B.

***

### responseRoomPK

This API is used by a host to respond to a cross-room competition request.

```
abstract int responseRoomPK(String userID, boolean agree, String reason)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------- | ------------------------- |
| userID | String | ID of the host who initiates the competition request |
| agree | boolean | `true`: accept; `false`: reject |
| reason | String  | Reason for accepting or rejecting the competition request |

__Response__

0: successful. Other values: failed.

__Introduction__

Once the invited host responds to the cross-room competition request, the inviting host will receive the [IMLVBLiveRoomListener.RequestRoomPKCallback](https://intl.cloud.tencent.com/document/product/1071/41674#requestroompkcallback) callback notification.

***

### quitRoomPK

This API is used to exit cross-room competition.

```
abstract void quitRoomPK(final IMLVBLiveRoomListener.QuitRoomPKCallback callback)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------------------------------------------------------------ | ------------------------ |
| callback | [final IMLVBLiveRoomListener.QuitRoomPKCallback](https://intl.cloud.tencent.com/document/product/1071/41674#quitroompkcallback) | Callback of the result of exiting cross-room competition |

__Introduction__

If either host exits cross-room competition, the other host will receive the [IMLVBLiveRoomListener#onQuitRoomPK(AnchorInfo)](https://intl.cloud.tencent.com/document/product/1071/41674#onquitroompk) callback notification.

***


## Video APIs

### startLocalPreview

This API is used to enable the preview image of the local video.

```
abstract void startLocalPreview(boolean frontCamera, TXCloudVideoView view)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ---------------- | --------------------------------- |
| frontCamera | boolean          | `YES`: front camera; `NO`: rear camera |
| view        | TXCloudVideoView | Control that carries the video image              |

***

### stopLocalPreview

This API is used to stop local video capturing and preview.

```
abstract void stopLocalPreview()
```

***

### startRemoteView

This API is used to start rendering remote video images.

```
abstract void startRemoteView(final AnchorInfo anchorInfo, final TXCloudVideoView view, final IMLVBLiveRoomListener.PlayCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ------------------------------------------------------------ | -------------------- |
| anchorInfo | final AnchorInfo                                             | Information of the remote user     |
| view     | final TXCloudVideoView                                       | Control that carries the video image |
| callback   | [final IMLVBLiveRoomListener.PlayCallback](https://intl.cloud.tencent.com/document/product/1071/41674#playcallback) | Player listener       |

>?Call this API upon `onUserVideoAvailable` callback.

***

### stopRemoteView

This API is used to stop rendering remote video images.

```
abstract void stopRemoteView(final AnchorInfo anchorInfo)

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------------- | ---------------- |
| anchorInfo | final AnchorInfo                                             | Information of the remote user     |

***

### startScreenCapture

This API is used to start screen capturing.

```
abstract void startScreenCapture()

```

***

### stopScreenCapture

This API is used to stop screen capturing.

```
abstract void stopScreenCapture()

```

***


## Audio APIs

### muteLocalAudio

This API is used to specify whether to mute local audio.

```
abstract void muteLocalAudio(boolean mute)

```

__Parameters__

| Parameter | Type | Description |
| ---- | ------- | ------------------------- |
| mute | boolean | `true`: mute; `false`: unmute. |

***

### muteRemoteAudio

This API is used to specify whether to mute a specified user.

```
abstract void muteRemoteAudio(String userID, boolean mute)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------- | --------------------------- |
| userID | String  | ID of the specified user            |
| mute | boolean | `true`: mute; `false`: unmute |

***

### muteAllRemoteAudio

This API is used to specify whether to mute all remote users.

```
abstract void muteAllRemoteAudio(boolean mute)
```

__Parameters__

| Parameter | Type | Description |
| ---- | ------- | --------------------------- |
| mute | boolean | `true`: mute; `false`: unmute |

***


## Camera APIs

### switchCamera

This API is used to switch between cameras.

```
abstract void switchCamera()
```

***

### setZoom

This API is used to set the camera zoom factor (focal length).

```
abstract boolean setZoom(int distance)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ---- | ------------------------------------------------------------ |
| distance | int  | Value range: 1-5. The value `1` indicates the furthest view (normal lens), and `5` indicates the nearest view (enlarging lens). The maximum value is recommended to be `5`. If the maximum value is greater than 5, the video image will become blurry. |

***

### enableTorch

This API is used to enable or disable flash.

```
abstract boolean enableTorch(boolean enable)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------- | ------------------------- |
| enable | boolean | `true`: enable; `false`: disable |

***

### setCameraMuteImage

This API is used to set the waiting picture to be displayed when the host blocks the camera.

```
abstract void setCameraMuteImage(Bitmap bitmap)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------ | ------ |
| bitmap | Bitmap | Bitmap |

__Introduction__

When the host blocks the camera, or the camera cannot be used because the application is switched to the background, we need to display a waiting picture to viewers saying like "the host leaves temporarily and will come back soon".

***

### setCameraMuteImage

This API is used to set the waiting picture to be displayed when the host blocks the camera.

```
abstract void setCameraMuteImage(final int id)
```

__Parameters__

| Parameter | Type | Description |
| ---- | --------- | ---------------------------- |
| id   | final int | Resource file of the default waiting picture to be displayed |

__Introduction__

When the host blocks the camera, or the camera cannot be used because the application is switched to the background, we need to display a waiting picture to viewers saying like "the host leaves temporarily and will come back soon".

***


## Beauty Filter APIs

### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://intl.cloud.tencent.com/document/product/1071/41677).

```
public TXBeautyManager getBeautyManager()
```

With TXBeautyManager, you can use the following features:

- Set beauty effects such as the beauty filter style, skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening or shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, mouth shape, nose wings, nose position, lip thickness, and face shape.
- Set animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.

***


### setFilter

This API is used to specify the material filter effect.

```
abstract void setFilter(Bitmap image)
```

__Parameters__

| Parameter | Type | Description |
| ----- | ------ | --------------------------------------------------------- |
| image | Bitmap | Specified material, which is an image from the color lookup table. **The material must be in PNG format.** |

***

### setFilterConcentration

This API is used to set the strength of a filter.

```
abstract void setFilterConcentration(float concentration)
```

__Parameters__

| Parameter | Type | Description |
| ------------- | ----- | ----------------------------------------- |
| concentration | float | Value range: 0-1. The larger the value, the more obvious the effect. Default value: 0.5. |

***

### setWatermark

This API is used to set the watermark. You do not need to specify the watermark height. The SDK will automatically calculate the height according to the aspect ratio of the watermark.

```
abstract void setWatermark(Bitmap image, float x, float y, float width)
```

__Parameters__

| Parameter | Type | Description |
| ----- | ------ | --------------------------------------- |
| image | Bitmap | Watermark image. If `null` is passed in, the watermark will be removed.             |
| x     | float  | Normalized X coordinate of the watermark position. Value range: [0,1]. |
| y     | float  | Normalized Y coordinate of the watermark position. Value range: [0,1]. |
| width | float  | Normalized width of the watermark. Value range: [0,1].            |

***

### setGreenScreenFile

This API is used to configure the green screen file.

```
abstract boolean setGreenScreenFile(String file)
```

__Parameters__

| Parameter | Type | Description |
| ---- | ------ | ------------------------------------------------------------ |
| file | String | Path to the green screen file. Two settings modes are supported: 1. place the resource file in the `assets` directory and use the file name as the path name; 2. use the absolute path of the file as the path name. |

__Response__

false: failed. true: successful.

__Introduction__

Green screen files must be JPG or PNG images or MP4 or 3GP videos supported by Android.

>?API level 18 is required.

***

### setExposureCompensation

This API is used to adjust the exposure.

```
abstract void setExposureCompensation(float value)
```

__Parameters__

| Parameter | Type | Description |
| ----- | ----- | ------------------------------------------------------------ |
| value | float | Exposure ratio, which indicates the ratio of the maximum exposure adjustment value that the phone supports. Value range: -1 to 1. A negative value means to decrease exposure, and a positive value means to increase exposure. 0 means no exposure adjustment. |

***


## Message Sending APIs

### sendRoomTextMsg

This API is used to send text messages.

```
abstract void sendRoomTextMsg(String message, final IMLVBLiveRoomListener.SendRoomTextMsgCallback callback)
```

__Parameters__

| Parameter | Type | Description |
| -------- | ------------------------------------------------------------ | -------------- |
| message  | String                                                       | Text message     |
| callback | [final IMLVBLiveRoomListener.SendRoomTextMsgCallback](https://intl.cloud.tencent.com/document/product/1071/41674#sendroomtextmsgcallback) | Callback of the sending result of the text message |

***

### sendRoomCustomMsg

This API is used to send custom text messages.

```
abstract void sendRoomCustomMsg(String cmd, String message, final IMLVBLiveRoomListener.SendRoomCustomMsgCallback callback)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------------------------------------------------------------ | -------------------------------------------------- |
| cmd      | String                                                       | Custom command word used to distinguish between different message types |
| message  | String                                                       | Custom text message                                         |
| callback | [final IMLVBLiveRoomListener.SendRoomCustomMsgCallback](https://intl.cloud.tencent.com/document/product/1071/41674#sendroomcustommsgcallback) | Callback of the sending result of the custom text message                                      |

***


## Background Audio Mixing APIs

### playBGM

This API is used to play background music.

```
abstract boolean playBGM(String path)
```

__Parameters__

| Parameter | Type | Description |
| ---- | ------ | ------------------ |
| path | String | Path to the background music file |

__Response__

true: success. false: failure.

***

### stopBGM

This API is used to stop background music playback.

```
abstract void stopBGM()
```

***

### pauseBGM

This API is used to pause background music playback.

```
abstract void pauseBGM()
```

***

### resumeBGM

This API is used to resume background music playback.

```
abstract void resumeBGM()
```

***

### getBGMDuration

This API is used to get the total length of the background music file.

```
abstract int getBGMDuration(String path)
```

__Parameters__

| Parameter | Type | Description |
| ---- | ------ | ------------------------------------------------------------ |
| path | String | Path to the music file. If `path` is left empty, the length of the music file being played back will be returned. |

__Response__

If this API is successfully called, the length of the music file will be returned, in milliseconds. Otherwise, `-1` will be returned.

***

### setMicVolumeOnMixing

This API is used to set the microphone volume when background music is played back.

```
abstract void setMicVolumeOnMixing(int volume)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------------ |
| volume | int  | Volume. 100 indicates a normal volume. Recommended value range: 0-200. |

***

### setBGMVolume

This API is used to set the background music volume when background music is played back.

```
abstract void setBGMVolume(int volume)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------------------------------ |
| volume | int  | Volume. 100 indicates a normal volume. Recommended value range: 0-200. If you need to turn up the background music volume, use a larger value. |

***

### setReverbType

This API is used to set the reverb effect.

```
abstract void setReverbType(int reverbType)
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---- | ------------------------------------------------------------ |
| reverbType | int  | Reverb type. Valid values: <br>TXLiveConstants#REVERB_TYPE_0: disable reverb <br> TXLiveConstants#REVERB_TYPE_1: karaoke room <br>TXLiveConstants#REVERB_TYPE_2: small room <br> TXLiveConstants#REVERB_TYPE_3: big hall <br> TXLiveConstants#REVERB_TYPE_4: deep <br> TXLiveConstants#REVERB_TYPE_5: resonant <br>TXLiveConstants#REVERB_TYPE_6: metallic |

***

### setVoiceChangerType

This API is used to set the voice changing type.

```
abstract void setVoiceChangerType(int voiceChangerType)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ---------------- | ---- | ----------------------------------- |
| voiceChangerType | int  | Voice changing type. For more information, please see `TXVoiceChangerType`. |

***

### setBgmPitch

This API is used to adjust the pitch of background music.

```
abstract void setBgmPitch(float pitch)
```

__Parameters__

| Parameter | Type | Description |
| ----- | ----- | --------------------------------- |
| pitch | float | Pitch. 0 indicates a normal pitch. Value range: -1 to 1. |

__Introduction__

This API is used for audio mixing, for example, mixing background music with sounds collected from the microphone for playback.

***
