TXLivePusherプッシュSDKは、主にビデオクラウドのライブイベントブロードキャスト（超低遅延ライブブロードキャスト）のプッシュに使用され、ブラウザがキャプチャしたオーディオとビデオ画面を、WebRTCを介してライブブロードキャストサーバーにプッシュする役割を担います。現在、カメラプッシュ、スクリーンレコーディングプッシュおよびローカルメディアファイルプッシュをサポートしています。
>! WebRTCプロトコルプッシュを使用して、各プッシュドメイン名は、デフォルトで**100パス並列処理**プッシュ数に制限されています。このプッシュ制限を超える必要がある場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してお申し出ください。

## 基礎知識

ドッキング前に次の基本的な知識を理解してください：

### プッシュアドレスの結合

Tencent Cloud CSSを使用する場合、プッシュアドレスは、次に示すように4つの部分で構成されるTencent Cloud標準ライブブロードキャストプッシュURLの形式を満たす必要があります：

![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

ただし、認証Key部分は必ずしも必要ではなく、防犯リンクが必要な場合に、プッシュ認証を有効にしてください。具体的な使用説明については、[ライブブロードキャストURLの自己結合](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。

### ブラウザサポート

ライブイベントブロードキャストプッシュはWebRTCに基づき実装され、WebRTCに対するOSとブラウザのサポートに依存します。

さらに、モバイル端末ではブラウザがオーディオとビデオ画像をキャプチャする機能が充分にサポートされていません。たとえば、モバイル端末ブラウザはスクリーンレコーディングをサポートしておらず、ユーザーカメラデバイスの取得をサポートしているのは、iOS 14.3以降のバージョンのみです。以上より、プッシュSDKは主にデスクトップブラウザに使用され、現在、chrome、FirefoxおよびSafariブラウザの最新バージョンはすべてライブイベントブロードキャストプッシュをサポートしています。

モバイル端末では、[MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38157)を使用してプッシュを実行することをお勧めします。

## ドッキングレイダース

### 手順1：ページの準備作業

ライブブロードキャストプッシュが必要なページ（デスクトップ）に初期化スクリプトを導入します。

```html
<script src="https://imgcache.qq.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```
>? スクリプトはHTMLのbodyセクションに導入する必要があり、headセクションに導入した場合はエラーになります。

ドメイン名制限エリアである場合は、次のリンクを導入することができます：

```html
<script src="https://cloudcache.tencent-cloud.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```

### 手順2：HTMLにコンテナを配置

ローカルオーディオとビデオ画像を表示する必要があるページに、プレーヤーコンテナを追加します。たとえば、id_local_videoのように、divを設定し、命名することによって、ローカルビデオ画像がコンテナにレンダリングされます。コンテナのサイズ制御については、divのcssスタイルを使用して制御できます。サンプルコードは次のとおりです：

```html
<div id="id_local_video" style="width:100%;height:500px;display:flex;align-items:center;justify-content:center;"></div>
```

### 手順3：ライブブロードキャストプッシュ
1. **プッシュSDKインスタンスの生成：**
グローバルオブジェクト`TXLivePusher`を介してSDKインスタンスを生成し、後続の操作はすべてインスタンスを介して完了します。
```javascript
var livePusher = new TXLivePusher();
```
2. **ローカルビデオプレーヤーコンテナの指定：**
ローカルビデオプレーヤーコンテナdivを指定し、ブラウザがキャプチャしたオーディオとビデオスクリーンはこのdivにレンダリングされます。
```javascript
livePusher.setRenderView('id_local_video');
```
>?`setRenderView`を呼び出して生成されたvideo要素はデフォルトで音声があります。ミュートにする場合は、video要素を直接取得し、操作を実行することができます。
>```javascript
>document.getElementById('id_local_video').getElementsByTagName('video')[0].muted = true;
>```

3. **オーディオとビデオ品質の設定：**
オーディオとビデオストリーミングをキャプチャする前に、まずオーディオとビデオ品質を設定します。事前に設定された品質パラメータが要件を満たしていない場合は、設定を個別にカスタマイズすることができます。
```javascript
// ビデオ品質の設定
livePusher.setVideoQuality('720p');
// オーディオ品質の設定
livePusher.setAudioQuality('standard');
// フレームレートのカスタマイズ設定
livePusher.setProperty('setVideoFPS', 25);
```

4. **ストリーミングキャプチャ開始：**
現在、カメラデバイス、マイクデバイス、スクリーンレコーディング、ローカルメディアファイルストリーミングのキャプチャをサポートしています。オーディオとビデオストリーミングが正常にキャプチャされると、ローカルでキャプチャされたオーディオとビデオ画像の再生がプレーヤーコンテナで開始されます。
```javascript
// カメラを起動
livePusher.startCamera();
// マイクを起動
livePusher.startMicrophone();
```
5. **プッシュ開始：**
Tencent Cloudライブイベントブロードキャストプッシュアドレスを渡し、プッシュを開始します。プッシュアドレスの形式については、[Tencent Cloud標準ライブブロードキャストURL](https://intl.cloud.tencent.com/document/product/267/38393)をご参照ください。RTMPプッシュアドレス冒頭の`rtmp://`を`webrtc://`に変更するだけで完了です。
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```
>?プッシュする前にオーディオとビデオストリーミングがキャプチャされていることを確認します。キャプチャされていない場合、プッシュインターフェースの呼び出しに失敗することがあります。オーディオとビデオストリーミングをキャプチャした後に自動的にプッシュを実現したい場合は、コールバックイベントを介して通知することができます。最初のフレームのキャプチャ成功通知を受信した後に、プッシュを実行します。オーディオストリーミングとビデオストリーミングを同時にキャプチャした場合、最初のビデオフレームとオーディオフレームのキャプチャ成功のコールバック通知の両方を受信した後に、もう一度プッシュを開始してください。
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
6. **ライブイベントブロードキャストプッシュの停止：**
```javascript
livePusher.stopPush();
```
7. **オーディオとビデオストリーミングキャプチャの停止：**
```javascript
// カメラを終了
livePusher.stopCamera();
// マイクを終了
livePusher.stopMicrophone();
```

## アドバンスドレイダース
### 互換性
SDKは、WebRTCに対するブラウザの互換性をチェックするための静的メソッドを提供します。

<dx-codeblock>
::: javascript javascript
TXLivePusher.checkSupport().then(function(data) {  
  // WebRTCをサポートしているか  
  if (data.isWebRTCSupported) {    
    console.log('WebRTC Support');  
  }else{    
    console.log('WebRTC Not Support');  
  }  
  // H264コードをサポートしているか  
  if (data.isH264EncodeSupported) {    
    console.log('H264 Encode Support');  
  }else{    
    console.log('H264 Encode Not Support');  
  }
});
:::
</dx-codeblock>

### コールバックイベント通知
SDKは、現在、コールバックイベント通知を提供しています。Observerを設定することで、SDK内部の状態情報とWebRTCの関連データの統計を把握できます。 詳細については、[TXLivePusherObserver](https://intl.cloud.tencent.com/document/product/1071/42709)をご参照ください。
<dx-codeblock>
::: javascript javascript
livePusher.setObserver({
  // プッシュ警告情報
  onWarning: function(code, msg) {
    console.log(code, msg);
  },
  // プッシュ接続状態
  onPushStatusUpdate: function(status, msg) {
    console.log(status, msg);
  },
  // プッシュ統計データ
  onStatisticsUpdate: function(data) {
    console.log('video fps is ' + data.video.framesPerSecond);
  }
});
:::
</dx-codeblock>

### デバイス管理

SDKは、ユーザーがデバイスリストの取得やデバイスの切り替えなどの操作を実行するのに役立つデバイス管理インスタンスを提供しています。
<dx-codeblock>
::: javascript javascript
var deviceManager = livePusher.getDeviceManager();
// デバイスリストの取得
deviceManager.getDevicesList().then(function(data) {
  data.forEach(function(device) {
      console.log(device.deviceId, device.deviceName);  
  });
});
// カメラデバイスの切り替え
deviceManager.switchCamera('camera_device_id');
:::
</dx-codeblock>



