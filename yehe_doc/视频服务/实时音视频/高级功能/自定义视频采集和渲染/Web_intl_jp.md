このドキュメントでは、主にローカルストリームのカスタムキャプチャおよびオーディオビデオストリームのカスタム再生とレンダリングなどの高レベルの使用方法を紹介します。

## キャプチャのカスタマイズ

{@link TRTC.createStream createStream()}によって、ローカルストリームを作成する場合、SDKを使用してデフォルトのキャプチャ方法を指定できます。

以下のように、カメラとマイクからオーディオビデオのデータをキャプチャします：

```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
localStream.initialize().then(() => {
  // local stream initialized success
});
```

または、画面共有ストリームをキャプチャします：

```
const localStream = TRTC.createStream({ userId, audio: false, screen: true });
localStream.initialize().then(() => {
  // local stream initialized success
});
```

ローカルストリームを作成する上記の2つの方法は、SDKのデフォルトのキャプチャ方法を使用します。開発者がオーディオビデオストリームを前処理できるようにするために、createStreamは、外部のオーディオビデオソースからのローカルストリームの作成をサポートします。この方法でローカルストリームを作成することにより、開発者は次のようなカスタムキャプチャを実装できます：

- [getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)を使用してカメラとマイクのオーディオビデオストリームをキャプチャできます。
- [getDisplayMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia)を使用して画面共有ストリームをキャプチャします。
- [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/captureStream)を使用してページで再生されているオーディオビデオをキャプチャします。
- [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/captureStream)を使用してcanvasキャンバスでアニメーションをキャプチャします。

### ページで再生されているビデオソースのキャプチャ

```javascript
// 現在のブラウザがvideo要素からのstreamのキャプチャをサポートするかどうかを確認します
const isVideoCapturingSupported = () => {
	['captureStream', 'mozCaptureStream', 'webkitCaptureStream'].forEach((item) => {
		if (item in document.createElement('video')) {
			return true;
		}
	});
	return false;
};

// 現在のブラウザがvideo要素からのstreamのキャプチャをサポートするかどうかを確認します
if (!isVideoCapturingSupported()) {
	console.log('your browser does not support capturing stream from video element');
	return
}
// ページで再生されているビデオのvideoタグを取得します 
const video = document.getElementByID('your-video-element-ID');
// 再生されているビデオからビデオストリームをキャプチャします
const stream = video.captureStream();
const audioTrack = stream.getAudioTracks()[0];
const videoTrack = stream.getVideoTracks()[0];

const localStream = TRTC.createStream({ userId, audioSource: audioTrack, videoSource: videoTrack });

// ビデオプロパティが外部から渡されたビデオソースと一致していることを確認してください。一致していないと、ビデオ通話のユーザー体験に影響を及ぼします
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
    // local stream initialized success
});
```

### canvasからの動画のキャプチャ

```javascript
// 現在のブラウザがcanvas要素からのstreamのキャプチャをサポートするかどうかを確認します
const isCanvasCapturingSupported = () => {
	['captureStream', 'mozCaptureStream', 'webkitCaptureStream'].forEach((item) => {
		if (item in document.createElement('canvas')) {
			return true;
		}
	});
	return false;
};

// 現在のブラウザがcanvas要素からのstreamのキャプチャをサポートするかどうかを確認します
if (!isCanvasCapturingSupported()) {
	console.log('your browser does not support capturing stream from canvas element');
	return
}
// canvasタグを取得します 
const canvas = document.getElementByID('your-canvas-element-ID');

// canvasから15 fpsのビデオストリームをキャプチャします
const fps = 15;
const stream = canvas.captureStream(fps);
const videoTrack = stream.getVideoTracks()[0];

const localStream = TRTC.createStream({ userId, videoSource: videoTrack });

// ビデオプロパティが外部から渡されたビデオソースと一致していることを確認してください。一致していないと、ビデオ通話のユーザー体験に影響を及ぼします
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
    // local stream initialized success
});
```

## 再生とレンダリングのカスタマイズ

TRTC.createStream()によって作成および初期化されたローカルストリーム、またはClient.on('stream-added')によって受信されたリモートストリームの場合、オーディオビデオストリームのオブジェクトの{@link Stream#play Stream.play()}方法を使用してオーディオとビデオを再生とレンダリングできます。Stream.play()の内部は、オーディオプレーヤーとビデオプレーヤーを自動的に作成し、対応する<audio>/<video>タグをAppから渡されたDivコンテナに挿入します。

Appが独自のプレーヤーを使用する場合は、Stream.play()/stop()メソッドを使用せずに呼び出すことができます。{@link Stream#getAudioTrack Stream.getAudioTrack()}/{@link Stream#getVideoTrack Stream.getVideoTrack()}メソッドを使用して対応するオーディオビデオトラックを取得し、独自のプレーヤーを使用してオーディオビデオを再生およびレンダリングします。このようなカスタム再生とレンダリング方法を使用して、Stream.on('player-state-changed')イベントはトリガーされず、Appはオーディオビデオトラック[MediaStreamTrack](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack)の`mute/unmute/ended`などのイベントを自己監視して、現在のオーディオビデオデータストリームの状態を判断してください。

また、App層は、`Client.on('stream-added')`、`Client.on('stream-updated')`および`Client.on('stream-removed')`などのイベントを監視して、オーディオビデオストリームのライフサイクルを処理してください。

> !
> - 'stream-added'と'stream-updated'の2つのイベントの処理コールバックでは、オーディオまたはビデオトラックがあるかどうかを確認してください。’stream-updated‘イベントの処理では、オーディオまたはビデオトラックがある場合、必ずプレーヤーを更新し、最新のオーディオビデオtrackを使用して再生してください。
> - [オンラインの例](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/custom-capture-render/index.html)
