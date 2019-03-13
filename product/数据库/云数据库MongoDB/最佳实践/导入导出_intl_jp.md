>!local データベースには主にレプリカセットの構成情報、oplogなどのメタデータが格納されます。adminデータベースには主にユーザー、ロールなどの情報が格納されます。データの混乱、認証失敗などの現象発生を防止するよう、TencentDB for MongoDBではlocalとadminデータベースをインスタンスにインポートすることが禁止されます。

CVMでMongoDBから提供されたshellクライアントを用いてTencentDB for MongoDBに接続してデータのインポートとエクスポートを行います。最新バージョンのMongoDBクライアントスイートが使用されていることに注意してください。具体的な操作について[操作ガイド > 接続例](https://cloud.tencent.com/document/product/240/3563)を参照してください。

## インポートコマンド
#### mongodumpおよびmongorestore

公式MongoDBが2セットのデータインポート・エクスポートツールを提供します。データベース全体のインポート・エクスポートを行うとき、通常[mongodump](https://docs.mongodb.com/manual/reference/program/mongodump/)と[mongorestore](https://docs.mongodb.com/manual/reference/program/mongorestore/)を使用します。この組み合わせて実行するデータがBSON形式であり、大量のdumpとrestoreを実行するときに効率が高い。

mongodumpのインポートコマンドは次の通りです。
```
mongodump --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb -o /data/dump_testdb
```

![mongodumpサンプルのスクリーンショット例](https://mc.qcloudimg.com/static/img/4071cfd5d9b54c720349f41fc2e07b0c/dump_default.png)
mongorestoreのインポートコマンドは次の通りです。
```
mongorestore --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --dir=/data/dump_testdb
```

![mongorestoreサンプルのスクリーンショット例](https://mc.qcloudimg.com/static/img/335dbef8f11a5417e42740472df1a5b8/restore_default.png)

## エクスポートコマンド
#### mongoexportおよびmongoimport

単一のコレクションのエクスポート・インポートを行うとき、通常[mongoexport](https://docs.mongodb.com/manual/reference/program/mongoexport/)と[mongoimport](https://docs.mongodb.com/manual/reference/program/mongoimport/)を使用します。この組み合わせて実行するデータがJSON形式であり、読み取り可能性が高い。

mongoexportのエクスポートコマンドは次の通りです。

```
mongoexport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection -o /data/export_testdb_testcollection.json
```

また、-fパラメーターを使用して必須フィールドを指定することもできます。-qパラメーターは、エクスポートするデータを制限するための照合条件を指定します。

mongoimportのエクスポートコマンドは次の通りです。

```
mongoimport --host 10.66.187.127:27017 -u mongouser -p thepasswordA1 --authenticationDatabase=admin --db=testdb --collection=testcollection2 --file=/data/export_testdb_testcollection.json
```

## 複数の認証方法のパラメータ説明

[接続例](https://cloud.tencent.com/doc/product/240/3563)に記載されるように、TencentDB for MongoDBがデフォルトで「rwuser」と「mongouser」の2つのユーザー名を提供し、それぞれ「MONGODB-CR」と「SCRAM-SHA-1」の2つの認証方式をサポートしています。
- 「mongouser」とコンソールで作成されたすべての新規ユーザーについては、エクスポート・インポートコマンドツールを使用するときに上記の例に従ってください。
- 「rwuser」の場合は、各コマンドにパラメーター--authenticationMechanism=MONGODB-CRを追加する必要があります。

mongodumpの例：
```
mongodump --host 10.66.187.127:27017 -u rwuser -p thepasswordA1 --authenticationDatabase=admin --authenticationMechanism=MONGODB-CR --db=testdb -o /data/dump_testdb
```




