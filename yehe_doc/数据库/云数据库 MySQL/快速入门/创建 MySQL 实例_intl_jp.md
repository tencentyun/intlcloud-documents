
このドキュメントでは、コンソールでTencentDB for MySQLインスタンスを作成する方法について説明します。

## 前提条件
Tencent Cloudアカウントを登録し、実名認証を完了する必要があります。
- Tencent Cloudアカウントを登録するには：
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">ここをクリックしてください</a></div>
- 実名認証を行うには：
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">ここをクリックしてください</a></div>

## 操作手順
1. [MySQL購入ページ](https://buy.cloud.tencent.com/cdb)にログインし、実際のニーズに応じて各設定情報を選択し、誤りがないことを確認した後、**今すぐ購入**をクリックします。
 - **課金モード**：従量課金がサポートされています。
    - トラフィック量が瞬間的に大きく変動するケースの場合は、従量課金を選択することをお勧めします。
 - **リージョン**：TencentDB for MySQLインスタンスがデプロイするリージョンを選択します。CVMインスタンスと同じリージョンを選択することをお勧めします。異なるリージョンのクラウド製品はプライベートネットワークを介して互いに通信できません。購入後にリージョンを変更することはできません。
 -**データベースバージョン**：TencentDB for MySQLは現在、MySQL 8.0、MySQL 5.7、MySQL 5.6、MySQL 5.5をサポートしています。各バージョンに関する特性については、[公式ドキュメント](https://dev.mysql.com/doc/refman/5.7/en/)をご参照ください。
  - **アーキテクチャ**：2ノード、3ノードおよびシングルノードを提供します。各アーキテクチャの概要については、[データベースアーキテクチャ](https://intl.cloud.tencent.com/document/product/236/38328)をご参照ください。
  - **データレプリケーション方法**：非同期レプリケーション、半同期レプリケーション、強制同期レプリケーションという3種類の方法を提供します。[データベースインスタンスのレプリケーション](https://intl.cloud.tencent.com/document/product/236/7913)をご参照ください。
 - **プライマリAZとセカンダリAZ**：異なるプライマリAZとセカンダリAZ（すなわち、[マルチAZ配置](https://intl.cloud.tencent.com/document/product/236/8459)）を選択して、データベースを障害やAZの中断から保護できます。
>?
>- ホストと待機マシンが異なるアベイラビリティーゾーンにある場合、ネットワークの同期遅延が2ms～3ms増加する可能性があります。
>- クラウドサービスを購入する際には、お客様に最も近いリージョンを選択することをお勧めします。アクセスの遅延を減らし、ダウンロードスピードを向上させることができます。
>
 - **インスタンスタイプ**：汎用型と専用型という2つのインスタンスタイプが提供されています。詳細については、[インスタンスタイプ](https://intl.cloud.tencent.com/document/product/236/39794)をご参照ください。
 - **インスタンス仕様**：ビジネスニーズに応じて対応する仕様を選択してください。
 - **ハードディスク**：ハードディスク容量はMySQL実行時の必須ファイルを保存するのに使用されます。
 - **ネットワーク**：TencentDB for MySQLがあるネットワークです。CVMと同じリージョンにある同じVirtual Private Cloudを選択することをお勧めします。そうしない場合、プライベートネットワークを介してCVMとデータベースを接続し、デフォルト設定をDefault-VPC（デフォルト）にすることができません。
 - **セキュリティグループ**：セキュリティグループの新規作成と管理については、[TencentDBセキュリティグループ](https://intl.cloud.tencent.com/document/product/236/14470)をご参照ください。
>? セキュリティグループのインバウンドルールはMySQLインスタンスの3306ポートを開放する必要があります。MySQLインスタンスのプライベートネットワークのデフォルトポートは3306で、カスタムポートもサポートされています。デフォルトのポート番号が変更された場合は、セキュリティグループ内で新しいポートを開放する必要があります。
 - **パラメータテンプレート**：TencentDBが提供するシステムパラメータテンプレートに加えて、カスタムパラメータテンプレートも作成できます。詳細については、 [パラメータテンプレートの使用](https://intl.cloud.tencent.com/document/product/236/31906)をご参照ください。
 - **アラームポリシー**：Tencent Cloudリソースの状態が変化したときに通知を受け取るようにアラームポリシーを設定することもできます。詳細については、 [アラームポリシー](https://intl.cloud.tencent.com/document/product/236/8457)をご参照ください。
 - **プロジェクトの指定**：TencentDBインスタンスが属するプロジェクトを選択します。デフォルトではデフォルトのプロジェクトが使用されます。
 - **タグ**：インスタンスリソースのカテゴリー管理に便利です。[タグの概要](https://intl.cloud.tencent.com/document/product/236/31917)をご参照ください。
 - **インスタンス名**：作成後に名前を付けるか、今すぐ名前を付けるかを選択できます。
 - **購入数量**：各AZで最大10個の従量課金インスタンスを購入できます。
 - **利用規約**：[CDB利用規約](https://intl.cloud.tencent.com/document/product/236/35543)。
2. 支払いが完了すると、インスタンスリストが返され、インスタンスに**出荷中**と表示されます（おおよそ3～5分かかります。少々お待ちください）。インスタンスステータスが**未初期化**に変更されると、初期化操作を実行できます。

## 後続の操作
インスタンスを購入した後、インスタンスを手軽に有効にするには、MySQLインスタンスを初期化する必要があります。詳細については、[MySQLインスタンスの初期化](https://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。

