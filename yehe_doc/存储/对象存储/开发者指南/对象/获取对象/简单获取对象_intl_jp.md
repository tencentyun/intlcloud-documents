## 適用ケース

リクエストを直接送信してCOS内のオブジェクトを取得することができます。オブジェクトの取得は次の機能をサポートしています。

- 完全な単一のオブジェクトの取得：GETリクエストを直接送信すると、完全なオブジェクトデータを取得できます。
- 単一のオブジェクトの内容の一部を取得：GETリクエストにRangeリクエストヘッダーを含めることで、ある特定の文字範囲を検索することができます。複数の範囲を検索することはできません。

オブジェクトのメタデータはHTTPレスポンスヘッダーとして、オブジェクトの内容と共に返されます。GETリクエストはURLパラメータを使用する方法で、応答の一部のメタデータ値を上書きします。
Content-Dispositonの応答値を例にとります。変更可能なレスポンスヘッダーには次のものがあります。
- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## 使用方法

### COSコンソールの使用

COSコンソールを使用してオブジェクトを取得することができます。詳細については、[オブジェクトのダウンロード](https://intl.cloud.tencent.com/document/product/436/13322)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用してオブジェクトの取得リクエストを送信できます。 詳細については、[GET Object](https://intl.cloud.tencent.com/document/product/436/7753)のAPIドキュメントをご参照ください。

### SDKの使用

SDKのオブジェクトダウンロードメソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37675#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37684#.E8.8E.B7.E5.8F.96.E5.AF.B9.E8.B1.A1)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
