The `trtc-electron-education` component is a secondary encapsulation of TRTC and IM capabilities used in real-time interactive teaching scenarios. In addition to basic audio/video chat and screen sharing capabilities, it also offers various teaching features such as Q&A, raise hand, invite, and end answering for online education scenarios.
`trtc-electron-education` is an open-source npm component depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Real-Time Interactive Teaching (Electron)](https://intl.cloud.tencent.com/document/product/647/37278).
* TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency audio/video call component.
* IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to send and process signaling messages.

## Component Integration
```
// Import by using YARN
yarn add trtc-electron-education
// Import by using npm
npm i trtc-electron-education --save
```

## Component Parameters

The required key parameters are as detailed below:

| Parameter | Type | Description |
| ----- | ----- | ----- |
| sdkAppId | number | `SDKAppID`, which is required and can be viewed in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>. |
| userID | string | User ID, which is required and can be specified by your account system. |
| userSig | string | Identity signature, which is required and acts as the login password. It can be calculated based on the `userID`. For more information on the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

## Initialization Sample

```typescript
import TrtcElectronEducation from 'trtc-electron-education';
const rtcClient = new TrtcElectronEducation({
     sdkAppId: 1400***803,
     userID: '123'
     userSig: 'eJwtzM9****-reWMQw_'
 });
```

## Component Overview
### Basic APIs

#### on(EventCode, handler, context)
This API is used to listen on the events delivered by the component.  
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| EventCode |	String |	Event code |
| handler |	Function |	Listener function |
| context |	Object |	Current execution context |

Sample code:
```typescript
const EVENT = rtcClient.EVENT
rtcClient.on(EVENT.MESSAGE_RECEIVED, onMessageReceived);
```

#### off(EventCode, handler)
This API is used to cancel listening on events.  
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| EventCode |	String | Event code |
| handler |	Function | Named listener function to be canceled |

Sample code:
```typescript
const EVENT = rtcClient.EVENT
rtcClient.off(EVENT.MESSAGE_RECEIVED, onMessageReceived);
```

[](id:createRoom)
#### createRoom(params: CreateRoomParams)
This API is used by the teacher to create a classroom.  
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| classId |	number |	Classroom ID |
| nickName |	string |	Nickname |
| avatar |	string |	Profile photo address, which is optional |

Sample code:
```typescript
interface CreateRoomParams {
  classId: number; // Classroom ID
  nickName: string; // Nickname
  avatar?:string; // Profile photo address
}
rtcClient.createRoom(params).then(() => {
})
```

#### destroyRoom(classId: number)
This API is used by the teacher to exit and terminate a classroom.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| classId |	number |	Classroom ID |

Sample code:
```typescript
rtcClient.destroyRoom(classId)
```

[](id:enterRoom)
#### enterRoom(params: EnterRoomParams)
This API is used by the teacher to start teaching or by the student to enter the classroom and prepare to listen.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| classId |	number |	Classroom ID |
| nickName |	string | Nickname |
| role |	string |	Role. Valid values: teacher, student |
| avatar |	string |	Profile photo address, which is optional |

Sample code:
```typescript
interface EnterRoomParams {
  role: string; // Role
  classId: number; // Classroom ID
  nickName?: string; // Nickname
  avatar?:string; // Profile photo address
}
rtcClient.enterRoom(params).then(() => {
})
```

#### exitRoom(role:string, classId: number)
This API is used by the teacher to end teaching or by the student to exit the classroom.
Parameters:

| Parameter Name |Type| Description |
| ----- | ----- | ----- |
| classId |	number |	Classroom ID |
| role |string | Role. Valid values: teacher, student |

Sample code:
```typescript
rtcClient.exitRoom(role, classId);
```

### Raise hand APIs
<span id="startQuestionTime"></span>
#### startQuestionTime(classId: number)
This API is used by the teacher to start Q&A. The teacher broadcasts a notification, and the student receives the Q&A start event and can raise hand.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| classId |	number |	Classroom ID |

Sample code:
```typescript
rtcClient.startQuestionTime(classId)
```

[](id:raiseHand)
#### raiseHand()
This API is used by the student to raise hand. The student sends a raise hand notification, which will be received by the teacher.  
Parameters: none
Sample code:
```typescript
rtcClient.raiseHand()
```

[](id:inviteToPlatform)
#### inviteToPlatform(userID: string)
This API is used by the teacher to invite a student to answer a question. The teacher selects the `userID` of a student in the "raise hand" list and sends an invitation notification. The invited student will receive the invitation event and mic on. If no student raises hand, the teacher can directly select a student. The selected student will receive the answering invitation event and mic on.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |  ----- |
| userID |	string | User ID |

Sample code:
```typescript
rtcClient.inviteToPlatform(userID).then(() => {
})
```

[](id:finishAnswering)
#### finishAnswering(userID: string)
This API is used to end answering. The teacher ends answering by the student. The student receives the answering end notification and exits co-anchoring.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |   ----- |
| userID |	string |	User ID |

Sample code:
```typescript
rtcClient.finishAnswering(userID).then(() => {
})
```

#### stopQuestionTime(classId: number)
This API is used to stop Q&A. The teacher stops Q&A, and students receive the Q&A stop notification. The co-anchoring student needs to stop co-anchoring and disable the "raise hand" feature.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| classId |	number |	Classroom ID |

Sample code:
```typescript
rtcClient.stopQuestionTime(classId)
```

### Push/Pull APIs
[](id:getScreenShareList)
#### getScreenShareList()
This API is used to get the list of windows for screen sharing.
Parameters: none
Sample code:
```typescript
rtcClient.getScreenShareList();
```


[](id:startScreenCapture)
#### startScreenCapture(source: SourceParam)
This API is used to select the shared screen and start push.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| type |	number |	Capturing source type |
| sourceId | string |	Capturing source ID. For a window, this field indicates a window handle; for a screen, this field indicates a screen ID |
| sourceName | string | Capturing source name encoded in UTF-8 |

Sample code:
```typescript
interface SourceParam {
  type: number; // Capturing source type
  sourceId: string; // Capturing source ID
  sourceName: string; // Capturing source name encoded in UTF-8
}
rtcClient.startScreenCapture({
   type,
   sourceId,
   sourceName
 })
```

[](id:startRemoteView)
#### startRemoteView(params: RemoteParams) 
This API is used to start displaying the remote video image or screen sharing image.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |  ---- |
| userID |	string |	User ID |
| streamType | number |	Image type. 1: big image; 2: small image; 3: screen sharing |
| view | HTMLElement |	DOM that carries the displayed image |

Sample code:
```typescript
interface RemoteParams {
  userID: string; // User ID
  streamType: number; // Image type. 1: big image; 2: small image; 3: screen sharing
  view: HTMLElement; // DOM that carries the displayed image
}
const view = document.getElementById('localVideo');
rtcClient.startRemoteView({
  userID: userID,
  streamType: 1,// 1: big image; 2: small image; 3: screen sharing
  view: view
});
```

#### stopRemoteView(params: StopRemoteParams)
This API is used to stop displaying the remote video image or screen sharing image and pulling the data stream from the remote user.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |  ----- |
| userID |	string |	User ID |
| streamType | number |Image type. 1: big image; 2: small image; 3: screen sharing |

Sample code:
```typescript
interface StopRemoteParams {
  userID: string; // User ID
  streamType: number; // Image type. 1: big image; 2: small image; 3: screen sharing
}
rtcClient.stopRemoteView({
   userID: userID,
   streamType: 1 // 1: big image; 2: small image; 3: screen sharing
 });
```

### Message sending/receiving APIs
#### sendTextMessage(params: MessageParams) 
This API is used to send a message in the chat room.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |  ----- |
| classId | number | Classroom ID |
| message | string | Message text |

Sample code:
```typescript
interface MessageParams {
  classId: number; // Classroom ID
  message: string; // Message text
}
rtcClient.sendTextMessage(params).then(() => {
})
```

#### sendCustomMessage(userID: string, data: string)
This API is used to send a custom C2C message. 
Parameters:

| Parameter Name |	Type	|	Description |
| ----- | ----- | ----- |
| userID | string | User ID |
| data | string |	Custom message |

Sample code:
```typescript
rtcClient.sendCustomMessage(userID, JSON.stringify(params)
```

#### sendGroupCustomMessage(classId: number, data: string)
This API is used to send a custom group message.  
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| classId | number | Classroom ID |
| data | string | Custom message |

Sample code:
```typescript
rtcClient.sendGroupCustomMessage(classId, JSON.stringify(params))
```

### Device operation APIs
[](id:openCamera)
#### openCamera(view: HTMLElement)
This API is used to enable the camera.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- | ----- |
| view | HTMLElement |	DOM that carries the displayed image |

Sample code:
```typescript
const domEle = document.getElementById('localVideo');
rtcClient.openCamera(domEle);
```

#### closeCamera()
This API is used to disable the camera. 
Parameters: none
Sample code:
```typescript
rtcClient.closeCamera();
```

[](id:getCameraList)
#### getCameraList()
This API is used to get the list of cameras.
Parameters: none
Sample code:
```typescript
rtcClient.getCameraList()
```

[](id:setCurrentCamera)
#### setCurrentCamera(deviceId:string)
This API is used to set the camera. The parameter is a device ID obtained from `getCameraDevicesList`.
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |  ---- |
| deviceId | string | Device ID |

Sample code:
```typescript
rtcClient.setCurrentCamera(deviceId)
```

[](id:openMicrophone)
#### openMicrophone()
This API is used to enable the mic.
Parameters: none
Sample code:
```typescript
rtcClient.openMicrophone();
```

[](id:closeMicrophone)
#### closeMicrophone()
This API is used to disable the mic.
Parameters: none
Sample code:
```typescript
rtcClient.closeMicrophone();
```


[](id:getMicrophoneList)
#### getMicrophoneList()
This API is used to get the list of mics.  
Parameters: none
Sample code:
```typescript
rtcClient.getMicrophoneList()
```
#### setCurrentMicDevice(micId:string)
This API is used to set the mic. The parameter is a device ID obtained from `getMicDevicesList`.
Parameters:

| Parameter Name |	Type	| 	Description |
| ----- | ----- | ----- |
| micId | string |	 Device ID |

Sample code:
```typescript
rtcClient.setCurrentMicDevice(micId)
```

[](id:setBeautyStyle)
#### setBeautyStyle(params: BeautyParams) 
This API is used to set the effect levels of beauty, brightening, and rosy skin filters. 
Parameters:

| Parameter Name |	Type	| Description |
| ----- | ----- |  ----- |
| beautyStyle | number | 1: smooth, which is suitable for shows since it has more obvious effect <br>2: natural, which retains more facial details and seems more natural subjectively |
| beauty | number |	Effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect |
| white | number |Effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect |
| ruddiness | number |	Effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. This parameter does not take effect on Windows currently |

Sample code:
```typescript
interface BeautyParams {
  beautyStyle: number;// Smooth or natural
  beauty: number; // Effect level of beauty filter
  white: number; // Effect level of brightening filter
  ruddiness: number; // Effect level of rosy skin filter
}
rtcClient.setBeautyStyle({
	beautyStyle: 1,
	beauty: 5,
	white: 5,
	ruddiness: 5
})
```

## Component Events
### Sample code
```typescript
const EVENT = rtcClient.EVENT
rtcClient.on(EVENT.STUDENT_RAISE_HAND, () => {
   // A student raises hand
})
```
### Detailed events

| Code | Description |
| ----- | ----- |
| ENTER_ROOM_SUCCESS | Entered room successfully |
| LEAVE_ROOM_SUCCESS | Exited room successfully |
| TEACHER_ENTER | The teacher entered the room |
| TEACHER_LEAVE | The teacher exited the room |
| STUDENT_ENTER | The student entered the room |
| STUDENT_LEAVE | The student exited the room |
| SCREEN_SHARE_ADD | The teacher started screen sharing |
| SCREEN_SHARE_REMOVE | The teacher stopped screen sharing |
| REMOTE_VIDEO_ADD | A remote video stream was added. This notification will be received when a remote user publishes a video stream |
| REMOTE_VIDEO_REMOVE | A remote video stream was removed. This notification will be received when a remote user cancels video stream release |
| REMOTE_AUDIO_ADD | A remote audio stream was added |
| REMOTE_AUDIO_REMOVE | A remote audio stream was removed |
| ROOM_DESTROYED | The room was terminated |
| QUESTION_TIME_STARTED | Q&A started |
| QUESTION_TIME_STOPPED | Q&A ended |
| STUDENT_RAISE_HAND | A student raised hand |
| BE_INVITED_TO_PLATFORM | A student was invited to answer |
| ANSWERING_FINISHED | Answering ended, and audio was muted |
| MESSAGE_RECEIVED | A message was received |
| KICKED_OUT | The same account logged in at another place and was kicked out
| ERROR | Exception |
| WARNING | Warning |
