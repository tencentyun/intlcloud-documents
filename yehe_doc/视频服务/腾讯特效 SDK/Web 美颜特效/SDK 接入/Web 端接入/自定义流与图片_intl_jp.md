## SDKステップへのアクセス
[](id:step1)
### ステップ1：SDKの統合
```javascript
import { ArSdk } from 'tencentcloud-webar';// SDKクラス
```
プロジェクトをコンパイルする必要がない場合は、直接次の方式を引用することができます。
```html
<script charset="utf-8" src="https://webar-static.tencent-cloud.com/ar-sdk/resources/latest/webar-sdk.umd.js"></script>
```

[](id:step2)
### ステップ2：インスタンスの初期化
1. SDKインスタンスを初期化します。
```javascript
// 認証パラメータの取得
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 詳細については「License の設定と使用 - 署名方法」をご参照ください
};
// SDKのストリームを入力します
const stream = await navigator.mediaDevices.getUserMedia({
	audio: true,
	video: { width: w, height: h }
})

const config = {
    module: { // 0.2.0バージョンの追加
		beautify: true, // 美顔モジュールを有効にするかどうか。有効にすると美顔、メイクアップ、ステッカーなどの機能を使用することができます
		segmentation: true // 人物画像分割モジュールを有効にするかどうか。有効にすると背景機能が使用できます
	},
	auth: authData, // 認証パラメータ
    input: stream, // input入力ストリームの転送
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
```
>! 美顔検出および人物画像分割はいずれも一定のロード時間およびリソースを消費するため、初期化設定でモジュール設定を提供することよって必要な機能を選択します。無効化したモジュールはプリロードおよび初期化を行わず、関連する効果を設定することもできません。

2. 入力はメディアストリーム以外に、 `string|HTMLImageElement`を渡すことで画像を処理することもサポートしています。
```javascript
const config = {
	auth: authData, // 認証パラメータ
    input: 'https://xxx.png', // input転送入力ストリーム
}
const sdk = new ArSdk(
	// configオブジェクトを渡してsdkの初期化に使用します
	config
)

// ページ表示のためにcreatedコールバックでエフェクトおよびフィルターリストをプルすることができます。詳細については、「SDKへのアクセス - パラメータと方法」をご参照ください
sdk.on('created', () => {
    // 内蔵メイクアップの取得
    sdk.getEffectList({
        Type: 'Preset',
        Label: 'メイクアップ',
    }).then(res => {
        effectList = res
    });
    // 内蔵フィルターの取得
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

[](id:step3)
### ステップ3：ストリームの再生
`ArSdk.prototype.getOutput`メソッドを使用して出力するメディアストリームを取得することができます
異なるコールバックイベント内で取得した出力ストリームには若干の違いがあり、異なるケースに適用されるため、自身の業務ニーズに応じて処理方式を選択することができます。

- 画面表示に対する時間制限の要求がある場合、`cameraReady`コールバックで出力ストリームを取得して再生することができます。この時SDKがリソースのロードおよび検出の初期化を開始していない場合、元の画面のみを表示します。
```javascript
sdk.on('cameraReady', async () => {
	// camerareadyコールバック内でより早く出力画面を取得することができます。この時初期化で渡された美顔パラメータはまだ有効ではなく、入力画面と同じです
	// できるだけ早く画面を表示する必要がありますが、画面が表示されたらすぐに美顔のシーンを要求されるわけではありません
	// その後美顔が有効になった後streamを更新する必要はなく、SDK内部で処理されます
	const output = await ar.getOutput();
    // video再生出力するメディアストリームを使用し、効果をプレビューします
	const video = document.createElement('video')
    video.setAttribute('playsinline', '');
    video.setAttribute('autoplay', '');
    video.srcObject = output
    document.body.appendChild(video)
    video.play()
})
```
- 初期化の完了を検出し、美顔を有効化した後に再び再生する必要がある場合は、readyコールバックで出力を取得して再生することができます。
```javascript
sdk.on('ready', async () => {
    // readyコールバックで出力画面を取得します。この時、初期化され渡された美顔パラメータが有効であれば、取得したoutput streamにはすでに美顔効果があります
	// 上記のcameraReadyでoutputを取得することとは異なり、このコールバック実行タイミングはわずかに遅くなります。画面を表示するとすぐに美顔シーンがありますが、できるだけ早く画面を表示するシーンを要求されるわけではありません
	const output = await ar.getOutput();
    // video再生出力するメディアストリームを使用し、効果をプレビューします
    const video = document.createElement('video')
    video.setAttribute('playsinline', '');
    video.setAttribute('autoplay', '');
    video.srcObject = output
    document.body.appendChild(video)
    video.play()
})
```

[](id:step4)
### ステップ4：出力の取得
出力する`MediaStream`を取得してから、サードパーティーのSDK（例えばTRTC Web SDK、ライブイベントストリーミングWeb SDK）を組み合わせてプッシュなどの後続処理を行うことができます。
```javascript
const output = await sdk.getOutput()
```


>!
>- 渡すinputが画像の場合、stringタイプのDataURLを返し、他の場合はいずれも`MediaStream`タイプを返します。
>- 出力するメディアストリーム内の`video`トラックはArSdkのリアルタイム処理であり、`audio`トラックがあれば変更されません。
>- getOutputメソッドは非同期メソッドで、SDKが一連の初期化動作を実行するまで待機し、ストリームを生成した後に返すことができます。
>- getOutputメソッドはFPSパラメータを渡し、出力するフレームレートをFPS（例えば15）に設定することをサポートし、渡されない場合、デフォルトで入力ストリームのフレームレートを使用します。
>- getOutputは複数回実行でき、1回実行すると1つの新しいメディアストリームが生成され、異なるフレームレートのメディアストリームを出力するシーンに使用することができます（例えばプレビュー時に高フレームレートのストリームを使用し、プッシュ時に低フレームレートのストリームを使用します）。

[](id:step5)
### ステップ5：美顔およびエフェクトの設定
詳細については、[美顔およびエフェクトの設定](https://intl.cloud.tencent.com/document/product/1143/50104)をご参照ください。

## 入力ストリームの更新（0.1.19バージョン以降にサポートを開始）
デバイスの切り替え、カメラの停止などの必要がある場合、新しいストリーム入力sdkを取得する必要があります。何度もsdkの初期化を繰り返さず、直接`sdk.updateInputStream`を呼び出して入力ストリームを切り替えてください。
以下ではコンピュータのデフォルトカメラおよび外付けカメラの切り替えを例に、updateInputStreamの使用方法をご紹介します。

```javascript

