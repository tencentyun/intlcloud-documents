## ユースケース

バケットコピールールを設定することで、ユーザーはオブジェクトデータをソースバケットから別の指定するターゲットバケットにコピーすることができます。バケットコピー機能は、リモートディザスタリカバリ、業界のコンプライアンス要件への適合、データマイグレーションおよびバックアップ、顧客アクセス遅延の低減、異なるリージョン間のクラスターのデータアクセス利便性向上などのケースに適しています。

>!バージョン管理機能を有効にしている場合、新たにアップロードするオブジェクトには複数のバージョンが生成され、ストレージスペースを占有します。このためこれらのバージョンのオブジェクトも同様にストレージ料金の課金対象となります。

## 利用方法

### COSコンソールの使用

COSコンソールでバケットコピールールを設定することができます。[バケットコピーの設定](https://intl.cloud.tencent.com/document/product/436/19235)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用して、バケットのバケットコピールールの設定と管理を行うことができます。具体的には次のAPIドキュメントをご参照ください。

- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### SDKの使用

SDKのバケットコピーメソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36196)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35272)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37696)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31535)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)