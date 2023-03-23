特定の状況下でバケットを削除する必要がある場合、コンソール、ツール、APIまたはSDK方式によってバケットを削除することができます。

>! バケットは削除すると元に戻せませんので、慎重に操作してください。

## 制限事項

- 現時点ではデータが消去されているバケットの削除のみサポートしています。バケット内にオブジェクトまたはファイルフラグメントが残っている場合は削除に失敗します。バケットの削除を実行する前に、バケット内のオブジェクトが空になっていることをご確認ください。その方法についてお知りになりたい場合は、[バケットのクリア](https://intl.cloud.tencent.com/document/product/436/30926)にお進みください。
- バケットを削除する際は、操作を行うIDがこの操作の権限承認をすでに受けていることを確実にするとともに、正しいバケット名（Bucket）およびリージョン（Region）パラメータを渡していることを確認する必要があります。


## 利用方法

### COSコンソールの使用

COSコンソールを使用してバケットを削除することができます。詳細については、[バケットの削除](https://intl.cloud.tencent.com/document/product/436/30361)のコンソールガイドドキュメントをご参照ください。

### ツールの使用

COSBrowserツール、COSCMDツールなどを使用してバケットを削除することができます。詳細については、[ツールの概要](https://intl.cloud.tencent.com/document/product/436/6242)をご参照ください。

### REST APIの使用

REST APIを直接使用してバケット削除リクエストを送信できます。 詳細については、[DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732)のAPIドキュメントをご参照ください。

### SDKの使用

SDKのバケット削除メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31477)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/31472)

