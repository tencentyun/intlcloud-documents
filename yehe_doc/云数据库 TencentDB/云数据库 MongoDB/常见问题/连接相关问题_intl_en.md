
### What should I do in case of disconnection from TencentDB for MongoDB?
Please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092) to eliminate authentication issues.

### What should I do if the message "Remote server has closed the connection" is displayed in TencentDB for MongoDB?
First, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092) to eliminate authentication issues. If you can connect to MongoDB but still encounter this problem, you may need a reconnection mechanism. For more information, please see [Reconnection Sample](https://intl.cloud.tencent.com/document/product/240/4980).

### WiredTiger 3.2 has the problem of table lock. Is TencentDB for MongoDB affected by the same issue?
It depends on the specific conditions. For example, a global lock is required during index creation by default, and a lock is also needed when you run the `fsynclock` command.
Lock is a databases feature used to deal with the problems of concurrent access. Generally, a lock is required as long as it does not affect the operation of your business.

### Which version of the driver should be used in TencentDB for MongoDB?
You are recommended to use the latest version, such as mongo-1.6 or above for PHP.
 
### What programming languages can be used to connect to TencentDB for MongoDB?
TencentDB for MongoDB can be connected through a variety of programming languages, such as Shell, PHP, Node.js, Java, and Python. For more information, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092).

### What programming language clients are supported by TencentDB for MongoDB?
TencentDB for MongoDB provides the same compatibility as MongoDB. It supports any client that is officially supported by MongoDB, such as C, C++, c#, Java, Node.js, Python, PHP, and Perl. For more information, please see [Start Developing with MongoDB](https://docs.mongodb.org/ecosystem/drivers/).

### How do I connect to TencentDB for MongoDB in shell?
For more information, please see [Shell Connection Sample](https://intl.cloud.tencent.com/document/product/240/3978).

### What URIs in business applications can be used to connect to TencentDB for MongoDB?
For more information, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092).

### What should I do if I cannot connect to TencentDB for MongoDB by using meteor and other types of frameworks and class libraries?
This is usually caused by incorrect connection methods or URIs. Please check and verify the cause first.

### How do I set the maximum number of connections to TencentDB for MongoDB in PHP?
In the [MongoDB driver](http://php.net/manual/en/set.mongodb.php), you can control the number of connections by configuring the `maxPoolSize` parameter in the URL connection.
In the [MongoDB driver](http://php.net/manual/en/set.mongodb.php), you can set the connection count through the `Mongo::setPoolSize()` method. For more information, please see [MongoPool::setSize](http://php.net/manual/en/mongopool.setsize.php).
 

### What is the limit on the number of connections to TencentDB for MongoDB?

| MEM | Connection Cap |
| :------: | :------------: |
|   2 GB    |      1,500      |
|   4 GB    |      1,500      |
|   6 GB    |      1,500      |
|   8 GB    |      1,500      |
|   12 GB   |      1,500      |
|   16 GB   |      2,500      |
|   24 GB   |      3,500      |
|   32 GB   |      4,500      |
|   48 GB   |      6,000      |
|   64 GB   |      9,000      |
|  128 GB   |     15,000      |
|  240 GB   |     15,000      |
|  512GB   |     15,000      |

The upper limit on number of connections is applicable to instances rather than nodes. For more information, please see [Use Limits](https://intl.cloud.tencent.com/document/product/240/31183).
 
### How do I reconnect to TencentDB for MongoDB manually?
Instead of simply allowing you to access mongod, TencentDB for MongoDB provides a load balancer IP for access. You can use this IP to connect to a range of route access layers similar to mongos.
The client driver establishes a persistent connection with an access server by using a load balancer IP. If the connection is active for a long period of time, Tencent Cloud will not impose an intervention on this status. However, if the persistent connection is inactive for more than one day (this period will be adjusted as the version is optimized), the route access layer will terminate the connection.
Generally, the client driver will implement automatic reconnection. However, this process cannot be implemented by certain programming language drivers. For such drivers, if you attempt to communicate with the TencentDB for MongoDB service through a terminated connection, an error message such as "Remote server has closed the connection" will be returned. Therefore, manual reconnection is required. Below is a demo for PHP reconnection.

**Reconnection based on PHP mongo driver** 
![](https://main.qcloudimg.com/raw/a0b428c51f0ba06b91788b391e1650ea.png)


### How do I use mongoose to connect to TencentDB for MongoDB?
Below are the parameters for mongoose to connect to TencentDB for MongoDB:

``` 
var dbUri = " mongodb:// " + user + " : " +password + " @ " +host + ":" +port + " / " + dbName;

var opts = {
　　auth: {
　　　　authMechanism : ' MONDODB-CR'
      ｝
}；
var connection = mongodb.createConnection(dbUri, opts);
```

### Can I connect to TencentDB for MongoDB over the public network?
TencentDB for MongoDB can only be connected over the private network. For more information, please see [Connection Sample](https://intl.cloud.tencent.com/document/product/240/7092).
Connection over the public network is not supported currently. To connect to TencentDB for MongoDB locally, you can implement port forwarding by using the server on the same private network under the same MongoDB account.
 
