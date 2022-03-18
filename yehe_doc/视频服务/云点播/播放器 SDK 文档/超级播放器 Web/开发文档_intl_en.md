
This document describes the **parameters and APIs** of the web superplayer of VOD, which should be used together with [Integration Guide](https://intl.cloud.tencent.com/document/product/266/33977). This document is intended for developers who have a basic knowledge of JavaScript.

## Initialization Parameters
Two parameters should be passed in for initializing the player, namely, the player container ID and the function parameter object.
```
var player = TCPlayer('player-container-id', options);
```

### options parameter list
The parameters that can be configured for the `options` object include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  appID |  String |   None | Required. |
| fileID | String | None | Required. |
|  width | String/Number| None | Player zone width in pixels, which should be set as needed and can control the player size through CSS. |
|  height | String/Number| None | Player zone height in pixels, which should be set as needed and can control the player size through CSS. |
| controls | Boolean | true | Whether to display the control bar of the player. |
| poster | String | None | Sets the full address of the cover image (if the uploaded video already has a generated cover, it will be used preferably. For more information, please see [Managing Video](https://intl.cloud.tencent.com/document/product/266/33896)). |
| autoplay | Boolean | false | Whether to play back automatically. |
|  playbackRates | Array | [0.5, 1, 1.25, 1.5, 2] | Sets the adjustable-speed playback option, which is available only for HTML5. |
| loop | Boolean | false | Whether to loop the video. |
| muted | Boolean | false | Whether to mute the video. |
| preload | String | auto | Whether preloading is required. There are three attributes: "auto", "meta", and "none". Due to the system restrictions, "auto" doesn't take effect for mobile devices. |
| swf | String | None | URL of the .swf file in the Flash player. |
| posterImage | Boolean | true | Whether to display the cover. |
| bigPlayButton | Boolean | true | Whether to display the centered play button (the play button embedded by browser-hijacking cannot be removed). |
| language | String | "zh-CN" | Sets the language. |
| languages | Object | None | Sets the multilingual dictionary. |
| controlBar | Object | None | Sets the parameter combination of the control bar attributes as detailed below. |
| plugins | Object | None | Sets the parameter combination of the plugin function attributes as detailed below. |
| hlsConfig | Object | None | hls.js startup configuration. For more information, please see [Fine Tuning](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning). |

>! The `controls`, `playbackRates`, `loop`, `preload`, and `posterImage` parameters won't take effect during browser-hijacking playback.

#### controlBar parameter list
The `controlBar` parameters can configure the features of the player's control bar. The supported attributes include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| playToggle | Boolean | true | Whether to display the play/pause toggle button. |
| progressControl | Boolean | true | Whether to display the progress bar. |
| volumePanel | Boolean | true | Whether to display the volume control. |
| currentTimeDisplay | Boolean | true | Whether to display the current time of the video. |
| durationDisplay | Boolean | true | Whether to display the video duration. |
| timeDivider | Boolean | true | Whether to display the time separator. |
| playbackRateMenuButton | Boolean | true | Whether to display the playback speed selection button. |
| fullscreenToggle | Boolean | true | Whether to display the full screen toggle button. |
| QualitySwitcherMenuButton | Boolean | true | Whether to display the definition switching menu. |

>! The `controlBar` parameters won't take effect during browser-hijacking playback.

#### plugins parameter list
The `plugins` parameters can configure the features of the player plugins. The supported attributes include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| ContinuePlay | Object | None | Controls the playback resumption feature. The supported attributes include: <br><li>auto: false (whether to automatically resume during playback). <br><li>text: "You left off at" (prompt text). <br><li>btnText: "Resume" (button text).<br>

## Object Methods
Below lists the methods of the objects returned by player initialization:

| Name | Parameter and Type | Returned Value and Type | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
| ready(function) | (Function) | None | Sets the callback after the player is initialized. |
| play() | None | None | Plays and resumes the video. |
| pause() | None | None | Pauses the video. |
| currentTime(seconds) | (Number) | (Number) | Gets the current playback timepoint, or sets the playback timepoint, which cannot exceed the video duration. |
| duration() | None | (Number) | Gets the video duration. |
| volume(percent) | (Number) [0, 1] [optional] | (Number) / No return when setting | Gets or sets the player volume. |
| poster(src) | (String) | (String) / No return when setting | Gets or sets the player cover. |
| requestFullscreen() | None | None | Enters full screen mode. |
| exitFullscreen() | None | None | Exits full screen mode. |
| isFullscreen() | None | Boolean | Returns whether full screen mode is entered. |
| on(type,listerner) | (String, Function) | None | Listens on events. |
| one(type,listerner) | (String, Function) | None | Listens on events. The event handler can be executed at most once. |
| off(type,listerner) | (String, Function) | None | Unbinds event listening. |
| buffered() | None | TimeRanges | Returns the time range of video buffering. |
| bufferedPercent() | None | Value range [0, 1] | Returns the percentage of the buffered length in the video duration. |
| width() | (Number) [optional] | (Number) / No return when setting | Gets or sets the width of the player zone. If the player size is set through CSS, this method won't take effect. |
| height() | (Number) [optional] | (Number) / No return when setting | Gets or sets the height of the player zone. If the player size is set through CSS, this method won't take effect. |
| videoWidth() | None | (Number) | Gets the width of the video resolution. |
| videoHeight() | None | (Number) | Gets the height of the video resolution. |
| dispose() | None | None | Terminates the player. |

>! Object methods cannot be called synchronously but can be called only after the corresponding events (such as `loadedmetadata`) are triggered, except `ready`, `on`, `one`, and `off`.

## Event
The player can perform event listening through the objects returned by the initialization, for example:
```
var player = TCPlayer('player-container-id', options);
// player.on(type, function);
player.on('error', function(error) {
   // Process
});
```
Here, `type` is the event type. The supported events include:

| Name | Description |
|------------|---------------------------------|
| play| Playback has started. This is triggered when the `play()` method is called or `autoplay` is set to `true` and takes effect. At this time, the `paused` attribute is `false`. |
| playing | Triggered when the playback is paused due to buffering or resumed after pause. The `paused` attribute is `false`. Usually, this event is used to mark that the video playback has actually started, as the `play` event just starts the playback, but the image has not started rendering. |
| loadstart | Triggered when data loading starts. |
| durationchange | Triggered when the duration data of the video changes. |
| loadedmetadata | The video metadata has been loaded. |
| loadeddata | This event is triggered when the data of the current frame is loaded but there is no enough data to play back the next frame of the video. |
| progress | Triggered when the media data is obtained. |
| canplay | Triggered when the player is able to start playing back the video. |
| canplaythrough | Triggered when the player is expected to be able to continue playing back the specified video without buffering. |
| error | Triggered when an error occurs in video playback. |
| pause | Triggered when the video is paused. |
| ratechange | Triggered when the playback speed changes. |
| seeked | Triggered when seeking for the specified playback position ends. |
| seeking | Triggered when seeking for the specified playback position starts. |
| timeupdate | The current playback position has changed, which can be understood as that `currentTime` has changed. |
| volumechange | Triggered when the volume is set or the value of the `muted` attribute changes. |
| waiting | Triggered when the video is stopped and the next frame of content is unavailable. |
| ended | Triggered when the video playback ends. In this case, the `currentTime` value is equal to the maximum value of the media resource. |
| resolutionswitching | Definition switching is in progress. |
| resolutionswitched | Definition switching is completed. |
| fullscreenchange | Triggered when full screen mode is switched. |

## Error Codes
When the player triggers an error event, the listener will return an error code. Error codes containing more than 3 digits are for media data APIs. Below is the error code list:

| Name | Description |
|------|----------------------------------------------|
| -1 | The player didn't detect an available video address. |
| -2 | Getting video data timed out. |
| 1 | The video data was interrupted during loading. <br>Possible causes: <br><li>The network was interrupted. <br><li>The browser was interrupted. <br>Solutions: <br><li>Check the network request information in the network console to confirm whether the network request was normal. <br><li>Restart the playback process. |
| 2 | Failed to load the video due to network problems. <br>Possible causes: the network was interrupted. <br>Solutions: <br><li>Check the network request information in the network console to confirm whether the network request was normal. <br><li>Restart the playback process. |
| 3 | An error occurred while decoding the video. <br>Possible causes: the video data was exceptional and the decoder failed to decode it. <br>Solutions:<br><li>Try transcoding and playing back the video again to troubleshoot problems introduced by the transcoding process. <br><li>Check whether the original video is normal. <br><li>Contact technical support and provide playback parameters for troubleshooting. |
| 4 | The video couldn't be loaded due to unsupported format or server or network issues. <br>Possible causes: <br><li>The video data couldn't be obtained, the CDN resource does not exist, or the video data was not returned. <br><li>The current playback environment does not support this video format. <br>Solutions:<br><li>Check the network request information in the network console to confirm whether the video data request was normal. <br><li>Check whether the corresponding playback script for this video format was loaded according to the user guide. <br><li>Check whether the current browser and webpage environment support this video format. <br><li>Contact technical support and provide playback parameters for troubleshooting. |
| 5 | An error occurred while decrypting the video. <br>Possible causes: <br><li>The decryption key is incorrect. <br><li>The key requesting API returned exceptionally. <br><li>The current playback environment doesn't support the video decryption feature. <br>Solutions: <br><li>Check whether the key is correct and whether the key API returns normally. <br><li>Contact technical support and provide playback parameters for troubleshooting.<br> |
| 10 | Requesting the VOD media data API timed out. When trying to get the media data, if the player still has no response after 3 retries, this error will be thrown. <br>Possible causes: <br><li>The current network couldn't connect to the media data API, or the media data API was hijacked. <br><li>The media data API was exceptional. <br>Solutions:<br><li>Try opening the demo page provided by us to see whether it can play back the video normally. <br><li>Contact technical support and provide playback parameters for troubleshooting. <br> |
| 11 | The VOD media data API didn't return any data. When trying to get the media data, if the player still doesn't receive data after 3 retries, this error will be thrown. <br>Possible causes: <br><li>The current network couldn't connect to the media data API, or the media data API was hijacked. <br><li>The media data API was exceptional. <br>Solutions:<br><li>Try opening the demo page provided by us to see whether it can play back the video normally. <br><li>Contact technical support and provide playback parameters for troubleshooting. <br> |
| 12 | The VOD media data API returned exceptional data. When trying to get the media data, if the player still receives unparseable data after 3 retries, this error will be thrown. <br>Possible causes: <br><li>The current network couldn't connect to the media data API, or the media data API was hijacked. <br><li>The playback parameters were incorrect and thus couldn't be processed by the media data API. <br><li>The media data API was exceptional. <br>Solutions:<br><li>Try opening the demo page provided by us to see whether it can play back the video normally. <br><li>Contact technical support and provide playback parameters for troubleshooting. <br> |
| 13 | The player didn't detect video data that could be played back in the current player. Please transcode the video. |
| 14 | A network exception occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, please see [Network Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#network-errors). |
| 15 | A multimedia exception occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, please see [Media Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#media-errors). |
| 16 | A remuxing exception occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, please see [Mux Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#mux-errors). |
| 17 | An exception of other types occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, please see [Other Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#other-errors). |
| 10008| The media data service did not find the media data corresponding to the playback parameters. Please check whether the request parameters `appID` and `fileID` are correct and whether the corresponding media data has been deleted. |
