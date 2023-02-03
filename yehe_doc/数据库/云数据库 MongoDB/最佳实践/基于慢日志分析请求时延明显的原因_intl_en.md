## Problem description

The **latency monitoring** metrics stay high on the **System Monitoring** tab on the **Instance Details** page of an instance in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). The latency metric mainly reflects the time from a request arriving at the access layer to it returning to the client after being processed. For more information, see [Monitoring Feature](https://intl.cloud.tencent.com/document/product/240/7117).

## Cause analysis

1. Check whether there are slow logs on mongod.
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID to enter the **Instance Details** page, and view the slow logs of the instance by using **Query statistics** on the **Database Management** > **Slow Log Query** tab. For more information, see [Slow Log Management](https://intl.cloud.tencent.com/document/product/240/31454). Pay attention to keywords such as **command**, **COLLSCAN**, **IXSCAN**, **keysExamined**, and **docsExamined**.
  - **command** indicates an operation request recorded in a slow log.
  - **COLLSCAN** indicates that a full-collection scan is performed for the query.
  - **IXSCAN** indicates that an index scan is performed. For descriptions of other fields, see [Explain Results](https://docs.mongodb.com/manual/reference/explain-results/index.html).
  - **keysExamined** indicates the number of index entries scanned.
  - **docsExamined** indicates the number of documents scanned. Larger **keysExamined** and **docsExamined** values indicate that no index is created or the created index is less distinctive.
For more information on slow log, see [Log Messages](https://docs.mongodb.com/manual/reference/log-messages/index.html).
2. If there are no slow queries on mongod, check whether the load on mongos is too high.
The latency monitoring metric mainly reflects the time from a request arriving at the access layer to it returning to the client after being processed. If there are no slow queries on mongod, but the request latency is high, the problem may be caused by a high mongos load.
There are many causes for this; for example, a large number of connections are established in a short time, or data in multiple shards needs to be aggregated.
In these cases, you can restart mongos in the instance list in the [console](https://console.cloud.tencent.com/mongodb/instance).
>!All instance connections will be interrupted at the moment of restarting mongos, but the business can be directly reconnected.
3. If there are index scans in the slow logs of mongod, check whether the request is locked due to an index created in the foreground.
   If there is no problem with the index used for business queries, check whether an index is created in the foreground during peak business hours.
   - An index is created in the foreground by default for a collection (with the `background` option being `false`), which will block all other operations until the index is created in the foreground.
   - If you choose to create an index in the background, MongoDB can still provide read/write services during the creation of the index. However, it takes more time to create the index in this way. For options to create an index, see [db.collection.createIndex()](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/).
You can also view the progress of index creation by running the `currentOp` command:
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
The returned result is shown as follows. The `msg` field indicates the progress of index creation. The `locks` field indicates the lock type of the operation. For more information on locks, see [Database Profiler Output](https://docs.mongodb.com/v3.2/reference/database-profiler/). 
![](https://qcloudimg.tencent-cloud.cn/raw/bae5f6d68e91f78d33b7bf2cb755b39a.png)
