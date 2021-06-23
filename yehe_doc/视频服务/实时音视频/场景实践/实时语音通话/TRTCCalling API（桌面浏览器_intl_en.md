## `TRTCCalling` Overview

The [TRTCCalling](https://www.npmjs.com/package/trtc-calling-js) component is based on Tencent Cloud Real-Time Communication (TRTC) and Instant Message (IM). It supports one-to-one and group video/audio calls. For detailed instructions how to implement it, see [Real-Time Audio Call (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/38928).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047) is used to send and process signaling messages.

## `TRTCCalling` APIs 

#### Event subscribing/unsubscribing APIs 
This component bases its management on the dispatching of events. The application layer can change UI interactions according to dispatched events.

| API                                                          | Description                                                         |
| --------------------------------------------------------------------------- | ------------ |
| [on(eventName, callback, context)](#on(eventname.2C-callback.2C-context))   | Subscribes to an event.     |
| [off(eventName, callback, context)](#off(eventname.2C-callback.2C-context)) | Unsubscribes from an event. |

### Basic SDK APIs

| API                                                          | Description                                                         |
| ----------------------------------------------------------- | ---------------------------------------------- |
| [login({userID, userSig})](#login(.7Buserid.2C-usersig.7D)) | Logs in to IM. All IM features can be used only after login. |
| [logout()](#logout())                                       | Logs out. No calls can be made after logout.            |

#### Call operation APIs
| API                                                          | Description                                                         |
| ----------------------------------------------------------------------------------------- | ------------ |
| [call({userID, type, timeout}))](#call(.7Buserid.2C-type.2C-timeout.7D))               | Makes a one-to-one call. |
| [groupCall({userIDList, type, groupID})](#groupcall(.7Buseridlist.2C-type.2C-groupid.7D)) | Makes a group call. |
| [accept({inviteID, roomID, callType})](#accept(.7Binviteid.2C-roomid.2C-calltype.7D))      | Accepts a call invitation. |
| [reject({inviteID, isBusy, callType})](#reject(.7Binviteid.2C-isbusy.2C-calltype.7D))      | Rejects a call invitation. |
| [hangup()](#hangup())                                                                     | Hangs up. |

#### Video APIs
| API                                                          | Description                                                         |
| --------------------------------------------------------------------------------------------- | ------------------ |
| [startRemoteView({userID, videoViewDomID})](#startremoteview(.7Buserid.2C-videoviewdomid.7D)) | Starts rendering the image of a remote user.   |
| [stopRemoteView({userID, videoViewDomID})](#stopremoteview(.7Buserid.2C-videoviewdomid.7D))  | Stops rendering the image of a remote user.   |
| [startLocalView({userID, videoViewDomID})](#startlocalview(.7Buserid.2C-videoviewdomid.7D))  | Starts rendering the image of the local user.   |
| [stopLocalView({userID, videoViewDomID})](#stoplocalview(.7Buserid.2C-videoviewdomid.7D))    | Stops rendering the image of the local user.   |
| [openCamera()](#opencamera())                                                                 | Turns on the camera.         |
| [closeCamera()](#closecamera())                                                               | Turns off the camera.         |
| [setMicMute(isMute)](#setmicmute(ismute))                                                     | Mutes/Unmutes the mic. |
| [setVideoQuality(profile)](#setvideoquality(profile)) | Sets video quality.|


## Closer Look at `TRTCCalling`

### Creating a `TRTCCalling` instance

First, create an application in the [TRTC console](https://console.cloud.tencent.com/trtc/app) and get the `SDKAppID`.
Then, obtain an instance of the `TRTCCalling` component using `new TRTCCalling()`.

<dx-codeblock>
::: javascript javascript
let options = {
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM application when connecting.
};
let trtcCalling = new TRTCCalling(options);
:::
</dx-codeblock>

### Event subscribing/unsubscribing APIs 



#### on(eventName, callback, context)
This API is used to subscribe to an event dispatched by the component. For details about the events, see the [event list](#event).

<dx-codeblock>
::: javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
:::
</dx-codeblock>



#### off(eventName, callback, context)
This API is used to unsubscribe from an event.

<dx-codeblock>
::: javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
:::
</dx-codeblock>

### Basic SDK APIs



#### login({userID, userSig})
This API is used to log in.

<dx-codeblock>
::: javascript javascript
trtcCalling.login({userID, userSig})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| userID | String | ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For how to calculate it, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |



#### logout()
 This API is used to log out.
<dx-codeblock>
::: javascript javascript
trtcCalling.logout()
:::
</dx-codeblock>

### Call operation APIs



#### call({userID, type, timeout})

This API is used to make one-to-one calls. `type` indicates the type of a call. `1`: audio call; `2`: video call.

<dx-codeblock>
::: javascript javascript
trtcCalling.call({userID, type, timeout})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ------------------------ |
| userID  | String | User ID of the invitee          |
| type    | Number | `1`: audio call; `2`: video call |
| timeout | Number | Timeout period in seconds. `0` means the call will never time out.  |



#### groupCall({userIDList, type, groupID})
The `groupID` parameter is the group ID in the IM SDK. If this parameter is set, call invitations will be broadcast by the group messaging system, which is a simple and reliable way of sending call invitations. If this parameter is left empty, the `TRTCCalling` component will send an invitation to every invitee.

<dx-codeblock>
::: javascript javascript
trtcCalling.groupCall({userIDList, type, groupID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------ | ------------------------ |
| userIDList | Array  | List of the user IDs of invitees                 |
| type       | Number | `1`: audio call; `2`: video call |
| groupID    | String | ID of the IM group (optional)      |


#### accept({inviteID, roomID, callType})
This API is used to accept an invitation.
>? If a prior invitation has not been processed, the component will return a message indicating that the line is busy.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.accept({inviteID, roomID, callType})
})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------ | ------------------------ |
| inviteID | String | Invitation ID, which identifies an invitation |
| roomID   | Number | Room ID            |
| callType | Number | `1`: audio call; `2`: video call |


#### reject({inviteID, isBusy, callType})
This API is used to reject an invitation.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.reject({inviteID, isBusy, callType})
})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------- | ------------------------ |
| inviteID | String | Invitation ID, which identifies an invitation |
| isBusy   | Boolean | Whether the line is busy             |
| callType | Number | `1`: audio call; `2`: video call |



#### hangup()
1. If you are in a call, you can use this API to end the call.
2. If your call is not answered yet, you can use this API to cancel the call.

<dx-codeblock>
::: javascript javascript
trtcCalling.hangup()
:::
</dx-codeblock>


### Video APIs


#### startRemoteView({userID, videoViewDomID})
This API is used to render the camera data of a remote user in a specified DOM node.
<dx-codeblock>
::: javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------ | --------------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | The DOM node in which the user’s data is to be rendered. The data will be played via the video tag of the node. |


#### stopRemoteView({userID, videoViewDomID})
This API is used to delete the DOM node in which the camera data of a remote user is rendered.
<dx-codeblock>
::: javascript javascript
trtcCalling.stopRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------------- | ------ | ------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | The DOM node whose video tag is to be deleted. The playback will stop. |


#### startLocalView({userID, videoViewDomID})
This API is used to render the camera data of the local user in a specified DOM node.
<dx-codeblock>
::: javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------ | ----------------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | The DOM node in which the local user’s data is to be rendered. The data will be played via the video tag of the node. |


#### stopLocalView({userID, videoViewDomID})
This API is used to delete the DOM node in which the camera data of the local user is rendered.
<dx-codeblock>
::: javascript javascript
trtcCalling.stopLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------------- | ------ | ------------------------------------------------- |
| UserID | String | User ID |
| videoViewDomID | String | The DOM node whose video tag is to be deleted. The playback will stop. |


#### openCamera()
This API is used to turn on the local camera.
<dx-codeblock>
::: javascript javascript
trtcCalling.openCamera()
:::
</dx-codeblock>


#### closeCamera()
This API is used to turn off the camera.
<dx-codeblock>
::: javascript javascript
trtcCalling.closeCamera()
:::
</dx-codeblock>


####  setMicMute(isMute) 
This API is used to turn on/off the mic.
<dx-codeblock>
::: javascript javascript
trtcCalling.setMicMute(true) // Turn on the mic
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------- | --------------------------------------------- |
| isMute | Boolean | <li/>`true`: turns off the mic. <li/>`false`: turns on the mic. |

####  setVideoQuality(profile) 
This API is used to set video quality.
>? 
>- This is a new API in v0.8.0 and later versions.
>- This API must be called before `call`, `groupCall`, and `accept` to take effect.

<dx-codeblock>
::: javascript javascript
trtcCalling.setVideoQuality('720p') // Set video quality to 720p
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------- | -------------------------------------------- |
| profile | String | <li/>`480p`: 640 x 480 <li/>`720p`: 1280 x 720  <li/>`1080p`: 1920 x 1080  |

[](id:event)
## `TRTCCalling` Events
The code below demonstrates how to listen for [TRTCCalling events](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/module-EVENT.html).

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject)
:::
</dx-codeblock>

### Inviter events
|                     Code                      |   Event Recipient   |           Description            |
| :-------------------------------------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     Inviter     |     The invitee rejected the call.      |
|       [NO_RESP](#no_resp)        |     Inviter     |    The invitation timed out without response from the invitee.      |
|      [LINE_BUSY](#line_busy)       |     Inviter     | The invitee is in a call, i.e., the line is busy. |
|       [INVITED](#invited)        |     Invitee     |      You received an invitation.       |
|    [CALLING_CANCEL](#calling_cancel)    |     Invitee     |     The call is cancelled.      |
|   [CALLING_TIMEOUT](#calling_timeout)    |     Invitee     |    The invitation timed out.     |
|      [USER_ENTER](#user_enter)      | Inviter and invitee |         A user entered the room.          |
|      [USER_LEAVE](#user_leave)      | Inviter and invitee |       A user left the room.        |
|       [CALL_END](#call_end)       | Inviter and invitee |       The call ended.        |
|      [KICKED_OUT](#kicked_out)      | Inviter and invitee |   A user was kicked out due to repeated login.    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | Inviter and invitee | A remote user turned on/off the camera. |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | Inviter and invitee | A remote user turned on/off the mic. |

### Common event callback APIs

#### USER_ENTER
A user entered the room.

<dx-codeblock>
::: javascript javascript
function handleUserEnter({userID}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------- |
| userID | String | User ID |

#### USER_LEAVE
A user left the room.

<dx-codeblock>
::: javascript javascript
function handleUserLeave({userID}) {

}
:::
</dx-codeblock>
The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------- |
| userID | String | User ID |

#### CALL_END
The call ended.

<dx-codeblock>
::: javascript javascript
function handleCallEnd() {

}
:::
</dx-codeblock>

#### KICKED_OUT
A user was kicked out due to repeated login.

<dx-codeblock>
::: javascript javascript
function handleKickedOut() {

}
:::
</dx-codeblock>

#### USER_VIDEO_AVAILABLE
A remote user turned on/off the camera.

<dx-codeblock>
::: javascript javascript
function handleUserVideoChange({userID, isVideoAvailable}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------- | ------------------------------------------------------------- |
| userID | String | User ID |
| isVideoAvailable | Boolean | <li/>`true`: the remote user turned on the camera.  <li/> `false`: the remote user turned off the camera. |

#### USER_AUDIO_AVAILABLE
A remote user turned on/off the mic.

<dx-codeblock>
::: javascript javascript
function handleUserAudioChange({userID, isAudioAvailable}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------- | -------------------------------------------------------------- |
| userID | String | User ID |
| isAudioAvailable | Boolean | <li/>`true`: the remote user turned on the mic. <li/> `false`: the remote user turned off the mic. |

### Inviter event callback APIs

#### REJECT
The user rejected the call.

<dx-codeblock>
::: javascript javascript
function handleInviteeReject({userID}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------- |
| userID | String | User ID |

#### NO_RESP
The invitee did not answer.

<dx-codeblock>
::: javascript javascript
function handleNoResponse({userID, userIDList}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------ | ------------ |
| UserID | String | User ID |
| userIDList | Array  | List of timed out users |

#### LINE_BUSY
The invitee is in a call, i.e., the line is busy.

<dx-codeblock>
::: javascript javascript
function handleInviteeLineBusy({userID}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------- |
| userID | String | User ID |

### Invitee event callback APIs

#### INVITED
You received an invitation.

<dx-codeblock>
::: javascript javascript
function handleNewInvitationReceived({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {

}
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ------- | -------------------------------------------------------------------------------------------------------- |
| sponsor     | String  | Inviter                                                                                                    |
| userIDList  | Array   | Users invited to the same call                                                                                          |
| isFromGroup | Boolean | Whether it is an IM group invitation                                             |
| inviteData  | Object  |<li/>For a new user invitation: {version, callType, roomID}<li/>For the last user hanging up: {version, callType, callEnd} |
| inviteID    | String  | Invitation ID, which identifies an invitation                                        |

#### CALLING_CANCEL
The call is cancelled.

<dx-codeblock>
::: javascript javascript
function handleInviterCancel() {

}
:::
</dx-codeblock>

#### CALLING_TIMEOUT
The call timed out.

<dx-codeblock>
::: javascript javascript
function handleCallTimeout() {

}
:::
</dx-codeblock>

## `TRTCCalling` Error Codes

You can handle the errors thrown by the `TRTCCalling` component by listening for the “error” field in events. Below is an example.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error);
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
:::
</dx-codeblock>

## FAQ
#### Why can’t I get through to the invitee? Why am I kicked offline?
The `TRTCCalling` component does not support login of multiple instances or **offline signaling** for the time being. Please check that your current login is unique.
> ?
> - **Multiple instances**: a user ID logs in multiple times or on different devices, which disrupts signaling.
> - **Offline signaling**: only online instances can receive a message. Messages sent to offline instances will not be sent again when the instances go online.
