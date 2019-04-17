This article is a detailed description with the purpose of helping H5 developers debug and access APIs for Tencent Cloud's Game Multimedia Engine (GME).


| API | Description |
|--------------|-------------------|
| Init | Initializes API |
| SetTMGDelegate | Sets delegate |
| EnterRoom | Enters a voice room |
| EnableMic | Enables/Disables a capturing device |
| EnableSpeaker | Enables/Disables a playback device |
| SetMicVolume | Sets microphone volume |
| ExitRoom | Exits a voice room |


**Notes**
- After a GME API is called successfully, QAVError.OK will be returned with a value of 0.
- The request for entering a room via GME API should be authenticated. For more information, see authentication section in relevant documentation.
- The operation on devices shall be carried out after successful entry into a room.


## Initialization APIs
For an uninitialized SDK, you must initialize it via initialization authentication to enter a room.

### Initialize the SDK
SdkAppId and openId are the required parameters for requesting this API, where openId is for identifying a user and must be unique in an Application (only INT64 value type is supported). You can get SdkAppId from Tencent Cloud Console, and set rules for creating openId as a developer.


> SDK must be initialized before a user can enter a room.

### Function prototype

```
WebGMEAPI.fn.Init = function (document, SdkAppId, openId) {...}
```

| Parameter | Description |
| ------------- |-------------|
| document | HTML DOM Document object |
| SdkAppId | The SdkAppId obtained from the Tencent Cloud Console |
| openId | User ID. Developer-defined. The value must be greater than 10000 |

### Sample code 
```
const cSdkAppId = () => document.getElementById("input-SdkAppId").value;
const cOpenID = () => document.getElementById("input-OpenID").value;
gmeAPI.Init(document, cSdkAppId(), cOpenID());
```

### Set callback
With the API class, the Delegate method is used to send callback notifications to your application. Register the callback function to the SDK to receive callback messages. Register the callback function to the SDK (before a user enters the room).


#### Function prototype
```
WebGMEAPI.fn.SetTMGDelegate = function (delegate){...}
```
| Parameter | Description |
| ------------- |-------------|
| onEvent | SDK callback event |

#### Sample code  
```
gmeAPI.SetTMGDelegate(onEvent);
```





## APIs for Voice Chat
You must initialize and call the SDK to enter a room before Voice Chat can start.


### Enter a room
When you enter a room with the generated authentication credentials, you receive a callback indicating ITMG_MAIN_EVENT_TYPE_ENTER_ROOM. By default, Microphone and speaker will not be enabled after you enter the room. If you successfully enter a room, the API returns  AV_OK.

#### Function prototype
```
WebGMEAPI.fn.EnterRoom = function (roomId, roomType, authBuffer) {...}
```
| Parameter | Description |
| ------------- |-------------|
| roomId | Room ID, which is limited to 127 characters |
| roomType | Audio type of the room |
| authBuffer | Authentication key. See [Project Configuration](https://cloud.tencent.com/document/product/607/32156) to learn about how to obtain it. |



#### Sample code  
```
 function bindButtonEvents() {
        $("#start_btn").click(function () {
            console.log('start!');
            // Step 1: get AuthBuffer
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
                    // Step 2: AuthBuffer obtained successfully
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
The ITMG_MAIN_EVENT_TYPE_ENTER_ROOM message is returned after a user enters a room, which is checked in the OnEvent function.

#### Sample code  
```
 onEvent = function (eventType, result) {
         if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
        {
            // Entered the room successfully
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVNET_TYPE_USER_UPDATE)
        {
            app._data.downStreamInfoList = result.PeerInfo;// Peer information received. See the table below.
            app._data.brSend = result.UploadBRSend;// Upload bitrate
            app._data.rtt = result.UploadRTT;// Upload RTT
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM)
        {
            // Exited the room successfully
        }
        else if (eventType === gmeAPI.event.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT)
        {
            // Room disconnected
        }
    };
```


The peer information received is as follows (downStreamInfoList): 

| Parameter | Description |
| ------------- |------------|
| brRecv | Bitrate of information receiving |
| delay | Delay of information receiving |
| jitterBufferMs | Delay caused by jitter |
| jitterReceived | Jitter of information receiving |


### Exit a room
This API is used to exit the current room. It is an asynchronous API, and a callback response is returned after the user exits the room. The returned value of AV_OK indicates a successful asynchronous delivery.
#### Function prototype  
```
WebGMEAPI.fn.ExitRoom = function (){...}
```
#### Sample code  
```
gmeAPI.ExitRoom();
```

### Enable/disable the microphone
This API is used to enable/disable the microphone. Microphone and speaker are not enabled by default after a user enters a room.

#### Function prototype  
```
WebGMEAPI.fn.EnableMic = function (bEnable) {...}
```
| Parameter | Description |
| ------------- |------------|
| isEnabled | To enable the microphone, set this parameter to true, otherwise set it to false. |

#### Sample code  
```
gmeAPI.EnableMic(false);
```



### Set the microphone volume
This API is used to set microphone volume. The corresponding parameter is "volume". "0" means the volume is set to Mute, and "100" means the volume remains unchanged. It defaults to 100.

#### Function prototype  
```
WebGMEAPI.fn.SetMicVolume = function (volume){...}
```
| Parameter | Description |
| -------------|-------------|
| volume | Sets the volume. Value range: 0 to 100. |

#### Sample code  
```
gmeAPI.SetMicVolume(100);
```


### Enable/disable the speaker
This API is used to enable/disable the speaker.
#### Function prototype  
```
WebGMEAPI.fn.EnableSpeaker = function (bEnable){...}
```
| Parameter | Description |
| ------------- |------------|
| isEnabled | To disable the speaker, set this parameter to false, otherwise set it to true. |

#### Sample code  
```
gmeAPI.EnableSpeaker(true);
```

