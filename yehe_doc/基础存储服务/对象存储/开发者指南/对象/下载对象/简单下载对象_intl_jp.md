## ユースケース

リクエストを直接送信してCloud Object Storage（COS）内のオブジェクトをダウンロードすることができます。オブジェクトのダウンロードについては次の機能をサポートしています。

- 完全な単一のオブジェクトのダウンロード：GETリクエストを直接送信すると、完全なオブジェクトデータをダウンロードできます。
- 単一のオブジェクトの内容の一部をダウンロード：GETリクエストにRangeリクエストヘッダーを含めることで、ある特定の文字範囲を検索することができます。複数の範囲を検索することはできません。

オブジェクトのメタデータはHTTPレスポンスヘッダーとして、オブジェクトの内容と共に返されます。GETリクエストはURLパラメータを使用する方法で、応答の一部のメタデータ値を上書きします。
Content-Dispositionの応答値を例にとります。変更可能なレスポンスヘッダーには次のものがあります。
- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## 利用方法

### COSコンソールの使用

COSコンソールを使用してオブジェクトをダウンロードすることができます。詳細については、[オブジェクトのダウンロード](https://intl.cloud.tencent.com/document/product/436/13322)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用してオブジェクトのダウンロードリクエストを送信できます。 詳細については、[GET Object](https://intl.cloud.tencent.com/document/product/436/7753)のAPIドキュメントをご参照ください。

### SDKの使用

SDKのオブジェクトダウンロードメソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37675)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44873)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/44065)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37684)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/44016)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/43862)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/43872)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/45499)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/46469)
- [ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/436/43882)

