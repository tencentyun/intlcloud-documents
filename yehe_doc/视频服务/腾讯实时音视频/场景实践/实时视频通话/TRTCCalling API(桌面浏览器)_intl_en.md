## TRTCCalling Overview

The [TRTCCalling](https://www.npmjs.com/package/trtc-calling-js) component is based on Tencent Cloud Real-Time Communication (TRTC) and Instant Message (IM). It supports one-to-one and group video/audio calls. For detailed instructions how to implement it, see [Real-Time Video Call (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/38927).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647) is used as the low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047) is used to send and process signaling messages.

## TRTCCalling APIs 

#### Event subscribing/Subscription cancelling APIs 

This component bases its management on the dispatching of events. The application layer can perform different actions in response to dispatched events.

| API                                                          | Description                                                         |
| --------------------------------------------------------------------------- | ------------ |
| [on(eventName, callback, context)](#on(eventname.2C-callback.2C-context))   | Subscribes to an event.     |
| [off(eventName, callback, context)](#off(eventname.2C-callback.2C-context)) | Cancels a subscription. |

### Basic SDK APIs

| API                                                          | Description                                                         |
| ----------------------------------------------------------- | ---------------------------------------------- |
| [login({userID, userSig})](#login(.7Buserid.2C-usersig.7D)) | Logs in to IM. All features can be used only after login. |
| [logout()](#logout())                                       | Logs out. No calls can be made after logout.            |

#### Call operation APIs

| API                                                          | Description                                                         |
| ----------------------------------------------------------------------------------------- | ------------ |
| [call({userID, type, timeout}))](#call(.7Buserid.2C-type.2C-timeout.7D))               | Makes a one-to-one call. |
| [groupCall({userIDList, type, groupID})](#groupcall(.7Buseridlist.2C-type.2C-groupid.7D)) | Makes a group call. |
| [accept({inviteID, roomID, callType})](#accept(.7Binviteid.2C-roomid.2C-calltype.7D))      | Answers a call. |
| [reject({inviteID, isBusy, callType})](#reject(.7Binviteid.2C-isbusy.2C-calltype.7D))      | Rejects a call. |
| [hangup()](#hangup())                                                                     | Hangs up. |

#### Video control APIs

| API                                                          | Description                                                         |
| --------------------------------------------------------------------------------------------- | ------------------ |
| [startRemoteView({userID, videoViewDomID})](#startremoteview(.7Buserid.2C-videoviewdomid.7D)) | Starts rendering the image of a remote user.   |
| [stopRemoteView({userID, videoViewDomID})](#stopremoteview(.7Buserid.2C-videoviewdomid.7D))  | Stops rendering the image of a remote user.   |
| [startLocalView({userID, videoViewDomID})](#startlocalview(.7Buserid.2C-videoviewdomid.7D))  | Starts rendering the image of the local user.   |
| [stopLocalView({userID, videoViewDomID})](#stoplocalview(.7Buserid.2C-videoviewdomid.7D))    | Stops rendering the image of the local user.   |
| [openCamera()](#opencamera())                                                                 | Enables the camera.         |
| [closeCamera()](#closecamera())                                                               | Disables the camera.         |
| [setMicMute(isMute)](#setmicmute(ismute))                                                     | Mutes or unmutes the mic. |


## Closer Look at TRTCCalling

### Creating a TRTCCalling instance

First， create an application in the [TRTC console](https://console.cloud.tencent.com/trtc/app) and get the SDKAppID.
Then, obtain an instance of the TRTCCalling component using `new TRTCCalling()`.

```plaintext
let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting.
};
let trtcCalling = new TRTCCalling(options);
```

### Event subscribing/Subscription cancelling APIs 




#### on(eventName, callback, context)

This API is used to listen for events dispatched by the component. For details about the events, see the [event list](#event).

```plaintext
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
```




#### off(eventName, callback, context)

This API is used to stop listening for events.

```plaintext
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
```

### Basic SDK APIs

#### login({userID, userSig})

This API is used to log in.

```plaintext
trtcCalling.login({userID, userSig})
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| userID | String | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For how to calculate userSig, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |




#### logout()

 This API is used to log out.

```plaintext
trtcCalling.logout()
```

### Call operation APIs




#### call({userID, type, timeout})

This API is used to make one-to-one calls. Type is the type of a call. 1: audio call; 2: video call.

```plaintext
trtcCalling.call({userID, type, timeout})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------------ |
| userID  | String | User ID of the invitee          |
| type    | Number | 1: audio call; 2: video call |
| timeout | Number | In seconds; 0 means no timeout threshold set.  |



#### groupCall({userIDList, type, groupID})
The `groupID` parameter is the group ID in the IM SDK. If this parameter is set, the call invitation will be broadcast by the group messaging system, which is a simple and reliable way of sending call invitations. If this parameter is left empty, the TRTCCalling component will send an invitation to every invitee.

```plaintext
trtcCalling.groupCall({userIDList, type, groupID})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | ------------------------ |
| userIDList | Array  | List of the user IDs of invitees                 |
| type       | Number | 1: audio call; 2: video call |
| groupID    | String | ID of the IM group (optional)      |




#### accept({inviteID, roomID, callType})
This API is used to accept an incoming invitation.
>? If an invitation has yet to be processed, the component will return a message saying that the line is busy to other invitations sent to the same user.

```plaintext
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TrtcCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.accept({inviteID, roomID, callType})
})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------ | ------------------------ |
| inviteID | String | Invitation ID, which identifies an invitation |
| roomID   | Number | Room ID            |
| callType | Number  | 1: audio call; 2: video call |



#### reject({inviteID, isBusy, callType})
This API is used to reject an incoming invitation.

```plaintext
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TrtcCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.reject({inviteID, isBusy, callType})
})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------- | ------------------------ |
| inviteID | String | Invitation ID, which identifies an invitation |
| isBusy   | Boolean | Whether the line is busy             |
| callType | Number  | 1: audio call; 2: video call |


#### hangup()
1. If you are in a call, you can use this API to end the current call.
2. If your call is not answered yet, you can use this API to cancel the call.

```plaintext
trtcCalling.hangup()
```


### Video control APIs
#### startRemoteView({userID, videoViewDomID})
This API is used to render the camera data of a remote user to a specified DOM ID node.

```plaintext
trtcCalling.startRemoteView({userID, videoViewDomID})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------ | --------------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | Plays the data of the user via the video tag rendered to the DOM ID node. |

#### stopRemoteView({userID, videoViewDomID})
This API is used to delete the DOM node to which the camera data of a remote user is rendered.

```plaintext
trtcCalling.stopRemoteView({userID, videoViewDomID})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------ | ------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | Deletes the video tag of the DOM ID node, and stops video playback. |

#### startLocalView({userID, videoViewDomID})
This API is used to render the camera data of the local user to a specified DOM ID node.

```plaintext
trtcCalling.startLocalView({userID, videoViewDomID})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------ | ----------------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | Plays the data of the local user via the video tag rendered to the DOM ID node. |

#### stopLocalView({userID, videoViewDomID})

This API is used to delete the DOM node to which the camera data of the local user is rendered.

```plaintext
trtcCalling.stopLocalView({userID, videoViewDomID})
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------ | ------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | Deletes the video tag of the DOM ID node, and stops video playback. |

#### openCamera()
This API is used enable the local camera.

```plaintext
trtcCalling.openCamera()
```

#### closeCamera()
This API is used to disable the camera.

```plaintext
trtcCalling.closeCamera()
```

####  setMicMute(isMute) 
This API is used to enable/disable the mic.

```plaintext
trtcCalling.setMicMute(true) // Enables the mic.
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | -------------------------------------------- |
| isMute | Boolean | <li/>true: the mic is disabled. <li/>false: the mic is enabled. |


[](id:event)
## TRTCCalling Events

You can use the code below to capture different events from the TRTCCalling component.

```plaintext
import TRTCCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TrtcCalling.EVENT.REJECT, handleInviteeReject)
```

### Inviter events

|                     Code                      |   Event Receiver   |           Description            |
| :-------------------------------------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     Inviter     |     The invitee rejected the call.      |
|       [NO_RESP](#no_resp)        |     Inviter     |    The timeout threshold is reached without response from the invitee.      |
|      [LINE_BUSY](#line_busy)       |     Inviter     | The invitee is in a call; the line is busy. |
|       [INVITED](#invited)        |     Invitee     |      You have received an invitation.       |
|    [CALLING_CANCEL](#calling_cancel)    |     Invitee     |     The call is cancelled.      |
|   [CALLING_TIMEOUT](#calling_timeout)    |     Invitee     |    The timeout threshold is reached.     |
|      [USER_ENTER](#user_enter)      | Inviter and invitee |         A user entered the room.          |
|      [USER_LEAVE](#user_leave)      | Inviter and invitee |       A user exited the room.        |
|       [CALL_END](#call_end)       | Inviter and invitee |       The call ended.        |
|      [KICKED_OUT](#kicked_out)      | Inviter and invitee |   A user was kicked out due to repeated login.    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | Inviter and invitee | A remote user enabled/disabled the camera. |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | Inviter and invitee | A remote user enabled/disabled the mic. |

### General event callbacks

#### USER_ENTER

A user entered the room.

```plaintext
function handleUserEnter({userID}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userId | String | User ID |

#### USER_LEAVE

A user exited the room.

```plaintext
function handleUserLeave({userID}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userId | String | User ID |

#### CALL_END

The call ended.

```plaintext
function handleCallEnd() {

}
```

#### KICKED_OUT

A user was kicked out for repeated login.

```plaintext
function handleKickedOut() {

}
```

#### USER_VIDEO_AVAILABLE

A remote user enabled/disabled the camera.

```plaintext
function handleUserVideoChange({userID, isVideoAvailable}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------- | ----------------------------------------------------------- |
| userID | String | User ID |
| isAudioAvailable | Boolean | <li/>true: a remote user enabled the camera. <li/> false: a remote user disabled the camera. |

#### USER_AUDIO_AVAILABLE

A remote user enabled/disabled the mic.

```plaintext
function handleUserAudioChange({userID, isAudioAvailable}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------- | ------------------------------------------------------------- |
| userID | String | User ID |
| isAudioAvailable | Boolean | <li/>true: a remote user enabled the mic. <li/> false: a remote user disabled the mic. |

### Inviter event callbacks

### reject

The user rejected the call.

```plaintext
function handleInviteeReject({userID}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userId | String | User ID |

#### NO_RESP

The invitee did not answer.

```plaintext
function handleNoResponse({userID, userIDList}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userId | String | User ID |
| userIDList | Array  | Timed-out user list |

#### LINE_BUSY

The invitee is in a call. The line is busy.

```plaintext
function handleInviteeLineBusy({userID}) {

}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userId | String | User ID |

### Invitee event callbacks

#### INVITED
You have received an invitation.

```plaintext
function handleNewInvitationReceived({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {

}
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| sponsor     | String  | Inviter                                                                                                    |
| userIDList  | Array   | Users invited to the same call                                                                                          |
| isFromGroup | Boolean | Whether it is an IM group invitation                                             |
| inviteData  | Object  | <li/>For a new user invitation: {version, callType, roomID} <li/> For the last user hanging up: {version, callType, callEnd} |
| inviteID    | String  | Invitation ID, which identifies an invitation                                        |

#### CALLING_CANCEL

The call is cancelled.

```plaintext
function handleInviterCancel() {

}
```

#### CALLING_TIMEOUT

The timeout threshold is reached.

```plaintext
function handleCallTimeout() {

}
```

## TRTCCalling Error Codes

You can handle the errors thrown by the TRTCCalling component by listening for the “error” field in events. Below is an example code.

```plaintext
import TRTCCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error);
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
```

## FAQs

#### Why can’t I get through to the invitee? Why am I kicked offline?
The TRTCCalling component does not support login of multiple instances or **offline signaling** for the time being. Please check that your current login is unique.
> ?
> - **Multiple instances**: a user ID logs in multiple times or on different devices, which disrupts signaling.
> - *Offline signaling*: only online instances can receive a message. Messages sent to offline instances will not be sent again when the instances go online.
