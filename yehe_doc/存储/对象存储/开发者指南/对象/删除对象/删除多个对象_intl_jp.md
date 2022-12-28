## ユースケース

Tencent Cloud COSは複数のオブジェクトの一括削除をサポートしています。コンソール、API、SDKなどの複数の方式でオブジェクトの一括削除を行うことができます。

デフォルトでは、削除タスクがすべて正常に完了した時点で、通常は空の内容が返されます。エラーが発生した場合はエラーメッセージが返されます。

>!1回のリクエストで最大1000個のオブジェクトを削除することができます。それ以上のオブジェクトを削除したい場合は、リストを分割してからそれぞれリクエストを送信してください。

## 利用方法

### COSコンソールの使用

COSコンソールを使用して複数のオブジェクトの一括削除を行うことができます。詳細については、[オブジェクトの削除](https://intl.cloud.tencent.com/document/product/436/13323)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用して複数のオブジェクトの削除リクエストを送信できます。 詳細については、[DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)のAPIドキュメントをご参照ください。

### SDKの使用

SDKの複数オブジェクト削除メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38065)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43884)
