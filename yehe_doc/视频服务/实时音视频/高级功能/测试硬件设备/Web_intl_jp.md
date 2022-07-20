## 内容紹介

ビデオ通話の前に、ブラウザ環境の確認およびカメラとマイクなどのデバイスのテストを先に行うことをお勧めします。テストしない場合、ユーザーが実際に通話を行うときにデバイスの問題を見つけることが難しくなります。

## ブラウザ環境の確認

SDKの通信機能を呼び出す前に、まず{@link TRTC.checkSystemRequirements checkSystemRequirements()}インターフェイスを使用して、SDKが現在のWebページをサポートしているかどうかを確認することをお勧めします。SDKが現在のブラウザをサポートしていない場合、ユーザーのデバイスタイプに応じて、SDKでサポートされているブラウザを使用するようにユーザーに提案してください。

```javascript
TRTC.checkSystemRequirements().then(checkResult => {
  if (checkResult.result) {
    // 入室をサポートします
    if (checkResult.isH264DecodeSupported) {
    	// プルをサポートします
    }
    if (checkResult.isH264EncodeSupported) {
    	// プッシュをサポートします
    }
  }
})
```

ユーザーがSDKでサポートされているブラウザを使用し、`TRTC.checkSystemRequirements`によって返される検出結果がfalseの場合、次の理由が考えられます：

ケース1：リンクが次の3つの条件のいずれかを満たしているかどうかを確認してください
- localhostドメイン（Firefoxブラウザはlocalhostとローカルipアクセスをサポートします）
- HTTPSがオンになっているドメイン
- file:///プロトコルで開いたローカルファイル

ケース2：Firefoxブラウザをインストールした後、H264コーデックを動的にロードする必要があるため、検出結果はしばらくの間falseになります。しばらく待ってから再試行するか、先に別の推奨ブラウザを使用してリンクを開いてください。


### 既知のブラウザの使用制限の説明

**Firefox**
- Firefoxは30fpsのビデオフレームレートのみをサポートします。フレームレートを設定する必要がある場合は、SDKでサポートされている他のブラウザを使用してください。

**QQブラウザ**
- カメラとマイクが通常に動作する一部のWindowsデバイスは、localhost環境でlocalStream.initialize()を呼び出すとき、NotFoundErrorエラーをスローします。


## オーディオビデオデバイスのテスト

ユーザーがTRTC-SDKを使用する過程でより良いユーザーエクスペリエンスを確実に得られるために、ユーザーがTRTCルームに参加する前に、ユーザーのデバイスとネットワーク状態を確認し、提案とガイダンスを提供することをお勧めします。

デバイス検出機能とネットワーク確認機能を迅速に統合できるために、参照するための以下の方法を提供します：

- [rtc-detectのJSライブラリ](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-4)
- [デバイスを検出するReactコンポーネント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-5)
- [TRTC機能検出ページ](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-6)

## rtc-detectライブラリ

