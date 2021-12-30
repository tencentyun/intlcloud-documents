The TXLivePusher SDK is mainly used to publish streams for LEB (ultra-low latency streaming). It can publish audio and video the browser captures from the camera, screen, or a local media file to live streaming servers via WebRTC.
>! With WebRTC, each push domain name can be used for up to **concurrent 100 streams** by default. If you want to push more streams, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Basics

Below are some basics you need to know before integrating the SDK.

### Splicing publishing URLs

To use Tencent Cloud live streaming services, you need to splice publishing URLs in the format required by Tencent Cloud, which consists of four parts.

![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

An authentication key is not required. You can enable publishing authentication if you need hotlink protection. For details, please see [Splicing CSS URLs](https://intl.cloud.tencent.com/document/product/267/38393).

### Browser support

Publishing for LEB relies on WebRTC and therefore can only be used on OS and browsers that support WebRTC.

The audio/video capturing feature is poorly supported on mobile browsers. For example, mobile browsers do not support screen recording, and only iOS 14.3 and above allow requesting camera access. Therefore, the publishing SDK is mainly used on desktop browsers. The latest version of Chrome, Firefox, and Safari all support publishing for LEB.

To publish streams on mobile browsers, use the [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38157).

## SDK Integration

### Step 1. Prepare the page

Add an initialization script to the (desktop) page from which streams are to be published.

```html
<script src="https://imgcache.qq.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```
>? The script needs to be imported into the `body` part of the HTML code. If it is imported into the `head` part, an error will be reported.

If your business is in a domain-limited region, you can import the following link:

```html
<script src="https://cloudcache.tencent-cloud.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```

### Step 2. Add a container to the HTML page

Add a player container to the section of the page where local video is to be played. This is achieved by adding a div and giving it a name, for example, `id_local_video`. Local video will be rendered in the container. To adjust the size of the container, style the div using CSS.

```html
<div id="id_local_video" style="width:100%;height:500px;display:flex;align-items:center;justify-content:center;"></div>
```

### Step 3. Publish streams
1. **Generate an instance of the publishing SDK:**
Generate an instance of the global object `TXLivePusher`. All subsequent operations will be performed via the instance.
```javascript
var livePusher = new TXLivePusher();
```
2. **Specify the local video player container:**
Specify the div for the local video player container, which is where audio and video captured by the browser will be rendered.
```javascript
livePusher.setRenderView('id_local_video');
```
>?The video element generated via `setRenderView` is unmuted by default. To mute video, obtain the video element using the code below.
>```javascript
>document.getElementById('id_local_video').getElementsByTagName('video')[0].muted = true;
>```
```
3. **Set audio/video quality:**
Audio/video quality should be set before capturing. You can specify quality parameters if the default settings do not meet your requirements.
​```javascript
// Set video quality
livePusher.setVideoQuality('720p');
// Set audio quality
livePusher.setAudioQuality('standard');
// Set the frame rate
livePusher.setProperty('setVideoFPS', 25);
```
4. **Capture streams:**
You can capture streams from the camera, mic, screen and local media files. If capturing is successful, the player container will start playing the audio/video captured.
```javascript
// Turn the camera on
livePusher.startCamera();
// Turn the mic on
livePusher.startMicrophone();
```
5. **Publish streams:**
Pass in the LEB publishing URL to start publishing streams. For the format of publishing URLs, please see [Splicing CSS URLs](https://intl.cloud.tencent.com/document/product/267/38393). You need to replace the prefix `rtmp://` with `webrtc://`.
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```
>?Before publishing, make sure that audio/video streams are captured successfully, or you will fail to call the publishing API. You can use the code below to publish streams automatically after audio/video is captured, that is, after the callback for capturing the first audio or video frame is received. If both audio and video are captured, publishing starts only after both the callback for capturing the first audio frame and that for the first video frame are received.
```javascript
var hasVideo = false;
var hasAudio = false;
var isPush = false;
livePusher.setObserver({
		onCaptureFirstAudioFrame: function() {
			hasAudio = true;
			if (hasVideo && !isPush) {
				isPush = true;
				livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
			}
		},
		onCaptureFirstVideoFrame: function() {
			hasVideo = true;
			if (hasAudio && !isPush) {
				isPush = true;
				livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
			}
		}
});
```
</dx-codeblock>
6. **Stop publishing:**
```javascript
livePusher.stopPush();
```
7. **Stop capturing audio and video:**
```javascript
// Turn the camera off
livePusher.stopCamera();
// Turn the mic off
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

### Event callbacks
The SDK supports callback event notifications. You can set an observer to receive callbacks of the SDK’s status and WebRTC-related statistics. For details, see [TXLivePusherObserver](https://intl.cloud.tencent.com/document/product/1071/42709).
<dx-codeblock>
::: javascript javascript
livePusher.setObserver({
	// Warnings for publishing
	onWarning: function(code, msg) {
		console.log(code, msg);
	},
	// Publishing status
	onPushStatusUpdate: function(status, msg) {
		console.log(status, msg);
	},
	// Publishing statistics
	onStatisticsUpdate: function(data) {
		console.log('video fps is ' + data.video.framesPerSecond);
	}
});
:::
</dx-codeblock>

### Device management

You can use a device management instance to get the device list, switch devices, and perform other device-related operations.
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



