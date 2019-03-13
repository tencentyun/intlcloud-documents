### MongoDBデータベースからデータをエクスポートする場合、パラメーターを設定する方法は？
mongodumpのパラメーター中に--readPreference=secondaryPreferredを設定します。

### MongoDBはどんなデータ移行をサポートしますか？
現在、クラウドデータベースCVMの自作インスタンスの移行と外部ネットワークのインスタンスの移行の2種類の移行がサポートされています。詳細については、[MongoDBデータ移行](https://cloud.tencent.com/document/product/240/8271)を参照してください。

### mongodump（ライブラリ全体）またはmongoexport（単一コレクション）を使用して、MongoDBデータをローカルにエクスポートする方法は？

CVMでは、MongoDBが提供する[shellクライアント](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)を使用してデータエクスポートのためにTencentDB for MongoDBに接続できます。**最新バージョンのMongoDBクライアントスイートが使用されていることに注意してください**。
MongoDB公式は2セットのデータエクスポートツールを提供します。一般的には、mongodumpはライブラリ全体のエクスポートに使用され、操作のデータはBSONフォーマットであり、大量のdumpを実行するのが効率的です。単一のコレクションをエクスポートする場合はmongoexportが使用され、操作のデータはJSONフォーマットであり、読みやすくなっています。

**1. ライブラリ全体のエクスポートバックアップにmongodumpを使用すること**
 エクスポートコマンドは次のとおりです。

```
 mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![イメージの説明](//bot1024-1253841380.file.myqcloud.com/598299decb2a1.png)

**2. 単一コレクションのエクスポートバックアップにmongoexportを使用すること**
エクスポートコマンドは次のとおりです。

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection  -o /data/export_testdb_testcollection.json
```

> ? -fパラメーターを使用して必須フィールドを指定することもできます。-qパラメーターは、エクスポートするデータを制限するための照合条件を指定します。

**3. エクスポートコマンドを書くときのrwuserとmongouserのユーザー名のパラメーター説明** 
[接続例](https://cloud.tencent.com/document/product/240/3563)ドキュメントに記載されているように、TencentDB for MongoDBはデフォルトで2つのユーザー名rwuserとmongouserを提供し、それぞれMONGODB-CRとSCRAM-SHA-1の2つの認証方法をサポートします。

- mongouserとコンソールで作成されたすべての新規ユーザーについては、エクスポートコマンドツールを使用するときに上記の例に従ってください。
- rwuserの場合は、各コマンドにパラメーター--authenticationMechanism=MONGODB-CRを追加する必要があります。

mongodumpの例の説明：

```
 mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### mongorestore（ライブラリ全体）またはmongoimport（単一コレクション）を使用して、ローカルからMongoDBにデータをインポートする方法は？

CVMでは、MongoDBが提供する[shellクライアント](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/)を使用してデータインポートのためにTencentDB for MongoDBに接続できます。**最新バージョンのMongoDBクライアントスイートが使用されていることに注意してください**。
MongoDB公式は2セットのデータインポートツールを提供します。一般的には、mongorestoreはライブラリ全体のインポートに使用され、操作のデータはBSONフォーマットであり、大量のmongorestoreを実行するのが効率的です。単一のコレクションをインポートする場合はmongoimportが使用され、操作のデータはJSONフォーマットであり、読みやすくなっています。    
**1. ライブラリ全体のインポートバックアップにmongorestoreを使用すること**
インポートコマンドは次のとおりです。

```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![イメージの説明](//bot1024-1253841380.file.myqcloud.com/5982b30189287.png)
**2. 単一コレクションのインポートバックアップにmongoimportを使用すること**
インポートコマンドは次のとおりです。

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2  --file=/data/export_testdb_testcollection.json
```

**3. インポートコマンドを書くときのrwuserとmongouserのユーザー名のパラメーター説明**
[接続例](https://cloud.tencent.com/document/product/240/3563)ドキュメントに記載されているように、TencentDB for MongoDBはデフォルトで2つのユーザー名rwuserとmongouserを提供し、それぞれMONGODB-CRとSCRAM-SHA-1の2つの認証方法をサポートします。

- mongouserとコンソールで作成されたすべての新規ユーザーについては、インポートコマンドツールを使用するときに上記の例に従ってください。
- rwuserの場合は、各コマンドにパラメーター--authenticationMechanism=MONGODB-CRを追加する必要があります。

mongorestoreの例：

```
 mongorestore --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```

### データがMongoDBインスタンスにインポートされた後、データが自作MongoDBより少ないスペースを占めるのはなぜですか？

次のいくつかの原因があるかもしれません。

- 元のデータベースは長時間実行されて、多数の追加、削除、および変更操作が累積されました。
- 書き込み時に、パフォーマンス上の理由から、MongoDBはスペース割り当て時に実際のデータよりも多くのスペースを割り当てます。
- データが削除された後、元のスペースは再利用されませんでした。
  その結果、データベース空間全体の空隙率が高くなり、データのインポートはディスク整理のような操作と同等になるため、インポートされたデータは比較的コンパクトになり、データは小さくなったように見えます。

### MongoDBのmongodumpはデータをエクスポートできない場合は、どうやって対処するのですか？
mongodumpの使用については、[インポートとエクスポート](https://cloud.tencent.com/document/product/240/5321)を参照してください。mongodumpツールはバージョン3.2.10以上を使用することを推奨します。

