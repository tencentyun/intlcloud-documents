## ユースケース

デフォルトでは、バケットとオブジェクトはすべてプライベートなものです。第三者がオブジェクトをダウンロードできるようにし、なおかつ相手にCAMアカウントまたは一時キーなどの方法を使用させたくない場合は、署名付きURLを使用して署名を第三者に渡し、ダウンロード操作を完了させることができます。有効な署名付きURLを受領した人は誰でもオブジェクトをダウンロードできます。

URLを署名付きにする際、署名の中にオブジェクトキーを含める設定にすることで、指定されたオブジェクトのダウンロードのみを許可することができます。プログラム内で署名付きURLの有効期間を指定することで、タイムアウト後にそのURLが非権限者によって使用されないよう保証することもできます。

>!
> - CDNドメイン名にアクセスするにはCDNの認証プロセスに従う必要があり、COSの署名は使用できないため、署名付きURLではCDNドメイン名の使用をサポートしていません。
> - ユーザーには一時キーを使用して署名付きURLを生成し、一時権限承認方式によってさらにアップロード、ダウンロードなどの署名付きリクエストの安全性を向上させることをお勧めします。一時キーを申請する際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従い、目的のバケットまたはオブジェクト以外のリソースが漏洩しないようにしてください。
> - やむを得ずパーマネントキーを使用して署名付きURLを生成する場合は、リスク回避のため、パーマネントキーの権限の範囲をアップロードまたはダウンロード操作のみに限定することをお勧めします。また、生成した署名の有効期間を、今回のアップロードまたはダウンロード操作に必要な最短の期限までに設定し、指定した署名付きURLの有効期限が過ぎるとリクエストが中断するようにします。失敗したリクエストは新しい署名を申請後に再度実行する必要があります。中断からの再開はサポートしていません。
> 


## 利用方法

### SDKの使用

SDKの署名付きURL生成メソッドを直接呼び出すことができます。詳細については下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37680)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31520)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31524)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38068)
- [Flutter SDK](https://www.tencentcloud.com/document/product/436/54513)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31528)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37690)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31536)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31540)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/32455)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31544)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31548)
- [React Native SDK](https://www.tencentcloud.com/document/product/436/54312)
- [ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/436/31711)
