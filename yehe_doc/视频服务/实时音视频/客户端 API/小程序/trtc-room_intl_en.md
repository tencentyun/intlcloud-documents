## Component Overview

The **&lt;trtc-room&gt;** tag is a custom component for TRTC intercommunication implemented based on `&lt;live-pusher&gt;` and `&lt;live-player&gt;`, which supports various use cases:

**Audio/Video call (scene = "rtc")**
- In video call scenarios, [720p and 1080p](#quality) HD image quality options are supported.
- In audio call scenarios, 48 kHz full band and dual-channel are supported.
- A single room can sustain up to 300 concurrent online users, and up to 50 of them can speak simultaneously.
- Use cases: one-to-one video call, video conferencing with up to 300 participants, online medical diagnosis, video interview, video customer service, online Werewolf, etc.
- Use method: you need to set the [scene](#Config) attribute of `&lt;trtc-room&gt;` to **rtc**.

**Interactive live streaming and voice chat room (scene = "live")**
- Live streaming to up to 100,000 concurrent viewers is supported with the playback latency down to 1,000 ms.
- Mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms.
- Use cases: low-latency video live streaming, interactive classroom for up to 100,000 participants, video dating room, remote training, large-scale conferencing, etc.
- Use method: you need to set the [scene](#Config) attribute of `&lt;trtc-room&gt;` to **live**.

<h2 id="API">API Overview</h2>

**Basic methods**

| API | Description |
|-----|-----|
| [on(EventCode, handler, context)](#on(eventcode.2C-handler.2C-context)) | Listens on events delivered by the component. For more information on events, please see [Event List](#Event). |
| [off(EventCode, handler)](#off(eventcode.2C-handler))| Cancels listening on events. |
| [enterRoom(params)](#enterroom(params)) | Enters room. If the room does not exist, the system will automatically create a room. |
| [exitRoom()](#exitroom()) | Stops push, unsubscribes from all remote audio/video streams, and exits room. |

**Release and subscription**

| API | Description |
|-----|-----|
| [publishLocalVideo()](#publishlocalvideo()) | Publishes local video, i.e., enabling local camera capturing and starting video push. |
| [unpublishLocalVideo()](#unpublishlocalvideo()) | Cancels local video release and stops local video push. |
| [publishLocalAudio()](#publishlocalaudio())| Publishes local audio, i.e., enabling local mic capturing and starting audio push. |
| [unpublishLocalAudio()](#unpublishlocalaudio()) | Cancels local audio release and stops local audio push. |
| [subscribeRemoteVideo(params)](#subscriberemotevideo(params)) | Subscribes to remote user's video stream and plays it back. |
| [unsubscribeRemoteVideo(params)](#unsubscriberemotevideo(params)) | Unsubscribes from remote user's video stream and stops playback. |
| [subscribeRemoteAudio(params)](#subscriberemoteaudio(params)) | Subscribe to remote user's audio stream and plays it back. |
| [unsubscribeRemoteAudio(params)](#unsubscriberemoteaudio(params)) | Unsubscribes from remote user's audio stream and stops playback. |
| [getRemoteUserList()](#getremoteuserlist()) | Gets remote user list. |

**View control**

| API | Description |
|-----|-----|
| [enterFullscreen(params)](#enterfullscreen(params)) | Enables full-screen playback for remote video. Playback in full screen mode is generally suitable for the substream (screen sharing) image. |
| [exitFullscreen(params)](#exitfullscreen(params)) | Cancels full screen mode for remote video. |
| [setViewOrientation(params)](#setvieworientation(params))| Sets the display orientation of specified remote image. |
| [setViewFillMode(params)](#setviewfillmode(params))| Sets filling mode for specified remote image. |
| [setViewVisible(params)](#setviewvisible(params))| Displays or hides the image of specified video stream. |
| [setViewRect(params)](#setviewrect(params))| Sets the coordinates and size of specified video image. |
| [setViewZIndex(params)](#setviewzindex(params))| Sets the layer of specified video image. |

**Background music**

| API | Description |
|-----|-----|
| [playBGM(params)](#playbgm(params)) | Plays back background music. The background music will be mixed with the voice captured by the mic and published to the cloud together, which is called "background audio mix". |
| [stopBGM()](#stopbgm()) | Stops background music. |
| [pauseBGM()](#pausebgm()) | Pauses background music. |
| [resumeBGM()](#resumebgm()) | Resumes background music. |
| [setBGMVolume(params)](#setbgmvolume(params))| Sets the volume level of background music in audio mix. |
| [setMICVolume(params)](#setmicvolume(params))| Sets mic capturing volume level in audio mix. |

**Message sending and receiving**
The message sending/receiving feature takes effect only after you activate the [IM](https://intl.cloud.tencent.com/product/im) service and set `enableIM` to `true` in the [attribute table](#Config).

| API | Description |
|-----|-----|
| [sendC2CTextMessage(params)](#sendc2ctextmessage(params)) | Sends C2C text message (i.e., sending message to specified user). |
| [sendC2CCustomMessage(params)](#sendc2ccustommessage(params)) | Sends C2C custom message. A custom message can be used to send control signaling (such as invitation to speak and application for mic-on). |
| [sendGroupTextMessage(params)](#sendgrouptextmessage(params)) | Sends group text message. |
| [sendGroupCustomMessage(params)](#sendgroupcustommessage(params)) | Sends group custom message. |

**Other features**

| API | Description |
|-----|-----|
| [switchCamera()](#switchcamera()) | Switches between local front and rear cameras. |
| [snapshot()](#snapshot(params)) | Captures specified remote or local video image and saves it into system album. |


<h2 id="Config">Attribute Table</h2>
`&lt;trtc-room&gt;` has only one `config` attribute, through which the following parameters can be passed in:

| Parameter | Type | Default Value | Description |
|:---------------------|:--------|:----------|:-------------|
| scene                | String  | rtc       | Scenario, which is required. Valid values: <li>rtc: real-time call, which uses high-quality lines and supports up to 300 users in a room.</li><li>live: live streaming, which uses hybrid lines and supports up to 100,000 users in a room (up to 50 users can mic on concurrently).</li> |
| sdkAppID             | String  | -         | `SDKAppID` that will be assigned to a created application after TRTC is activated, which is required. |
| userID               | String  | -         | User ID, which is required and can be specified by your account system. |
| userSig              | String  | -         | Identity signature, which is required and acts as the login password. It can be calculated based on the `userID`. For more information on the calculation method, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| template             | String  | custom    | Image layout mode built in the component, which is required. Valid values: <li>"1v1": the small image is displayed on top of the big image.</li><li>"grid": grid mode, where the images can overlay each other, and the images of up to 9 streams can be displayed.</li><li>"custom": custom mode, which requires you to modify the `custom.wxml` template of the component.</li> |
| enableCamera         | Boolean | false     | Whether to enable the camera. If the value is `true`, after `enterRoom` is called, video will be automatically published. |
| enableMic            | Boolean | false     | Whether to enable the mic. If the value is `true`, after `enterRoom` is called, audio will be automatically published. |
| enableAgc            | Boolean | false     | Whether to enable audio AGC. This feature can compensate for the low volume level of the mic on certain mobile phones but will also amplify the noise. We recommend you enable this feature together with ANS. |
| enableAns            | Boolean | false     | Whether to enable ANS. This feature automatically detects and filters out background noise, but the desired audio may also be filtered out. This feature is suitable only for scenarios such as conferencing and teaching. |
| enableEarMonitor     | Boolean | false     | Whether to enable in-ear monitoring (currently, it is available only for iOS). |
| enableAutoFocus      | Boolean | true      | Whether to enable camera autofocus. To disable autofocus, you need to click on the preview image of the camera to manually focus. |
| enableZoom           | Boolean | false     | Whether to enable focal length adjustment through two-finger swipe. |
| minBitrate<span id="quality"></span>          | String  | 200       | Minimum bitrate. We recommend you not set a very low bitrate. |
| maxBitrate           | String  | 1000      | Maximum bitrate, which needs to match the resolution. We recommend you set this parameter based on [Resolution-Bitrate Reference Table](https://intl.cloud.tencent.com/document/product/647/35153). |
| videoWidth           | String  | 360       | Video width. If the video width and height are set, `aspect` will be ignored. |
| videoHeight          | String  | 640       | Video height. If the video width and height are set, `aspect` will be ignored. |
| beautyLevel          | Number  | 0         | Beauty filter. Value range: 0–9. 0 indicates to disable the filter. |
| whitenessLevel       | Number  | 0         | Skin brightening filter. Value range: 0–9. 0 indicates to disable the filter. |
| videoOrientation     | String  | vertical  | Local image orientation. Valid values: vertical, horizontal. |
| videoAspect          | String  | 9:16      | Aspect ratio. Valid values: 3:4, 9:16. |
| frontCamera          | String  | front     | Whether to use the front or rear camera. Valid values: front, back. |
| enableRemoteMirror   | Boolean | false     | Image mirroring effect viewed by viewers. Changing this attribute will not affect the local image. Only the image effect viewed by viewers will be changed. |
| localMirror          | String  | auto      | Mirroring effect of preview image of anchor's local camera. Valid values: <li>auto: only the front camera image is mirrored (system camera configuration).</li><li>enable: both the front and rear camera images are mirrored.</li><li>disable: neither camera image is mirrored.</li>|
| enableBackgroundMute | Boolean | false     | Whether to pause audio capturing if the anchor's Mini Program is switched to the background. |
| audioQuality         | String  | high      | Whether to use high (48 KHz) or low (16 KHz) audio quality. Valid values: high, low. |
| audioVolumeType      | String  | voicecall | System volume type. Valid values: <li>media: media volume.</li><li>voicecall: call volume.</li>|
| audioReverbType      | Number  | 0         | Audio reverb type. Valid values: 0: disabled; 1: karaoke room; 2: small room; 3: big hall; 4: deep; 5: resonant; 6: metallic; 7: husky. |
| enableIM             | Boolean | false     | Whether to enable the IM feature. |
| debugMode            | Boolean | false     | Whether to enable the debugging mode of the component. After enablement, a translucent floating layer showing audio and video metrics will be displayed on top of the video image. |


Sample code:
``` 
 // index.wxml
<trtc-room id="trtcroom" config="{{trtcConfig}}"></trtc-room>
```

```
// videocall.js
trtcConfig = {
  sdkAppID: '1401000123', // `SDKAppID` that will be assigned to a created application after TRTC is activated
  userID: 'test_user_001', // User ID, which can be specified by your account system
  userSig: 'xxxxxxxxxxxx', // Identity signature, which acts as the login password
  template: 'grid', // Image layout mode
}
```

## Component Methods

### selectComponent()
You can get the component instance through the `this.selectComponent()` method provided by WeChat Mini Program.

Sample code:

```
let trtcRoomContext = this.selectComponent('#trtcroom')
trtcRoomContext.enterRoom({roomID: 2233})
```

### on(EventCode, handler, context)

**Note:**

This API is used to listen on the events delivered by the component. For more information on events, please see [Event List](#Event).
>! Please listen on events before calling `enterRoom` to avoid missing component distribution events.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:----------|:---------|:-------|:-------------|
| EventCode | String   | -      | Event code |
| handler   | Function | -      | Listener function |
| context   | Object   | -      | Current execution context |

**Returned value:**

None

**Sample code:**
```
function onLocalJoin(event) {
  // Local room entry succeeded
}
trtcRoomContext.on(trtcRoomContext.EVENT.LOCAL_JOIN, onLocalJoin, this)
```

### off(EventCode, handler)

**Note:**

This API is used to cancel listening on events.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:----------|:---------|:-------|:---------------------|
| EventCode | String   | -      | Event code |
| handler   | Function | -      | Named listener function to be canceled |

**Returned value:**

None

**Sample code:**
```
function onLocalJoin(event) {
  // Local room entry succeeded
}
trtcRoomContext.off(trtcRoomContext.EVENT.LOCAL_JOIN, onLocalJoin)
```

### enterRoom(params)

**Note:**
This API is used to enter a room. The `roomID` must be passed in before other parameters are called.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-------|:-------|:-------|:-------------------------------------------|
| roomID | Number | -      | Room ID, which is specified by your system. Value range: 1–4294967295 |

**Returned value:**
Promise

**Sample code:**
```
trtcRoomContext.enterRoom({roomID: 2233}).catch((error)=>{
  // Failed to enter the room
  // Note: a room entry success is notified through the `LOCAL_JOIN` event
})
```

### exitRoom()
**Note:**

This API is used to stop push, unsubscribe from all remote audio/video streams, and exit the room.

>! Due to the limit of the WeChat Mini Program engine on the latest version, please do not call `exitRoom()` in the `onHide()` callback function; otherwise, various bugs will occur.

**Parameters:**

None

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.exitRoom().then(()=>{
  // Exited room successfully
})
```

### publishLocalVideo()
**Note:**

This API is used to publish a local video, i.e., enabling local camera capturing and starting video push. Generally, it needs to be used together with `publishLocalAudio()`.

**Parameters:**

None

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.publishLocalVideo().then(()=>{
  // Published successfully
})
```

### unpublishLocalVideo()
**Note:**

This API is used to cancel local video release and stop local video push.

**Parameters:**

None

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.unpublishLocalVideo().then(()=>{
  // Canceled release successfully
})
```

### publishLocalAudio()
**Note:**

This API is used to publish the local audio, i.e., enabling local mic capturing and starting audio push. In a pure audio call scenario, `publishLocalVideo()` does not need to be called. 

**Parameters:**

None

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.publishLocalAudio().then(()=>{
  // Published successfully
})
```

### unpublishLocalAudio()
**Note:**

This API is used to cancel local audio release and stop local audio push.

**Parameters:**

None

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.unpublishLocalAudio().then(()=>{
  // Canceled release successfully
})
```

### subscribeRemoteVideo(params)
**Note:**

This API is used to subscribe to a remote user's video stream and play it back.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:---------------------------------------------------------------------------------------------|
| userID     | String | -      | Remote user ID, which is required. You can get the `userID` and `streamType` of a (subscribable) remote video stream through the `REMOTE_VIDEO_ADD` event notified by the component. |
| streamType | String | -      | Remote user stream type, which is required. Valid values: <li> main: big image.</li><li>small: small image.</li><li>aux: substream (i.e., screen sharing). |

**Returned value:**

Promise

**Sample code:**

```
// There is a subscribable remote video stream
function onRemoteVideoAdd(event) {
  trtcRoomContext.subscribeRemoteVideo({
    userID: event.data.userID,
    streamType: event.data.streamType
  }).then(()=>{
    // Subscribed successfully
  })
}

trtcRoomContext.on(trtcRoomContext.EVENT.REMOTE_VIDEO_ADD, onRemoteVideoAdd)
```

### unsubscribeRemoteVideo(params)
**Note:**

This API is used to unsubscribe from a remote user's video stream and stop playback.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:----------------------------------------------------------------|
| userID     | String | -      | Remote user ID, which is required. You can get the `userID` and `streamType` of the remote video stream (whose release is canceled) through the `REMOTE_VIDEO_REMOVE` event notified by the component. |
| streamType | String | -      | Remote user stream type, which is required. Valid values: <li>main: big image.</li><li>aux: substream (i.e., screen sharing).</li> |

**Returned value:**

Promise

**Sample code:**

```
// A remote video stream is closed
function onRemoteVideoRemove(event) {
  trtcRoomContext.unsubscribeRemoteVideo({
    userID: event.data.userID,
    streamType: event.data.streamType
  }).then(()=>{
    // Unsubscribed successfully
  })
}
trtcRoomContext.on(trtcRoomContext.EVENT.REMOTE_VIDEO_REMOVE, onRemoteVideoRemove)
```

### subscribeRemoteAudio(params)
**Note:**

This API is used to subscribe to a remote user's audio stream and play it back.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-------|:-------|:-------|:----------------------------------------------------|
| userID | String | -      | Remote user ID. You can get the `userID` of a (subscribable) remote audio stream through the `REMOTE_AUDIO_ADD` event notified by the component. |

**Returned value:**

Promise

**Sample code:**
```
// There is a subscribable remote audio stream
function onRemoteAudioAdd(event) {
  trtcRoomContext.subscribeRemoteAudio({
    userID: event.data.userID
  }).then(()=>{
    // Subscribed successfully
  })
}

trtcRoomContext.on(trtcRoomContext.EVENT.REMOTE_AUDIO_ADD, onRemoteAudioAdd)
```

### unsubscribeRemoteAudio(params)
**Note:**

This API is used to unsubscribe from a remote user's audio stream and stop playback.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-------|:-------|:-------|:-------------------------------------------------------|
| userID | String | -      | Remote user ID. You can get the `userID` of the remote audio stream (whose release is canceled) through the `REMOTE_AUDIO_REMOVE` event delivered by the component. |

**Returned value:**

Promise

**Sample code:**
```
// A remote audio stream is closed
function onRemoteAudioRemove(event) {
  trtcRoomContext.unsubscribeRemoteAudio({
    userID: event.data.userID
  }).then(()=>{
    // Unsubscribed successfully
  })
}

trtcRoomContext.on(trtcRoomContext.EVENT.REMOTE_AUDIO_REMOVE, onRemoteAudioRemove)
```

### switchCamera()
**Note:**

This API is used to switch between local front and rear cameras.

**Parameters:**

None

**Returned value:**

None

**Sample code:**
```
trtcRoomContext.switchCamera()
```

### getRemoteUserList()
**Note:**

This API is used to get the remote user list.

**Parameters:**

None

**Returned value:**

Array[Object]

**Sample code:**
```
let userList = trtcRoomContext.getRemoteUserList()
// Sample data format
// userList = [
//   {
//     userID:'xxx',       // User ID 
//     hasMainVideo: true, // Whether the user has a primary video stream
//     hasMainAudio: true, // Whether the user has a primary audio stream
//     hasAuxVideo: false  // Whether the user has a video substream (screen sharing)
//   }
//   ...
// ]
```

### enterFullscreen(params)
**Note:**

This API is used to enable full-screen playback for remote video. Playback in full screen mode is generally suitable for the substream (screen sharing) image.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:----------------------------------------------------------------|
| userID     | String | -      | User ID, which is required. |
| streamType | String | -     | Stream type, which is required. Valid values: <li>main: primary stream.</li> <li>aux: substream (screen sharing).</li>|

**Returned value:**

Promise

**Sample code:**

```javascript
trtcRoomContext.enterFullscreen({
  userID: 'xxx',
  streamType: 'main'
}).then((event)=>{
  // Enabled full screen mode successfully
}).catch((event)=>{
  // Failed to enable full screen mode
})
```

### exitFullscreen(params)

**Note:**

This API is used to cancel the full screen mode for a remote video.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:----------------------------------------------------------------|
| userID     | String | -      | User ID, which is required. |
| streamType | String | -      | Stream type, which is required. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li>|

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.exitFullscreen({
  userID: 'xxx',
  streamType: 'main'
}).then((event)=>{
  // Exited full screen mode successfully
}).catch((event)=>{
  // Failed to exit full screen mode
})
```

### setViewOrientation(params)
**Note:**

This API is used to set the display orientation of a specified remote image.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:------------|:-------|:-------|:------------------------------------------------------------------|
| userID      | String | -      | Remote user ID, which is required. |
| streamType  | String | -      | Remote user stream type, which is required. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li> |
| orientation | String | -      | Image orientation, which is required. Valid values: vertical, horizontal.                    |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.setViewOrientation({
  userID: 'xxx',
  streamType: 'main',
  orientation: 'vertical'
}).then((event)=>{
  // Set successfully
})
```

### setViewFillMode(params)
**Note:**

This API is used to set the filling mode of a specified remote image.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:-----------------------------------------------------|
| userID     | String | -      | Remote user ID, which is required. |
| streamType | String | -      | Remote user stream type, which is required. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li> |
| fillMode   | String | -      | Filling mode, which is required. Valid values:<li>contain: fit mode (the complete video image can be displayed, but black bars may exist).</li><li>fillCrop: fill mode (the entire screen is covered by the video image, but the image may be cropped).</li> |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.setViewFillMode({
  userID: 'xxx',
  streamType: 'main',
  fillMode: 'contain'
}).then((event)=>{
  // Set successfully
})
```

### setViewVisible(params)
**Note:**
This API is used to display or hide the image of a specified video stream.
>!This method takes effect only if `template:"custom"` is configured.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:--------|:-------|:------------------------------------------------------------------|
| userID     | String  | -      | User ID, which is required. |
| streamType | String  | -      | Remote user stream type, which is required when the remote user is set. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li> |
| isVisible  | Boolean | -      | Whether to display the view, which is required. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.setViewVisible({
  userID: 'xxx',
  streamType: 'main',
  isVisible: true
}).then((event)=>{
  // Set successfully
})
```

### setViewRect(params)
**Note:**

This API is used to set the coordinates and size of a specified video image.
>!This method takes effect only if `template:"custom"` is configured.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:------------------------------------------------------------------|
| userID     | String | -      | User ID, which is required. |
| streamType | String | -      | Remote user stream type, which is required when the remote user is set. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li> |
| xAxis      | String | -      | View horizontal coordinate, which is optional. |
| yAxis      | String | -      | View vertical coordinate, which is optional. |
| width      | String | -      | View width, which is optional. |
| height     | String | -      | View height, which is optional. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.setViewRect({
  userID: 'xxx',
  streamType: 'main',
  xAxis: '480rpx',
  yAxis: '160rpx',
  width: '240rpx',
  height: '320rpx',
}).then((event)=>{
  // Set successfully
})
```

### setViewZIndex(params)
**Note:**

This API is used to set the layer of a specified video image.
>!
>- This method takes effect only if `template:"custom"` is configured.
>- This method takes effect only in same-layer mode of WeChat Mini Program. WeChat v7.0.8 and above supports the same-layer mode.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:------------------------------------------------------------------|
| userID     | String | -      | User ID, which is required. |
| streamType | String | -      | Remote user stream type, which is required when the remote user is set. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li> |
| zIndex     | Number | -      | View layer, which is an integer and required. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.setViewZIndex({
  userID: 'xxx',
  streamType: 'main',
  zIndex: 10
}).then((event)=>{
  // Set successfully
})
```

### playBGM(params)
**Note:**

This API is used to play back background music. The background music will be mixed with the voice captured by the mic and published to the cloud together, which is called "background audio mix".

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-------|:-------|:-------|:------------------------------------------------|
| url    | String | -      | Background music playback address. Only online MP3 and AAC music files over the HTTPS protocol are supported. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.playBGM({
  url: 'https://a.xxx.com/bgm.mp3' 
}).then(()=>{
    // Playback succeeded
}).catch(()=>{
    // Playback failed
})
```

### stopBGM()
**Note:**

This API is used to stop background music.

**Parameters:**

None

**Returned value:**

None

**Sample code:**
```
trtcRoomContext.stopBGM()
```

### pauseBGM()
**Note:**

This API is used to pause background music.

**Parameters:**

None

**Returned value:**

None

**Sample code:**
```
trtcRoomContext.pauseBGM()
```

### resumeBGM()
**Note:**

This API is used to resume background music.

**Parameters:**

None

**Returned value:**

None

**Sample code:**
```
trtcRoomContext.resumeBGM()
```

### setBGMVolume(params)
**Note:**

This API is used to set the volume level of the background music in audio mix.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-------|:-------|:-------|:--------------------|
| volume | number | -      | Volume level. Value range: 0–1. |

**Returned value:**

None

**Sample code:**
```
trtcRoomContext.setBGMVolume({
  volume: 0.5
})
```

### setMICVolume(params)
**Note:**

This API is used to set the mic capturing volume level in audio mix.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-------|:-------|:-------|:--------------------|
| volume | number | -      | Volume level. Value range: 0–1. |

**Returned value:**

None

**Sample code:**
```
trtcRoomContext.setMICVolume({
  volume: 0.5
})
```

### snapshot(params)
**Note:**

This API is used to capture the specified remote or local video image and save it into the system album.

**Parameters:**

| Parameter | Type | Default Value | Description |
|:-----------|:-------|:-------|:----------------------------------------------------------------|
| userID     | String | -      | User ID, which is required. |
| streamType | String | -      |  Stream type, which is required. Valid values: <li>main: primary stream.</li><li>aux: substream (screen sharing).</li>Only the `main` type is supported for local video streams. |

**Returned value:**

None

**Sample code:**
```
// Capture the video image of a remote user
trtcRoomContext.snapshot({
  userID: 'xxx',            // Remote user ID
  streamType: 'main'        // Remote user stream type
}).then((event)=>{
  // Screencaptured successfully
})

// Capture the video image of a local user
trtcRoomContext.snapshot({
  userID: 'xxx',            // Local user ID
  streamType: 'main'        // Only the `main` type (primary stream) is supported for local user streams 
}).then((event)=>{
  // Screencaptured successfully
})
```

### sendC2CTextMessage(params)
**Note:**

This API is used to send a C2C text message (i.e., sending a message to a specified user). It takes effect only after you activate the [IM](https://intl.cloud.tencent.com/product/im) service and set `enableIM` to `true` in the [attribute table](#Config).

**Parameters:**

| Parameter | Type | Default Value | Description |
|:--------|:-------|:-------|:-----------------------|
| userID  | String | -      | Message recipient ID, which is required. |
| message | String | -      | Text message to be sent, which is required. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.sendC2CTextMessage({
  userID: 'xxx',
  message: 'Hello!'
})
```


### sendC2CCustomMessage(params)
**Note:**

This API is used to send a C2C custom message. A custom message can be used to send control signaling (such as invitation to speak and application for mic-on).
This API takes effect only after you activate the [IM](https://intl.cloud.tencent.com/product/im) service and set `enableIM` to `true` in the [attribute table](#Config).

**Parameters:**

| Parameter | Type | Default Value | Description |
|:--------|:-------|:-------|:--------------------|
| userID  | String | -      | Message recipient ID, which is required. |
| payload | Object | -      | Custom message payload, which is required. |

`payload` supports three parameters:

| Parameter | Type | Default Value | Description |
|:------------|:-------|:-------|:-------------------|
| data        | String | -      | Custom message data. |
| description | String | -      |  Custom message description. |
| extension   | String | -      | Extended field of custom message. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.sendC2CCustomMessage({
  userID: 'xxx',
  payload: {
    data: 'custom message data',
    description: 'custom message description',
    extension: 'extended field of custom message'
  } 
})
```

### sendGroupTextMessage(params)
**Note:**

This API is used to send a group text message. It takes effect only after you activate the [IM](https://intl.cloud.tencent.com/product/im) service and set `enableIM` to `true` in the [attribute table](#Config).

**Parameters:**

| Parameter | Type | Default Value | Description |
|:--------|:-------|:-------|:-----------------------|
| roomID  | Number | -      | Room ID, which is required. |
| message | String | -      | Text message to be sent, which is required. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.sendGroupTextMessage({
  roomID: 'xxx', // Room ID
  message: 'Hello!'
})
```


### sendGroupCustomMessage(params)
**Note:**

This API is used to send a group custom message. It takes effect only after you activate the [IM](https://intl.cloud.tencent.com/product/im) service and set `enableIM` to `true` in the [attribute table](#Config).

**Parameters:**

| Parameter | Type | Default Value | Description |
|:--------|:-------|:-------|:--------------------|
| roomID  | Number | -      | Room ID, which is required. |
| payload | Object | -      | Custom message payload, which is required. |

`payload` supports three parameters:

| Parameter | Type | Default Value | Description |
|:------------|:-------|:-------|:-------------------|
| data        | String | -      | Custom message data. |
| description | String | -      |  Custom message description. |
| extension   | String | -      | Extended field of custom message. |

**Returned value:**

Promise

**Sample code:**
```
trtcRoomContext.sendGroupCustomMessage({
  roomID: 'xxx', // Room ID
  payload: {
    data: 'custom message data',
    description: 'custom message description',
    extension: 'extended field of custom message'
  }
})
```

<h2 id="Event">Event Table</h2>

You can get event constant fields through the component instance's `EVENT` attribute; for example:

```
let EVENT = trtcRoomContext.EVENT
trtcRoomContext.on(EVENT.REMOTE_VIDEO_ADD,(event)=>{
    // A remote video stream was added. This notification will be received when a remote user publishes a video stream
})

// Receive an IM message
trtcRoomContext.on(EVENT.IM_MESSAGE_RECEIVED,(event)=>{
  let messageEvent = event.data
  // A newly pushed one-to-one chat, group chat, group reminder, or group system notification message was received. The message list data can be obtained and rendered onto the page through traversal of `messageEvent.data`
  // messageEvent.data: array storing `Message` objects
})
```
| Code | Description |
|----------------------------|----------------------------------------------------------|
| LOCAL_JOIN                 | Entered room successfully |
| LOCAL_LEAVE                | Exited room successfully |
| REMOTE_USER_JOIN           | A remote user entered the room |
| REMOTE_USER_LEAVE          | A remote user exited the room |
| REMOTE_VIDEO_ADD           | A remote video stream was added. This notification will be received when a remote user publishes a video stream |
| REMOTE_VIDEO_REMOVE        | A remote video stream was removed. This notification will be received when a remote user cancels video stream release |
| REMOTE_AUDIO_ADD           | A remote audio stream was added. This notification will be received when a remote user publishes an audio stream |
| REMOTE_AUDIO_REMOVE        | A remote audio stream was removed. This notification will be received when a remote user cancels audio stream release |
| REMOTE_STATE_UPDATE        | The remote user playback status changed |
| LOCAL_AUDIO_VOLUME_UPDATE  | Local volume changed                      |
| LOCAL_NET_STATE_UPDATE     | The local push network status changed |
| REMOTE_NET_STATE_UPDATE    | The remote user network status changed |
| REMOTE_AUDIO_VOLUME_UPDATE | The remote user volume level changed |
| VIDEO_FULLSCREEN_UPDATE    | The remote view full-screen status changed |
| BGM_PLAY_PROGRESS          | Background music playback timestamp changed |
| BGM_PLAY_COMPLETE          | Background music ended |
| ERROR                      | A local push error, rendering error, or error in other types occurred |
| IM_READY                   | IM is ready. You can send and receive messages after receiving this notification |
| IM_MESSAGE_RECEIVED        | An IM message was received. For more information, please see [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) |
| IM_NOT_READY               | IM is not ready. You cannot send or receive messages after receiving this notification |
| IM_ERROR                   | An IM error occurred. For more information, please see [Error Codes](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#%E9%94%99%E8%AF%AF%E7%A0%81%E5%AF%B9%E7%85%A7%E8%A1%A8) |                                            |

## Error Codes
A response error code will be returned when the `ERROR` event is triggered, and an error code is as described below:
```
let EVENT = trtcRoomContext.EVENT
trtcRoomContext.on(EVENT.ERROR,(event)=>{
  console.log(event.data.code)
})
```
