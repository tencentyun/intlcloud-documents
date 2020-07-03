## 前提条件
購入する前に実名認証を行う必要があり、 [実名認証の手順](https://intl.cloud.tencent.com/document/product/378/3629)をご参照ください。

## 公式サイトでの購入
1. [MySQL コンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストで【新規作成】をクリックすると、購入ページが入ります。
 ![](https://main.qcloudimg.com/raw/8440c63d34e0cdbfec26348ee37f1f17.png)
2. 実際のニーズに合わせて、【購入】ページで各コンフィグレーション情報を設定し、間違いがないことを確認したら、【今すぐ購入】をクリックします。
 - **課金モード**：従量課金。
 - **地域**：ユーザーサービスに MySQL を配置する必要な地域を選んでください。クラウド製品のプライベートネットワークは地域によって互いにアクセスできず、購入後に交換することができません。
 -**Master Availability ZoneとSlave Availability Zone**：選択したMaster Availability ZoneとSlave Availability Zoneが異なる場合（すなわち、[Multi Availability Zoneの配置](https://intl.cloud.tencent.com/document/product/236/8459)）、データベースを障害やAvailability Zoneの中断から保護します。
 >マスター・スレーブ機が異なるAvailability Zoneにある場合は、2ms～3msの同期ネットワーク遅延が増加する可能性があります。
 - **ネットワーク**：MySQLが属するネットワーク。デフォルト設定は「Default-VPC」（デフオルト）です。
 - **セキュリティグループ**：セキュリティグループの新規作成と管理については、[MySQLセキュリティグループ](https://intl.cloud.tencent.com/document/product/236/14470)をご参照ください。
 >セキュリティグループのインバウンドルールは MySQL インスタンスの3306ポートをインターネットにオープンする必要があります。MySQLのプライベートネットワークのデフォルトポートは3306で、カスタムポートもサポートされています。デフォルトのポート番号が変更された場合は、セキュリティグループ内でMySQLの新しいポート情報をオープンする必要があります。
 - **アーキテクチャ**：基本版、高可用版及び金融版が用意されています。各バージョンの説明については、[データベーススキーマ](https://intl.cloud.tencent.com/document/product/236/17136)をご参照ください。
 - **指定項目**：データベースインスタンス所属のプロジェクトを選択します。デフォルト設定はデフォルトのプロジェクトです。
 - **購入数量**：ユーザーが各Availability Zoneで購入できる従量課金インスタンスの合計数量は10個です。
 
## API購入
APIを使用してMySQLを購入するユーザーについては、[インスタンスの新規作成](https://intl.cloud.tencent.com/document/product/236/15865)をご参照ください。


## 次の手順
- [MySQLデータベースの初期化](https://intl.cloud.tencent.com/document/product/236/3128)
- [MySQLデータベースへのアクセス](https://intl.cloud.tencent.com/document/product/236/3130)

