## Description

TencentDB for MongoDB provides more than mongod processes for the database - it offers a load balancer IP for each user. You can use this IP to connect to multiple route access layers similar to mongos.

A MongoDB client driver establishes a persistent connection with an access server using load balancer IP. If the connection is active for a long period of time, we will not change this status. However, if this persistent connection is inactive for more than one day (the duration is adjusted as the version is updated), it will be terminated in the route access layer.

Generally, MongoDB client drivers can automatically reconnect to the database service. But this is not working for some languages. When the driver is still disconnected, if you attempt to communicate with TencentDB for MongoDB using a terminated connection, you will see an error message such as "Remote server has closed the connection". In this case, you need to reconnect to the service manually. 

Here is a demo for PHP reconnection.

## Reconnection with PHP Mongo Driver
```
<?php

function getConnection() {
    $connection = false;
    $uri = 'mongodb://rwuser:1234567a@10.66.148.142:27017/admin?authMechanism=MONGODB-CR';
    $maxRetries = 5;
    for( $counts = 1; $counts <= $maxRetries; $counts++ ) {
        try {
            $connection = new MongoClient($uri);
        } catch( Exception $e ) {
     // Or use the catch code line below as needed. Please note that "\" is needed for a namespace .
     // } catch( \Exception $e ) {
            continue;
        }
        break;
    }
    return $connection;
}

$connection = getConnection();

if($connection) {
		$db = $connection->testdb;
		$collection = $db->testcollection;

		$one = $collection->findOne();

		var_dump($one);
}
```


