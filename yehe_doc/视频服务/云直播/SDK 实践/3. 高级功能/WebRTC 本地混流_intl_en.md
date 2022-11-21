>?The stream push SDK is currently in beta test. The billing rules of the official version shall apply.

The SDK provides various video stream image processing features, including mixing multiple video streams (such as PiP), processing image effects (such as mirroring and filters), and adding other elements (such as watermarks and text). The basic process is as follows: The SDK first collects multiple streams and mixes them locally to combine the images and mix the audios. Then, it processes other effects. As all the features rely on the browser's support, the SDK has certain requirements for the browser performance. For the specific API protocols, see [TXVideoEffectManager](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXVideoEffectManager.html). This document describes the basic usage of local stream mix.

## Basic Usage
To use the local stream mix feature, you should initialize the SDK and get the SDK instance `livePusher`. For the initialization code, see [WebRTC Push](https://intl.cloud.tencent.com/document/product/267/41620).

### Step 1. Get the video effect management instance
```javascript
var videoEffectManager = livePusher.getVideoEffectManager();
```

### Step 2. Enable local stream mix
First, you need to enable the local stream mix feature. By default, the SDK collects only one video stream and audio stream. After this feature is enabled, the SDK can collect multiple streams, which will be mixed locally by the browser.
```javascript
videoEffectManager.enableMixing(true);
```

### Step 3. Set the stream mix parameters
Set the stream mix parameters, especially the resolution and frame rate of the video output after stream mix.
```javascript
videoEffectManager.setMixingConfig({
	videoWidth: 1280,
	videoHeight: 720,
	videoFramerate: 15
});
```

### Step 4. Collect multiple streams
After local stream mix is enabled, the SDK starts collecting multiple streams such as the camera and shared screen. Be sure to keep the stream IDs, as they are required in subsequent operations.
```javascript
var cameraStreamId = null;
var screenStreamId = null;

livePusher.startCamera().then((streamId) => {
	cameraStreamId = streamId;
}).catch((error) => {
	console.log('Failed to turn on the camera:'+ error.toString());
});

livePusher.startScreenCapture().then((streamId) => {
	screenStreamId = streamId;
}).catch((error) => {
	console.log('Failed to share the screen:'+ error.toString());
});
```

### Step 5. Set the image layout

Set the layout of the images of the collected two streams. Here, the shared screen is displayed as the main image, with the camera image in the top-left corner. For the specific parameter configuration, see [TXLayoutConfig](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXVideoEffectManager.html#~TXLayoutConfig).
```javascript
videoEffectManager.setLayout([{
	streamId: screenStreamId,
	x: 640,
	y: 360,
	width: 1280,
	height: 720,
	zOrder: 1
}, {
	streamId: cameraStreamId,
	x: 160,
	y: 90,
	width: 320,
	height: 180,
	zOrder: 2
}]);
```

### Step 6. Set the mirroring effect
Mirror the camera image, as the image collected by the camera is actually reversed.
```javascript
	videoEffectManager.setMirror({
	streamId: cameraStreamId,
	mirrorType: 1
});
```

### Step 7. Add a watermark
Prepare an image object and add it to the video stream image as a watermark. Here, the watermark image is placed in the top-right corner.
```javascript
var image = new Image();
image.src = './xxx.png'; // Note that the image address cannot be under another domain; otherwise, cross-domain issues will occur.

videoEffectManager.setWatermark({
	image: image,
	x: 1230,
	y: 50,
	width: 100,
	height: 100,
	zOrder: 3
});
```

### Step 8. Start stream push
Push the video stream with a PiP layout, mirrored image, and watermark output after the above steps to the server.
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```

>? For more information on WebRTC-based stream mix APIs, see [TXLivePusher](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXLivePusher.html).