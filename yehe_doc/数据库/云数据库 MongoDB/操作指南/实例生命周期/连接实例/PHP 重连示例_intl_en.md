## Notes
Instead of simply allowing you to access mongod, the TencentDB for MongoDB database service provides a load balancer IP for access. You can use this IP to connect to a range of route access layers similar to mongos.
The client driver establishes a persistent connection with an access server through the load balancer IP. If the connection is active for a long period of time, no intervention will be imposed on this status. However, if the persistent connection is inactive for more than one day (this period will be adjusted with version optimization), the route access layer will terminate the connection.
Generally, the client driver will implement an automatic reconnection process. However, this process cannot be implemented by certain language drivers. For such language drivers, if you attempt to communicate with the TencentDB for MongoDB service through a terminated connection, an error message such as "Remote server has closed the connection" will be returned, and manual reconnection will be required. The document provides a demo for PHP reconnection.

## Reconnection Based on PHP Mongo Driver
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
     // Or use the `catch` code line below as required. Please note that "\" is needed when some frameworks use namespace.
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

