
### Notes
TencentDB for MongoDB provides two usernames `rwuser` and `mongouser` by default to support the MONGODB-CR and SCRAM-SHA-1 authentication methods, respectively. The connecting URIs for the two authentication methods are formed differently. For more information, please see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).

For PHP, there is a driver that can be used to connect to and manipulate a MongoDB database, namely, [MongoDB driver](http://php.net/manual/en/set.mongodb.php). The MongoDB driver is officially recommended by MongoDB, but it requires PHP 5.4 or above.

The following shows you how to connect to TencentDB for MongoDB and read/write data by using the aforementioned driver.

### Using MongoDB driver
For more information on how to install the MongoDB driver, please see [Installation](http://php.net/manual/zh/mongodb.installation.php).
**The MongoDB driver can use both the MONGODB-CR and SCRAM-SHA-1 authentication methods.** For more information, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/3563).

Sample code:
```
<?php
// Splice the connection URI
$uri = 'mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin';
$manager = new MongoDB\Driver\Manager($uri);

// Prepare to write data
$document1 = [
    'username' => 'lily',
    'age'      => 34,
    'email'    => 'lily@qq.com'
];

// Preprocess the data with the driver. Here, you can see that `_id` of MongoDB is generated by the driver
$bulk = new MongoDB\Driver\BulkWrite;
$_id1 = $bulk->insert($document1);

$result = $manager->executeBulkWrite('tsdb.table1', $bulk);

// You can also use the following code as needed to ensure that data is written to a majority of nodes
// $writeConcern = new MongoDB\Driver\WriteConcern(MongoDB\Driver\WriteConcern::MAJORITY, 1000);
// $result = $manager->executeBulkWrite('testdb.testcollection', $bulk, $writeConcern);

// Query
$filter = ['_id' => $_id1];
$query = new MongoDB\Driver\Query($filter);
$rows = $manager->executeQuery('tsdb.table1', $query); // You can also select to read a secondary database first
foreach($rows as $r){
   print_r($r);
}


```
Output:
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


### Using PHPLIB library (encapsulated based on MongoDB driver)
We recommend you use [PHPLIB](http://php.net/manual/zh/mongodb.tutorial.library.php) with the MongoDB driver. For more information, please see [CRUD Operations](http://mongodb.github.io/mongo-php-library/tutorial/crud/).
For more information on how to install PHPLIB, please see [Install the MongoDB PHP Library](http://mongodb.github.io/mongo-php-library/getting-started/). Please note that PHPLIB depends on the MongoDB driver.

Sample code:
```
<?php
require_once __DIR__ . "/vendor/autoload.php";

// Initialize
$mongoClient = new MongoDB\Client('mongodb://mongouser:thepasswordA1@10.66.187.127:27017/admin');

// Use the `users` collection under the `demo` library
$collection = $mongoClient->demo->users;

// Write a data entry
$insertOneResult = $collection->insertOne(['name' => 'gomez']);

printf("Inserted %d document(s)\n", $insertOneResult->getInsertedCount());
var_dump($insertOneResult->getInsertedId());

// Query data
$document = $collection->findOne(['name' => 'gomez']);

var_dump($document);

```
Output:
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
