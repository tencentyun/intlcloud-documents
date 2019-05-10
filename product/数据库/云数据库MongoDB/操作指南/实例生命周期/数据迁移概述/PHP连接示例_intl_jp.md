### 関連説明
TencentDB for MongoDBはデフォルトで「rwuser」と「mongouser」の2つのユーザー名を提供し、それぞれ「MONGODB-CR」と「SCRAM-SHA-1」の2つの認証方法をサポートしています。この2つの認証方法について、URI接続は異なる方法で処理する必要があります。詳細は[接続例](https://cloud.tencent.com/doc/product/240/3563)のドキュメントを参照してください。

PHPには、MongoDBデータベースに接続するために使用できる[2セットのドライバー](https://docs.mongodb.com/ecosystem/drivers/php/)があります。それぞれは：
- mongodb ([PHP公式Webサイトのドキュメント](http://php.net/manual/en/set.mongodb.php))  - MongoDBは公式にmongodbドライバーを推奨しますが、PHP 5.4以上のバージョンが必要です。
- mongo ([PHP公式Webサイトのドキュメント](http://php.net/manual/en/book.mongo.php)) - Mongoは比較的古いですが、使用することもできますので、使用したい場合はバージョン1.6を選択してください。

次は上記の2つのドライバーを例として、TencentDB for MongoDBへの接続および読み書きを実行します。

### mongodbドライバーの使用
mongodbのインストール方法は、[公式のインストール手順](http://php.net/manual/zh/mongodb.installation.php)を参照してください。
**mongodbドライバーは「MONGODB-CR」と「SCRAM-SHA-1」2つの認証方法を使用できます**。詳細は[接続例](https://cloud.tencent.com/doc/product/240/3563)を参照してください。

サンプルコード：
```
<?php
// URIのつなぎ合わせ
$uri = 'mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin';
$manager = new MongoDB\Driver\Manager($uri);

// データを書き込む準備をします
$document1 = [
    'username' => 'lily',
    'age'      => 34,
    'email'    => 'lily@qq.com'
];

// 事前処理データを駆動すると、ここでMongoDBの_idがドライバーによって生成されていることがわかります。
$bulk = new MongoDB\Driver\BulkWrite;
$_id1 = $bulk->insert($document1);

$result = $manager->executeBulkWrite('tsdb.table1', $bulk);

// あるいは、必要に応じて、次のコードを使用して、データがほとんどのノードに書き込まれるようにします。
// $writeConcern = new MongoDB\Driver\WriteConcern(MongoDB\Driver\WriteConcern::MAJORITY, 1000);
// $result = $manager->executeBulkWrite('testdb.testcollection', $bulk, $writeConcern);

// 照合
$filter = ['_id' => $_id1];
$query = new MongoDB\Driver\Query($filter);
$rows = $manager->executeQuery('tsdb.table1', $query); // まずスレーブデータベースから読み取ることも選択できます。詳細はドキュメントを参照してください
foreach($rows as $r){
   print_r($r);
}


```
**出力：**
```
stdClass Object
(
    [_id] => MongoDB\BSON\ObjectID Object
        (
            [oid] => 582c001618c90a16363abc31
        )

    [username] => lily
    [age] => 34
    [email] => lily@qq.com
)
```


### mongoドライバーの使用
**mongoドライバーは「MONGODB-CR」認証のみをサポートし**、対応するものは「rwuser」でしか接続できません。詳細は[接続例](https://cloud.tencent.com/doc/product/240/3563)を参照してください。

サンプルコード：

```
<?php
// URIを使用して接続することをお勧めします。2つのURIのうち1つを選択してください
$uri = "mongodb://rwuser:thepasswordA1@10.66.187.127:27017/admin?authMechanism=MONGODB-CR";
$uri = "mongodb://rwuser:thepasswordA1@10.66.187.127:27017/?authMechanism=MONGODB-CR&authSource=admin";
$connection = new MongoClient($uri);

/*
// またはこれもいいです
$connection = new MongoClient("mongodb://10.66.116.103:27017/admin",
    array(
        "username" => "rwuser",
        "password" => "password",
        "authMechanism" => "MONGODB-CR"
    )
);
*/
$db = $connection->tsdb;
$collection = $db->table1;

$q = array(
    'id' => 1,
    'test1' => 'xxx',
    'ss' => 'xxxxxxxx',
);
$collection->save($q);
$one = $collection->findOne();
var_dump($one);
```

### PHPLIBライブラリー（mongodbドライバーに基づいてカプセル化）を使用することをお勧めします
mongodbドライバーを使用する場合は、[PHPLIB](http://php.net/manual/zh/mongodb.tutorial.library.php)と一緒に使用することをお勧めします。[関連文書の確認](http://mongodb.github.io/mongo-php-library/tutorial/crud/)。
PHPLIBのインストール方法は、[公式のインストール手順](http://mongodb.github.io/mongo-php-library/getting-started/)を参照してください。PHPLIB依頼とmongodbドライバーに注意してください。

サンプルコード：
```
<?php
require_once __DIR__ . "/vendor/autoload.php";

// 初期化
$mongoClient = new MongoDB\Client('mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin');

// demoライブラリーのusersコレクションを使います
$collection = $mongoClient->demo->users;

// データを書き込みます
$insertOneResult = $collection->insertOne(['name' => 'gomez']);

printf("Inserted %d document(s)\n", $insertOneResult->getInsertedCount());
var_dump($insertOneResult->getInsertedId());

// データ照合
$document = $collection->findOne(['name' => 'gomez']);

var_dump($document);

```
出力
```
Inserted 1 document(s)
object(MongoDB\BSON\ObjectID)#11 (1) {
  ["oid"]=>
  string(24) "57e3bf20bf605714a53e69c1"
}
object(MongoDB\Model\BSONDocument)#16 (1) {
  ["storage":"ArrayObject":private]=>
  array(2) {
    ["_id"]=>
    object(MongoDB\BSON\ObjectID)#14 (1) {
      ["oid"]=>
      string(24) "57e3bf20bf605714a53e69c1"
    }
    ["name"]=>
    string(5) "gomez"
  }
}

```

