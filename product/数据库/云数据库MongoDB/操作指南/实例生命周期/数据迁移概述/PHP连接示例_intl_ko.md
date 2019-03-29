### 관련 설명
TecentDB for MongoDB는 기본적으로 "rwuser"와 "mongouser" 두 개 사용자 이름을 제공하며 각각 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 지원합니다. 이 두 가지 인증 방식의 경우 URI를 연결 시 서로 다른 방식으로 처리해야 합니다. 자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563) 문서를 참조하십시오.

PHP는 MongoDB 데이터베이스에 연결하는 데 사용되는 [두 세트 드라이브](https://docs.mongodb.com/ecosystem/drivers/php/)를 제공합니다. 자세한 정보는 다음을 참조하십시오.
- MongoDB([PHP 공식 웹사이트 문서](http://php.net/manual/en/set.mongodb.php))  - MongoDB는 공식으로 추천하는 MongoDB 드라이브입니다. 단, PHP 5.4 이상 버전을 요구합니다.
- Mongo([PHP 공식 웹사이트 문서](http://php.net/manual/en/book.mongo.php)) - Mongo는 비교적 오래되었지만 사용은 가능합니다. 사용할 경우, 1.6 버전을 사용하십시오.

상기 두 드라이브로 TencentDB for MongoDB에 연결하여 읽기/쓰기 작업을 진행하는 것을 보여드립니다.

### MongoDB 드라이브 사용하기
MongoDB 설치 방법은 [공식 설치 절차](http://php.net/manual/zh/mongodb.installation.php)를 참조하십시오.
**MongoDB 드라이브는 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 사용할 수 있습니다. ** 자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563)를 참조하십시오.

예제 코드:
```
<?php
// 연결 URI 병합
$uri = 'mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin';
$manager = new MongoDB\Driver\Manager($uri);

// 데이터 쓰기 준비
$document1 = [
    'username' => 'lily',
    'age'      => 34,
    'email'    => 'lily@qq.com'
];

// 드라이브 사전 처리 데이터, MongoDB의 _ID 가 드라이브에서 생성한 것인지를 볼 수 있습니다.
$bulk = new MongoDB\Driver\BulkWrite;
$_id1 = $bulk->insert($document1);

$result = $manager->executeBulkWrite('tsdb.table1', $bulk);

// 또는 실제 수요에 따라 아래의 코드를 사용하여 데이터를 과반수 노드에 쓸 수 있습니다.
// $writeConcern = new MongoDB\Driver\WriteConcern(MongoDB\Driver\WriteConcern::MAJORITY, 1000);
// $result = $manager->executeBulkWrite('testdb.testcollection', $bulk, $writeConcern);

// 조회
$filter = ['_id' => $_id1];
$query = new MongoDB\Driver\Query($filter);
$rows = $manager->executeQuery('tsdb.table1', $query); // 슬레이브 데이터베이스에서 읽기를 시작하는 것을 선택할 수 있습니다. 자세한 내용은 해당 문서를 참조하십시오.
foreach($rows as $r){
   print_r($r);
}


```
**출력:**
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


### Mongo 드라이브 사용하기
**Mongo 드라이브는 "MONGODB-CR" 인증만 지원하고** "rwuser"로만 연결할 수 있습니다. 자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563)를 참조하십시오.

예제 코드:

```
<?php
// URI 방식으로 연결하는 것을 권장합니다. 두 가지 URI 중 하나를 선택하십시오.
$uri = "mongodb://rwuser:thepasswordA1@10.66.187.127:27017/admin?authMechanism=MONGODB-CR";
$uri = "mongodb://rwuser:thepasswordA1@10.66.187.127:27017/?authMechanism=MONGODB-CR&authSource=admin";
$connection = new MongoClient($uri);

/*
// 또는, 다음 방식도 가능합니다.
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

### PHPLIB 데이터베이스(MongoDB 드라이브 캡슐화에 기반함)를 권장합니다.
MongoDB 드라이브를 사용하려면 [PHPLIB](http://php.net/manual/zh/mongodb.tutorial.library.php)와 함께 사용하는 것을 권장합니다. [관련 문서 보기](http://mongodb.github.io/mongo-php-library/tutorial/crud/)
PHPLIB의 설치 방법은 [공식 설치 절차](http://mongodb.github.io/mongo-php-library/getting-started/)를 참조하십시오. PHPLIB는 MongoDB 드라이브에 의존성이 있으니 주의하십시오.

예제 코드:
```
<?php
require_once __DIR__ . "/vendor/autoload.php";

// 초기화
$mongoClient = new MongoDB\Client('mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin');

// Demo 데이터베이스의 Users 집합 사용
$collection = $mongoClient->demo->users;

// 데이터 한 항목 쓰기
$insertOneResult = $collection->insertOne(['name' => 'gomez']);

printf("Inserted %d document(s)\n", $insertOneResult->getInsertedCount());
var_dump($insertOneResult->getInsertedId());

// 데이터 조회
$document = $collection->findOne(['name' => 'gomez']);

var_dump($document);

```
출력
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
