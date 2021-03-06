TencentDB for MySQLでは、単一ノード、2ノード、3ノードの3種類のアーキテクチャをサポートしています。ここでは主に2ノードのアーキテクチャについてご紹介いたします。

- 2ノードでは1マスター1スレーブの高可用性モード、リアルタイムなホットバックアップを採用し、マシンクラッシュの自動検出と障害時の自動的な移行を提供しています。
- 2ノードアーキテクチャは、隔離ポリシーの違いに基づき、汎用型、専用型に分類できます。[隔離ポリシー](https://intl.cloud.tencent.com/document/product/236/39794)をご参照ください。

## 適用ケース
ゲーム、インターネット、IoT、小売りEC、物流、保険、証券などの業界への適用を網羅しています。

## アーキテクチャの特徴
- マスター/スレーブレプリケーション方式には、非同期（デフォルト）、準同期の2種類があります。レプリケーション方式は、[コンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページで修正できます。またコンソールにて、[3ノードにアップグレード](https://intl.cloud.tencent.com/document/product/236/35986)することも可能です（1マスター2スレーブの強力な同期モード）。
- 読み取り専用インスタンス、セキュリティグループ、データ移行、マルチアベイラビリティーゾーンのデプロイなどの特性がすべて備わっています。具体的な特性は、[製品の優位性](https://intl.cloud.tencent.com/document/product/236/5148)をご参照ください。
- 2ノードインスタンスの可用性は99.95%に達しています。具体的なアグリーメントは、[サービスレベルアグリーメント](https://intl.cloud.tencent.com/document/product/301/30977)をご参照ください。
- 2ノードインスタンスでは、データストレージの永続性を保障するため、マルチレプリケーション方式を提供しています。マスターインスタンスに発生したデータが他のスレーブインスタンスに同期され、データセキュリティが効果的に保障されます。これによりデータストレージの永続性は99.99999%以上になっています。
- データノードは強力なハードウェアにデプロイし、基盤ストレージにはローカルのNVMe SSDを使用することで、強力なIO性能を提供し、IOPSは最高240000を達成可能です（実際のIOPS速度は設定、ページサイズ、業務負荷と関係します。この数値は MySQLのデフォルトの16KBページサイズで測定したものです。参考として提供します）。

アーキテクチャの基本フレームワーク
![Alt text](https://main.qcloudimg.com/raw/19d5619f983d3dc550b3218c0520b447.png)

## アップグレード関連操作
- TencentDB for MySQLは、データベースエンジンのアップグレードに対応しています。[データベースエンジンのバージョンアップ](https://intl.cloud.tencent.com/document/product/236/8126)をご参照ください。
- TencentDB for MySQLは、2ノードインスタンスから3ノードインスタンスへのアップグレードに対応しています。[2ノードから3ノードへのアップグレード](https://intl.cloud.tencent.com/document/product/236/35986)をご参照ください。
- TencentDB for MySQLは、自動または手動によるカーネルマイナーバージョンのアップグレードに対応しています。[カーネルマイナーバージョンのアップグレード](https://intl.cloud.tencent.com/document/product/236/36816)をご参照ください。
