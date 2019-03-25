
### What do I do in case of disconnection from MongoDB?
See [Connection Example](https://cloud.tencent.com/document/product/240/3563) to eliminate authentication issues.

### What do I do if a message that "Remote server has closed the connection" displays?
First, see [Connection Example](https://cloud.tencent.com/document/product/240/3563) to eliminate authentication issues. If you can connect to MongoDB but still encounter this problem, you may need a [Reconnection Mechanism](https://cloud.tencent.com/document/product/240/4980).

### WiredTiger 3.2 has the problem of table lock. Is TencentDB for MongoDB affected by the same issue?
It depends on the specific situation. For example, a global lock is required to create indexes by default, and a lock is also needed when you execute the fsynclock command.
Lock is a feature of databases, and is used to deal with the problems of concurrent access. Generally, a lock is required, as long as it does not affect the operation of your business.

### Which version of the driver should be used in MongoDB?
It is recommended to use the latest version, for example, using mongo-1.6 or above for PHP.
 
### Which languages can be used to connect to MongoDB?
TencentDB for MongoDB can be connected through a variety of languages, such as Shell, PHP, Node.js, Java and Python. For more information, see [Connection Example](https://cloud.tencent.com/document/product/240/3563).

### Which language clients are supported by TencentDB for MongoDB?
TencentDB for MongoDB provides the same compatibility as MongoDB. TencentDB for MongoDB supports any client that is supported by the official MongoDB. For example: C, C++, c#, java, node.js, python, php, and perl. For more information, see [MongoDB official documentation](https://docs.mongodb.org/ecosystem/drivers/).

### How do I connect to TencentDB for MongoDB in shell?
For more information, see [Shell Connection Example](https://cloud.tencent.com/doc/product/240/3978).

### What URIs in service applications can be used to connect to MongoDB?
For more information, see [Connection Example](https://cloud.tencent.com/doc/product/240/3563).

### What do I do if I cannot connect to TencentDB for MongoDB using meteor and other types of frameworks and class libraries?
This is usually caused by incorrect connection method or URI combinations. Please check and verify the cause first.

### How do I set the maximum number of connections to MongoDB in PHP?
MongoDB driver ([Official PHP documentation](http://php.net/manual/en/set.mongodb.php)) can control the number of connections by configuring the maxPoolSize parameter in the URL connection.
MongoDB driver ([Official PHP documentation](http://php.net/manual/en/set.mongodb.php)) can set the number of connections through Mongo::setPoolSize() method. For more information, see [MongoPool::setSize](http://php.net/manual/en/mongopool.setsize.php)。.
 

### What is the limit on the number of connections to MongoDB?
![](//bot1024-1253841380.file.myqcloud.com/3defdf809c3d11e7bd8b525400a3183e.png)
The upper limit on number of connections is applicable to instances rather than nodes. For more information, see [Use Limits](https://cloud.tencent.com/document/product/240/622).
 
### How do I reconnect to MongoDB manually?
Instead of simply allowing you to access mongod, TencentDB for MongoDB database service provides a load balancer IP for access. You can use this IP to connect to a range of route access layers similar to mongos.
The client driver establishes a persistent connection with an access server using a load balancer IP. If the connection is active for a long period of time, Tencent Cloud will not impose an intervention on this status. However, if the persistent connection is inactive for more than one day (this period will be adjusted with optimized version), the route access layer will terminate the connection.
Generally, the client driver will implement an automatic reconnection. However, this process cannot be implemented by some language drivers. For the language drivers that cannot implement automatic reconnection, if you attempt to communicate with the TencentDB for MongoDB service using a terminated connection, an error message such as "Remote server has closed the connection" will be returned. So manual reconnection is required. Here is a demo for PHP reconnection.

**Reconnection Based on PHP Mongo Driver** 
![](//bot1024-1253841380.file.myqcloud.com/aa398f929c4211e79a34525400a3183e.png)


### How do I use mongoose to connect to TencentDB for MongoDB?
Here are the parameters for mongoose to connect to TencentDB for MongoDB:

``` 
var dbUri = " mongodb:// " + user + " : " +password + " @ " +host + ":" +port + " / " + dbName;

var opts = {
　　auth:｛
　　　　authMechanism : ' MONDODB-CR'
      ｝
}；
var connection = mongodb.createConnection(dbUri, opts);
```

### Can I connect to MongoDB from a public network?
MongoDB can only be connected via a private network. For more information, see [Connection Example](https://cloud.tencent.com/document/product/240/3563).
Connection through a public network is not supported. To connect to MongoDB locally, you can implement port forwarding using the server within the same private network under the same MongoDB account.
 

