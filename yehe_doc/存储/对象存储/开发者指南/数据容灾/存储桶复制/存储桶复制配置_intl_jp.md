## 適用ケース

バケットコピールールを設定することで、ユーザーはオブジェクトデータをソースバケットから別の指定するターゲットバケットにコピーすることができます。バケットコピー機能は、リモート障害復旧、業界のコンプライアンス要件への適合、データマイグレーションおよびバックアップ、顧客アクセス遅延の低減、異なるリージョン間のクラスターのデータアクセス利便性向上などのケースに適しています。

特殊なケース：
- マルチリージョンバックアップ：ソースバケットに複数のレプリケーションルールを設定し、オブジェクトを異なるリージョンのバケットにコピーすることで、マルチリージョナルなバックアップと障害復旧を実現できます。
- 双方向レプリケーション：ソースバケットとターゲットバケットでそれぞれレプリケーションルールを作成することにより、2つのバケット間での双方向レプリケーションを実現し、バケットデータの同期を実現することができます。

>!バージョン管理機能を有効にしている場合、新たにアップロードするオブジェクトには複数のバージョンが生成され、ストレージスペースを占有します。このためこれらのバージョンのオブジェクトも同様にストレージ料金の課金対象となります。

## 使用方法

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
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/12301)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/43245)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/30601)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37696)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
