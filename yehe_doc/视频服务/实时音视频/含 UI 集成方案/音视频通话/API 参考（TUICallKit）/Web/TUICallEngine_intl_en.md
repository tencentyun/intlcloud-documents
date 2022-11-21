## TUICallEngine APIs

`TUICallEngine` is an audio/video call component that **does not include UI elements**.

## Overview

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance)                            | Creates a `TUICallEngine` instance (singleton mode). |
| [destroyInstance](#destroyinstance)                          | Terminates a `TUICallEngine` instance (singleton mode). |
| [on](#on) | Listens for events.                            |
| [off](#off) | Stops listening for events.                        |
| [login](#login) | Logs in.                            |
| [logout](#logout) | Logs out.                   |
| [setSelfInfo](#setselfInfo) | Sets the alias and profile photo.                  |
| [call](#call) | Makes a one-to-one call.                         |
| [groupCall](#groupcall) | Makes a group call.                        |
| [accept](#accept) | Accepts a call. |
| [reject](#reject) | Rejects a call. |
| [hangup](#hangup) | Ends a call.                            |
| [switchCallMediaType](#switchcallmediatype) | Changes the call type.                    |
| [startRemoteView](#startremoteview) | Starts rendering a remote video.                    |
| [stopRemoteView](#stopremoteview) | Stops rendering a remote video.                    |
| [startLocalView](#startlocalview) | Starts rendering the local video.                    |
| [stopLocalView](#stoplocalview) | Stops rendering the local video.                    |
| [openCamera](#opencamera) | Turns the camera on.                          |
| [closeCamara](#closecamara) | Turns the camera off.                          |
| [openMicrophone](#openmicrophone) | Turns the mic on.                          |
| [closeMicrophone](#closemicrophone) | Turns the mic off.                          |
| [setVideoQuality](#setvideoquality) | Sets the video quality.                        |
| [getDeviceList](#getdevicelist) | Gets the device list.                        |
| [switchDevice](#switchdevice) | Changes to a different camera/mic.              |

## Details

### createInstance

This API is used to create a `TUICallEngine` singleton.



```swift
const tuiCallEngine = TUICallEngine.createInstance({
    SDKAppID: 0 // Replace 0 with the SDKAppID of your IM application.
    // If you already have TIM instances, you can use this parameter to guarantee the uniqueness of a TIM instance.
});
```

**The parameters are described below:**

| Parameter        | Type    | Description                                                                                                      |
| -------- | ------ | --------------------- |
| SDKAppID | Number | The SDKAppID of the IM application.                                        |
|. tim      | Any    | The TIM instance (optional).      |

### destroyInstance

This API is used to terminate a `TUICallEngine` singleton.



```swift
tuiCallEngine.destroyInstance().then(() => {
    //success
.catch(error => {
    console.warn('destroyInstance error:', error);
});
```

### on

This API is used to listen for events.



```swift
let onError = function(error) {
    console.log(error);
};
tuiCallEngine.on(TUICallEvent.ERROR, onError, this);
```

**The parameters are described below:**

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------- | ---------------------------- |
| eventName | String   | The event name.                       |
| callback  | function | The event callback.                 |
| context   | Any      | The context. |

### off

This API is used to stop listening for events.



```swift
let onError = function(error) {
    console.log(error);
};
tuiCallEngine.off(TUICallEvent.ERROR, onError, this);
```

**The parameters are described below:**

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------- | ---------------------------- |
| eventName | String   | The event name.                       |
| callback  | function | The event callback.                 |
| context   | Any      | The context. |

### login

This API is used to log in.



```swift
let promise = tuiCallEngine.login({userID: 'your userID', userSig: 'your userSig'});
promise.then(() => {
    //success
.catch(error => {
    console.warn('login error:', error);
});
```

**The parameters are described below:**

| Parameter       | Type                            | Description  |
| ------- | ------ | ------------------------------------------------------------ |
| userID | String | The ID of the current user, which is a string that can contain only letters (a-z and A-Z), numbers (0-9), hyphens (-), and underscores (_). |
| userSig | String | Tencent Cloud's proprietary security signature. For details, see [How do I calculate UserSig](https://www.tencentcloud.com/document/product/647/35166). |

### logout

This API is used to log out.



```swift
let promise = tuiCallEngine.logout();
promise.then(() => {
    //success
.catch(error => {
    console.warn('logout error:', error);
});
```

### setSelfInfo

This API is used to set the alias and profile photo.



```swift
let promise = tuiCallEngine.setSelfInfo({
    nickName: 'video', 
    avatar:'http(s)://url/to/image.jpg'
});
promise.then(() => {
    //success
.catch(error => {
    console.warn('setSelfInfo error:', error);
});
```

**The parameters are described below:**

| Parameter | Type | Description |
| -------- | ------ | -------- |
| nickName | String | The alias.     |
| avatar | String | The URL of the profile photo. |

### call

This API is used to make a one-to-one call. The invitee will receive the `TUICallEvent.INVITED` callback.

>! Offline notifications are supported for Android and iOS. It’s not supported for web.



```javascript
let promise = tuiCallEngine.call({
    userID: 'user1', 
    type: 1, 
});
promise.then(() => {
    //success
.catch(error => {
    console.warn('call error:', error);
});
```

**The parameters are described below:**

| Parameter       | Type                            | Description  |
| ------ | ------ | ------------------------------- |
| userID  | String | The user ID of the invitee.          |
| type   | Number | The call type. 0: Unknown; 1: Audio call; 2: Video call. |

### groupCall

This API is used to make a group call. The invitees will receive the `EVENT.INVITED` callback.

>! Offline notifications are supported for Android and iOS. It’s not supported for web.



```javascript
let promise = tuiCallEngine.groupCall({
    userIDList: ['user1', 'user2'], 
    type: 1, 
    groupID: 'IM group ID', 
});
promise.then(() => {
    //success
.catch(error => {
    console.warn('groupCall error:', error);
});
```

**The parameters are described below:**

| Parameter        | Type    | Description                                                                                                      |
| ------------------------------------------------------------ | ------ | ------------------------------------------------------- |
| userIDList                                                   | Array  | The IDs of the users to call.                                                |
| type                                                         | Number | 0: Unknown; 1: Audio call; 2: Video call.                         |
| groupID                                                      | String | The IM group ID.                                                 |
| timeout                                                      | String | The timeout period (optional).                                          |
| roomID                                                       | String | The room ID (optional).                                          |
| [offlinePushInfo](#offlinePushInfo) | Object | A custom offline notification. This parameter is optional and is valid only on tsignaling 0.8.0 or later. |

#### offlinePushInfo

| Parameter    | Type   | Description                                                                                                                    |
| -------------------- | ------ | ------------------------------------------------------- |
| title                | String | The title of the offline notification (optional).                                   |
| description          | String | The content of the offline notification (optional).                                    |
| androidOPPOChannelID | String | The channel ID for the offline notification on OPPO 8.0 or later (optional). |
| extension            | string | The pass-through content. This parameter is optional and is valid only on tsignaling 0.9.0 or later.    |

### accept

This API is used to accept the call after you receive the `TUICallEvent.INVITED` callback.



```javascript
tuiCallEngine.on(TUICallEvent.INVITED, () => {
    tuiCallEngine.accept().promise.then(() => {
        //success
    .catch(error => {
        console.warn('accept error:', error);
    });
});
```

### reject

This API is used to reject the call after you receive the `TUICallEvent.INVITED` callback.



```javascript
tuiCallEngine.on(TUICallEvent.INVITED, () => {
    tuiCallEngine.reject().then(() => {
        //success
    .catch(error => {
        console.warn('reject error:', error);
    });
});
```

### hangup

This API is used to end a call.

If you are in a call, this API hangs up the call.

If a call is not answered yet, this API cancels the call.



```javascript
tuiCallEngine.hangup().then(() => {
     //success
 .catch(error => {
        console.warn('hangup error:', error);
 });
```

### switchCallMediaType

This API is used to change the call type.

This API only works for a one-to-one call.

The 60001 error callback indicates that the switch failed.



```javascript
// 1: Audio call; 2: Video call.
tuiCallEngine.switchCallMediaType(2).then(() => {
  //success
.catch(error => {
  console.warn('switchCallMediaType error:', error);
});
```

**The parameters are described below:**

| Parameter | Type | Description |
| ------------ | ------ | ---------------------- |
| newMediaType | Number | 1: Audio call; 2: Video call. |

### startRemoteView

This API is used to start rendering a remote video.



```javascript
let promise = tuiCallEngine.startRemoteView({
    userID: 'user1', 
    videoViewDomID: 'video_1',
});
promise.then(() => {
    //success
.catch(error => {
    console.warn('startRemoteView error:', error);
});
```

**The parameters are described below:**

| Parameter       | Type                            | Description  |
| -------------- | ------ | ---------------------------------- |
| userID | String | The user ID. |
| videoViewDomID | String | The user’s data will be rendered in this DOM node. |

### stopRemoteView

This API is used to stop rendering a remote video.



```javascript
tuiCallEngine.stopRemoteView({userID: 'user1'});
```

**The parameters are described below:**

| Parameter | Type | Description |
| ------ | ------ | ------ |
| userID | String | The user ID. |

### startLocalView

This API is used to start rendering the local video.



```javascript
let promise = tuiCallEngine.startLocalView({
    userID: 'user1', 
    videoViewDomID: 'video_1'
});
promise.then(() => {
    //success
.catch(error => {
    console.warn('startLocalView error:', error);
});
```

**The parameters are described below:**

| Parameter       | Type                            | Description  |
| -------------- | ------ | ---------------------------------- |
| userID | String | The user ID. |
| videoViewDomID | String | The data will be rendered in this DOM node. |

### stopLocalView

This API is used to stop rendering the local video.



```javascript
let promise = tuiCallEngine.stopLocalView({userID: 'user1'});
promise.then(() => {
    //success
.catch(error => {
    console.warn('stopLocalView error:', error)
});
```

**The parameters are described below:**

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userID | String | The user ID. |

### openCamera

This API is used to turn the camera on.



```javascript
tuiCallEngine.openCamera().then(() => {
    //success
.catch(error => {
    console.warn('openCamera error:', error);
});
```

### closeCamara

This API is used to turn the camera off.



```javascript
tuiCallEngine.closeCamera().then(() => {
    //success
.catch(error => {
    console.warn('closeCamara error:', error);
});
```

### openMicrophone

This API is used to turn the mic on.



```javascript
tuiCallEngine.openMicrophone().then(() => {
    //success
.catch(error => {
    console.warn('openMicrophone error:', error);
});
```

### closeMicrophone

This API is used to turn the mic off.



```javascript
tuiCallEngine.closeMicrophone().then(() => {
    //success
.catch(error => {
    console.warn('closeMicrophone error:', error);
});
```

### setVideoQuality

This API is used to set the video quality.



```javascript
const profile = '720p';
tuiCallEngine.setVideoQuality(profile).then(() => {
    //success
.catch(error => {
    console.warn('setVideoQuality error:', error)
});    // Set the video quality to 720p     
```

**The parameters are described below:**

| Video Profile | Resolution (Width x Height) |
| ------------ | ----------------- |
| 480p         | 640 x 480         |
| 720p         | 1280 x 720        |
| 1080p        | 1920 x 1080       |

### getDeviceList

This API is used to get the device list.



```javascript
tuiCallEngine.getDeviceList("camera").then((devices) => {
    console.log(devices);
.catch(error => {
    console.warn('getDeviceList error:', error);
});
```

**The parameters are described below:**

| Parameter       | Type                            | Description  |
| ---------- | ------ | ------------------------------------- |
| deviceType | String | The device type. Valid values: `camera`, `microphones`. |

### switchDevice

This API is used to change to a different camera or mic.



```javascript
let promsie = tuiCallEngine.switchDevice({
    deviceType: 'video', 
    deviceId: cameras[0].deviceId
});
promise.then(() => {
    //success
.catch(error => {
    console.warn('switchDevice error:', error)
});
```

**The parameters are described below:**

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------ | ------------------------------------------------------------ |
| deviceType | String | The device type. `video`: Camera; `audio`: Mic.                                 |
| deviceId   | String | The ID of the device to change to. You can use `getCameras()` to get the ID of a camera and use `getMicrophones()` to get the ID of a mic. |

 
