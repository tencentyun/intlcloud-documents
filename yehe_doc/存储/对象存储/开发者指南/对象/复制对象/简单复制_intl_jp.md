## ユースケース

Cloud Object Storage（COS）に保存済みのオブジェクトのシンプルなコピー操作を行うことで、新しいオブジェクトレプリカを作成することができます。1回の操作で最大5GBのオブジェクトをコピーすることができます。オブジェクトが5GBを超える場合は、必ず[マルチパートコピー](https://intl.cloud.tencent.com/document/product/436/14118)インターフェースを使用してコピーを行わなければなりません。オブジェクトコピーには次の機能があります。

- 新しいオブジェクトレプリカを作成します。
- オブジェクトをコピーして名前を変更し、元のオブジェクトを削除することでリネームを実現します。
- オブジェクトのストレージタイプを変更します。コピー時に同一のソースおよびターゲットオブジェクトキーを選択することで、ストレージタイプを変更します。
- 異なるTencent Cloud COSリージョンにあるオブジェクトをコピーします。
- オブジェクトのメタデータを変更します。コピー時に同一のソースおよびターゲットオブジェクトキーを選択し、その中のメタデータを変更します。

オブジェクトをコピーする際は、元のオブジェクトのメタデータがデフォルトで継承されますが、作成日は新しいオブジェクトの時間に基づいて計算されます。

>?
>- CASタイプのオブジェクトのコピー＆ペーストはサポートされていません。
>- マルチAZ設定を有効にしているバケットでは、マルチAZストレージタイプをシングルAZストレージタイプにコピーすることはサポートされていません。
>- サブアカウントでオブジェクトをコピーするには、PutObject、GetObject、GetObjectACLという3つの権限が必要です。

## 利用方法

### COSコンソールの使用

COSコンソールを使用してオブジェクトをコピーすることができます。詳細については、[オブジェクトのコピー](https://intl.cloud.tencent.com/document/product/436/33456)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用してオブジェクトコピーリクエストを送信できます。 詳細については、[PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)のAPIドキュメントをご参照ください。

### SDKの使用

SDKのオブジェクトコピー設定メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/40494)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/40171)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/40495)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/44019)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/43865)
- [Node.js SDK ](https://intl.cloud.tencent.com/document/product/436/43874)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/45498)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/46470)
- [ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/436/43885)
