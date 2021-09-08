The TXLivePusher SDK is mainly used for live push of Live Event Broadcasting (LEB). The SDK can use the WebRTC protocol to push audio and video contents captured by the browser from the camera, screen, or a local media file to live streaming servers.

## Basics

Read the following basics before the SDK integration:

### Splicing the push URL

To use Tencent Cloud live streaming services, you should splice the push URL in the following format, which contains 4 parts:

![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

The authentication key is optional. To use hotlink protection, you need to enable push authentication. For details, see [Splicing Live Streaming URLs](https://intl.cloud.tencent.com/document/product/267/38393).

### Browsers

LEB push can be used on operating systems and browsers that support WebRTC.

Audio and video capture is poorly supported on mobile browsers. For example, mobile browsers do not support screen recording, and only iOS 14.3 and above support getting user cameras. Therefore, this push SDK is mainly applicable to desktop browsers, including the latest-version Chrome, Firefox and Safari browsers.

You’re advised to use the [MLVB SDK](https://intl.cloud.tencent.com/zh/document/product/1071) for push on mobile clients.

## SDK Integration

### Step 1. Prepare the page

Add an initialization script to the page (desktop) for live push.

```html
<script src="https://imgcache.qq.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.1.min.js" charset="utf-8"></script>
```

If your business is in a domain-limited region, you can import the following link:

```html
<script src="https://cloudcache.tencent-cloud.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.1.min.js" charset="utf-8"></script>
```

### Step 2. Add a container to the HTML page

Add a player container to the page for displaying the local audio and video contents. That is, add a div and name it, such as `id_local_video`. The local video image will be rendered in the container. You can apply CSS style to the div to control the container size. The sample code is as follows:

```html
<div id="id_local_video" style="width:100%;height:500px;display:flex;align-items:center;justify-content:center;"></div>
```

### Step 3. Push live stream
1. **Generate a push SDK instance:**
Generate an SDK instance of the global class object `TXLivePlayer`. The instance will be used to perform subsequent operations.
```javascript
var livePusher = new TXLivePusher();
```
2. **Specify the local video player container:**
Specify a local video player container div, where the captured audios and video images will be rendered.
```javascript
livePusher.setRenderView('id_local_video');
```
>?If you call the `setRenderView` API, the audio is unmuted as set by the `video` parameters by default. You can also set the `video` parameters to mute the audio.
>```javascript
>document.getElementById('id_local_video').getElementsByTagName('video')[0].muted = true;
>```
```
3. **Set the audio/video quality:**
Before audio and video streams are captured, you can customize the audio and video quality parameters if the default ones cannot meet your requirements.
​```javascript
// Set the video quality
livePusher.setVideoQuality('720p');
// Set the audio quality
livePusher.setAudioQuality('standard');
// Set a custom frame rate
livePusher.setProperty('setVideoFPS', 25);
```
4. **Start to capture the streams:**
The system support capturing streams from the camera, mic, screen recording, and local media files. Once the audio and video streams are captured successfully, the player container will start to play back them.
```javascript
// Enable the camera
livePusher.startCamera();
// Enable the mic
livePusher.startMicrophone();
```
5. **Start to push:**
Pass in the LEB push URL to start the push. The format of an LEB push URL is the same as that of an [LVB push URL](https://intl.cloud.tencent.com/document/product/267/38393), except that the former starts with `webrtc://` while the latter starts with `rtmp://`.
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```

>?Before pushing streams, ensure that the audio and video streams have been captured; otherwise, push API calls will fail. To achieve auto push after the audio and video streams are captured, you can set to start push automatically when the notification of successful capture of the first frame is received. If both the video stream and audio stream are captured, you need to set to start push after the callback notifications of successful capture of both the first video frame and the first audio frame are received.
>```javascript
>var hasVideo = false;
>var hasAudio = false;
>var isPush = false;
>livePusher.setObserver({
>	onCaptureFirstAudioFrame: function() {
>		hasAudio = true;
>		if (hasVideo && !isPush) {
>			isPush = true;
livePlayer.startPlay('webrtc://domain/AppName/StreamName? txSecret=xxx&txTime=xxx');
>		}
>	},
>	onCaptureFirstVideoFrame: function() {
>		hasVideo = true;
>		if (hasAudio && !isPush) {
>			isPush = true;
livePlayer.startPlay('webrtc://domain/AppName/StreamName? txSecret=xxx&txTime=xxx');
>		}
>	}
>});
>```
```
</dx-codeblock>
6. **Stop LEB push:**
​```javascript
livePusher.stopPush();
```
7. **Stop capturing audio and video streams:**
```javascript
// Disable the camera
livePusher.stopCamera();
// Disable the mic
livePusher.stopMicrophone();
```

## Advanced Features
### Compatibility
The SDK provides a static method to check whether a browser supports WebRTC.

<dx-codeblock>
::: javascript javascript
TXLivePusher.checkSupport().then(function(data) {  
	// Whether WebRTC is supported   
	if (data.isWebRTCSupported) {    
		console.log('WebRTC Support');  
	} else {    
		console.log('WebRTC Not Support');  
	}  
	// Whether H.264 is supported  
	if (data.isH264EncodeSupported) {    
		console.log('H264 Encode Support');  
	} else {    
		console.log('H264 Encode Not Support');  
	}
});
:::
</dx-codeblock>

### Callback event notifications
The SDK supports callback event notifications. You can configure the `Observer` parameters to set the callbacks to observe the SDK internal status and WebRTC statistics. For more information, please see [TXLivePusherObserver](https://intl.cloud.tencent.com/zh/document/product/1071/41272).
<dx-codeblock>
::: javascript javascript
livePusher.setObserver({
	// Push alarm information
	onWarning: function(code, msg) {
		console.log(code, msg);
	},
	// Push status
	onPushStatusUpdate: function(status, msg) {
		console.log(status, msg);
	},
	// Push statistics
	onStatisticsUpdate: function(data) {
		console.log('video fps is ' + data.video.framesPerSecond);
	}
});
:::
</dx-codeblock>

### Device management

The SDK provides device management instances to help users get the list of devices, switch between devices, and perform other operations.
<dx-codeblock>
::: javascript javascript
var deviceManager = livePusher.getDeviceManager();
// Get the device list
deviceManager.getDevicesList().then(function(data) {
	data.forEach(function(device) {
			console.log(device.deviceId, device.deviceName);  
	});
});
// Switch cameras
deviceManager.switchCamera('camera_device_id');
:::
</dx-codeblock>









