
Junior developers can use basic feature APIs to access and try out basic TRTC features, such as detecting whether a device supports WebRTC, initializing WebRTC, creating and entering a room, and exiting a room. Such APIs are described in detail as below:

### WebRTCAPI.fn.detectRTC
This API is used to detect whether device supports WebRTC.
#### Sample syntax
```javascript
WebRTCAPI.fn.detectRTC(options, callback)
```

#### Descriptions of parameters

| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| options         | object | Parameter      |

#### options

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- | ----|
| screenshare         | boolean |No| Whether to perform screen sharing detection. Default value: true      |
| extensionId         | String |No| Screen sharing extension ID (unique extension ID in Chrome) |


#### `info` field in the callback

| Field | Description | Remarks |
| ------ | ----- | ------ |
| isTBS      | Whether the service is TBS (Android WeChat/Mobile QQ WebView) |   [What Is TBS?](https://x5.tencent.com/tbs/index.html)              |
| TBSversion      | TBS version number |   -              |
| isTBSValid      | Whether the TBS version supports WebRTC |        -         |
| support      | Whether WebRTC is supported | - |
| h264Support      | Whether H.264 is supported |H.264 must be supported |
| screenshare      | Whether screen sharing is supported |The extension must be installed |


#### Sample code
```javascript
WebRTCAPI.fn.detectRTC({
        screenshare : false
    }, function(info){
    if( !info.support ) {
        alert('WebRTC is not supported')
    }
});
```

### WebRTCAPI
This API is used to initialize WebRTC.
#### Sample syntax
```javascript
var RTC = new WebRTCAPI( options )
```
#### Descriptions of parameters

| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| options         | object | Parameter      |

#### Descriptions of options

| Parameter | Type | Description | Remarks |
| ---------------- | ------- | ---------------------------------------- | ------------ |
| **sdkAppId**         | integer | `sdkAppId` of the application (for more information, please see [Integrating the SDK ](/document/product/647/16863))              | Required           |
| **userId**           | string  | Unique user ID, i.e., username (for more information, please see [Integrating the SDK](/document/product/647/16863)) | Required           |
| **userSig**          | string  | Identity signature, which acts as the login password and is required (for more information, please see [Integrating the SDK](/document/product/647/16863))                     | Required           |
| debug            | object | Debugging mode (log printing in the console) `{ log: true, uploadLog: true, vconsole: true}`                                 | Required |
| peerAddNotify            | boolean | Notification of P2P connection establishment. Before a P2P connection is established, the business side determines whether a connection is needed.<br />It must be used together with `onPeerConnectionAdd` of "advanced event notifications" | Optional. Default value: false  |

- Disused parameters (for the SDK v3.0 or below)
closeLocalMedia => New SDK versions do not perform push by default
audio, video => New SDK versions no longer support configuration of whether to enable audio/video push

#### Sample code
```javascript
    var RTC = new WebRTCAPI( {
        "userId": userId,
        "sdkAppId":  sdkappid,
        "userSig": userSig
    } );

    // Debugging mode
    var RTC = new WebRTCAPI( {
        "userId": userId,
        "sdkAppId":  sdkappid,
        "userSig": userSig,
        "debug":{
            "log": true, // Whether to print debugging logs in the console. Default value: false
            "vconsole": true, // Whether to display `vconsole` (for convenient viewing of logs on mobile devices)
            "uploadLog": true // Whether to report logs
        }
    } );
```





### WebRTCAPI.getLocalStream

>!This API is supported by SDK v2.5 or above.

This API is used to get local audio/video stream.




| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- |-------- |
| opts         | Object | No | An empty object `{}` can be passed in    |
| succ         | function |Yes |  Callback on success      |
| fail         | function |No |  Callback on failure      |

#### Definitions of `opts` parameters

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- |-------- |
| audio         | Boolean |No | Whether to capture audio. Default value: true  |
| video         | Boolean |No | Whether to capture video. Default value: true   |
| screen         | Boolean |No | Whether to capture screen sharing video. Default value: false   |
| screenSources | string   |No | Screen sharing media to be captured, which are separated by commas (,). Valid values: screen, window, tab, audio |
| attributes         | Object |No | Attributes of push configuration items |
| videoDevice         | Device \| Object |No | Specifies the device, i.e., the video device obtained by `getVideoDevices`<br /> The `facingMode` parameter can be used to specify a device that supports differentiation between the front and rear cameras   |
| audioDevice         | Device |No | Specifies the device, i.e., the audio device obtained by `getVideoDevices`   |
| needRetry         | Boolean |No | Whether to allow downgrade to remove configurations and retry when the parameter configurations fail to be obtained. Default value: true |

#### Definitions of `attributes` parameters

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- |-------- |
| width         | Integer |No | Resolution width  |
| height         | Integer |No | Resolution height |
| frameRate         | Integer |No | Frame rate   |

#### `succ` callback (`Object`)
| Parameter | Type | Description |
| -------------------- | -------- |-------- |
| stream         | MediaStream |Audio/video stream. For more information, please see [MediaStream ](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)   |



#### Sample syntax

```javascript
    var RTC = new WebRTCAPI({ ... });
    ...

    RTC.getLocalStream({
        video:true,
        audio:true,
        attributes:{
            width:640,
            height:480,
            frameRate:20
        }
    },function( info ){
        // info { stream }
        var stream = info.stream;
        document.getElementById("localVideo").srcObject = stream
    },function ( error ){
        console.error( error )
    });


    // Specify the device by enumerating devices or setting `VideoDevice`
    ···
    var devices = [];
    RTC.getVideoDevices( function( ret ){
        devices = ret
    })
    ··· 
    //`getVideoDevices` is an async API. Please pay attention to the time sequence of calling `getLocalStream` in actual development
    RTC.getLocalStream({
        video:true,
        audio:true,
        videoDevice: devices[0]
    },function( info ){
       ...
    },function ( error ){
       ...
    });


    // Use the `facingMode` parameter to specify the device
    RTC.getLocalStream({
        video:true,
        audio:true,
        videoDevice: {
            facingMode:{
                ideal:'user'  // `environment` indicates the rear camera  | `user` indicates the front camera
            }
        }
    },function( info ){
       ...
    },function ( error ){
       ...
    });
```
[Sample code](https://gitee.com/vqcloud/webrtc-samples/blob/master/pushStream/js/index.js)



### WebRTCAPI.enterRoom
This API is used to create or enter audio/video room.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI( ... )
    ...
    // Note: this API must be called in the callback of successful `WebRTCAPI` initialization
    RTC.enterRoom( options, succ , error );
```

#### Descriptions of parameters

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- |-------------            |
| **options**         | object | No      |Parameter            |
| **succ**         | function | No      |Callback on success            |
| **error**         | function | No      |Callback on failure            |

#### Descriptions of options

| Parameter | Type | Required | Description |
| ---------------- | ------- | ---------------------- |--------------------------------- |
| **roomid**         | integer | Yes      | Room ID in `uint32` data type     |
| **privateMapKey**  | string  | No      | If the business does not need to control user permissions, this parameter can be ignored, which acts as the key to the specified `roomID` (for more information, please see [Integrating the SDK](/document/product/647/16863))                     |
| pureAudioPushMod   | integer |  No      |Pure audio stream push mode, which needs to be carried in **relayed LVB and recording** scenarios<br>1 indicates that the stream is pure audio push and does not need to be recorded as an MP3 file <br>2 indicates that the stream is pure audio push and the recording file format is MP3         |
| recordId         | integer |  No      | Custom ID in automatic recording in `int32` data type. This parameter will be returned to the business through the LVB recording callback API ([Console - LVB Recording Callback](https://console.cloud.tencent.com/live/livecodemanage)) after recording. For more information, please see [Event Message Notification](https://intl.cloud.tencent.com/document/product/267/31566)<br>**Note**: if `recordId` is delivered when a WeChat Mini Program communicates with another WeChat Mini Program and a web client, the values delivered to the web client and WeChat Mini Program must be the same       |
| appScene          | string   |No  | Application scenario. `VideoCall` indicates the real-time call mode, and `Live` indicates the ILVB mode |
| role          | string   |No  | Role name. The role determines the bitrate control mode for the server to receive a video stream. When the `appScene` parameter is set, `role` can be set to `anchor` or `audience`; if neither `appScene` nor `role` is set, the role will be anchor in real-time call by default; if `appScene` is set to `Live` and `role` is set to `audience`, i.e., the viewer role in the ILVB mode, the user can only receive remote audio/video streams but cannot publish local audio/video streams.|


>!
>- `role` informs the backend of the bitrate range of the current stream. Please configure an appropriate bitrate in the console.
>- `role` can be carried when `enterRoom` or `startRTC` is called. It is recommended to carry it during room entry so that processing will be faster.
>- `privateMapKey` does not affect business development. If user permission control is not required currently, this section can be ignored.


#### Sample code
```javascript
var RTC = new WebRTCAPI({
    "userId": "username",
    "sdkAppId":  1400012345,
    "userSig": "xxxxxxxxxxxxxxxxxxxxxxxxx",
});

RTC.enterRoom( {
    roomid : 123456,
    role: 'user'
    // privateMapKey: "xxxxxxxxxxxxx" // Optional
}, function(){
    // The user successfully entered the room
} ,  function(data){
    // The user failed to enter the room
} );
```



### WebRTCAPI.startRTC


This API is used to actively initiate push/pull.

#### Parameters

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- | ---- |
| opt         | object | Yes      | -  |
| succ         | function | No | Callback on success    |
| fail         | function | No | Callback on failure     |

#### Definitions of `opts` parameters

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- |------------- |
| stream         | MediaStream |No | Audio/video stream [ MediaStream](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)   |
| role          | string   |Yes  | Role name. The role determines the bitrate control mode for the server to receive the video stream |

#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...

    RTC.startRTC({
        role: 'user',
        stream: stream
    }, function(){
        // Success
    },function(){
        // Failure
    });
```


### WebRTCAPI.stopRTC
This API is used to stop push.

| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| opt         | object | Reserved field. Pass in an empty object for it     |
| succ         | function | Callback on success      |
| fail         | function | Callback on failure    |

#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.stopRTC({}, function(){
        console.debug('stop succ')
    }, function(){
        console.debug('stop end')
    });

```


### WebRTCAPI.quit
This API is used to exit audio/video room.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI( ... )
    ...
    // Note: this API must be called in the callback of successful `WebRTCAPI` initialization
    RTC.quit(  succ , error );
```

#### Descriptions of parameters

| Parameter | Type | Description | Remarks |
| -------------------- | -------- | ------------- | ---- |
| succ         | function | Callback on success     |      |    Optional |
| error         | function | Callback on failure      |Optional |

#### Sample code
```javascript
    var RTC = new WebRTCAPI( ... )
    ...
    // Note: this API must be called in the callback of successful `WebRTCAPI` initialization
    RTC.quit(  function(){
        //The user successfully exited the room
    } , function(){
        //The user failed to exit the room
    } );
```
