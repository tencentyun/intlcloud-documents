## Overview

Thank you for using Tencent Cloud Game Multimedia Engine (GME) SDK. This document describes how to access GME's HTML5 SDK to make it easy for HTML5 developers to debug and access the APIs of GME.

### Table of GME's HTML5 APIs

| API | Meaning |
|--------------|-------------------|
| Init | Initialize API |
| SetTMGDelegate | Set delegation |
| EnterRoom | Enter audio room |
| EnableMic | Turn acquisition device on or off |
| EnableSpeaker | Turn playback device on or off |
| SetMicVolume | Set microphone volume |
| ExitRoom | Exit audio room |


**Note**

**If a GME API is called successfully, QAVError.OK is returned with a value of 0.**

**Authentication is needed when entering a room in GME. See the authentication section in relevant documentation for more information.**

**The operations for devices should be performed after the user enters the room successfully.**


## Initialization-related APIs
Before initialization, the SDK is in the uninitialized state. A room can be entered only after the initialization and authentication are performed and the SDK is initialized.

## Initializing the SDK
See [GME Access Guide](/GME%20Introduction.md) for the parameters.
This AIP requires the SdkAppId from the Tencent Cloud Console and the openId as parameters. The openId uniquely identifies a user with the rules stipulated by the app developer and must be unique in the app (currently, only INT64 is supported).
The SDK must be initialized before a user can enter a room.
#### Function Prototype

```
WebGMEAPI.fn.Init = function (document, sdkAppId, openId) {...}
```

| Parameter | Meaning |
| ------------- |-------------|
| document | HTML DOM Document Object |				
| sdkAppId | SdkAppId from the Tencent Cloud Console |			
| openId | User's account defined by the developer, which must be greater than 10000 and is used to identify the user |		

#### Sample Code 
```
const cSdkAppId = () => document.getElementById("input-sdkappid").value;
const cOpenID = () => document.getElementById("input-openid").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### Setting the Callback
The API class uses the Delegate method to send callback notifications to the application. Register the callback function to the SDK to accept the callback messages.
This should be set before entering the room.

#### Function Prototype
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
| Parameter | Meaning |
| ------------- |-------------|
| onEvent | SDK callback event |

#### Sample Code  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## Voice Chat-related APIs
After initialization, API for entering a room should be called by the SDK before voice chat can start.
For the acquisition of the authentication information, see [Preparations Document](./H5%20SDK%20Project%20Configuration.md).

### Entering a Room
After the user enters the room with the generated authentication information, a callback with the message ITMG_MAIN_EVENT_TYPE_ENTER_ROOM will be received. Entering the room does not turn on the microphone or speaker by default.
For the authentication information, see the project configuration document.

#### Function Prototype
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
| Parameter | Meaning |
| ------------- |-------------|
| roomId | Room ID, up to 127 characters |	
| roomType | Audio type of the room |	
| authBuffer | Authentication code |	



| Audio type | Meaning | Parameter | Recommended sampling rate in the console | Application scenario |
|-------|---|----|----------------|------|
| ITMG_ROOM_TYPE_FLUENCY | Fluent | 1 | 16k sampling rate is recommended if there is no special requirement for sound quality | Fluent sound quality and ultra-low delay; suitable for team speak scenarios in games like FPS and MOBA															
|ITMG_ROOM_TYPE_STANDARD | Standard | 2 | Choose 16k or 48k sampling rate depending on different requirements for sound quality | Good sound quality and acceptable delay; suitable for voice chat scenarios in casual games like Werewolf and board games															
| ITMG_ROOM_TYPE_HIGHQUALITY | High-quality | 3 | To ensure optimum effect, it is recommended to enable HQ configuration with 48k sampling rate | Super-high sound quality and relative high delay; suitable for scenarios demanding high sound quality such as music playback and online karaoke					

- If you have special needs for audio type or scenario, please contact customer service;
- The sampling rate set in the console directly affects the in-game voice effect. Please confirm again in the [console](https://console.cloud.tencent.com/gamegme) that the selected sampling rate is suitable for the application scenario.


#### Sample Code  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            // Step 1: Obtain the AuthBuffer
            var FetchSigCgi = 'http://134.175.146.244:10005/';
            $.ajax({
                type: "POST",
                url: FetchSigCgi,
                dataType: 'json',
                data: {
                    sdkappid: cSdkAppId(),
                    roomid: cRoomNum(),
                    openid: cOpenID(),
                },
                success: function (json) {
                    //Step 2: The AuthBuffer is obtained successfully
                    if (json && json.errorCode === 0) {
                        let userSig = json.userSig;
                        gmeAPI.Init(document, cSdkAppId(), cOpenID());
                        gmeAPI.SetTMGDelegate(onEvent);
                        gmeAPI.EnterRoom(cRoomNum(), 1, userSig);
                    } else {
                        console.error(json);
                    }
                },
                error: function (err) {
                    console.error(err);
                }
            });
        });
```

### Event Callback
After the user enters the room, the message ITMG_MAIN_EVENT_TYPE_ENTER_ROOM will be sent and judged in the OnEvent function.

#### Sample Code  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            //The user successfully enters the room
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;// Information of the receiver; see the table below
            app._data.brSend = result.UploadBRSend;// Uploaded rate
            app._data.rtt = result.UploadRTT;// Uploaded RTT
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            // The user successfully exited the room
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            // The room is disconnected
        }
    };
```


The information of the receiver is as follows: downStreamInfoList: 

| Parameter | Meaning |
| ------------- |------------|
| brRecv | Received bit rate |
| delay | Received delay |
| jitterBufferMs | Jitter delay |
| jitterReceived | Received jitter |


### Exiting a Room
Calling this API can exit the room. This is an asynchronous API. There is a callback after the user exits the room. If the return value is AV_OK, the asynchronous delivery is successful.
#### Function Prototype  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
#### Sample Code  
```
gmeAPI.ExitRoom();
```

### Turning on/off the Microphone
This API is used to turn on/off the microphone. Entering the room does not turn on the microphone or speaker by default.

#### Function Prototype  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
| Parameter | Meaning |
| ------------- |------------|
| isEnabled | If the microphone needs to be turned on, the parameter passed in should be true; otherwise, the parameter should be false |

#### Sample Code  
```
gmeAPI.EnableMic(false);
```



### Setting Microphone Volume
This API is used to set the volume of the microphone. The parameter "volume" is used to set the volume of the microphone. If the value is 0, the microphone is mute; if the value is 100, the volume remains unchanged. The default value is 100.

#### Function Prototype  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
| Parameter | Meaning |
| -------------|-------------|
| volume | Set the volume between 0 and 100 |

#### Sample Code  
```
gmeAPI.SetMicVolume(100);
```


### Turning on/off the Speaker
This API is used to turn on/off the speaker.
#### Function Prototype  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
| Parameter | Meaning |
| ------------- |------------|
| isEnabled | If the speaker needs to be turned off, the parameter passed in should be false; otherwise, the parameter should be true |

#### Sample Code  
```
gmeAPI.EnableSpeaker(true);
```
