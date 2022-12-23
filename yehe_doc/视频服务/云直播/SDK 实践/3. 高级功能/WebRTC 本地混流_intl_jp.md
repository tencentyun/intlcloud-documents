>?現在のプッシュSDKはベターテスト版です。課金ルールについては、今後リリースする正式版の内容をご参照ください。

SDKはビデオストリーム画面を処理する機能を提供します。具体的には、複数のチャネルのビデオストリームのミックス(PiP)、画面エフェクトの処理（ミラー、フィルター）、エレメントの追加（ウォーターマーク、テキスト）があります。基本的な処理フローとして、SDKではまず複数のチャネルのストリームを採取します。次に採取したストリームに対してローカルでミクスストリーミングを行い、画面をマージしたり、音声をミクスしたりします。最後に、その他のエフェクト処理を実行します。これらはブラウザ自体の機能に依存するため、ブラウザの性能をある程度要求します。インターフェースプロトコルについては、[TXVideoEffectManager](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXVideoEffectManager.html)をご参照ください。以下でローカルミクスストリーミングの基本的な使用方法を簡単に説明します。

## 基本的な使用方法
ローカルミクスストリーミング機能を使用するには、SDKを初期化しSDKインスタンスlivePusherを取得してください。初期化のソースコードについては、[アクセスガイド](https://intl.cloud.tencent.com/document/product/267/41620)をご参照ください。

### ステップ1：ビデオエフェクト管理インスタンスを取得します
```javascript
var videoEffectManager = livePusher.getVideoEffectManager();
```

### ステップ2：ローカルミクスストリーミングを有効にします
まず、ローカルミクスストリーミング機能を有効にする必要があります。デフォルトでは、SDKは1チャネルのビデオストリームと1チャネルのオーディオストリームだけを採取できます。ローカルミクスストリーミング機能が有効になっている場合、複数のチャネルのストリームを採取し、採取したストリームをブラウザを経由してローカルでミクスできます。
```javascript
videoEffectManager.enableMixing(true);
```

### ステップ3：ミクスストリーミングパラメータを設定します
ミクスストリーミングパラメータを設定します。主にミクスを行って最終的に生成するビデオの解像度とフレームレートを設定します。
```javascript
videoEffectManager.setMixingConfig({
	videoWidth: 1280,
	videoHeight: 720,
	videoFramerate: 15
});
```

### ステップ4：複数のチャネルのストリームを採取します
ローカルミクスストリーミングを有効にした後、複数のチャネルのストリームを採取します。例えば、カメラを起動しスクリーンを共有します。ストリームIDを保存しなければなりません。これは、これからの操作ではストリームIDを使用する必要があるためです。
```javascript
var cameraStreamId = null;
var screenStreamId = null;

livePusher.startCamera().then((streamId) => {
	cameraStreamId = streamId;
}).catch((error) => {
	console.log(‘カメラ起動失敗：'+ error.toString());
});

livePusher.startScreenCapture().then((streamId) => {
	screenStreamId = streamId;
}).catch((error) => {
	console.log(‘スクリーン共有失敗：'+ error.toString());
});
```

### ステップ5：画面レイアウトを設定します

採取した2チャネルの画面のレイアウトを設定します。ここでは、スクリーンの共有画面をメインに、カメラ画面を左上側に配置します。具体的なパラメータの設定は、[TXLayoutConfig](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXVideoEffectManager.html#~TXLayoutConfig)をご参照ください。
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

### ステップ6：ミラーエフェクトを設定します
カメラで採取した画面は実際のと逆です。そのため、ここでは、カメラの画面を左右反転するように設定します。
```javascript
	videoEffectManager.setMirror({
	streamId: cameraStreamId,
	mirrorType: 1
});
```

### ステップ7：ウォーターマークを追加します
まず画像を1枚用意します。次にこの画像をウォーターマークとしてビデオストリーム画面に追加します。ここでは、ウォーターマーク画像を右上側に配置します。
```javascript
var image = new Image();
image.src = './xxx.png'; // 画像のアドレスは同じリージョンにする必要があります。そうしないと、クロスリージョンの問題が発生します

videoEffectManager.setWatermark({
	image: image,
	x: 1230,
	y: 50,
	width: 100,
	height: 100,
	zOrder: 3
});
```

### ステップ8：プッシュを開始します
上記の操作を完了すると、レイアウトがPiPで、ミラーエフェクトとウォーターマークがあるビデオストリームができました。この処理後のビデオストリームをサーバーにプッシュします。
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```

>? WebRTCミクスストリーミングに関するインターフェースについては、[API概要](https://webrtc-demo.myqcloud.com/push-sdk/v2/docs/TXLivePusher.html)をご参照ください。