## 機能の説明
TXSQLでは、MySQLの透過的暗号化システムを踏襲し、KEYRINGプラグインのもう一つの実装であるKEYRING_KMSを提供しています。これはKEYRINGにTencent Cloudのエンタープライズレベルの[Key Management Service(KMS)](https://intl.cloud.tencent.com/zh/document/product/1030)を統合したものです。

KMSはTencent Cloudのデータおよびキーのセキュリティを保護するキーサービスであり、サービスにかかわる各フローではいずれも安全性の高いプロトコル通信を用いることで、サービスの高度なセキュリティを保証します。また分散型クラスター管理およびホットバックアップを提供し、サービスの高い信頼性と高可用性を保証します。

KMSには二重キーシステムを採用し、カスタマーマスターキー（CMK）とデータキー（Datakey）という2種類のキーがこれに関与します。カスタマーマスターキーはデータキーの暗号化またはパスワード、証明書、設定ファイル等のスモールパケットデータ（最大4KB）に用いられます。データキーは業務データの暗号化に用いられます。大量の業務データはストレージまたは通信の過程で、データキーを使用して対称暗号化方式で暗号化され、データキーはさらにカスタマーマスターキーによって非対称暗号化方式で暗号化されて保護されます。二重キーシステムにより、データをメモリとファイル内の両方で確実に暗号化することができます。

## サポートするバージョン
- カーネルバージョン MySQL 5.7 20171130およびそれ以降
- カーネルバージョン MySQL 8.0 20200630およびそれ以降

## ユースケース
透過的データ暗号化とは、データの暗号化/復号操作をユーザーに対して透明にすることを指し、データファイルに対するリアルタイムな I/Oの暗号化と復号をサポートしています。データをディスクに書き込む前に暗号化して、ディスクから内部記憶装置に読み込む時に復号しますので、静的データの暗号化におけるコンプライアンス要件を満たすことができます。

## 利用説明
透過的データ暗号化機能を有効にするには、[透過的データ暗号化](https://intl.cloud.tencent.com/document/product/236/38491)をご参照ください。
