If you find the request latency is longer than expected when using MongoDB, you can troubleshoot the problem following the steps below.<br>
1. Check if the monitoring metric Latency for instances is exceptional.
Check the instance monitoring data as shown below. The metric Latency mainly reflects the time from a request arriving at the access layer to it returning to the client after processed. If the request latency is high, check if there is a slow operation log on mongod.
![](https://main.qcloudimg.com/raw/d67c9fad80b03829168fbd92ad095378.png)

 To view the slow operation log, see the following steps.<br>
2. Check if there is a slow operation log on mongod.
Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb) and view the slow operation log of the instance by using "Query statistics" as shown below.
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
Pay attention to keywords such as command, COLLSCAN, IXSCAN, keysExamined and docsExamined. For more log descriptions, see [MongoDB official website](https://docs.mongodb.com/manual/reference/log-messages/index.html).
Keywords are described below.
 - command indicates the operations recorded in a slow operation log.
 - COLLSCAN indicates a full table scan is performed. IXSCAN indicates an index scan is performed. For more information on field descriptions, see [MongoDB official website](https://docs.mongodb.com/manual/reference/explain-results/index.html).<br>
 - keysExamined the number of index entries scanned. docsExamined indicates the number of documents scanned. Larger keysExamined and docsExamined values mean that no index is created or the index is less distinctive. Please confirm the fields for which an index is created.<br>
 
 
3. Confirm whether the request is locked due to an index created at the foreground.
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

4. Check if the mongos load is too high.
The metric Latency mainly reflects the time from a request arriving at the access layer to it returning to the client after processed. If there is no slow operation log on mongod, but the request latency is high, it may result from high mongos load. There are many reasons for this, such as a large number of connections are established in a short time, or data in multiple shards needs to be summarized. In these cases, you can restart mongos on the console, as shown in the figure below.<br>
![](https://main.qcloudimg.com/raw/0ab109e9a0adad49c3d96660132ea290.png)
> !All instance connections will be interrupted at the moment of restarting mongos, but the business can be directly reconnected. So restarting mongos will not continuously affect the business.

