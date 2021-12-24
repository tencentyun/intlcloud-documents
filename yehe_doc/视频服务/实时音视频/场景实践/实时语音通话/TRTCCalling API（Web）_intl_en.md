## `TRTCCalling` Overview

The [TRTCCalling](https://www.npmjs.com/package/trtc-calling-js) component is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). It supports one-to-one and group audio/video calls. For detailed instructions on how to implement it, see [Real-Time Audio Call (Web)](https://intl.cloud.tencent.com/document/product/647/38928).

- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video call component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.

## `TRTCCalling` APIs 

#### Event subscribing/unsubscribing APIs 

This component bases its management on the dispatching of events. The application layer can change UI interactions according to dispatched events.

| API                                             | Description                                                         |
| ------------ | ------------ |
| [on(eventName, callback, context)](#on)   | Subscribes to an event.     |
| [off(eventName, callback, context)](#off) | Unsubscribes from an event. |


#### Basic SDK APIs

| API     | Description |
| ---------------------------------- | ----------------- |
| [login({userID, userSig})](#login) | Logs in to IM. All IM features can be used only after login. |
| [logout()](#logout()) | Logs out. No calls can be made after logout.            |

#### Call operation APIs

| API  | Description       |
| ------------------------------- | ------------ |
| [call({userID, type, offlinePushInfo}))](#call)              | Invites a user to a one-to-one call. |
| [groupCall({userIDList, type, groupID, offlinePushInfo})](#groupCall) | Invites users to a group call. |
| [accept()](#accept)                                          | Accepts a call. |
| [reject()](#reject)                                          | Rejects a call. |
| [hangup()](#hangup())                                                                     | Hangs up. |


#### Video APIs

| API                                             | Description                                                         |
| ------------------------------- | ---------------------- |
| [startRemoteView({userID, videoViewDomID})](#startRemoteView) | Starts rendering the video of a remote user.   |
| [stopRemoteView({userID})](#stopRemoteView) | Stops rendering the video of a remote user.                                      |
| [startLocalView({userID, videoViewDomID})](#startLocalView) | Starts rendering the video of the local user.   |
| [stopLocalView({userID})](#stopLocalView) | Stops rendering the video of the local user.       |
| [openCamera()](#openCamera)                                                                 | Turns the camera on.         |
| [closeCamera()](#closeCamera)              | Turns the camera off.         |
| [setMicMute(isMute)](#setMicMute)     | Mutes/Unmutes the mic. |
| [setVideoQuality(profile)](#setVideoQuality) | Sets video quality.|
| [switchToAudioCall()](#switchToAudioCall) | Switches to audio call. |
| [switchToVideoCall()](#switchToVideoCall) | Switches to video call. |
| [getCameras()](#getCameras)                 | Gets the camera list.   |
| [getMicrophones()](#getMicrophones)     | Gets the mic list.   |
| [switchDevice({deviceType, deviceID})](#switchDevice) | Switches to a different camera or mic. |


## API Details

### Creating a `TRTCCalling` instance

First, create an application in the [TRTC console](https://console.cloud.tencent.com/trtc/app) and get the `SDKAppID`.
Then, obtain an instance of the `TRTCCalling` component using `new TRTCCalling()`.

<dx-codeblock>
::: javascript javascript
let options = {
  SDKAppID: 0, // Replace 0 with the `SDKAppID` of your IM application when connecting
  // The `tim` parameter was introduced in v0.10.2.
  // The parameter guarantees the uniqueness of an existing TIM instance.
  tim: tim
};
let trtcCalling = new TRTCCalling(options);
:::
</dx-codeblock>

### Event subscribing/unsubscribing APIs 


[](id:on)
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


[](id:off)
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

[](id:login)
#### login({userID, userSig})

This API is used to log in.

<dx-codeblock>
::: javascript javascript
trtcCalling.login({userID, userSig})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ------------------------------------------------------------- |
| userID | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_) |
| userSig | String | Tencent Cloud's proprietary security signature. For how to calculate it, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |


[](id:logout)
#### logout()

 This API is used to log out.

<dx-codeblock>
::: javascript javascript
trtcCalling.logout()
:::
</dx-codeblock>

### Call operation APIs


[](id:call)
#### call({userID, type, offlinePushInfo})

This API is used to make one-to-one calls. `type` indicates the type of a call. `1`: audio call; `2`: video call.

>?
>- The `timeout` parameter is deleted from v1.0.0 and later versions.
>- A new parameter, `offlinePushInfo`, is introduced for offline notifications, **which are supported only on Android and iOS, not on web or WeChat Mini Program.**

<dx-codeblock>
::: javascript javascript
// Versions earlier than v1.0.0
trtcCalling.call({userID, type, timeout})

// v1.0.0 and later versions
const offlinePushInfo = {
  title: '',
  description: 'You are invited to a call.',
}
trtcCalling.call({userID, type, offlinePushInfo})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------------- | ------ | -------------------------- |
| userID  | String | User ID of the invitee          |
| type       | Number | `1`: audio call; `2`: video call |
| timeout         | Number | Timeout period (s). `0` means the call never times out. **This parameter is available only in versions earlier than v1.0.0.**         |
| offlinePushInfo | Object | Offline notifications (optional). **This parameter is available only in v1.0.0 and later versions.** |

offlinePushInfo (in v1.0.0 and later versions)

| Parameter    | Type   | Description                     |
| -------------------- | ------ | ------------------------- |
| title                | String | Title of an offline notification (optional)                                   |
| description          | String | Content of an offline notification (optional)                                    |
| androidOPPOChannelID | String | Channel ID for an offline notification on OPPO 8.0 and above (optional) |

[](id:groupCall)
#### groupCall({userIDList, type, groupID, offlinePushInfo})
The `groupID` parameter is the group ID in the IM SDK. If this parameter is set, call invitations will be broadcast by the group messaging system, which is a simple and reliable way of sending call invitations. If this parameter is left empty, the `TRTCCalling` component will send an invitation to every invitee.

>? In v1.0.0 and later versions, a new parameter, `offlinePushInfo`, is introduced for offline notifications, **which are supported only on Android and iOS, not on web or WeChat Mini Program.**

<dx-codeblock>
::: javascript javascript
// Versions earlier than v1.0.0
trtcCalling.groupCall({userIDList, type, groupID})

// v1.0.0 and later versions
const offlinePushInfo = {
  title: '',
  description: 'You are invited to a call.',
}
trtcCalling.groupCall({userIDList, type, groupID, offlinePushInfo})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------------- | ------ | -------------------------- |
| userIDList | Array  | List of the user IDs of invitees                 |
| type       | Number | `1`: audio call; `2`: video call |
| groupID    | String | ID of the IM group (optional)      |
| offlinePushInfo | Object | Offline notifications (optional). **This parameter is available only in v1.0.0 and later versions.** |

offlinePushInfo (in v1.0.0 and later versions)

| Parameter    | Type   | Description                     |
| -------------------- | ------ | ------------------------- |
| title                | String | Title of an offline notification (optional)                                   |
| description          | String | Content of an offline notification (optional)                                    |
| androidOPPOChannelID | String | Channel ID for an offline notification on OPPO 8.0 and above (optional) |

[](id:accept)
#### accept()
This API is used to accept an invitation.

>?
>- If a prior invitation has not been processed, the component will return a message indicating that the line is busy.
>- `params` is deleted from v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  // Versions earlier than v1.0.0
  trtcCalling.accept({inviteID, roomID, callType})
  // v1.0.0 and later versions
  trtcCalling.accept();
})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter     | Type   | Description                     |
| -------- | ------ | --------------------- |
| inviteID | String | Invitation ID, which identifies an invitation. **This parameter is available only in versions earlier than v1.0.0.**    |
| roomID   | Number | Room ID. **This parameter is available only in versions earlier than v1.0.0.**            |
| callType | Number | Call type. `1`: audio call; `2`: video call. **This parameter is available only in versions earlier than v1.0.0.** |

[](id:reject)
#### reject()
This API is used to reject an invitation.

>? `params` is deleted from v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  // Versions earlier than v1.0.0
  trtcCalling.reject({inviteID, isBusy, callType})
  // v1.0.0 and later versions
  trtcCalling.reject();
})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------- | --------------------- |
| inviteID | String | Invitation ID, which identifies an invitation. **This parameter is available only in versions earlier than v1.0.0.**    |
| isBusy   | Boolean | Whether the line is busy. **This parameter is available only in versions earlier than v1.0.0.**             |
| callType | Number | Call type. `1`: audio call; `2`: video call. **This parameter is available only in versions earlier than v1.0.0.** |

[](id:hangup)
#### hangup()
1. If you are in a call, you can use this API to end the call.
2. If your call is not answered yet, you can use this API to cancel the call.

<dx-codeblock>
::: javascript javascript
trtcCalling.hangup()
:::
</dx-codeblock>


### Video APIs

[](id:startRemoteView)
#### startRemoteView({userID, videoViewDomID})
This API is used to render the camera data of a remote user in a specified DOM node.

<dx-codeblock>
::: javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter       | Type   | Description                     |
| -------------- | ------ | ---------------------------- |
| userID | String | User ID |
| videoViewDomID | String | The DOM node in which the user’s data is to be rendered. The data will be played via the video tag of the node. |

[](id:stopRemoteView)
#### stopRemoteView({userID})
This API is used to delete the DOM node in which the camera data of a remote user is rendered.

>?`videoViewDomID` is deleted from v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
// Versions earlier than v1.0.0
trtcCalling.stopRemoteView({userID, videoViewDomID});
// v1.0.0 and later versions
trtcCalling.stopRemoteView({userID});

:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------------- | ------ | ------------------------------- |
| userID | String | User ID |
| videoViewDomID | String | The DOM node whose video tag is to be deleted. The playback will stop. **This parameter is available only in versions earlier than v1.0.0.** |

[](id:startLocalView)
#### startLocalView({userID, videoViewDomID})
This API is used to render the camera data of the local user in a specified DOM node.

<dx-codeblock>
::: javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------------- | ------ | ------------------------------ |
| userID | String | User ID |
| videoViewDomID | String | The DOM node in which the local user’s data is to be rendered. The data will be played via the video tag of the node. |

[](id:stopLocalView)
#### stopLocalView({userID})

This API is used to delete the DOM node in which the camera data of the local user is rendered.

>?`videoViewDomID` is deleted from v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
// Versions earlier than v1.0.0
trtcCalling.stopLocalView({userID, videoViewDomID});
// v1.0.0 and later versions
trtcCalling.stopLocalView({userID});
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------------- | ------ | ------------------------------- |
| userID | String | User ID |
| videoViewDomID | String | The DOM node whose video tag is to be deleted. The playback will stop. **This parameter is available only in versions earlier than v1.0.0.** |

[](id:openCamera)
#### openCamera()
This API is used to turn the local camera on.

<dx-codeblock>
::: javascript javascript
trtcCalling.openCamera()
:::
</dx-codeblock>

[](id:closeCamera)
#### closeCamera()
This API is used to turn the camera off.

<dx-codeblock>
::: javascript javascript
trtcCalling.closeCamera()
:::
</dx-codeblock>

[](id:setMicMute)
####  setMicMute(isMute) 
This API is used to turn the mic on/off.

<dx-codeblock>
::: javascript javascript
trtcCalling.setMicMute(true) // Turn the mic off
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------- | --------------- |
| isMute | Boolean | <li/>`true`: turn the mic off <li/>`false`: turn the mic on |

[](id:setVideoQuality)
####  setVideoQuality(profile) 
This API is used to set video quality.
>?  
>- This is a new API in v0.8.0 and later versions.
>- This API must be called before `call`, `groupCall`, or `accept` to take effect.

<dx-codeblock>
::: javascript javascript
trtcCalling.setVideoQuality('720p') // Set video quality to `720p`
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------- | --------------- |
| profile | String | <li/>`480p`: 640 × 480 <li/>`720p`: 1280 × 720  <li/>`1080p`: 1920 × 1080  |

[](id:switchToAudioCall)
####  switchToAudioCall() 
This API is used to switch from video call to audio call.
>?  
>- This is a new API in v0.10.0 and later versions.
>- It can be used only in one-to-one calls.
>- The error callback (code: 60001) indicates that the switching has failed.

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToAudioCall() // Switch from video call to audio call
:::
</dx-codeblock>

[](id:switchToVideoCall)
####  switchToVideoCall() 
This API is used to switch from audio call to video call.
>?  
>- This is a new API in v0.10.0 and later versions.
>- It can be used only in one-to-one calls.
>- The error callback (code: 60002) indicates that the switching has failed.

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToVideoCall() // Switch from audio call to video call
:::
</dx-codeblock>

[](id:getCameras)
####  getCameras() 

This API is used to get the camera list.

>? This is a new API in v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
trtcCalling.getCameras() // Get the camera list
:::
</dx-codeblock>

[](id:getMicrophones)
####  getMicrophones() 

This API is used to get the mic list.

>? This is a new API in v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
trtcCalling.getMicrophones() // Get the mic list
:::
</dx-codeblock>

[](id:switchDevice)
####  switchDevice({deviceType,deviceID}) 

This API is used to switch to a different camera or mic.

>? This is a new API in v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
trtcCalling.switchDevice(deviceType, deviceID) // Switch to a different device
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | ------------------------------- |
| deviceType | String | Device type. `video`: camera; `audio`: mic                                 |
| deviceID   | String | Device ID. <li/>You can use `getCameras()` to get the ID of a camera.<li/>You can use `getMicrophones()` to get the ID of a mic. |


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

|      Code       |   Event Recipient   |  Description   |
| :--------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     Inviter     |     The invitee rejected the call.      |
|       [NO_RESP](#no_resp)        |     Inviter     |    The invitation timed out without response from the invitee.      |
|      [LINE_BUSY](#line_busy)       |     Inviter     | The invitee is in a call, i.e., the line is busy. |
|       [INVITED](#invited)        |     Invitee     |      An invitation was received.       |
|    [CALLING_CANCEL](#calling_cancel)    |     Invitee     |     The call is canceled.      |
|   [CALLING_TIMEOUT](#calling_timeout)    |     Invitee     |    The invitation timed out.     |
|      [USER_ENTER](#user_enter)      | Inviter and invitee |         A user entered the room.          |
|      [USER_LEAVE](#user_leave)      | Inviter and invitee |       A user left the call.        |
|       [CALL_END](#call_end)       | Inviter and invitee |       The call ended.        |
|      [KICKED_OUT](#kicked_out)      | Inviter and invitee |   A user was kicked out due to repeated login.    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | Inviter and invitee | A remote user turned the camera on/off. |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | Inviter and invitee | A remote user turned the mic on/off. |

### Common event callback APIs


#### SDK_READY

The SDK is ready.

>?This is a new callback in v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
let onSDKReady = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.SDK_READY, onSDKReady);
:::
</dx-codeblock>

#### USER_ENTER

A user entered the room.
This callback is triggered when a user joins the call.

<dx-codeblock>
::: javascript javascript
let handleUserEnter = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.USER_ENTER, handleUserEnter);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userID | String | User ID |

#### USER_LEAVE

A user left the room.
This callback is triggered when a user leaves the call.

<dx-codeblock>
::: javascript javascript
let handleUserLeave = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.USER_LEAVE, handleUserLeave);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userID | String | User ID |

#### GROUP_CALL_INVITEE_LIST_UPDATE

The invitee list for a group call was updated.

>?This is a new callback in v1.0.0 and later versions.

<dx-codeblock>
::: javascript javascript
let handleGroupInviteeListUpdate = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.GROUP_CALL_INVITEE_LIST_UPDATE, handleGroupInviteeListUpdate);
:::
</dx-codeblock>

#### CALL_END

The call ended.
This callback is triggered when a call ends.

<dx-codeblock>
::: javascript javascript
let handleCallingEnd = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALL_END, handleCallingEnd);
:::
</dx-codeblock>

#### KICKED_OUT

A user was kicked out due to repeated login.
This callback is triggered if a user logs in with the same account twice.

<dx-codeblock>
::: javascript javascript
let handleKickedOut = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.KICKED_OUT, handleKickedOut);
:::
</dx-codeblock>

#### USER_VIDEO_AVAILABLE

A remote user turned the camera on/off.
This callback is triggered when a remote user turns the camera on/off.

<dx-codeblock>
::: javascript javascript
let handleUserVideoChange = function({userID, isVideoAvailable}) {
  console.log(userID, isVideoAvailable)
};
trtcCalling.on(TRTCCalling.EVENT.USER_VIDEO_AVAILABLE, handleUserVideoChange);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---------------- | ------- | ------------------------------ |
| userID | String | User ID |
| isVideoAvailable | Boolean | <li/>`true`: The remote user turned the camera on. <li/> `false`: The remote user turned the camera off. |

#### USER_AUDIO_AVAILABLE

A remote user turned the mic on/off.
This callback is triggered when a remote user turns the mic on/off.

<dx-codeblock>
::: javascript javascript
let handleUserAudioChange = function({userID, isAudioAvailable}) {
  console.log(userID, isAudioAvailable)
};
trtcCalling.on(TRTCCalling.EVENT.USER_AUDIO_AVAILABLE, handleUserAudioChange);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------------- | ------- | -------------------------------- |
| userID | String | User ID |
| isAudioAvailable | Boolean | <li/>`true`: The remote user turned the mic on. <li/> `false`: The remote user turned the mic off. |

### Inviter event callback APIs

#### REJECT

The user rejected the call.
The inviter of a call will receive this callback if an invitee rejects the call.

<dx-codeblock>
::: javascript javascript
let handleInviteeReject = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userID | String | User ID |

#### NO_RESP

The invitee did not answer.
In cases where a timeout period is specified for a one-to-one or group call, the inviter will receive this callback if an invitee does not answer the call within the specified timeout period.

<dx-codeblock>
::: javascript javascript
let handleNoResponse = function({userID, userIDList}) {
  console.log(userID, userIDList)
};
trtcCalling.on(TRTCCalling.EVENT.NO_RESP, handleNoResponse);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------ | ------------ |
| userID | String | User ID |
| userIDList | Array  | List of timed out users |

#### LINE_BUSY

The invitee is in a call, i.e., the line is busy.
The inviter of a call will receive this callback if the invitee is already in a call.

<dx-codeblock>
::: javascript javascript
let handleLineBusy = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.LINE_BUSY, handleLineBusy);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | ------- |
| userID | String | User ID |

### Invitee event callback APIs
#### INVITED
An invitation was received.
A user will receive this callback if he or she is invited to a call.

<dx-codeblock>
::: javascript javascript
let handleNewInvitationReceived = function({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {
  console.log(sponsor, userIDList, isFromGroup, inviteData, inviteID)
};
trtcCalling.on(TRTCCalling.EVENT.INVITED, handleNewInvitationReceived);
:::
</dx-codeblock>

The parameters are as detailed below:

| Parameter | Type | Description |
| ----------- | ------- | ------------------------------------------------ |
| sponsor     | String  | Inviter                                                       |
| userIDList  | Array   | Users invited to the same call                                             |
| isFromGroup | Boolean | Whether it is an IM group invitation                                             |
| inviteData  | Object  | <li/>For a new user invitation: {version, callType, roomID} <li/> For the last user hanging up: {version, callType, callEnd} |
| inviteID | String | Invitation ID, which identifies an invitation |

#### CALLING_CANCEL
The call is canceled.
An invitee of a call will receive this callback if the call is canceled.

<dx-codeblock>
::: javascript javascript
let handleCallingCancel = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALLING_CANCEL, handleCallingCancel);
:::
</dx-codeblock>


#### CALLING_TIMEOUT

The call timed out.
In cases where a timeout period is specified for a one-to-one or group call, an invitee will receive this callback if he or she does not answer the call within the specified timeout period.

<dx-codeblock>
::: javascript javascript
let handleCallingTimeout = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALLING_TIMEOUT, handleCallingTimeout);
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

[](id:Error)
#### Error codes

| Code      | Type    | Description                        |
| ----- | ------------ | -------------------------- |
| 60001     | API call failure  | Failed to call `switchToAudioCall`. |
| 60002     | API call failure  | Failed to call `switchToVideoCall`. |
| 60003 | Access failure | No available mic.       |
| 60004 | Access failure | No available camera.       |
| 60005 | Access failure | The user denied access.           |

## FAQs

#### Why can’t I get through to a user? Why am I kicked offline?
The `TRTCCalling` component does not support login of multiple instances or **offline signaling** for the time being. Please make sure that your current login is unique.
> ?
> - **Multiple instances**: a user ID logs in multiple times or on different devices, which disrupts signaling.
> - **Offline signaling**: only online instances can receive a message. Messages sent to offline instances will not be sent again when the instances go online.

