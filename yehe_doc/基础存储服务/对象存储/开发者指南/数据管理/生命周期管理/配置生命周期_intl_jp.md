## ユースケース

ライフサイクルルール設定を利用すると、ルールに該当するオブジェクトに対し、指定された条件下でいくつかの操作を自動的に実行することができます。例えば次のようなものがあります。

- ストレージタイプの切り替え：作成したオブジェクトを、指定の時間が経過した後に低頻度ストレージ（STANDARD_IA）、INTELLIGENT_TIERINGストレージ（INTELLIGENT_TIERING）、アーカイブストレージタイプ（ARCHIVE）、ディープアーカイブストレージタイプ（DEEP_ARCHIVE）に切り替えます。
- 期限切れの削除：オブジェクトの有効期限を設定し、オブジェクトが期限切れとなった後に自動的に削除します。

詳細については、[ライフサイクルの概要](https://intl.cloud.tencent.com/document/product/436/17028)のドキュメントおよび[ライフサイクル設定の要素](https://intl.cloud.tencent.com/document/product/436/17029)のドキュメントをご参照ください。

## 利用方法

### COSコンソールの使用

COSコンソールを使用してライフサイクルを設定することができます。詳細については、[ライフサイクルの設定](https://intl.cloud.tencent.com/document/product/436/14605)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用して、バケット内のオブジェクトのライフサイクルの設定と管理を行うことができます。詳細については次のAPIドキュメントをご参照ください。

- [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280)
- [GET Buket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278)
- [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284)

### SDKの使用

SDKのライフサイクルメソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36197)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/12301)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35269)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/39152)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37855)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35806)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35860)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/35002)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/35851)
