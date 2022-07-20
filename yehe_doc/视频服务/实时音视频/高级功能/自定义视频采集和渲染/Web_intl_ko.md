본문에서는 오디오와 비디오를 직접 캡처하고 렌더링하는 방법을 설명합니다.

## 사용자 정의 캡처

로컬 스트림을 생성하기 위해 {@link TRTC.createStream createStream()}을 호출할 때 캡처 방법을 지정할 수 있습니다.

마이크와 카메라에서 오디오 및 비디오 데이터 캡처:

```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
localStream.initialize().then(() => {
  // local stream initialized success
});
```

화면 공유 스트림 캡처:

```
const localStream = TRTC.createStream({ userId, audio: false, screen: true });
localStream.initialize().then(() => {
  // local stream initialized success
});
```

상기 두 가지 예시는 SDK에 내장된 캡처 프로세스를 사용합니다. 스트림을 사전 처리하려면 createStream을 사용하여 외부 오디오 및 비디오 소스, 즉 사용자 정의 캡처를 사용하여 로컬 스트림을 생성할 수 있습니다. 예를 들어 다음을 수행할 수 있습니다.

- [getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)를 사용하여 특정 마이크 및 카메라에서 오디오 및 비디오를 캡처합니다.
- [getDisplayMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia)를 사용하여 화면 콘텐츠를 캡처합니다.
- [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/captureStream)을 사용하여 웹페이지에서 재생되는 오디오 및 비디오를 캡처합니다.
- [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/captureStream)을 사용하여 canvas에서 애니메이션을 캡처합니다.

### 웹 페이지에서 재생되는 비디오 소스 캡처

```javascript
// 현재 브라우저가 video 요소에서 stream 캡처를 지원하는지 확인
const isVideoCapturingSupported = () => {
	['captureStream', 'mozCaptureStream', 'webkitCaptureStream'].forEach((item) => {
		if (item in document.createElement('video')) {
			return true;
		}
	});
	return false;
};

// 현재 브라우저가 video 요소에서 stream 캡처를 지원하는지 확인
if (!isVideoCapturingSupported()) {
	console.log('your browser does not support capturing stream from video element');
	return
}
// 페이지에서 재생 중인 video의 태그 가져오기 
const video = document.getElementByID('your-video-element-ID');
// 재생중인 비디오에서 비디오 스트림 캡처
const stream = video.captureStream();
const audioTrack = stream.getAudioTracks()[0];
const videoTrack = stream.getVideoTracks()[0];

const localStream = TRTC.createStream({ userId, audioSource: audioTrack, videoSource: videoTrack });

// 영상 통화 경험을 보장하기 위해 비디오 속성은 외부 비디오 소스의 속성과 동일해야 함
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
    // local stream initialized success
});
```

### canvas에서 애니메이션 캡처하기

```javascript
// 현재 브라우저가 canvas 요소에서 stream 캡처를 지원하는지 확인
const isCanvasCapturingSupported = () => {
	['captureStream', 'mozCaptureStream', 'webkitCaptureStream'].forEach((item) => {
		if (item in document.createElement('canvas')) {
			return true;
		}
	});
	return false;
};

// 현재 브라우저가 canvas 요소에서 stream 캡처를 지원하는지 확인
if (!isCanvasCapturingSupported()) {
	console.log('your browser does not support capturing stream from canvas element');
	return
}
// canvas 태그 가져오기 
const canvas = document.getElementByID('your-canvas-element-ID');

// canvas에서 15 fps 비디오 스트림 캡처
const fps = 15;
const stream = canvas.captureStream(fps);
const videoTrack = stream.getVideoTracks()[0];

const localStream = TRTC.createStream({ userId, videoSource: videoTrack });

// 영상 통화 경험을 보장하기 위해 비디오 속성은 외부 비디오 소스의 속성과 동일해야 함
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
    // local stream initialized success
});
```

## 사용자 정의 렌더링

{@link Stream#play Stream.play()}를 사용하여 TRTC.createStream()을 통해 생성 및 초기화된 로컬 스트림 또는 Client.on('stream-added')을 통해 수신된 원격 스트림을 렌더링할 수 있습니다. Stream.play() 메소드는 오디오 플레이어와 비디오 플레이어를 만들고 <audio>/<video> 태그를 App이 전달한 Div 컨테이너에 삽입합니다.

자신의 플레이어를 사용하려면 Stream.play()/stop()을 호출하는 대신 {@link Stream#getAudioTrack Stream.getAudioTrack()}/{@link Stream#getVideoTrack Stream.getVideoTrack()} 오디오 및 비디오 트랙을 가져오고 자신의 플레이어로 렌더링합니다. 이러한 경우 Stream.on('player-state-changed') 콜백이 트리거되지 않습니다. 현재 스트림의 상태에 대한 정보를 얻으려면 App이 'mute/unmute/ended' 및 [MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack)의 기타 이벤트를 수신해야 합니다.

또한 스트림의 라이프사이클을 모니터링하기 위해 `Client.on('stream-added')`, `Client.on('stream-updated')` 및 `Client.on('stream-removed')`을 수신해야 합니다.

> !
> - 'stream-added' 또는 'stream-updated' 이벤트 콜백을 수신한 후 스트림에 오디오 또는 비디오 track이 있는지 확인합니다. stream-updated 콜백에 대한 오디오 또는 비디오 track이 있는 경우 플레이어를 업데이트하고 최신 오디오 및 비디오 track을 재생해야 합니다.
> - [온라인 데모](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/custom-capture-render/index.html)
