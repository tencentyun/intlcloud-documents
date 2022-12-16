このSDKの主な機能は、[Web美顔エフェクト](https://www.tencentcloud.com/document/product/1143/51226)へのスピーディーかつ安全なアクセスを提供し、すべての機能を使用できるようにすることです。

## フロー説明
SDKはシンプルで侵入性が低いインターフェースを実現してアクセスを提供し、インスタンスを初期化すると、レンダリングノードを自身のページに追加するだけで迅速に**Web 美顔エフェクト**機能を実現することができます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a691e17a2a028c9fa00a92f37091465b.jpg" style="zoom:50%;" />

## インストール
本SDKはnpmパッケージを使用してWeb端末のSDKを提供しています。
```
npm install tencentcloud-webar
```

## SDKへのアクセス

- Web端末では内蔵Cameraとストリームのカスタマイズという2種類の初期化方式を提供しています。
	- [内蔵カメラとプレーヤー](https://intl.cloud.tencent.com/document/product/1143/50101)：内蔵されたカメラとプレーヤーパッケージを使用し、簡単且つ迅速に呼び出し、インタラクション機能が豊富です。
	- [カスタマイズストリームへのアクセス](https://intl.cloud.tencent.com/document/product/1143/50102)：自身でメディアストリームをメンテナンスする必要があるかまたはより高い柔軟性と制御性が求められる場合に使用されます。

## 美顔およびエフェクトの設定
詳細については、[美顔およびエフェクトの設定](https://intl.cloud.tencent.com/document/product/1143/50104)をご参照ください。

## 人物画像分割（0.2.0バージョンの追加）
人物画像分割を有効化すると背景設定機能をサポートすることができ、Web端末のみをサポートしています。詳細については、 [人物画像分割の使用](https://intl.cloud.tencent.com/document/product/1143/50105)をご参照ください。

## 3Dエフェクト（バージョン0.3.0から追加）
Web端末をサポートしています。呼び出しメソッドはエフェクトの設定と同じです。詳細については[美顔およびエフェクトの設定](https://www.tencentcloud.com/document/product/1143/50104)をご参照ください。

## Animoji表情およびバーチャルキャラクター（バージョン0.3.0から追加）
WebGL2実行環境に依存し、現在はWeb端末のみでサポートしています。詳細については[表情およびバーチャルキャラクターの使用](https://www.tencentcloud.com/document/product/1143/51231)をご参照ください。


## パラメータと方法の説明
[パラメータと方法](https://intl.cloud.tencent.com/document/product/1143/50106)をご参照ください。

## 互換性の処理

| ブラウザ   | サポートしているプラットフォーム |
| -----   | --- |
| Chrome  | デスクトップ、Android、iOS |
| Safari  | デスクトップ、iOS |
| FireFox | デスクトップ、Android、iOS |
| QQ webview | Android |
| WeChat webview | Android/iOS WeChat8.0.16以上|


>? **SDK 0.2.1バージョンでハードウェアアクセラレーションの検出機能が追加されました。**
Web端末の美顔SDKはスムーズなレンダリングを可能にするためにブラウザをサポートしてハードウェアアクセラレーションを有効化する必要があるため、SDKは検出方法を提供して業務を事前に判断し、サポートされていない場合はブロック処理します。
```javascript
import {ArSdk, isWebGLSupported} from 'tencentcloud-webar'

if(isWebGLSupported()) {
	const sdk = new ArSdk({
		...
	})
}else{
	// ロジックをブロックします
}
```
