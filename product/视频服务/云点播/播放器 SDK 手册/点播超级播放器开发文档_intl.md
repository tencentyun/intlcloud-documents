This document describes the parameters and APIs of the Super Player of Tencent Cloud Web VOD service. Use this document with the **Usage Guide**.  This document is written for developers who have at least basic JavaScript knowledge.

## Initializing Parameters
It is required to pass the player container ID and the options of the functional objects into the function to initialize the Super Player.
```
var player = TCPlayer('player-container-id', options);
```

### List of options Parameters
The parameters that can be configured for the object include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| appID | String | None | Required |
| fileID | String | None | Required |  
| width | String/Number | None | Player zone width in pixels, which should be set as needed and can control the player size via CSS. |
| height | String/Number | None | Player zone height in pixels, which should be set as needed and can control the player size via CSS. |  
| controls | Boolean | true | Whether to display the control bar of the player |  
| poster | String | None | Set the full address of the cover image (if the uploaded video already have a generated cover, it will be used preferably. For more information, see **VOD Console** > **Video Management**) |  
| autoplay | Boolean | false | Whether to play automatically |  
| playbackRates | Array | [0.5, 1, 1.25, 1.5, 2] | Set the adjustable-speed playback option, which is available only for HTML5 |  
| loop | Boolean | false | Whether to loop the playback |  
| muted | Boolean | false | Whether to mute the playback |  
| preload | String | auto | Whether preloading is required. There are three attributes: "auto", "meta", and "none". Due to the system restrictions, "auto" is invalid for mobile devices. |  
| swf | String | None | URL of the .swf file in the Flash player |  
| posterImage | Boolean | true | Whether to display the cover |  
| bigPlayButton | Boolean | true | Whether to display the centered play button (the play button embedded by browser-hijacking cannot be removed) |  
| language | String | "zh-CN" | Set the language |  
| languages | Object | None | Set the multilingual dictionary |  
| controlBar | Object | None | Set the parameter combination of the control bar attributes which are detailed later |  
| plugins | Object | None | Set the parameter combination of the plugin function attributes which are detailed later |  
| hlsConfig | Object | None | hls.js startup configuration. For more information, see the official documentation of [hls.js](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning) |  

#### List of controlBar Parameters
The controlBar parameters can configure the functions of the player's control bar. The supported attributes include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| playToggle | Boolean | true | Whether to display the play/pause toggle button |  
| progressControl | Boolean | true | Whether to display the progress bar |  
| volumePanel | Boolean | true | Whether to display the volume control |  
| currentTimeDisplay | Boolean | true | Whether to display the current time of the video |  
| durationDisplay | Boolean | true | Whether to display the video duration |  
| timeDivider | Boolean | true | Whether to display the time separator |  
| playbackRateMenuButton | Boolean | true | Whether to display the playback speed selection button |  
| fullscreenToggle | Boolean | true | Whether to display the full screen toggle button |  
| QualitySwitcherMenuButton | Boolean | true | Whether to display the definition switching menu |  

