You may encounter two types of connection problems when using MongoDB. You can troubleshoot the problems as follows.
## High Connection Usage ##
If you find that the connection usage of the instance is too high, you can refer to the following procedure for troubleshooting.<br>
1. Check whether a connection pool is used in the business.<br>
The MongoDB service is provided in such a mode that each network connection is processed by a single thread (one-thread-per-connection). Too many network connections generate too many threads, which will increase context switch overhead and memory usage. Establishing connections and performing authentication for each request greatly affect performance. Therefore, it is recommended to use a connection pool for business to limit the number of connections of the instance and to release the connections that are no longer in use. All language versions of MongoDB Drivers generally encapsulate an object, so you need to construct a global object and use it in subsequent requests to send requests to the instance when using MongoDB. You can use the default connection pool size for the object in Driver, or configure the connection pool size by specifying the maxPoolSize option when constructing an object.<br>

2. If you have set a connection pool, check your business for any unexpected exceptions.
 - Check whether there is any business release change or code logic defect that leads to a large number of connections.<br>
 - Check whether there is any connection leak, i.e., check whether the number of connections on relevant CVM is exceptional.<br>
 - Check whether the business really has a large number of sudden requests.<br>

3. Check whether there is any slow log that causes the connection to be occupied.<br>
 - If the business is confirmed to be normal, check whether there is any index exception, for example, a previously established index is deleted by mistake.<br> 
 - If the index is normal, check whether there are a large number of slow logs, which occupy the connections and lead to establishment of more connections.<br>
Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb), and view the slow log of the instance by using "Query statistics", as shown below.<br>
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
Pay attention to keywords such as command, COLLSCAN, IXSCAN, keysExamined and docsExamined. For more log descriptions, see [MongoDB official website](https://docs.mongodb.com/manual/reference/log-messages/index.html).<br>
   The keywords are described as follows:<br>
 1. command indicates the operations recorded in a slow log.<br>
 2. COLLSCAN indicates a full table scan is performed. IXSCAN indicates an index scan is performed. For descriptions of other fields, see [MongoDB official website](https://docs.mongodb.com/manual/reference/explain-results/index.html).<br>
 3. keysExamined refers to the number of index entries scanned. docsExamined refers to the number of documents scanned. Larger keysExamined and docsExamined values mean that no index is created or the index is less distinctive. Please confirm the fields for which an index is created.<br>
4. Confirm whether the request is locked due to an index created at the foreground.<br>
If there is no problem with the index used for business queries, check if an index is created at the foreground during peak business hours. An index is created at the foreground by default for a collection (the Background option is false), which will block all the other operations until the index is created at the foreground. If you select to create an index at the background, MongoDB can still provide read and write services during the creation of the index. However, it takes longer time to create an index in this way. For options to create an index, see [MongoDB official website](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/).<br>
You can view the progress of index creation using the currentOp command, as shown below:

   
	 db.currentOp(
        {
          $or: [
            { op: "command", "query.createIndexes": { $exists: true } },
            { op: "insert", ns: /\.system\.indexes\b/ }
          ]
        }
        )
The returned result is shown as follows. The msg field indicates the progress of index creation. The locks field indicates the lock type of the operation. For more information on locks, see [MongoDB official website](https://docs.mongodb.com/v3.2/reference/database-profiler/).<br>
![](https://main.qcloudimg.com/raw/355b6c06539ad6a5e3980b90bd200bf0.png)
![](https://main.qcloudimg.com/raw/155583329a2eb2a99575a2b5ce0b8647.png)<br>
5. Evaluate whether the instance configuration meets business requirements.<br>
If the business connection usage shown on the console is still high after a connection pool is set and highly-distinctive indexes are created, it may indicate that the instance configuration cannot meet the actual business needs any longer. In such case, you need to evaluate the instance specification you actually need based on your business model, peak traffic, QPS, and TPS, and then upgrade your instance.

## Connection Rejected ##
If a connection is rejected, you can troubleshoot the problem as follows.<br>
1. Check whether the connection usage of the instance is 100%.
Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb), and view the monitoring metrics "Number of Connections" and "Connection Usage" on the console, as shown below:<br>
![](https://main.qcloudimg.com/raw/b1a5ef8d203696142bd17c2427668bab.png)

 If the connection usage of the instance is 100%, check whether your business is exceptional. If necessary, you can quickly release the connections by restarting mongos on the console.
>!All instance connections will be interrupted at the moment of restarting mongos, but the business can be directly reconnected. So restarting mongos will not continuously affect the business. If the number of business connections increases rapidly and the connection usage reaches 100% again after the restart, it indicates that the business does have a large number of valid connections and there is no connection leak. In such case, you need to find why there is such a large number of connections in the business by referring to the troubleshooting procedure for high connection usage.

2. Check whether the user name and the password are correct.
Check whether the user name and the password are correct. If they are incorrect, log in to the console and go to **Management** -> **Account Management** to modify them, as shown below:<br>
![](https://main.qcloudimg.com/raw/1b505172b773dd5ebeb5f129eb1c790c.png)

3. Check whether the Mongoshell version is correct.
To ensure successful authentication, install Mongo Shell 3.0 and above. For specific installation procedure, see the [official documentation](https://docs.mongodb.com/v3.2/installation/).<br>
4. Check whether the authentication database is correct.<br>
>!The authentication database for users created on the console is the "admin" database, so the users need to specify "admin" as the authentication database on login. The users created with the command line, such as a user created under the "test" database, need to specify "test" as the authentication database.


