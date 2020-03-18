
Basic event notifications are for events such as addition/update of a local or remote video stream, disconnection of a remote video stream, WebSocket disconnection, disconnection from the video stream server due to timeout, and being kicked offline (due to repeated logins of the same user), which are described in detail as below:

Basic syntax of an event notification:
```javascript
    var RTC = new WebRTCAPI( { ... } );

    ......

    RTC.on( 'EVENT_NAME' , function(data){

    })
  ```


## onLocalStreamAdd
Notification for adding/updating a local video stream.
#### Sample code
```javascript
    var RTC = new WebRTCAPI( { ... } );

    RTC.on( 'onLocalStreamAdd' , function( data ){
        if( data && data.stream){
            var stream = data.stream
            document.querySelector("#localVideo").srcObject = stream
        }
    })
```
#### data
| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| stream         | Stream | Local video stream      |


## onRemoteStreamUpdate
Notification for adding/updating a remote video stream.
#### Sample code
```javascript
    var RTC = new WebRTCAPI( { ... } );

    RTC.on( 'onRemoteStreamUpdate' , function( data ){
        if( data && data.stream){
            var stream = data.stream
            console.debug( data.userId + 'enter this room with unique videoId '+ data.videoId  )
            document.querySelector("#remoteVideo").srcObject = stream
        }else{
            console.debug( 'somebody enter this room without stream' )
        }
    })
```
#### data
| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| userId     | String  | `userId` of the user to whom the video stream belongs    |
| stream     | Stream  | Video stream, which may be `null` (no matter whether push is enabled, this callback will be triggered whenever a user enters the room)  |
| videoId    | String  | Unique ID of the video stream, which is in the format of `tinyid + "_" + random string`      |
| videoType: | Integer | 0: NONE (none); 1: AUDIO (audio); 2: MAIN (primary channel); 7: AID (secondary channel) |


## onRemoteStreamRemove
Notification for remote video disconnection.
#### Sample code
```javascript
    var RTC = new WebRTCAPI( { ... } );

    RTC.on( 'onRemoteStreamRemove' , function( data ){
        console.debug( data.userId + ' leave this room with unique videoId '+ data.videoId  )
    })
```

#### data
| Parameter | Type | Description |
| -------------------- | -------- | ------------- | 
| userId         | String | `userId` of the user to whom the remote video stream belongs    |
| videoId    | String  | Unique ID of the remote video stream      |


## onWebSocketClose
Notification for WebSocket disconnection.
#### Sample code
```javascript
    var RTC = new WebRTCAPI( { ... } );

    RTC.on( 'onWebSocketClose' , function( data ){

    })
```

## onRelayTimeout
Notification for disconnection from the video stream server.
#### Sample code
```javascript
    var RTC = new WebRTCAPI( { ... } );

    RTC.on( 'onRelayTimeout' , function( data ){
        // The video server timed out
    })
```


## onKickout
Notification for being kicked offline (due to repeated logins of the same user).
#### Sample code
```javascript
    var RTC = new WebRTCAPI( { ... } );

    RTC.on( 'onKickout' , function( data ){
        // The user exited the room
    })
```

## onMuteAudio
Notification that reminds the remote application user to disable mic in audio call.
#### Sample code
```javascript
RTC.on('onMuteAudio', (evt) => {
    console.log(`user:${evt.userId} mute audio`);
});
```
#### evt
| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| userId     | String  | `userId` of the remote user    |
 
## onUnmuteAudio
Notification that reminds the remote application user to enable mic in audio call.

#### Sample code
```javascript
RTC.on('onUnmuteAudio', (evt) => {
    console.log(`user:${evt.userId} unmute audio`);
});
```
#### evt
| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| userId     | String  | `userId` of the remote user    |

## onMuteVideo
Notification that reminds the remote application user to disable camera in video call.

#### Sample code
```javascript
RTC.on('onMuteVideo', (evt) => {
    console.log(`user:${evt.userId} mute video`);
});
```
#### evt
| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| userId     | String  | `userId` of the remote user    |

## onUnmuteVideo
Notification that reminds the remote application user to enable camera in video call.

#### Sample code
```javascript
RTC.on('onUnmuteVideo', (evt) => {
    console.log(`user:${evt.userId} unmute video`);
});
```
#### evt
| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| userId     | String  | `userId` of the remote user    
