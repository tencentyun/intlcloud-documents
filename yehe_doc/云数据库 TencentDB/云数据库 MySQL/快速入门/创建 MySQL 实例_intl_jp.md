
このドキュメントでは、コンソールでTencentDB for MySQLインスタンスを作成する方法について説明します。

## 前提条件
Tencent Cloudアカウントを登録し、実名認証を完了させたことです。
- Tencent Cloudアカウントを登録するには：
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">ここをクリックしてTencent Cloudアカウントを登録します</a></div>
- 実名認証を行うには：
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">ここをクリックして実名認証を行います</a></div>

### 操作手順
1. [MySQL購入ページ](https://buy.cloud.tencent.com/cdb)にログインし、実際のニーズに応じて各設定情報を選択し、間違いがないことを確認したら、【今すぐ購入】をクリックします。
 - **課金モード**：従量課金がサポートされています。
    - トラフィック量が瞬間的に大きく変動するケースの場合は、従量課金を選択することをお勧めします。
 - **リージョン**：TencentDB for MySQLインスタンスがデプロイするリージョンを選択します。CVMインスタンスと同じリージョンを選択することをお勧めします。異なるリージョンのクラウド製品はプライベートネットワークを介して互いに通信できません。購入後にリージョンを変更することはできません。
 - **プライマリAZとセカンダリAZ**：異なるプライマリAZとセカンダリAZ（すなわち、[マルチAZ配置](https://intl.cloud.tencent.com/document/product/236/8459)）を選択して、データベースを障害やAZの中断から保護できます。
 >?ソースインスタンスとレプリカインスタンスが異なるAZにある場合、2ms～3msのネットワーク同期遅延が発生する可能性があります。
 - **ネットワーク**：TencentDB for MySQLインスタンスが存在するネットワークを選択します。CVMインスタンスと同じリージョンにある同じVPCを選択することをお勧めします。そうしないと、MySQLインスタンスはプライベートネットワークを介してCVMとデータベースに接続することはできません。デフォルトは「Default-VPC（デフォルト）」に設定されています。
 - **セキュリティグループ**：セキュリティグループの新規作成と管理については、[TencentDBセキュリティグループ](https://intl.cloud.tencent.com/document/product/236/14470)をご参照ください。
 >?セキュリティグループのインバウンドルールはMySQLインスタンスの3306ポートを開放する必要があります。MySQLインスタンスのプライベートネットワークのデフォルトポートは3306で、カスタムポートもサポートされています。デフォルトのポート番号が変更された場合は、セキュリティグループ内で新しいポートを開放する必要があります。
 - **アーキテクチャ**：高可用性エディション、ファイナンスエディションおよびBasic エディションが提供されています。各アーキテクチャの詳細については[データベースアーキテクチャ](https://intl.cloud.tencent.com/document/product/236/17136)をご参照ください。
 - **プロジェクトの指定**：TencentDBインスタンスが属するプロジェクトを選択します。デフォルトではデフォルトのプロジェクトが使用されます。
 - **購入数量**：各AZで最大10個の従量課金インスタンスを購入できます。
2. 支払いが完了し、インスタンスリストに戻ると、インスタンスに「出荷中」と表示されます（約3min～5minかかりますので、しばらくお待ちください）。インスタンスのステータスが「未初期化」になると、初期化操作を行うことができます。


## 後続の操作
コンソールでMySQLインスタンスを初期化する方法の詳細については、[MySQLインスタンスの初期化](https://intl.cloud.tencent.com/document/product/236/3128)をご参照ください。

