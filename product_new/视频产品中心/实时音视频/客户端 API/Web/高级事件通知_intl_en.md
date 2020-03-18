
### onStreamNotify
Video stream event notification.

#### Sample syntax
```javascript
    RTC.on( 'onStreamNotify' , function( info ){ })
```

#### info

| Parameter | Type | Description |
| --------- | ------ | ------------ |
| event | String | onadd: audio/video stream is added; inactive: audio/video stream is closed |
| isLocal | Bool | Whether the stream is local |
| stream | Stream | Stream data, which is a `MediaStream` object |
| type | Type | stream/audio/video (`stream` is the carrier of audio and video tracks. If `Type` is `stream`, it indicates that the stream has been closed)|

#### Sample code
```javascript
    RTC.on( 'onStreamNotify' , function( info ){
        
    })
```



### onErrorNotify
Error event notification.

#### Sample syntax
```javascript
    RTC.on( 'onErrorNotify' , function( info ){ })
```

#### info

| Parameter | Type | Description |
| --------- | ------ | ------------ |
| errorCode | Integer | Error code |
| errorMsg | String | Error message |

#### Sample code
```javascript
    RTC.on( 'onErrorNotify' , function( info ){
        
    })
```




### onWebSocketNotify
WebSocket event notification

#### Sample syntax
```javascript
    RTC.on( 'onWebSocketNotify' , function( info ){ })
```

#### info

| Parameter | Type | Description |
| --------- | ------ | ------------ |
| errorCode | Integer | Error code |
| errorMsg | String | Error message |
| extInfo | Object | Detailed WebSocket information |


#### Sample code
```javascript
    var error_code_map = WebRTCAPI.fn.getErrorCode();
    
    RTC.on( 'onWebsocketNotify' , function( info ){
        switch( info.errorCode ){
            case 0:
                // conn succ
                break;
            case error_code_map.WS_CLOSE:
                // close
                console.warn( info );
                break;
            case error_code_map.WS_ERROR:
                // error
                console.error( info );
                break;
            default:
                break;
        }
    })
```


### onPeerConnectionAdd
`PeerConnection` connection notification, through which the business can determine whether a P2P connection is needed before establishing it. It needs to be used together with the instantiated parameter `peerAddNotify`.

The demo provides sample code for `PeerConnection`.

#### Sample syntax
```javascript
    RTC.on( 'onPeerConnectionAdd' , function( info ){ })
```



#### info

| Parameter | Type | Description |
| --------- | ------ | ------------ |
| userId | String | Username of the user to whom the connection belongs |
| tinyId | String | Unique 64-bit ID in Tencent Cloud corresponding to the username of the user to whom the connection belongs. You do not have to understand what this parameter does; instead, you only need to pass it through when calling `startRTC`. |

#### Sample code
```javascript
    RTC.on( 'onPeerConnectionAdd' , function( info ){
        // Whether to establish `PeerConnection`, which is determined by the business
        if( info.userId === 'specify username'){
            WebRTCAPI.startRTC( info );
        }else{
            console.debug('Do not establish connection')
        }
    })
```
