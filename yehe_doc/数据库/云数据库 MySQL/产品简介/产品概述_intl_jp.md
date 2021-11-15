## 概要
クラウドデータベースMySQL (TencentDB for MySQL)はTencent CloudがオープンソースデータベースMySQLに基づいて専門的に構築した高性能分散式データストレージサービスです。ユーザーはクラウドでより手軽に関連データベースの設定、操作、拡張ができるようになります。
クラウドデータベースMySQLの主な特徴は次のとおりです：
- クラウドストレージサービスは、Tencent Cloudプラットフォームが提供するインターネットアプリケーション向けのデータストレージサービスです。
- MySQLプロトコルとの完全な互換性は、テーブル構造向けのユースケースに対応します。MySQLのリージョンであればどこでもクラウドデータベースを使用できます。
- 高性能、高い信頼性、アクセシビリティを備えた便利なMySQLクラスタサービスを提供し、データの信頼性は99.9996%にまで達します。
- バックアップ、拡張、マイグレーションなどの機能を統合するとともに、次世代のデータベースツールDMCを提供し、ユーザーはデータベース管理を容易に行えます。


## 関連コンセプト
[インスタンス](https://intl.cloud.tencent.com/document/product/236/17136)：Tencent Cloud上のMySQLデータベースリソース。

[インスタンスタイプ](https://intl.cloud.tencent.com/document/product/236/7268)：MySQLインスタンスではノード数、読み込み/書き込み機能、リージョンのデプロイは異なった設定になっています。

[読み取り専用インスタンス](https://intl.cloud.tencent.com/document/product/236/7270)：読み込み機能のみを有するMySQLインスタンス。

[ROグループ](https://intl.cloud.tencent.com/document/product/236/11361)：1つまたは複数の読み取り専用インスタンスを管理するロジックツールです。ユーザー管理に提供します。読み込み/書き込み分離のユースケースにおいてCLBを満たし、ユーザーデータベースの読み出し負荷容量を大きく高めます。

[災害復旧インスタンス](https://intl.cloud.tencent.com/document/product/236/7272)：クロスアベイラビリティーゾーン、クロスリージョンの災害復旧をサポートするMySQLインスタンス。

[Virtual Private Cloud（VPC）](https://intl.cloud.tencent.com/document/product/215/535)：カスタム仮想ネットワーク空間はその他のリソースと論理的に隔絶されます。

[セキュリティグループ](https://intl.cloud.tencent.com/document/product/236/14470)：MySQLインスタンスに対しセキュリティのためのアクセス制御を行います。インスタンスに入るIP、プロトコル、ポートルールを指定します。

[リージョンおよびアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/236/8458)：MySQLインスタンスおよびその他リソースの物理的位置。

[Tencent Cloudコンソール](https://console.cloud.tencent.com/cdb)：Webベースのユーザー画面。

## 関連サービス
課金関連ツールを利用して実際の出費を詳細かつ正確に計算します。 [費用総覧](https://intl.cloud.tencent.com/document/product/236/18335) および [価格計算機](https://buy.cloud.tencent.com/calculator/cdb)をご参照ください。

クラウドデータベースMySQLインスタンスの購入によってクラウド上のデータサービスを構築します。 [購入フロー](https://intl.cloud.tencent.com/document/product/236/5160) および  [クイックスタート](https://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。

クラウドデータベースのMySQLインスタンスのマイグレーションツールを使用して、クラウド間のデータ移行を行います。[データマイグレーション](https://intl.cloud.tencent.com/document/product/571/13706)をご参照ください。

クラウドデータベースMySQLのデータサブスクリプションツールを利用して、データバイパスのクレンジングと分析を行います。 [データサブスクリプション](https://intl.cloud.tencent.com/document/product/571/8774)をご参照ください。

CVMの購入により、コンピューティングサービスをデプロイします。 [CVM](https://intl.cloud.tencent.com/document/product/213)をご参照ください。

クラウド監視サービスを使用してクラウドデータベースMySQLインスタンスの運行状況を監視します。 [クラウド監視製品ドキュメント](https://intl.cloud.tencent.com/document/product/248)をご参照ください。

Tencent Cloud APIをコールし、Tencent Cloud製品とサービスにアクセスするコードを記述します。 [Tencent Cloud APIドキュメント](https://intl.cloud.tencent.com/document/api)をご参照ください。
