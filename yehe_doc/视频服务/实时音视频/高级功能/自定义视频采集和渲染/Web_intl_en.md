This document describes how to capture and render audio and video by yourself.

## Custom Capturing

You can specify the capturing method when calling {@link TRTC.createStream createStream()} to create a local stream.

Capture audio and video data from the mic and camera

```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
localStream.initialize().then(() => {
  // local stream initialized success
});
```

Capture the screen sharing stream

```
const localStream = TRTC.createStream({ userId, audio: false, screen: true });
localStream.initialize().then(() => {
  // local stream initialized success
});
```

The above two examples use the SDK’s built-in capturing process. If you want to pre-process your streams, `createStream` allows you to create a local stream using external audio and video sources, i.e., custom capturing. For example, you can: 

- Use [getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia) to capture audio and video from a specific mic and camera.
- Use [getDisplayMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia) to capture screen content.
- Use [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/captureStream) to capture the audio and video played on a webpage.
- Use [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/captureStream) to capture animation in the canvas.

### Capturing the video source played on a webpage

```javascript
// Check whether your current browser supports capturing streams from the `video` element 
const isVideoCapturingSupported = () => {
	['captureStream', 'mozCaptureStream', 'webkitCaptureStream'].forEach((item) => {
		if (item in document.createElement('video')) {
			return true;
		}
	});
	return false;
};

// Check whether your current browser supports capturing streams from the `video` element 
if (!isVideoCapturingSupported()) {
	console.log('your browser does not support capturing stream from video element');
	return
}
// Get the tag of the video being played back on the page 
const video = document.getElementByID('your-video-element-ID');
// Capture the video stream from the video being played back
const stream = video.captureStream();
const audioTrack = stream.getAudioTracks()[0];
const videoTrack = stream.getVideoTracks()[0];

const localStream = TRTC.createStream({ userId, audioSource: audioTrack, videoSource: videoTrack });

// To ensure video call experience, make sure the video properties are the same as those of the external video source
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
    // local stream initialized success
});
```

### Capturing animation in canvas

```javascript
// Check whether your current browser supports capturing streams from the `canvas` element
const isCanvasCapturingSupported = () => {
	['captureStream', 'mozCaptureStream', 'webkitCaptureStream'].forEach((item) => {
		if (item in document.createElement('canvas')) {
			return true;
		}
	});
	return false;
};

// Check whether your current browser supports capturing streams from the `canvas` element
if (!isCanvasCapturingSupported()) {
	console.log('your browser does not support capturing stream from canvas element');
	return
}
// Get the `canvas` tag 
const canvas = document.getElementByID('your-canvas-element-ID');

// Capture a 15 FPS video stream from the canvas
const fps = 15;
const stream = canvas.captureStream(fps);
const videoTrack = stream.getVideoTracks()[0];

const localStream = TRTC.createStream({ userId, videoSource: videoTrack });

// To ensure video call experience, make sure the video properties are the same as those of the external video source
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
    // local stream initialized success
});
```

## Custom Rendering

You can use {@link Stream#play Stream.play()} to render a local stream created and initialized via `TRTC.createStream()` or a remote stream received via `Client.on('stream-added')`. The `Stream.play()` method will create an audio player and a video player and insert the <audio>/<video> tag into the div container passed by the application.

If you want to use your own player, instead of calling `Stream.play()/stop()`, you can use {@link Stream#getAudioTrack Stream.getAudioTrack()}/{@link Stream#getVideoTrack Stream.getVideoTrack()} to get the audio and video tracks and render them with your own player. The `Stream.on('player-state-changed')` callback will not be triggered in such cases. Your application needs to listen for `mute/unmute/ended` and other events of [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) to get information on the status of the current stream.

It must also listen for `Client.on('stream-added')`, `Client.on('stream-updated')`, and `Client.on('stream-removed')` to monitor the lifecycle of streams.

> !
> - After receiving the `stream-added` or `stream-updated` event callback, check if the stream has an audio or video track. If there is an audio or video track for the `stream-updated` callback, make sure that you update the player and play the latest audio and video tracks.
> - [Online demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/custom-capture-render/index.html)
