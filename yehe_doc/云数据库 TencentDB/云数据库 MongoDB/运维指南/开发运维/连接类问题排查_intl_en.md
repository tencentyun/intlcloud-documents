You may encounter two types of connection problems when using TencentDB for MongoDB. You can troubleshoot them as follows.

## High Connection Utilization
If you find that the connection utilization of the instance is too high, you can refer to the following procedure for troubleshooting.
1. Check whether a connection pool is used in the business.
The MongoDB service is provided in a mode where each network connection is processed by a single thread (one-thread-per-connection). Too many network connections generate too many threads, which will increase context switch and memory overheads. Establishing connections and performing authentication for each request greatly affect performance. Therefore, you are recommended to use a connection pool for your business to limit the number of connections of the instance and release the connections no longer in use. All programming language versions of MongoDB drivers generally encapsulate an object, so you need to construct a global object and use it in subsequent requests to send requests to the instance when using MongoDB. You can use the default connection pool size for the object in the Driver or configure the size by specifying the `maxPoolSize` option when constructing an object.

2. If you have already set a connection pool, check your business for any unexpected exceptions.
 - Check whether there are any business release changes or code logic defects that lead to a large number of connections.
 - Check whether there are any connection leaks by checking whether the number of connections on relevant CVM instances is exceptional.
 - Check whether the business has a large number of sudden real requests.

3. Check whether there are any slow queries that cause connections to be occupied.
 - If your business is confirmed to be normal, check whether there are any index exceptions; for example, a previously established index is deleted by mistake.
 - If the index is normal, check whether there are a large number of slow queries, which occupy the connections and lead to establishment of more connections.
Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and view the slow logs of the instance by using "Query statistics".
![](https://main.qcloudimg.com/raw/bfa1b87481b272489bfae511b758a8d5.png)
Pay attention to keywords such as `command`, `COLLSCAN`, `IXSCAN`, `keysExamined`, and `docsExamined`. For more log descriptions, please see [Log Messages](https://docs.mongodb.com/manual/reference/log-messages/index.html). 
   The keywords that require attention include the following:
 1. `command` indicates an operation recorded in a slow log.
 2. `COLLSCAN` indicates that a full-table scan is performed. `IXSCAN` indicates that an index scan is performed. For descriptions of other fields, please see [Explain Results](https://docs.mongodb.com/manual/reference/explain-results/index.html).
 3. `keysExamined` refers to the number of index entries scanned. `docsExamined` refers to the number of documents scanned. Larger `keysExamined` and `docsExamined` values indicate that no index is created or the created index is less distinctive. Please check the fields for which an index is created.

4. Check whether the request is locked due to an index created in the foreground.
If there is no problem with the index used for business queries, check whether an index is created in the foreground during peak business hours. An index is created in the foreground by default for a collection (the `background` option is `false`), which will block all other operations until the index is created in the foreground. If you choose to create an index in the background, MongoDB can still provide read/write services during the creation of the index. However, it takes more time to create the index in this way. For options to create an index, please see [db.collection.createIndex()](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/).<br>
You can view the progress of index creation by running the `currentOp` command as shown below:
```
 db.currentOp(
        {
          $or: [
            { op: "command", "query.createIndexes": { $exists: true } },
            { op: "insert", ns: /\.system\.indexes\b/ }
          ]
        }
        )
```
The returned result is shown as follows. The `msg` field indicates the progress of index creation. The `locks` field indicates the lock type of the operation. For more information on locks, please see [Database Profiler Output](https://docs.mongodb.com/v3.2/reference/database-profiler/).<br>
![](https://main.qcloudimg.com/raw/355b6c06539ad6a5e3980b90bd200bf0.png)
![](https://main.qcloudimg.com/raw/155583329a2eb2a99575a2b5ce0b8647.png)<br>

5. Evaluate whether the instance configuration meets your business requirements.
If the business connection utilization displayed in the console is still high after a connection pool is set and a highly distinctive index is created, it may indicate that the instance configuration cannot meet the actual business needs. In such case, you need to evaluate the instance specification actually needed based on your business model, peak traffic, QPS, and TPS and then upgrade your instance accordingly.

## Connection Rejection 
If a connection is rejected, you can troubleshoot the problem as follows.

1. Check whether the connection utilization of the instance is 100%.
Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb) and view the monitoring metrics "Connection Count" and "Connection Utilization" on the system monitoring page.
If the connection utilization of the instance is 100%, check whether your business is exceptional. If necessary, you can quickly release the connections by restarting mongos in the console.
>! All instance connections will be interrupted at the moment of restarting mongos, but the business can be directly reconnected. Therefore, restarting mongos will not continuously affect the business. If the number of business connections increases rapidly and the connection utilization reaches 100% again after the restart, it indicates that the business does have a large number of valid connections and there are no connection leaks. In such case, you need to find why there is such a large number of connections in your business by referring to the troubleshooting procedure for high connection utilization.

2. Check whether the username and password are correct.
Make sure that the username and password are correct. If they are incorrect, log in to the console and modify them.
![](https://main.qcloudimg.com/raw/3dc1106070c23340a042c130ea6800ae.png)

3. Check whether the mongo shell version is correct.
To ensure successful authentication, install mongo shell 3.0 or above. For detailed directions, please see [Install MongoDB](https://docs.mongodb.com/v3.2/installation/).
4. Check whether the authentication database is correct.
>!The authentication database for users created in the console is the `admin` database, so the users need to specify `admin` as the authentication database during login. The users created with the command line, such as those created under the `test` database, need to specify `test` as the authentication database.

