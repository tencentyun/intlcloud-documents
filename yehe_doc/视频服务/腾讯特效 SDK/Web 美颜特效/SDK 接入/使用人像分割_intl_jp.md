人物画像分割を使用するには、まず初期化時に人物画像分割モジュールを有効化する必要があります。詳細については、[ストリームのカスタマイズ](https://intl.cloud.tencent.com/document/product/1143/50102)、[内蔵カメラ](https://intl.cloud.tencent.com/document/product/1143/50101)をご参照ください。
**この機能はWeb端末のみをサポートしています**。

[](id:set)
## 背景の設定
- SDKは背景のぼかし、画像背景の設定をサポートし、初期化パラメータでパススルーをサポートしています。
```javascript
const config = {
	module: {
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
	},
	background: {
		type: 'blur' // 背景のぼかし
	}
}
const sdk = new ArSdk(
	// configオブジェクトを渡してsdkの初期化に使用します
	config
)
```
- SDKも動的な背景の変更をサポートしています。
```javascript
sdk.setBackground({
	type: 'image', // 画像背景
	src: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg'
})
```

[](id:open)
## 透明な背景
SDKは一部のブラウザで透明な背景をサポートしています。
```javascript
sdk.setBackground({
	type: 'transparent'
})
```

>! ブラウザの互換性の問題のため、次のいくつかの点に注意してください。
>- 人物画像分割は同時にモバイル端末およびデスクトップブラウザをサポートしています。
>- ローカルのみで透明な背景を処理して表示します。WebRTCは透明なチャネルのエンコードをサポートしていないため、プッシュすると透明な背景は無効になります。
>- 透明な背景効果はデスクトップのChrome/Firefoxのみをサポートしています。デスクトップのSafariおよびiOSはいずれもサポートしていません。