[rtc-detect](https://www.npmjs.com/package/rtc-detect)を使用してTRTC SDKに対する現在の環境のサポートおよび現在の環境の詳細を確認できます。

### インストール

```shell
npm install rtc-detect
```

### 使用方法

```javascript
import RTCDetect from 'rtc-detect';
// 監視モジュールを初期化します
const detect = new RTCDetect();
// 現在の環境の検視結果を取得します
const result = await detect.getReportAsync();
// resultは、現在の環境システムの情報、APIサポート、コーデックサポートおよびデバイス関連情報が含まれています
console.log('result is: ' + result);
```

### API

#### (async) isTRTCSupported()

現在の環境がTRTCをサポートしているかどうかを判断します。

```javascript
const detect = new RTCDetect();
const data = await detect.isTRTCSupported();

if (data.result) {
  console.log('current browser supports TRTC.')
}else{
  console.log(`current browser does not support TRTC, reason: ${data.reason}.`)
}
```

#### getSystem()

現在のシステム環境パラメータを取得します。

| Item                   | Type   | Description                     |
| ---------------------- | ------ | ------------------------------- |
| UA                     | string | ブラウザのua                     |
| OS                     | string | 現在のデバイスのシステムモデル              |
| browser                | object | 現在のブラウザ情報{ name, version } |
| displayResolution      | object | 現在の解像度{ width, height }    |
| getHardwareConcurrency | number | デバイスのCPUコアの現在の数             |

```javascript
const detect = new RTCDetect();
const result = detect.getSystem();
```

#### getAPISupported()

現在の環境APIサポートを取得します。

| Item                              | Type    | Description                                           |
| --------------------------------- | ------- | ----------------------------------------------------- |
| isUserMediaSupported              | boolean | ユーザーメディアデータストリームの取得をサポートするかどうか                            |
| isWebRTCSupported                 | boolean | WebRTCをサポートするかどうか                                       |
| isWebSocketSupported              | boolean | WebSocketをサポートするかどうか                                    |
| isWebAudioSupported               | boolean | WebAudioをサポートするかどうか                                     |
| isScreenCaptureAPISupported       | boolean | 画面のストリームの取得をサポートするかどうか                                  |
| isCanvasCapturingSupported        | boolean | canvasからのデータストリームの取得をサポートするかどうか                          |
| isVideoCapturingSupported         | boolean | videoからのデータストリームの取得をサポートするかどうか                           |
| isRTPSenderReplaceTracksSupported | boolean | trackを置き換えるときにpeerConnectionと再ネゴシエーションを行わないことをサポートするかどうか     |
| isApplyConstraintsSupported       | boolean | getUserMediaを再度呼び出さずにカメラの解像度の変更をサポートするかどうか |

```javascript
const detect = new RTCDetect();
const result = detect.getAPISupported();
```

#### (async) getDevicesAsync()

現在の環境で利用可能なデバイスを取得します。

| Item                    | Type                | Description                                        |
|-------------------------|---------------------|----------------------------------------------------|
| hasWebCamPermissions    | boolean             | ユーザーのカメラデータの取得をサポートするかどうか                                      |
| hasMicrophonePermission | boolean             | ユーザーのマイクデータの取得をサポートするかどうか                                      |
| cameras                 | array<CameraItem>   | サポートされているビデオストリームの解像度情報、最大の幅と高さ、および最大フレームレートを含むユーザーのカメラデバイスリスト（最大フレームレートは一部のブラウザではサポートされていません） |
| microphones             | array<DeviceItem>   | ユーザーのマイクデバイスのリスト                                         |
| speakers                | array<DeviceItem>   | ユーザーのスピーカーデバイスのリスト                                         |

**CameraItem**

| Item       | Type    | Description                                                          |
|------------|---------|----------------------------------------------------------------------|
| deviceId   | string  | デバイスIDは、通常は一意であり、デバイスの収集と識別に使用できます                                             |
| groupId    | string  | グループの識別子です。2つのデバイスが同じ物理デバイスに属する場合、それらは同じ識別子を持ちます                                     |
| kind       | string  | カメラデバイスのタイプ：'videoinput'                                                 |
| label      | string  | デバイスを説明するタグ                                                             |
| resolution | object  | カメラでサポートされている最大解像度の幅と高さ、フレームレート{maxWidth: 1280, maxHeight: 720, maxFrameRate: 30} |

**DeviceItem**

| Item     | Type     | Description                          |
|----------|----------|--------------------------------------|
| deviceId | string   | デバイスIDは、通常は一意であり、デバイスの収集と識別に使用できます             |
| groupId  | string   | グループの識別子です。2つのデバイスが同じ物理デバイスに属する場合、それらは同じ識別子を持ちます     |
| kind     | string   | デバイスのタイプです。例えば：'audioinput', 'audiooutput' |
| label    | string   | デバイスを説明するタグ                             |

```javascript
const detect = new RTCDetect();
const result = await detect.getDevicesAsync();
```

#### (async) getCodecAsync()

現在の環境パラメータのコーデックサポートを取得します。

| Item                  | Type    | Description        |
| --------------------- | ------- | ------------------ |
| isH264EncodeSupported | boolean | h264エンコーディングをサポートするかどうか |
| isH264DecodeSupported | boolean | h264デコーディングをサポートするかどうか |
| isVp8EncodeSupported | boolean | vp8エンコーディングをサポートするかどうか |
| isVp8DecodeSupported | boolean | vp8デコーディングをサポートするかどうか |
エンコーディングのサポートとは、オーディオビデオのリリースをサポートすることを意味し、デコードのサポートとは、オーディオビデオ再生のプルをサポートすることを意味します

```javascript
const detect = new RTCDetect();
const result = await detect.getCodecAsync();
```

#### (async) getReportAsync()

現在の環境モニタリングレポートを取得します。

| Item            | Type   | Description                       |
| --------------- | ------ | --------------------------------- |
| system          | object | getSystem()の戻り値と一致します       |
| APISupported    | object | getAPISupported()の戻り値と一致します |
| codecsSupported | object | getCodecAsync()の戻り値と一致します   |
| devices         | object | getDevicesAsync()の戻り値と一致します |

```javascript
const detect = new RTCDetect();
const result = await detect.getReportAsync();
```

#### (async) isHardWareAccelerationEnabled()

Chromeブラウザでハードウェアアクセラレーションが有効になっているかどうかを確認します。

> !
> - このインターフェースの実装は、WebRTCネイティブインターフェースに依存します。isTRTCSupportedがサポートを確認した後、このインターフェースを呼び出して検出することをお勧めします。最大検出時間は30sです。テストにより、
>   1. ハードウェアアクセラレーションを有効にすると、このインターフェイスはWindowsで約2秒、Macで約10秒かかります。
>   2. ハードウェアアクセラレーションを無効にすると、このインターフェイスはWindowsとMacの両方で約30秒かかります。


```javascript
const detect = new RTCDetect();
const data = await detect.isTRTCSupported();

if (data.result) {
  const result = await detect.isHardWareAccelerationEnabled();
  console.log(`is hardware acceleration enabled: ${result}`);
}else{
  console.log(`current browser does not support TRTC, reason: ${data.reason}.`)
}
```


## デバイス検出用のReactコンポーネント

### デバイス検出UIコンポーネントの機能

1. デバイス接続とデバイス検出のロジックを処理します

2. ネットワーク検出のロジックを処理します

3. ネットワーク検出タブはオプションです

4. 中国語と英語の両方をサポートします

### デバイス検出UIコンポーネントの関連リンク

コンポーネントnpmパッケージの使用手順については、[rtc-device-detector-react](https://www.npmjs.com/package/rtc-device-detector-react)をご参照ください

コンポーネントのソースコードのデバッグについては、[github/rtc-device-detector](https://github.com/FTTC/rtc-device-detector)をご参照ください

コンポーネントの参照例については、[WebRTC API Example](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/index.html)をご参照ください

### デバイス検出UIコンポーネントのインターフェース

<img src="https://qcloudimg.tencent-cloud.cn/raw/d4868199e58d757c56a6e69fd58f93a9.png" alt="img" style="zoom:52%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/a7f8aab8091da5b8147d68c493271521.png" alt="img" style="zoom:62%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/e87cc19b7f8bf90bc23a9dce9e00d5dc.png" alt="img" style="zoom:87%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ff35e633d69acffac15ebe27cb6c9cc.png" alt="img" style="zoom:77%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/d4227a2d69cf209a57f395918831873b.png" alt="img" style="zoom:62%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ca749ec2d4fc52728c2a478a6067d83.png" alt="img" style="zoom:87%;" />

### デバイスとネットワークの検出ロジック

#### 1）デバイス接続

 デバイス接続の目的は、ユーザーが使用する機器にカメラ、マイク、またはスピーカーデバイスがあるかどうか、およびインターネットに接続されているかどうかを検出することです。カメラ、マイクデバイスがある場合は、オーディオビデオストリームを取得し、カメラとマイクへのアクセスを許可するようにユーザーに提案します。

+ デバイスにカメラ、マイク、スピーカーデバイスがあるかどうかを判断します

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  const cameraList = await TRTC.getCameras();
  const micList = await TRTC.getMicrophones();
  const speakerList = await TRTC.getSpeakers();
  const hasCameraDevice = cameraList.length > 0;
  const hasMicrophoneDevice = micList.length > 0;
  const hasSpeakerDevice = speakerList.length > 0;
  ```

+ カメラとマイクへのアクセス権限を取得します

  ```javascript
  navigator.mediaDevices
    .getUserMedia({ video: hasCameraDevice, audio: hasMicrophoneDevice })
    .then((stream) => {
    	// オーディオビデオストリームの取得に成功しました
      // ...
    	// カメラとマイクデバイスをリリースします
     	stream.getTracks().forEach(track => track.stop());
    })
    .catch((error) => {
      // オーディオビデオストリームの取得に失敗しました
    });
  ```

+ デバイスがインターネットに接続されているかどうかを判断します

  ```javascript
  export function isOnline() {
    const url = 'https://web.sdk.qcloud.com/trtc/webrtc/assets/trtc-logo.png';
    return new Promise((resolve) => {
      try {
        const xhr = new XMLHttpRequest();
        xhr.onload = function () {
          resolve(true);
        };
        xhr.onerror = function () {
          resolve(false);
        };
        xhr.open('GET', url, true);
        xhr.send();
      } catch (err) {
        // console.log(err);
      }
    });
  }
  const isOnline = await isOnline();
  ```



#### 2） カメラ検出

​	カメラ検出は、選択したカメラによってキャプチャされたビデオストリームをユーザーにレンダリングし、ユーザーがカメラが正常に使用できるかどうかを確認するのに役立ちます。

+ カメラリストを取得します。デフォルトでは、カメラリストの最初のデバイスを使用します

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  let cameraList = await TRTC.getCameras();
  let cameraId = cameraList[0].deviceId;
  ```

+ ビデオストリームを初期化し、idがcamera-videoのdom要素でストリームを再生します

  ```javascript
  const localStream = TRTC.createStream({
    video: true,
    audio: false,
    cameraId,
  });
  await localStream.initialize();
  localStream.play('camera-video');
  ```

+ ユーザーがカメラデバイスを切り替えた後にストリームを更新します

  ```javascript
  localStream.switchDevice('video', cameraId);
  ```

+ デバイスの抜き差しを監視します

  ```javascript
  navigator.mediaDevices.addEventListener('devicechange', async () => {
    cameraList = await TRTC.getCameras();
      cameraId = cameraList[0].deviceId; 
    localStream.switchDevice('video', cameraId);
  })
  ```

+ 検出が完了したら、カメラの占有をリリースします

  ```javascript
  localStream.close();
  ```



#### 3）マイク検出

​	マイク検出は、選択したマイクによってキャプチャされたオーディオストリームのボリュームをユーザーにレンダリングし、ユーザーがマイクが正常に使用できるかどうかを確認するのに役立ちます。

+ マイクリストを取得します。デフォルトでは、マイクリストの最初のデバイスを使用します

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  let microphoneList = await TRTC.getMicrophones();
  let microphoneId = microphoneList[0].deviceId;
  ```

+ オーディオストリームを初期化し、idがaudio-containerのdom要素でストリームを再生します

  ```javascript
  const localStream = TRTC.createStream({
    video: false,
    audio: true,
    microphoneId,
  });
  await localStream.initialize();
  localStream.play('audio-container');
  timer = setInterval(() => {
    const volume = localStream.getAudioLevel();
  }, 100);
  ```

+ ユーザーがマイクデバイスを切り替えた後にストリームを更新します

  ```javascript
  // ユーザーが新しく選択したmicrophoneIdを取得します
  localStream.switchDevice('audio', microphoneId);
  ```

+ デバイスの抜き差しを監視します

  ```javascript
  navigator.mediaDevices.addEventListener('devicechange', async () => {
    microphoneList = await TRTC.getMicrophones();
      microphoneId = microphoneList[0].deviceId;
    localStream.switchDevice('audio', microphoneId);
  })
  ```

+ 検出が完了したら、マイクの占有をリリースし、ボリュームの監視を停止します

  ```javascript
  localStream.close();
  clearInterval(timer);
  ```



#### 4） スピーカー検出

スピーカー検出はオーディオプレーヤーを提供し、ユーザーはオーディオの再生によって、選択したスピーカーが正常に使用できるかどうかを確認できます。

+ mp3プレーヤーを提供し、デバイスの再生ボリュームを上げるようにユーザーに通知し、mp3を再生して、スピーカーデバイスが正常であるかどうかを確認します

  ```html
  <audio id="audio-player" src="xxxxx" controls></audio>
  ```

+ 検出が終了したら、再生を停止します

  ```javascript
  const audioPlayer = document.getElementById('audio-player');
  if (!audioPlayer.paused) {
      audioPlayer.pause();
  }
  audioPlayer.currentTime = 0;
  ```



#### 5） ネットワーク検出

+ [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)を呼び出して、それぞれuplinkClientおよびdownlinkClientという2つのClientを作成します。

+ この2つのClientは、同じルームに入ります。

+ uplinkClientを使用してプッシュし、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視してアップリンクのネットワーク品質を確認します。

+ downlinkClientを使用してプルし、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視してダウンリンクのネットワーク品質を確認します。

+ プロセス全体は約15秒間続く可能性があり、最後に平均ネットワーク品質を使用して、アップリンクとダウンリンクのネットワーク状態を大まかに判断します。

> !  検出プロセスには少額の[基本サービス料金](https://cloud.tencent.com/document/product/647/17157#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1)が発生します。プッシュ解像度が指定されていない場合、デフォルトで640*480の解像度でプッシュします。

```javascript
let uplinkClient = null; // アップリンクネットワーク品質の確認に使用されます
let downlinkClient = null; //ダウンリンクネットワーク品質の確認に使用されます
let localStream = null; // テストされるストリームに使用されます
let testResult = {
  // アップリンクネットワーク品質のデータを記録します
  uplinkNetworkQualities: [],
  // ダウンリンクネットワーク品質のデータを記録します
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. アップリンクネットワーク品質を確認します
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppIdを記入します
    userId: 'user_uplink_test',
    userSig: '', // uplink_testのuserSig
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // 実際のサービスシーンに応じてvideo profileを設定します
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // テスト用ルームを追加します。競合を避けるためにルーム番号はランダムである必要があります
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. ダウンリンクネットワーク品質を確認します
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppIdを記入します
    userId: 'user_downlink_test',
    userSig: '', // userSig
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
		// サブスクリプションに成功した後、ネットワーク品質イベントの監視を開始します
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // テスト用ルームを追加します。競合を避けるためにルーム番号はランダムである必要があります
  await downlinkClient.join({ roomId: 8080 });
}

// 3. 確認を開始します
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. 15秒後に確認を停止し、平均ネットワーク品質を計算します
setTimeout(() => {
  // アップリンクの平均ネットワーク品質を計算します
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // ダウンリンクの平均ネットワーク品質を計算します
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // 確認が終了し、関連する状態がクリアされます。
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## TRTC機能検出ページ

現在環境の検出のために、現在、TRTCSDKを使用している場合に[TRTC検出ページ](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を使用できます。また、環境検出またはトラブルシューティングのために、レポート生成ボタンをクリックして、現在の環境のレポートを取得できます。

