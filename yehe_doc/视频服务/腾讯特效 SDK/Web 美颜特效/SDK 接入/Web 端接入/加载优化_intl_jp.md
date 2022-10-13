[](id:normal)
## 通常モード
通常モードでは`cameraReady`コールバック内でgetOutputインターフェースによって出力ストリームを取得することができます。この時取得した出力ストリームデータとSDKに渡す入力ストリームデータは同じもので、美顔効果はまだ有効ではなく、SDKが入力データをそのまま出力することであると理解できます。後続の関連する美顔効果の準備が完了すると自動的にこの出力ストリームに重ね合わされるため、改めてgetOutputを呼び出して取得する必要はありません。この方式ではページ初期化時にSDKを初期化し、できるだけ早く画面を表示する必要があります。しかし、画面が表示されたからといって、すぐに美顔効果のあるシーンを要求されるわけではありません。

したがって、`ready`コールバック内でgetOutputインターフェースによって出力ストリームを取得することもできます。上記の`cameraReady`と異なるのは、この時取得した出力ストリームデータはすでに美顔エフェクトがあり、このコールバックインターフェースがトリガーされるタイミングは`cameraReady`インターフェースよりわずかに遅いため、この方式は画面が表示されたらすぐに美顔効果を得られますが、できるだけ早く画面を表示するようなシーンを要求されることはありません。
![](https://qcloudimg.tencent-cloud.cn/raw/38365734db212ba293fbd283cdcbf3a9.jpg)

サンプルコードは次のとおりです。

```javascript
// 認証パラメータの取得
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 詳細については「License の設定と使用 - 署名方法」をご参照ください
};

// sdkを初期化する時にinputまたはcameraパラメータを渡し、通常モードでロードします
const config = {
	auth: authData, // 認証パラメータ
    beautify: { // 美顔パラメータ
        whiten: 0.1,
        dermabrasion: 0.5,
        lift: 0,
        shave: 0,
        eye: 0.2,
        chin: 0,
    },
    input: inputStream // SDKに渡すinputストリームデータを構築します。詳細については「パラメータと方法 - パラメータの初期化」をご参照ください
}
const sdk = new ArSdk(
	// configオブジェクトを渡してsdkの初期化に使用します
	config
)
// sdkは認証後すぐにcreatedイベントをトリガーします
sdk.on('created', () => {
    // ページ表示のためにcreatedコールバックでエフェクトおよびフィルターリストをプルします
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

// 異なるコールバック内でgetOutputが取得するデータの違いは次のとおりです。自身のニーズに応じて1つ選択します
sdk.on('cameraReady', async () => {
	const output = await sdk.getOutput() // 美顔パラメータが有効化されていません
    // 再生
    ...
})
sdk.on('ready', async () => {
    const output = await sdk.getOutput() // 美顔パラメータが有効化されています
    // 再生
    ...
    // readyコールバックでsetEffect/setBeautify/setFilterなどの効果を呼び出します
})

```

[](id:preliminary)
## プリフォーマット（0.2.0バージョン以降にサポートを開始）
SDKの初回ロード時にはリモートで静的リソースをダウンロードしてから検出モデルの初期化を完了する必要があり、ロードする所要時間はネットワークの影響を受けます。画面を素早く表示させる必要がある業務シーンでは、SDKはプリフォーマットするロード方法で事前に静的リソースをロードします。

**プリフォーマットのユースケース**
- ケース1：ページを初期化してロードする時は美顔SDKは不要です。ユーザーが特定の操作を行ってビデオ画面を表示する必要があります。
- ケース2：ページBは美顔効果に関連し、ページBからページAにジャンプします。
類似した状況ではいずれもまずリソースのロードを実行し（できるだけ早く）、その後業務上のニーズを組み合わせ、適切なタイミングでSDKに入力ストリームデータを提供し、さらに出力ストリームの表示効果を取得することができます。

例：ケース1では、ページ初期化時にリソースをロードすることができます。ケース2では、ページAでSDKインスタンスを取得し、Bに渡して使用することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/6cc0d286584d1a10db1e5764b167f092.jpg)

**ケース1を例にすると、コードは次のとおりです**
```html
<button id="start">カメラをオンにします</button>
```
```javascript
// 認証パラメータの取得
const authData = {
	licenseKey: 'xxxxxxxxx',
	appId: 'xxx',
	authFunc: authFunc // 詳細については「License の設定と使用 - 署名方法」をご参照ください
};

// sdkを初期化する時にinputまたはcameraパラメータを渡さなかった場合、インスタンス化後にsdkは必要なリソースのプリロードを開始します
const config = {
	auth: authData, // 認証パラメータ
    beautify: { // 美顔パラメータ
        whiten: 0.1,
        dermabrasion: 0.5,
        lift: 0,
        shave: 0,
        eye: 0.2,
        chin: 0,
    },
}
const sdk = new ArSdk(
	// configオブジェクトを渡してsdkの初期化に使用します
	config
)
// sdkは認証後すぐにcreatedイベントをトリガーします
sdk.on('created', () => {
    // ページ表示のためにcreatedコールバックでエフェクトおよびフィルターリストをプルします
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
// resourceReadyは関連するリソースの準備が完了し、このコールバックの後にinitCoreを呼び出して入力ストリームデータを提供することができることを意味します
sdk.on('resourceReady', () => {
})
// このモードでは、ユーザーが明示的にinitCoreを呼び出した後に、readyコールバックをトリガーすることができます
sdk.on('ready', async () => {
	const output = await sdk.getOutput() // 美顔が有効化されています
    // 再生
    ...
    // readyコールバックでsetEffect/setBeautify/setFilterなどの効果を呼び出します
})
// ユーザーがクリックしてカメラを起動するとSDKに入力ストリームデータを渡します
document.getElementById('start').onclick = async function(){
    const devices = await navigator.mediaDevices.enumerateDevices()
    const cameraDevice = devices.find(d=>d.kind === 'videoinput')
    navigator.mediaDevices.getUserMedia({
        audio: false,
        video: {
            deviceId: cameraDevice.deviceId
            ... // その他の設定
        }
    }).then(mediaStream => {
        // このモードでは、上記のresourceReadyイベントを確認後、initCoreメソッドを呼び出してください
        sdk.initCore({
            input: mediaStream // SDKに渡すinputストリームデータを構築します。詳細については「パラメータと方法 - パラメータの初期化」をご参照ください
        })
    })    
}
```

