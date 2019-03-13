## 関連説明
TencentDB for MongoDBはデフォルトで「rwuser」と「mongouser」の2つのユーザー名を提供し、それぞれ「MONGODB-CR」と「SCRAM-SHA-1」の2つの認証方法をサポートしています。この2つの認証方法について、URI接続は異なる方法で処理する必要があります。詳細は[接続例](https://cloud.tencent.com/doc/product/240/3563)のドキュメントを参照してください。

Node.js MongoDBドライバーのドキュメント：
https://docs.mongodb.org/ecosystem/drivers/node-js/

## クイックスタート
### Node.jsネイティブサンプルコード
Shellによるドライバーパッケージのインストール：
```
npm install mongodb --save
( インストールが成功しなかった場合は、ソースを交換してみてください。npm config set registry http://registry.cnpmjs.org )
npm init
```
プログラムコード：
```
'use strict';

var mongoClient = require('mongodb').MongoClient,
    assert = require('assert');

// URIのつなぎ合わせ
var url = 'mongodb://mongouser:thepasswordA1@10.66.161.177:27017/admin';

mongoClient.connect(url, function(err, db) {
	assert.equal(null, err);
	var db = db.db('testdb'); // dbを選択してください
	var col = db.collection('demoCol'); // コレクション（テーブル）を選択してください
   // データを挿入します
    col.insertOne(
        {
            a: 1,
            something: "yy"
        },
        //選択可能なパラメーター
        //{
        //    w: 'majority' // 「Most」モードをオンにして、データが確実にSecondaryノードに書き込まれるようにします
        //},
        function(err, r) {
            console.info("err:", err);
            assert.equal(null, err);
            // アサーション書き込みが成功しました
            assert.equal(1, r.insertedCount);
            // データ照合
            col.find().toArray(function(err, docs) {
                assert.equal(null, err);
                console.info("docs:", docs);
                db.close();
            });
        }
    );
});
```

出力：

```
[root@VM_2_167_centos node]# node index.js
docs: [ { _id: 567a1bf26773935b3ff0b42a, a: 1, something: 'yy' } ]
```

## Node.js mongoose 接続例

```
var dbUri = "mongodb://" + user + ":" + password + "@" + host + ":" + port + "/" + dbName;
var opts = {
    auth: {
        authMechanism: 'MONGODB-CR', // SCRAM-SHA-1認証が使用されている場合、このパラメーターは不要です
        authSource: 'admin'
    }
};
var connection = mongoose.createConnection(dbUri, opts);
```

