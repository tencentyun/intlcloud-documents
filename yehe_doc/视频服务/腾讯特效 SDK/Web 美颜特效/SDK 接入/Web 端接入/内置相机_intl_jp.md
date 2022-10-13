SDKは内蔵カメラを提供し、開発者が迅速にカメラを呼び出す、またはカメラにより多くのインタラクション制御する必要がある場合は、内蔵カメラ方式を使用することをお勧めします。

[](id:step1)
## ステップ1：SDKの統合
```javascript
import { ArSdk } from 'tencentcloud-webar';// SDKクラス
```
プロジェクトをコンパイルする必要がない場合は、直接次の方式を引用することができます。
```html
<script charset="utf-8" src="https://webar-static.tencent-cloud.com/ar-sdk/resources/latest/webar-sdk.umd.js"></script>
```

[](id:step2)
## ステップ2：インスタンスの初期化
続いて、SDKインスタンスを初期化して表示に使用します。
```javascript
// 認証パラメータの取得
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 詳細については「License の設定と使用 - 署名方法」をご参照ください
};

const config = {
    module: { // 0.2.0バージョンの追加
		beautify: true, // 美顔モジュールを有効にするかどうか。有効にすると美顔、メイクアップ、ステッカーなどの機能を使用することができますsegmentation: true // 人物画像分割モジュールを有効にするかどうか。有効にすると背景機能が使用できます
		segmentation: true // 人物画像分割モジュールを有効にするかどうか。有効にすると背景機能が使用できます
	},
    auth: authData, // 認証パラメータ
    camera: { // camera設定を渡して内蔵カメラを呼び出します
        width: 1280,
        height: 720
    },
	beautify: { // 美顔パラメータの初期化(オプション)
		whiten: 0.1,
		dermabrasion: 0.3,
		eye: 0.2,
		chin: 0,
		lift: 0.1,
		shave: 0.2
	}
}
const sdk = new ArSdk(
	// configオブジェクトを渡してsdkの初期化に使用します
	config
)

let effectList = [];
let filterList = [];

sdk.on('created', () => {
    // ページ表示のためにcreatedコールバックでエフェクトおよびフィルターリストをプルすることができます。詳細については、「SDKへのアクセス - パラメータと方法」をご参照ください
    sdk.getEffectList({
        Type: 'Preset',
        Label: 'メイクアップ',
    }).then(res => {
        effectList = res
    });
    sdk.getCommonFilter().then(res => {
        filterList = res
    })
})

// readyコールバックでsetBeautify/setEffect/setFilterなどのレンダリング方法を呼び出すことができます
// 詳細については「SDKへのアクセス - 美顔およびエフェクトの設定」をご参照ください
sdk.on('ready', () => {
    // 美顔設定
    sdk.setBeautify({
        whiten: 0.2
    });
    // エフェクトの設定
    sdk.setEffect({
        id: effectList[0].EffectId,
        intensity: 0.7
    });
    // フィルターの設定
    sdk.setFilter(filterList[0].EffectId, 0.5)
})
```
>! 
>- 美顔検出および人物画像分割はいずれも一定のロード時間およびリソースを消費するため、初期化設定でモジュール設定を提供することよって、必要な機能を選択できるようにします。無効化したモジュールはプリロードおよび初期化を行いません。
>- config内のcameraパラメータはSDKが現在のデバイスのカメラのメディアストリームを収集して入力とすることを表します。cameraパラメータを設定すると、SDKはさらに一連の基本的なデバイス管理方法を提供します。詳細については、[デバイス制御](#step5)をご参照ください。

[](id:step3)
## ステップ3：ストリームの再生
SDKは迅速にページで出力効果をプレビューできるプレーヤーを提供し、ローカルのプレビュー効果のシナリオに使用することができます。異なるコールバックイベントで取得したplayerには若干の違いがあり、異なるシナリオに適用されます。自身の業務ニーズに応じて処理方式を選択することができます。

- 画面表示に対する時間制限の要求がある場合、`cameraReady`コールバックでプレーヤーを取得することができます。この時SDKがリソースのロードおよび検出の初期化を開始していない場合、元の画面のみを表示します。
```javascript
sdk.on('cameraReady', async () => {
	// SDKのplayerを初期化します。その内、my-dom-idはプレーヤーを設定する必要があるコンテナidを表します
    const player = await sdk.initLocalPlayer('my-dom-id')
    // 直接再生
    await player.play()
})
```
- 初期化が完了し、美顔を有効化した後に再び再生したことを検出する必要がある場合は、readyコールバックでプレーヤーを取得することができます。
```javascript
sdk.on('ready', async () => {
    // SDKのplayerを初期化します。その内、my-dom-idはプレーヤーを設定する必要があるコンテナidを表します
    const player = await sdk.initLocalPlayer('my-dom-id')
    // 直接再生
    await player.play()
})
```

>! 
>- initLocalPlayerが取得したプレーヤーはデフォルトではミュートです。ミュートを解除するとエコーが発生する可能性があります。
>- 取得したplayerは、内部に`sdk.getOutput()`メソッドがパッケージ化され、ユーザーが使用しやすくなっています。

SDK initLocalPlayerの後、そのplayerオブジェクトはいくつかの一般的なインターフェースをパッケージ化し、以下のメソッドをサポートしています。

| 方法名          | 説明                       | 入力パラメータ        | 戻り値           |
| :-------------- | :------------------------- | :---------- | :--------------- |
| play            | 再生                       | -           | Promise;         |
| pause           | 一次停止（ストリーミングは停止せず、再開できます） | -           | -                |
| stop            | 停止（ストリーミングも停止します）       | -           | -                |
| mute            | ミュート                       | -           | -                |
| unmute          | ミュート解除                  | -           | -                |
| setMirror       | イメージの設定                   | true\|false | -                |
| getVideoElement | 内蔵videoオブジェクトの取得        | -           | HTMLVideoElement |
| destroy         | 破棄                       | -           | -                |

>! プレーヤーはデフォルトではcamera [デバイス制御](#step5)の変化に追従します。cameraのデバイス制御はメインスイッチで、localPlayerの再生制御はサブスイッチであることが簡単に理解できます。例：
>- `camera.muteVideo`を呼び出すと、デバイスのビデオストリームを無効化します。この時localPlayerが再びplayを呼び出しても再生停止状態になります。
>- `camera.unmuteVideo`を呼び出すと、再びビデオストリームを有効化します。この時localPlayerはデフォルトで再生状態を自動的に復元します。
>そのためcamera設定を有効にした状況ではlocalPlayerの状態を手動で制御する必要はなく、cameraデバイスの状態の管理のみとなります。

[](id:step4)
## ステップ4：出力の取得
ストリームをプッシュする必要がある場合は、getOutputメソッドを使用して出力するメディアストリームを取得することができます。
出力するMediaStreamを取得してから、サードパーティーのSDK（例えばTRTC Web SDK、ライブイベントストリーミングWeb SDK）を組み合わせてプッシュなどの後続処理を行うことができます。

```javascript
const output = await sdk.getOutput()
```
>!
>- 内蔵カメラを使用して初期化した場合、getOutput出力するメディアストリームはいずれも`MediaStream`タイプです。
>- 出力するメディアストリーム内のvideoトラックは ArSdkリアルタイムで処理され、`audio`トラックがあれば変更されません。
>- getOutputメソッドは非同期メソッドで、sdkが一連の初期化動作を実行するまで待機し、ストリームを生成した後に返すことができます。
>- getOutputメソッドはFPSパラメータを渡し、出力するフレームレートをFPS（例えば15）に設定することをサポートし、渡されない場合、デフォルトで入力ストリームのフレームレートを使用します。

[](id:step5)
## ステップ5：デバイス制御
カメラの起動/停止などの操作を行う必要がある場合、sdk.cameraインスタンスによって実現できます。サンプルコードは次のとおりです。
```javascript
const output = await sdk.getOutput()
// todoではいくつかのサービスロジックを省略しています
// ...

// getOutputの後にsdk.cameraの初期化がすでに完了していた場合は、直接取得することができます
const cameraApi = sdk.camera

// 現在のデバイスリストの取得
const devices = await cameraApi.getDevices()
console.log(devices)
// ビデオトラックの無効化
// cameraApi.muteVideo()
// ビデオトラックの有効化
// cameraApi.unmuteVideo()
// 複数のカメラがある場合はデバイスidに応じて切り替えできます
// await cameraApi.switchDevices('video', 'your-device-id')
```
すぐに`sdk.camera`を取得する必要がある場合は、初期化時に、cameraReadyイベントで取得できます。
```javascript
// todoではいくつかの初期化パラメータを省略しています
// ...
const sdk = new ArSdk(
    config
)

let cameraApi;
sdk.on('cameraReady', async () => {
    cameraApi = sdk.camera
    // 現在のデバイスリストの取得
    const devices = await cameraApi.getDevices()
    console.log(devices)
    // ビデオトラックの無効化
    // cameraApi.muteVideo()
    // ビデオトラックの有効化
    // cameraApi.unmuteVideo()
    // 複数のカメラがある場合はデバイスidに応じて切り替えできます
    // await cameraApi.switchDevices('video', 'your-device-id')
})
```
デバイスを制御しやすくするために、内蔵された`camera`は次のような方法の呼び出しを提供しています。
<table>
<thead><tr><th>メソッド名</th><th>説明</th><th>入力パラメータ</th><th>戻り値</th></tr></thead>
<tbody>
<tr>
<td>getDevices</td>
<td>現在のすべてのデバイスリストを取得します</td>
<td>-</td>
<td>Promise&lt;Array&lt;MediaDeviceInfo&gt;&gt;</td>
</tr><tr>
<td>switchDevice</td>
<td>デバイスを切り替えます</td>
<td><code>type:string, deviceId:string</code></td>
<td>Promise
</td>
</tr>
<tr>
<td>muteAudio</td>
<td>現在のカメラストリームをミュートする</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>unmuteAudio</td>
<td>ミュートの復元</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>muteVideo</td>
<td>現在のカメラストリーム内の画面を無効化します。この場合、ストリームは存在しますがビデオトラックはすでに無効化されています</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>unmuteVideo</td>
<td>現在のカメラストリーム内の画面を有効化します</td>
<td>-</td>
<td>-</td>
</tr><tr>
<td>stopVideo</td>
<td>現在のカメラデバイスを停止すると、ビデオストリームが停止します（オーディオストリームはまだ存在します）</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>restartVideo</td>
<td>現在のカメラを再起動し、stopVideoの後に使用します</td>
<td>-</td>
<td>Promise</td>
</tr>
<tr>
<td>stop</td>
<td>現在のカメラのビデオおよびオーディオデバイスを停止します</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>