>! controlBar parameters are invalid during browser-hijacking playback. For more information, see [What Is Hijacking Playback?](https://cloud.tencent.com/document/product/266/1303#.E6.B5.8F.E8.A7.88.E5.99.A8.E5.8A.AB.E6.8C.81.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE)).

#### List of plugins Parameters
The plugins parameters can configure the functions of the player plugins. The supported attributes include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| ContinuePlay | Object | None | Control the resumed playback function. The supported attributes included: <br>auto: false (whether to automatically resume during playback); <br>text: "You left off at" (prompt text); <br>btnText: "Resume playback" (button text). <br>

## Object Methods
The following methods return objects after the player initialization：

| Name | Parameter and Type | Return Value and Type | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| ready(function) | (Function) | None | Set the callback after the player is initialized |  
| play() | None | None | Play and resume playback |  
| pause() | None | None | Pause |  
| currentTime(seconds) | (Number) | (Number) | Get the current playback time point, or set the playback time point, which cannot exceed the video duration |  
| duration() | None | (Number) | Get the video duration |  
| volume(percent) | (Number) [0, 1] [optional] | (Number) / No return when setting | Get or set the player volume |
| poster(src) | (String) | (String) / No return when setting | Get or set the player cover |
| requestFullscreen() | None | None | Enter full screen mode |  
| exitFullscreen() | None | None | Exit full screen mode |  
| isFullscreen() | None | Boolean | Return whether full screen mode is entered |  
| on(type,listerner) | (String, Function) | None | Listen to events |  
| one(type,listerner) | (String, Function) | None | Listen to events. The event handler can be executed at most once |  
| off(type,listerner) | (String, Function) | None | Unbind event listening |  
| buffered() | None | TimeRanges | Return the time range of video buffering |  
| bufferedPercent() | None | Value range [0, 1] | Return the percentage of the buffered length in the video duration |  
| width() | (Number) [optional] | (Number) / No return when setting | Get or set the width of the player zone. If the player size is set via CSS, this method will be invalid |
| height() | (Number) [optional] | (Number) / No return when setting | Get or set the height of the player zone. If the player size is set via CSS, this method will be invalid |
| videoWidth() | None | (Number) | Get the width of the video resolution |  
| videoHeight() | None | (Number) | Get the height of the video resolution |  
| dispose() | None | None | Terminate the player |  

>! Object methods cannot be called synchronously and can be called only after the corresponding events (such as loadedmetadata) are triggered, except ready, on, one, and off.

## Events
The player can perform event listening through the objects returned by the initialization, for example:
```
var player = TCPlayer('player-container-id', options);
player.on(type, function);
```
Here, type is the event type. Supported events include:

| Name | Description |  
|------------|---------------------------------|
| play| Playback has started. This is triggered when the play() method is called or autoplay is set to true and takes effect. At this time, the paused attribute is false |  
| playing | Triggered when the playback is paused due to buffering or resumed after pause. The paused attribute is false. Usually, this event is used to mark that the video has actually started playing, as the play event just starts the playback but the image has not started rendering |  
| loadstart | Triggered when data loading starts |  
| durationchange | Triggered when the duration data of the video changes |  
| loadedmetadata | Metadata for the loaded video |  
| loadeddata | This event is triggered when the data of the current frame is loaded but there is not enough data to play the next frame of the video |  
| progress | Triggered when the media data is obtained |  
| canplay | Trigger when the player is able to start playing the video |  
| canplaythrough | Triggered when the player is expected to be able to continue playing the specified video without buffering |
| error | Triggered when an error occurs in video playback |  
| pause | Triggered on pause |  
| ratechange | Triggered when the playback speed changes |  
| seeked | Triggered at the end of the seeking for the specified playback position |  
| seeking | Trigger when seeking for the specified playback position |  
| timeupdate | The current playback position has changed, which can be understood as currentTime has changed |  
| volumechange | Triggered when the volume is set or the value of the muted attribute changes |  
| waiting | Triggered when the playback is paused and the next frame of content is unavailable |  
| ended | Triggered when the video has finished playing. At this time, the currentTime value is equal to the maximum value of the media resource |  
| resolutionswitching | Definition switching in progress |  
| resolutionswitched | Definition switched |  
| fullscreenchange | Triggered when full screen mode is switched |

## Error Codes
When the player triggers an error event, the listener returns an error code. Error code list:

| Name | Description |  
|------------|---------------------------------|
| -1 | No video address |  
| -2 | Getting video data timed out |  
| 1 | Video loading for playback is interrupted |  
| 2 | Video loading failed due to network problems |  
| 3 | An error occurred when decoding the video |  
| 4 | Unable to load the video due to unsupported format or server or network problems |  
| 5 | An error occurred when decrypting the video |  
| 10 | VOD API request timed out |  
| 11 | VOD API is not responding |  
| 12 | VOD API returned exceptional data |  
| 13 | VOD video was not transcoded and needs to be transcoded in the VOD console |
| 14 | A network exception occurred when playing an HLS video in HTML5 + hls.js mode. The exception details can be viewed in event.source. For more information. see the official document of hls.js: [Network Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#network-errors) |  
| 15 | A multimedia exception occurred when playing an HLS video in HTML5 + hls.js mode. The exception details can be viewed in event.source. For more information. see the official document of hls.js: [Media Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#media-errors) |  
| 16 | A multiplexing exception occurred when playing an HLS video in HTML5 + hls.js mode. The exception details can be viewed in event.source. For more information. see the official document of hls.js: [Mux Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#mux-errors) |  
| 17 | An exception of other types occurred when playing an HLS video in HTML5 + hls.js mode. The exception details can be viewed in event.source. For more information. see the official document of hls.js: [Other Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#other-errors) |  
