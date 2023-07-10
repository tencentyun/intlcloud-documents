## ユースケース
バージョン管理機能を利用すると、バケット内にオブジェクトの複数のバージョンを保存することができ、指定のバージョンのオブジェクトを検索、削除、復元することが可能になります。
バージョン管理についてより詳しい情報をお知りになりたい場合は、[バージョン管理の概要](https://intl.cloud.tencent.com/document/product/436/19883)のドキュメントをご参照ください。

>!バケットのバージョン管理状態を設定できるのはルートアカウントと権限を付与されたサブアカウントのみです。

## 使用方法

### COSコンソールの使用
COSコンソールを使用してバージョン管理機能を有効化することができます。詳細については、[バージョン管理の設定](https://cloud.tencent.com/document/product/436/19881)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用して、バケットのバージョン管理の設定およびバージョン管理状態にあるバケット内のオブジェクトの管理を行うことができます。次のAPIドキュメントのパートをご参照ください。
- [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889)
- [GET Buket versioning](https://intl.cloud.tencent.com/document/product/436/19888)
- [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
- [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### SDKの使用

SDKのバージョン管理メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36195#versioning)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#versioning)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523#versioning)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35271#versioning)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527#versioning)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31531#versioning)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31535#versioning)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35804#versioning)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35858)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34997#versioning)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547#versioning)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/35849)
