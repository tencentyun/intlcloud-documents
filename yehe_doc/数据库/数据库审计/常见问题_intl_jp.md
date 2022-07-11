
### 監査はどのように課金されますか？
データベース監査は、監査したログ保存量に応じた従量課金を採用します。1時間は1つの課金サイクルであり、1時間未満の場合、1時間として課金されます。詳しくは、[購入ガイド](https://intl.cloud.tencent.com/document/product/1102/41313)をご参照ください。

### 監査が有効になっている場合、どのように無効にしますか？
[MySQLコンソール](https://console.cloud.tencent.com/dls/mysql/policy)、[TDSQL-C for MySQLコンソール](https://console.cloud.tencent.com/dls/cynosdb/instance)、[MongoDBコンソール](https://console.cloud.tencent.com/dls/mongodb)にログインし、監査ログ画面で**サービス設定**をクリックして、**サービスを無効にする**を選択します。
>!サービスを無効にすると、このインスタンスに対応する監査ポリシー、ログ、ファイルはクリアされ、復元できませんので、事前に関連のログとファイルを保存してください。

### 監査データはどのくらいの期間保存できますか？
監査データの保存時間は7日から5年までです。[MySQLコンソール](https://console.cloud.tencent.com/dls/mysql/policy)、[TDSQL-C for MySQLコンソール](https://console.cloud.tencent.com/dls/cynosdb/instance)、[MongoDBコンソール](https://console.cloud.tencent.com/dls/mongodb)で監査サービスを有効にするとき、監査データの保存時間を設定できます。監査サービスが有効になっている場合、監査ログ画面で**サービス設定**をクリックして変更することができます。
