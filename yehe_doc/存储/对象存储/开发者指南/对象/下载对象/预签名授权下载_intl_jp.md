## ユースケース

デフォルトでは、バケットとオブジェクトはすべてプライベートなものです。第三者がオブジェクトをダウンロードできるようにし、なおかつ相手にCAMアカウントまたは一時キーなどの方法を使用させたくない場合は、署名付きURLを使用して署名を第三者に渡し、ダウンロード操作を完了させることができます。有効な署名付きURLを受領した人は誰でもオブジェクトをダウンロードできます。

URLを署名付きにする際、署名の中にオブジェクトキーを含める設定にすることで、指定されたオブジェクトのダウンロードのみを許可することができます。プログラム内で署名付きURLの有効期間を指定することで、タイムアウト後にそのURLが非権限者によって使用されないよう保証することもできます。

## 利用方法

### SDKの使用

SDKの署名付きURL生成メソッドを直接呼び出すことができます。詳細については下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37680)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37690)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/436/31711)

