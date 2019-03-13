
CVMでは、MongoDBが提供するshellクライアント（[インストールドキュメントの確認](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)）を使用してデータ管理のためにTencentDB for MongoDBサービスに接続できます。最新バージョンのMongoDBクライアントスイートが使用されていることに注意してください。

### クイックスタート
典型的な接続コマンドは次のとおりです。
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
図のように：
![典型的な接続コマンドのスクリーンショット例](https://mc.qcloudimg.com/static/img/ce6b26f8cd6b1cc2981bc0cd44f9d09d/shell_default.png)

### 複数の認証方法に対する接続の説明
[接続例](https://cloud.tencent.com/doc/product/240/3563)ドキュメントに記載されているように、Tencent CloudDB for MongoDBがデフォルトで「rwuser」と「mongouser」の2つのユーザー名を提供し、それぞれ「MONGODB-CR」と「SCRAM-SHA-1」の2つの認証方法をサポートしています。
この2つの認証方法については、shellコマンドのパラメーターが異なります。詳細は以下を参照してください。

### SCRAM-SHA-1認証（mongouser）
**デフォルトユーザー「mongouser」およびコンソールで作成されたすべての新規ユーザーはSCRAM-SHA-1認証を使用します**。shell接続パラメーターは、[クイックスタート](#.E5.BF.AB.E9.80.9F.E5.BC.80.E5.A7.8B)セクションとまったく同じです。追加のパラメーターは必要ありません。例は次のとおりです。
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
特に、MongoDBサービスに接続して「singer」などのdbに直接アクセスする場合は、次の例に従ってください。
```
mongo 10.66.187.127:27017/singer -u mongouser -p thepasswordA1 --authenticationDatabase admin
```
図のように：
![あるdbに直接アクセスする接続コマンドのスクリーンショット例](https://mc.qcloudimg.com/static/img/c30cc3e6e2db6c8bd3cce2e327ce63db/sha1_sonedb.png)

### MONGODB-CR認証（rwuser）
**デフォルトユーザー「rwuser」のみがMONGODB-CR認証を使用しており**、そのshell接続パラメーターは認証方法がMONGODB-CRであることを示す必要があることに注意してください。例をご覧ください。
```
mongo 10.66.187.127:27017/admin -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR
```
図のように：
![MONGODB-CR認証のスクリーンショット例](https://mc.qcloudimg.com/static/img/ff200b49c3fa5c70812027dd89e3ebc3/cr_default.png)
特に、MongoDBサービスに接続して「singer」などのdbに直接アクセスする場合は、次の例に従ってください。
```
mongo 10.66.187.127:27017/singer -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR --authenticationDatabase admin
```
図のように：
![あるdbに直接アクセスする接続コマンドのスクリーンショット例](https://mc.qcloudimg.com/static/img/d31bfa612a295fd070ea5dd09c7ce6a3/cr_somedb.png)

### shellでデータのインポートとエクスポートを実行します
上記の2つの認証方法は、shellでデータのインポートとエクスポートを実行できます。[こちらを参照してください](https://cloud.tencent.com/doc/product/240/5321)。

