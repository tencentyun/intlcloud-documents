TencentDB for MySQLは新しいデータベースエージェントバージョンをリリースしました。新しいデータベースエージェントバージョンのすべての機能をサポートするため、Tencent Cloudデータベースチームは新しいインターフェースサービスを提供し、データベースエージェントの置き換え、アップデート、設定に使用されます。次のリストを参照して、新しいインターフェースサービスを置き換えアップデートすることができます。

## 変更日
2022年11月17日（木）より。

##　インターフェース置換リスト

| オフラインインタフェース | 置き換え用インターフェース | インターフェース機能 |
|---------|---------|---------|
| UpgradeCDBProxy | [AdjustCdbProxy](https://intl.cloud.tencent.com/document/product/236/45187) | データベースエージェントのアップデート設定 |
| ModifyCDBProxy | [AdjustCdbProxyAddress](https://intl.cloud.tencent.com/document/product/236/45194) | データベースエージェントの読み書き切り離しの設定 |
