
If you find the request latency becomes obviously longer when using TencentDB for MongoDB, you can troubleshoot the problem in the following steps:
1. Check whether the "Latency" monitoring metric for instances is exceptional.
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID to enter the management page, and check the instance monitoring data on the **System Monitoring** tab. The "Latency" metric mainly reflects the time from a request arriving at the access layer to it returning to the client after being processed. If the request latency is high, check whether there are slow logs on mongod.

2. Check whether there are slow logs on mongod.
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID to enter the management page, and view the slow logs of the instance by using "Query statistics" on the **Database Management** > **Slow Log Query** tab.
Pay attention to keywords such as `command`, `COLLSCAN`, `IXSCAN`, `keysExamined`, and `docsExamined`. For more log descriptions, see [Log Messages](https://docs.mongodb.com/manual/reference/log-messages/index.html).
The keywords that require attention include the following:
 - `command` indicates an operation recorded in a slow log.
 - `COLLSCAN` indicates that a full-table scan is performed. `IXSCAN` indicates that an index scan is performed. For descriptions of other fields, see [Explain Results](https://docs.mongodb.com/manual/reference/explain-results/index.html).<br>
 - `keysExamined` refers to the number of index entries scanned. `docsExamined` refers to the number of documents scanned. Larger `keysExamined` and `docsExamined` values indicate that no index is created or the created index is less distinctive. Check the fields for which an index is created.
  
3. Check whether the request is locked due to an index created in the foreground.
If there is no problem with the index used for business queries, check whether an index is created in the foreground during peak business hours. An index is created in the foreground by default for a collection (the `background` option is `false`), which will block all other operations until the index is created in the foreground. If you choose to create an index in the background, MongoDB can still provide read/write services during the creation of the index. However, it takes more time to create the index in this way. For options to create an index, see [db.collection.createIndex()](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/).
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
The returned result is shown as follows. The `msg` field indicates the progress of index creation. The `locks` field indicates the lock type of the operation. For more information on locks, see [Database Profiler Output](https://docs.mongodb.com/v3.2/reference/database-profiler/).<br>
![](https://main.qcloudimg.com/raw/355b6c06539ad6a5e3980b90bd200bf0.png)
![](https://main.qcloudimg.com/raw/155583329a2eb2a99575a2b5ce0b8647.png)<br>

4. Check whether the mongos load is too high.
The "Latency" metric mainly reflects the time from a request arriving at the access layer to it returning to the client after being processed. If there are no slow logs on mongod, but the request latency is high, it may result from high mongos load. There are many reasons for this; for example, a large number of connections are established in a short time, or data in multiple shards needs to be aggregated. In these cases, you can restart mongos in the [console](https://console.cloud.tencent.com/mongodb/instance).
> !All instance connections will be interrupted at the moment of restarting mongos, but the business can be directly reconnected. Therefore, restarting mongos will not continuously affect the business.
