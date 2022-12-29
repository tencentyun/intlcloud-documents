
This document describes the parameters and APIs of [Player for web (TCPlayer)](https://intl.cloud.tencent.com/document/product/266/33977) suitable for VOD and live playback and is intended for developers who have a basic knowledge of JavaScript.

## Initialization Parameters
Two parameters must be passed in for initializing the player, namely, the player container ID and the function parameter object.
```
var player = TCPlayer('player-container-id', options);
```

### List of options Parameters
The parameters that can be configured for the `options` object include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  appID|  String |   None | The `appID` of the Tencent Cloud account, which is required for VOD file playback through `fileID`. |
|  fileID|  String| None | The ID of the target file, which is required for VOD file playback through `fileID`. |
|  sources|  Array| None | The playback address in the format of `[{ src: '//path/to/video.mp4', type: 'video/mp4' }]` |  
|  width |  String/Number|  None | The player width in pixels, which should be set as needed and can control the player size through CSS. |
|  height |  String/Number|  None |  The player height in pixels, which should be set as needed and can control the player size through CSS. |
| controls | Boolean | true | Whether to display the control bar of the player. |
| poster | String | None | Sets the full address of the thumbnail image (if the uploaded video already has a generated thumbnail, it will be used preferably. For more information, see [Managing Video](https://intl.cloud.tencent.com/document/product/266/33896). |
| autoplay | Boolean | false | Whether to play automatically |
|  playbackRates | Array | [0.5, 1, 1.25, 1.5, 2] | The adjustable-speed playback options, which are available only for HTML5. |
| loop | Boolean | false | Whether to loop the playback. |
| muted | Boolean | false | Whether to mute the playback. |
|  preload |  String |  auto |  Whether preloading is required. Valid values: `auto`, `meta`, `none`. Due to the system restrictions, `auto` doesn't take effect for mobile devices. |
| swf | String | None | URL of the .swf file in the Flash player. |
| posterImage | Boolean | true | Whether to display the thumbnail image. |
| bigPlayButton | Boolean | true | Whether to display the centered play button (the play button embedded if the browser takes over video playback cannot be removed). |
|  language|  String|  "zh-CN" |  Sets the language. Valid values: "zh-CN", "en" |
| languages | Object | None | Sets the multilingual dictionary. |
| controlBar | Object | None | Set the parameter combination of the control bar attributes, which are detailed below. |
|  reportable|  Boolean |  true | Whether to enable data reporting |
| plugins | Object | None | Set the parameter combination of the plugin function attributes which are detailed below. |
|  hlsConfig|  Object| None |  The startup configuration of `hls.js`. For more information, see [Fine Tuning](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning).|
|  webrtcConfig|  Object|  None |  The startup configuration of WebRTC as detailed below. |  


>! The `controls`, `playbackRates`, `loop`, `preload`, and `posterImage` parameters won't take effect if the browser takes over video playback (see [Web Playback](https://intl.cloud.tencent.com/document/product/266/1303)).

#### List of controlBar Parameters
The controlBar parameters can configure the functions of the player's control bar. The supported attributes include:

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
s| QualitySwitcherMenuButton | Boolean | true | Whether to display the definition selection menu. |

>! The `controlBar` parameter won't take effect if the browser takes over video playback (see [Web Playback](https://intl.cloud.tencent.com/document/product/266/1303)).

#### List of plugins Parameters
The `plugins` parameters can configure the functions of the player plugins. The supported attributes include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  ContinuePlay|  Object|  None |  Controls the playback resumption feature. The supported attributes include:<br><li>auto: (Boolean) Whether to automatically resume during playback<br><li>text: (String) The prompt text<br><li>btnText: (String) The button text |
| VttThumbnail | Object | None | Controls the thumbnail display. The supported attributes include:<br><li>vttUrl: (String) The absolute address of the VTT file, which is required<br><li>basePath: (String) The image path, which is optional. If it is not specified, the path of `vttUrl` will be used<br><li>imgUrl: (String) The absolute address of the image, which is optional |
| ProgressMarker | Boolean | None | Controls the progress bar display. |
| DynamicWatermark | Object | None | Controls the dynamic watermark display. The supported attributes include:<br><li>content: (String) The content of the text watermark, which is required<br><li>speed: (Number) The watermark movement speed, which is optional. Value range: 0–1. |
| ContextMenu | Object | None | The supported attributes include:<br><li>mirror: (Boolean) Whether to support flipping the video image<br><li>statistic: (Boolean) Whether to support displaying the data panel<br><li>levelSwitch: (Object) The prompt text displayed during definition switch<br><li>&emsp;{<br><li>&emsp;&emsp;open: (Boolean) Whether to enable the prompt<br><li>&emsp;&emsp;switchingText: (String) The prompt text displayed when definition switch starts<br><li>&emsp;&emsp;switchedText: (String) The prompt text displayed when switch succeeds<br><li>&emsp;&emsp;switchErrorText: (String) The prompt text displayed when switch fails<br><li>&emsp;}|


#### List of webrtcConfig parameters
The `webrtcConfig` parameters are used to control behaviors during WebRTC file playback. The supported attributes include:

| Name | Type | Default Value | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  connectRetryCount| Number|  3|  The maximum number of reconnections of the SDK to the server. |  
|  connectRetryDelay|  Number| 1|  The interval between reconnections of the SDK to the server. |  
|  receiveVideo|  Boolean|  true| Whether to pull the video stream. |  
|  receiveAudio|  Boolean|  true|  Whether to pull the audio stream. |  
|  showLog|  Boolean|  false|  Whether to print logs in the console. |  


<br>

## APIs
Below lists the methods of the objects returned by player initialization:

| Name | Parameter and Type | Return Value and Type | Description |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  src()|  (String)|  None |  Sets the playback address. |  
| ready(function) | (Function) | None | Sets the callback after the player is initialized. |
| play() | None | None | Plays the video and resumes playback. |
| pause() | None | None | Pauses the video. |
| currentTime(seconds) | (Number) | (Number) | Gets the current playback time point, or sets the playback time point, which cannot exceed the video duration. |
| duration() | None | (Number) | Gets the video duration. |
| volume(percent) | (Number) [0, 1] [optional] | (Number) / No return when setting | Gets or sets the player volume. |
| poster(src) | (String) | (String) / No return when setting | Get or set the player thumbnail |
| requestFullscreen() | None | None | Enters full screen mode. |
| exitFullscreen() | None | None | Exits full screen mode. |
| isFullscreen() | None | Boolean | Returns whether full screen mode is entered. |
|  on(type,listener)|  (String, Function)|  None |  Listens for events. |
|  one(type,listener)|  (String, Function)|  None |  Listens for events. The event handler can be executed at most once. |
|  off(type,listener)|  (String, Function)|  None |  Unbinds event listening. |
| buffered() | None | TimeRanges | Returns the time range of video buffering. |
| bufferedPercent() | None | Value range [0, 1] | Returns the percentage of the buffered video duration. |
|  width()|  (Number) [optional]|  (Number) / No return when setting | Gets or sets the width of the player. If the player size is set through CSS, this method won't take effect. |
|  height()|  (Number) [optional]|  (Number) / No return when setting | Gets or sets the height of the player. If the player size is set through CSS, this method won't take effect. |
| videoWidth() | None | (Number) | Gets the width of the video resolution. |
| videoHeight() | None | (Number) | Gets the height of the video resolution. |
| dispose() | None | None | Terminates the player. |

>! Object methods cannot be called synchronously but can be called only after the corresponding events (such as `loadedmetadata`) are triggered, except `ready`, `on`, `one`, and `off`.

## Events
The player can perform event listening through the objects returned by the initialization, for example:
```
var player = TCPlayer('player-container-id', options);
// player.on(type, function);
player.on('error', function(error) {
   // Process
});
```
Here, type is the event type. Supported events include:

| Name | Description |
|------------|---------------------------------|
| play| Playback started. This is triggered when the `play()` method is called or `autoplay` is set to `true` and takes effect. At this time, the `paused` attribute is `false`. |
| playing | Triggered when the playback is paused due to buffering or resumed after pause. The `paused` attribute is `false`. Usually, this event is used to mark that the video playback has actually started, as the `play` event just starts the playback, but the image has not started rendering. |
| loadstart | Triggered when data loading starts. |
| durationchange | Triggered when the duration data of the video changes. |
| loadedmetadata | Metadata for the loaded video. |
| loadeddata | This event is triggered when the data of the current frame is loaded but there is not enough data to play the next frame of the video. |
| progress | Triggered when the media data is obtained. |
| canplay | Triggered when the player is able to start playing the video. |
| canplaythrough | Triggered when the player is expected to be able to continue playing the specified video without buffering. |
| error | Triggered when an error occurs in video playback. |
| pause | Triggered when the video is paused. |
| ratechange | Triggered when the playback speed changes. |
| seeked | Triggered when seeking for the specified playback position ends. |
| seeking | Triggered when seeking for the specified playback position starts. |
| timeupdate | The current playback position has changed, which can be understood as `currentTime` has changed. |
| volumechange | Triggered when the volume is set or the value of the `muted` attribute changes. |
| waiting | Triggered when the playback is paused and the next frame of content is unavailable. |
| ended | Triggered when the video playback ends. In this case, the `currentTime` value is equal to the maximum value of the media resource. |
| resolutionswitching | Definition switching is in progress. |
| resolutionswitched | Definition has been switched. |
| fullscreenchange | Triggered when full screen mode is switched. |
|  webrtcevent | The collection of events during WebRTC file playback. |
|  webrtcstats | The statistics during WebRTC file playback. |


### List of webrtcevent status codes

The player can use `webrtcevent` to get all the events occurring during WebRTC file playback. For example:
```
var player = TCPlayer('player-container-id', options);
player.on('webrtcevent', function(event) {
   // Get the event status code and relevant data from the callback parameter `event`
});
```
The status codes of `webrtcevent` are as listed below:

| Status Code | Callback Parameter | Description |
|------|-------|-------|
| 1001 | None | Stream pull started. |
| 1002 | None | The server was connected. |
| 1003 | None | Video playback started. |
| 1004 | None | Stream pull stopped, and video playback ended. |
| 1005 | None | Failed to connect to the server. Automatic reconnection is enabled. |
| 1006 | None | The obtained stream data is empty. |
| 1007 | localSdp | The signaling server started to be requested. |
| 1008 | remoteSdp | The signaling server is requested successfully. |
| 1009 | None | The stream pull lags and is waiting to be buffered. |
| 1010 | None | The stream pull lagged, and playback ended. |


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
| 14 | A network exception occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, see [Network Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#network-errors). |
| 15 | A multimedia exception occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, see [Media Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#media-errors). |
| 16 | A remuxing exception occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, see [Mux Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#mux-errors). |
| 17 | An exception of another type occurred while playing back an HLS video in HTML5 + hls.js mode. The exception details can be viewed in `event.source`. For more information, see [Other Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#other-errors). |
| 10008| The media data service did not find the media data corresponding to the playback parameters. Please check whether the request parameters `appID` and `fileID` are correct and whether the corresponding media data has been deleted. |
