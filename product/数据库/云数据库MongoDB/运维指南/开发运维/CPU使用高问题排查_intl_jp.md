ユーザーがMongoDBを使用するときにCPU利用率が高いと判明した場合、以下の方法により問題をトラブルシューティングできます。<br>
1. まずは業務のデータベース操作頻度が高いかどうかを判断します。
コンソール監視指標を確認します。下図に示すように、業務QPSが高いと判定した場合、インスタンス構成をアップグレードする必要があるかどうかを検討してください。業務QPSが高くない場合、スロークエリが存在するかについてトラブルシューティングする必要があります。
![](https://main.qcloudimg.com/raw/e013e4387e144b8f98ab1de810503c0d.png)


2. 現在のmongodにスローログが存在するかどうかを確認します。
[TencentDB for MongoDBコンソール](https://console.cloud.tencent.com/mongodb)にログインし、インスタンスのスローログを確認し、下図に示すように、抽象クエリを選択してください。
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
command、COLLSCAN、IXSCAN、keysExamined、docsExaminedなどのキーワードに注意してください。
 
 
 - commandはスローログに記録される操作を指し示します。<br>
 - COLLSCANはこのクエリによる全テーブルスキャン、IXSCANは索引スキャンを示します。その他のフィールドの記述については、[MongoDB公式サイト](https://docs.mongodb.com/manual/reference/explain-results/index.html)を参照してください。<br>
 - keysExaminedは索引スキャンエントリを示し、docsExaminedはドキュメントスキャンエントリを示します。keysExaminedとdocsExaminedが多いほど、索引が作成されていない可能性または索引の差別が小さい可能性が高くなります。索引の作成フィールドを確認してください。<br>
その他のログについては、[MongoDB公式サイト](https://docs.mongodb.com/manual/reference/log-messages/index.html)を参照してください。