async function getVideoDeviceList(){
    const devices = await navigator.mediaDevices.enumerateDevices()
    const videoDevices = []
    devices.forEach((device)=>{
        if(device.kind === 'videoinput'){
            videoDevices.push({
                label: device.label,
                id: device.deviceId
            })
        }
    })
    return videoDevices
}

async function initDom(){
    const videoDeviceList = await getVideoDeviceList()
    let dom = ''
    videoDeviceList.forEach(device=>{
        dom = `${dom}
        <button id=${device.id} onclick='toggleVideo("${device.id}")'>${device.label}<nbutton>
        `
    })
    const div = document.createElement('div');
    div.id = 'container';
    div.innerHTML = dom;
    document.body.appendChild(div);
}

async function toggleVideo(deviceId){
    const stream = await navigator.mediaDevices.getUserMedia({
        video: {
            deviceId,
            width: 1280,
            height: 720,
          }
    })
	// sdkが提供する更新入力ストリームインターフェースを使用すると、古いトラックのstopを内部で処理します
	// 入力ストリームの更新後に再びgetOutputを呼び出す必要はなく、SDK内部で処理されます
    sdk.updateInputStream(stream) 
}

initDom()

```

## 一次停止と復元の検出
一次停止の検出はCPUの占有を節約することができます。ビジネスロジックで検出を一次停止する必要がある場合は、disableおよびenableインターフェースを呼び出して手動で起動/停止することができます。
```html
<button id="disable">検出停止</button>
<button id="enable">検出開始</button>
```
```javascript
// 検出を停止し、元の画面を出力します
disableButton.onClick = () => {
    sdk.disable()
}
// 検出を開始し、美顔などのエフェクトが有効化された画面を出力します
enableButton.onClick = () => {
    sdk.enable()
}
```
