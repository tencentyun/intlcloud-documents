This document describes how to access and debug the GME APIs for HTML5.


| API | Description |
|--------------|-------------------|
| Init | Initializes |
| SetTMGDelegate | Sets delegation |
| EnterRoom      | Enters audio room       |
| EnableMic      | Enables/disables capturing device |
| EnableSpeaker  | Enables/disables playback device |
| SetMicVolume   | Sets mic volume level      |
| ExitRoom       | Exits audio room        |


>
- After a GME API is called successfully, `QAVError.OK` will be returned with the value being 0.
- Authentication is required for room entry in GME. For more information, please see the authentication section in relevant documentation.
- Operation on devices should be performed after successful room entry.
- Starting from Chrome 74, `navigator.mediaDevices` can only be used in an HTTPS environment; therefore, please use HTTPS.


## Initialization APIs
Before initialization, the SDK is in the uninitialized state. A room can be entered only after the initialization authentication is performed and the SDK is initialized.

### Initializing the SDK
For more information on how to get parameters, please see [Access Guide](https://intl.cloud.tencent.com/document/product/607/10782).
This API requires the `SDKAppID` from the Tencent Cloud Console and the `openId` as parameters. The `openId` uniquely identifies a user with the rules stipulated by the application developer and must be unique in the application (currently, only INT64 is supported).

>The SDK must be initialized so that a room can be entered

### Function prototype

```
WebGMEAPI.fn.Init = function (document, SdkAppId, openId) {...}
```

| Parameter | Description |
| ------------- |-------------|
| document    	  |		HTML DOM Document object	|
| SdkAppId    		  | `SdkAppId` from the Tencent Cloud Console	|
| openId    		  | Developer-defined user account with a value greater than 10,000, which is used to identify the user |

### Sample code 
```
const cSdkAppId = () => document.getElementById("input-SdkAppId").value;
const cOpenID = () => document.getElementById("input-OpenID").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### Setting callbacks
The API class uses the `Delegate` method to send callback notifications to the application. Register the callback function to the SDK to receive callback messages. The callback function should be registered to the SDK before room entry.


#### Function prototype
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
| Parameter | Description |
| ------------- |-------------|
| onEvent     |SDK callback event |

#### Sample code  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## Voice Chat APIs
You should initialize and call the SDK to enter a room before voice chat can start.


### Entering a room
When a client enters a room with the generated authentication information, the `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` message will be received as a callback. Mic and speaker are not enabled by default after room entry.


#### Function prototype
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
| Parameter | Description |
| ------------- |-------------|
| roomId 	| Room ID, which can contain up to 127 characters |
| roomType 	| Room audio type |
| authBuffer	| Authentication key. For more information on how to get it, please see [Project Configuration](https://intl.cloud.tencent.com/document/product/607/10783) |



#### Sample code  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            // Step 1. Get the `AuthBuffer`
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
                    // Step 2. `AuthBuffer` is obtained successfully
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

### Event callback
After the client enters the room, the message `ITMG_MAIN_EVENT_TYPE_ENTER_ROOM` will be sent and identified in the `OnEvent` function.

#### Sample code  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            // Room successfully entered
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;// Received peer information. For more information, please see the table below
            app._data.brSend = result.UploadBRSend;// Bitrate of the uploaded audio data
            app._data.rtt = result.UploadRTT;// Upload RTT
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            // Room successfully exited
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            // Room disconnected
        }
    };
```


The received peer information is as follows (downStreamInfoList):

| Parameter | Description |
| ------------- |------------|
| brRecv | Receipt bitrate |
| delay | Receipt delay |
| jitterBufferMs      | Delay caused by jitter |
| jitterReceived      | Receipt jitter|


### Exiting a room
This API is called to exit the current room. It is an async API. There will be a callback after room exit. The returned value of `AV_OK` indicates a successful async delivery.
#### Function prototype  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
#### Sample code  
```
gmeAPI.ExitRoom();
```

### Enabling/Disabling the mic
This API is used to enable/disable the mic. Mic and speaker are not enabled by default after room entry.

#### Function prototype  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
| Parameter | Description |
| ------------- |------------|
| isEnabled    | To enable the mic, set this parameter to `true`; otherwise, set it to `false`. |

#### Sample code  
```
gmeAPI.EnableMic(false);
```



### Setting mic volume level
This API is used to set the mic volume level. The corresponding parameter is `volume`. 0 indicates that the audio is mute, while 100 indicates that the volume level remains unchanged. The default value is 100.

#### Function prototype  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
| Parameter | Description |
| -------------|-------------|
| volume    | Volume level. Value range: 0–100 |

#### Sample code  
```
gmeAPI.SetMicVolume(100);
```


### Enabling/Disabling the speaker
This API is used to enable/disable the speaker.
#### Function prototype  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
| Parameter | Description |
| ------------- |------------|
| isEnabled    | To disable the speaker, set this parameter to `false`; otherwise, set it to `true`. |

#### Sample code  
```
gmeAPI.EnableSpeaker(true);
```
