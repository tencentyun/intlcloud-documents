Senior developers can use the following advanced feature APIs and event notifications for development. These APIs are described in detail as below:


## WebRTCAPI.updateStream
>?This API is supported by versions above 2.5.3.

This API is used to stop push.

| Parameter | Type | Description |
| -------------------- | -------- | ------------- | 
| opt         | object | Parameter      |
| succ         | function | Callback on success      |
| fail         | function | Callback on failure    |

##### opt

| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| stream         | MediaStream | Reserved field. Pass in an empty object for it     |
| role         | string | This parameter will be used if the image role setting needs to be updated during stream update, which is optional      |


#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.updateStream({
        role: "user",
        stream: stream
    }, function(){
        console.debug('updateStream succ')
    }, function(){
        console.debug('updateStream failed')
    });

```


## WebRTCAPI.closeAudio
This API is used to disable audio capture (i.e., muting audio).
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...

    RTC.closeAudio();
```

## WebRTCAPI.openAudio
This API is used to capture the audio ID (i.e., unmuting audio).
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...

    RTC.openAudio();
```

## WebRTCAPI.closeVideo
This API is used to disable video capture.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...

    RTC.closeVideo();
```

## WebRTCAPI.openVideo
This API is used to enable video capture.
> Here, `openVideo` is called to enable video capture after video is disabled during audio/video push.


#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...

    RTC.openVideo();
```

## WebRTCAPI.getLocalMediaStatus
This API is used to get current video capture configuration.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    var status = RTC.getLocalMediaStatus();
```

## WebRTCAPI.changeSpearRole
This API is used to switch user roles set for image.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.changeSpearRole( "role_name" );
```

## WebRTCAPI.getVideoDevices
This API is used to enumerate cameras.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.getVideoDevices( function(devices){
        // `devices` is a `(DeviceObject)` array that enumerates video input devices of the current device
        // For example, `[device,device,device]`
        // These devices will be used during camera selection
    })
```

## WebRTCAPI.chooseVideoDevice
This API is used to select camera.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.chooseVideoDevice( device );

```

## WebRTCAPI.getAudioDevices
This API is used to enumerate mics.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.getAudioDevices( function(devices){
        // `devices` is a `(DeviceObject)` array that enumerates audio input devices of the current device
        // For example, `[device,device,device]`
        // These devices will be used during mic selection
    })
```

## WebRTCAPI.chooseAudioDevice
This API is used to select mic.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.chooseAudioDevice( device );

```


## WebRTCAPI.getSpeakerDevices

> This API is supported by versions above 2.6.

This API is used to enumerate audio output devices.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.getSpeakerDevices( function(devices){
        // `devices` is a `(DeviceObject)` array that enumerates audio output devices of the current device
        // For example, `[device,device,device]`
        // These devices will be used during selection of audio output device
    })
```

## WebRTCAPI.chooseSpeakerDevice

> This API is supported by versions above 2.6.


| Parameter | Type | Description |
| -------------------- | -------- | ------------- | 
| media         | HTMLMediaElement | Audio/Video      |
| device         | DeviceElement | Audio/Video      |
| succ         | function | Callback on success      |
| fail         | function | Callback on failure    |

This API is used to select audio output device.
#### Sample syntax
```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    var speakerList = [];
    RTC.getSpeakerDevices( function(devices){
        speakerList = devices;
    })
    ....
    document.querySelectorAll("video").forEach( function(video){
        // Set all video output devices on the current page
    	RTC.chooseSpeakerDevice( video, speakerList[1],function(){
            console.debug('change speaker succ ')
    	} ,function(error){
            console.error('change speaker error ', error)
    	} );
    });

```


## WebRTCAPI.getStats
This API is used to get or stop getting statistics.


| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- | ---- |
| opt         | object |  Yes     | -     |
| succ         | function |Yes |  Callback on success      |
| fail         | function | No | Callback on failure     |

#### Descriptions of `opt` parameters

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- | ---- |
| userId         | String | No       |  ID of the user whose audio/video stream statistics need to be obtained. If this parameter is left empty, the local audio/video stream statistics will be obtained |
| interval         | integer | No       | Timer in milliseconds, which indicates the time interval for getting statistics. If this parameter is left empty, the statistics will be obtained at a random interval. |


#### `result` description
```javascript
    // Send a stream
    {
        video:{
            ssrc        : "", // Data source id
            codec       : "", // Codec
            packetsSent : "", // Number of sent video packets
            packetsLost : "", // Number of lost video packets
            width       : "", // Video resolution - width
            height      : "", // Video resolution - height
        }
        audio:{
            ssrc        : "", // Data source ID
            codec       : "", // Codec
            packetsSent : "", // Number of sent audio packets
        }
    }

    // Receive a stream
    {
        video:{
            ssrc            : "", // Data source ID
            codec           : "", // Codec
            packetsReceived : "", // Number of received video packets
            packetsLost     : "", // Number of lost video packets
            width           : "", // Video resolution - width
            height          : "", // Video resolution - height
        }
        audio:{
            ssrc            : "", // Data source ID
            codec           : "", // Codec
            packetsReceived : "", // Number of received audio packets
            packetsLost     : "", // Number of lost audio packets
        }
    }


```

#### Sample syntax

```javascript
    var RTC = new WebRTCAPI({ ... });
    ...
    RTC.getStats( {
        interval:2000 // Get once every 2 seconds
    },function( result ){
        console.debug( result );
        // test code
        setTimeout( function(){
            // Stop collecting statistics
            result.nomore();
        },20000);
    } ,function( error ){
        console.error( error );
    } );

```


## WebRTCAPI.SoundMeter
This API is used to detect audio volume level.
#### Sample syntax

>?This API is supported by versions above 2.5.3.

#### Sample syntax
```javascript
    var soundMeter = WebRTCAPI.SoundMeter( opts )
```

#### opts

| Parameter | Type | Required | Description |
| -------------------- | -------- | ------------- |  ------------- |
| stream         | object |Yes | MediaStream     |
| onprocess         | function |Yes | Callback of audio stream monitoring      |

#### Callback parameters of `onprocess`

| Parameter | Type | Description |
| -------------------- | -------- | ------------- |
| volume         | String | Volume level (e.g., 0.02)     |
| status         | function | volume >= 0.01 ? "speaking" : "silence"      |
| event         | AudioProcessingEventObject |-   |


>?The value of `volume` indicates whether there is sound or not. If it is greater than or equal to 0.01, there is sound; otherwise, there is no sound, which can be considered as audio muting.


```javascript
    // Analyze an audio stream
    var meter = WebRTCAPI.SoundMeter({
        stream: info.stream,
        onprocess: function( data ){
            $("#volume").val( data.volume)
            $("#volume_str").text( "volume: "+ data.volume)
            $("#status").text( data.status )
        }
    })

    // Stop analyzing an audio stream
    meter.stop();

```
