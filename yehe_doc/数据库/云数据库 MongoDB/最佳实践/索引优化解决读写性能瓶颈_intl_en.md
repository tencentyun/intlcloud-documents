Index is a key factor affecting the MongoDB database query performance. Meeting your query needs with a minimal number of indexes can greatly improve the database performance and reduce the storage costs. This document describes how to analyze and optimize indexes to help you break through the bottleneck in database read/write performance.

## Problem Description
In daily Ops, you can log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) and click the instance ID to enter the **Instance Details** page and view the following information:
- Select the **System Monitoring** tab to view the instance monitoring data:
  - The CPU usage of the mongod node is too high. The CPU utilization is close to 90% or even 100%.
  - The disk reads/writes per second stays high continuously, and the I/O resource usage of a node accounts for 60% of that of the entire server.

- Select **Database Management** > **Slow Log Query** to view slow logs:
  - The instance has a high number of slow logs, which include many `find` and `update` requests of different types. Thousands of such requests are received per second during peak hours.
  - Slow logs are of diverse types and have various query conditions, and all slow queries have matching indexes. Below is the log content:
```
Mon Aug  2 10:34:24.928 I COMMAND  [conn10480929] command xxx.xxx command: find { find: "xxx", filter: { $and: [ { alxxxId: "xxx" }, { state: 0 }, { itemTagList: { $in: [ xx ] } }, { persxxal: 0 } ] }, limit: 3, maxTimeMS: 10000 } planSummary: IXSCAN { alxxxId: 1.0, itemTagList: 1.0 } keysExamined:1650 docsExamined:1650 hasSortStage:0 cursorExhausted:1 keyUpdates:0 writeConflicts:0 numYields:15 nreturned:3 reslen:8129 locks:{ Global: { acquireCount: { r: 32 } }, Database: { acquireCount: { r: 16 } }, Collection: { acquireCount: { r: 16 } } } protocol:op_command 227ms  
   
Mon Aug  2 10:34:22.965 I COMMAND  [conn10301893] command xx.txxx command: find { find: "txxitem", filter: { $and: [ { itxxxId: "xxxx" }, { state: 0 }, { itemTagList: { $in: [ xxx ] } }, { persxxal: 0 } ] }, limit: 3, maxTimeMS: 10000 } planSummary: IXSCAN { alxxxId: 1.0, itemTagList: 1.0 } keysExamined:1498 docsExamined:1498 hasSortStage:0 cursorExhausted:1 keyUpdates:0 writeConflicts:0 numYields:12 nreturned:3 reslen:8039 locks:{ Global: { acquireCount: { r: 26 } }, Database: { acquireCount: { r: 13 } }, Collection: { acquireCount: { r: 13 } } } protocol:op_command 158ms  
```

## Cause Analysis
By analyzing the slow logs, it is found that all query requests use the `{ alxxxId: 1.0, itemTagList: 1.0 }` index. `keysExamined` and `docsExamined` are both set to `1498` for scan by index; however, the number of returned documents (`nreturned`) is only `3`; that is, only 3 data entries out of the 1498 rows of data and indexes scanned meet the conditions. As can be seen, the key cause compromising the read/write performance is unreasonable index configuration.

>?`keysExamined` and `docsExamined` indicate the numbers of index entries and documents scanned respectively. Larger **keysExamined** and **docsExamined** values indicate that no index is created or the created index is less distinctive.

## Index Optimization Process
### Step 1. Collect the SQL statements
Common business query and update SQL statements as listed below:
```
Query based on `AlxxxId` (user ID) and `itxxxId` (one or multiple values).  
`count` query based on `AlxxxId`.  
Paginated query based on `AlxxxId` by time range (`createTime`). In some queries, `state` and other fields will be concatenated.
Query based on `AlxxxId`, `ParentAlxxxId`, `parentItxxxId`, and `state`.  
Query based on `ItxxxId` (one or multiple values).  
Query based on `AlxxxId`, `state`, and `updateTime`.  
Query based on `AlxxxId`, `state`, `createTime`, and `totalStock` (number of inventory items).  
Query based on `AlxxxId` (user ID), `itxxxId` (one or multiple values), and any other fields.  
Query based on `AlxxxId`, `digitalxxxrmarkId` (watermark ID), and `state`.
Query based on `AlxxxId`, `itemTagList` (tag ID), and `state`.
Query based on `AlxxxId`, `itxxxId` (one or multiple values), and any other fields.
Other queries
```

Common business statistics count SQL statements as listed below:
```
Query based on `AlxxxId`, `state`, and `persxxal`.  
Query based on `AlxxxId`, `state`, and `itemType`.  
Query based on `AlxxxId` (user ID), `itxxxId` (one or multiple values), and any other fields.
```

### Step 2. Get the existing indexes of the cluster
Use `db.xxx.getindex()` to get the collection index information. The query is complex, and there are 30 indexes in total as listed below:
```
{ "alxxxId" : 1, "state" : -1, "updateTime" : -1, "itxxxId" : -1, "persxxal" : 1, "srcItxxxId" : -1 }          
{ "alxxxId" : 1, "image" : 1 }                                                             
{ "itexxxList.vidxxCheck" : 1, "itemType" : 1, "state" : 1 }                                              
{ "alxxxId" : 1, "state" : -1, "newsendTime" : -1, "itxxxId" : 1, "persxxal" : 1 }                           
{ "_id" : 1 }                                                                              
{ "alxxxId" : 1, "createTime" : -1, "checkStatus" : 1 }                                                      
{ "alxxxId" : 1, "parentItxxxId" : -1, "state" : -1, "updateTime" : -1, "persxxal" : 1, "srcItxxxId" : -1 }     
{ "alxxxId" : 1, "state" : -1,  "parentItxxxId" : 1, "updateTime" : -1, "persxxal" : -1 }  
{ "srcItxxxId" : 1 }                                                                        
{ "createTime" : 1 }                                                                       
{ "itexxxList.boyunState" : -1, "itexxxList.wozhituUploadServerId": -1, "itexxxList.photoQiniuUrl" : 1, "itexxxList.sourceType" : 1 }      
{ "alxxxId" : 1, "state" : 1, "digitalxxxrmarkId" : 1, "updateTime" : -1 } 
{ "itxxxId" : -1 }                                                                   
{ "alxxxId" : 1, "parentItxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }                    
{ "alxxxId" : 1, "videoCover" : 1 }                                                        
{ "alxxxId" : 1, "itemType" : 1 }                                                          
{ "alxxxId" : 1, "state" : -1, "itemType" : 1, "persxxal" : 1, "updateTime" : 1 }  
{ "alxxxId" : 1, "itxxxId" : 1 }                                                            
{ "itxxxId" : 1, "alxxxId" : 1 }                                                            
{ "alxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }                                        
{ "alxxxId" : 1, "itemTagList" : 1 }                                                       
{ "itexxxList.photoQiniuUrl" : 1, "itexxxList.boyunState" : -1, "itexxxList.sourceType" : 1, "itexxxList.wozhituUploadServerId" : -1 }           
{ "alxxxId" : 1, "parentItxxxId" : 1, "state" : 1 }                                         
{ "alxxxId" : 1, "parentItxxxId" : 1, "updateTime" : 1 }                                    
{ "updateTime" : 1 }                                                                       
{ "itemPhoxxIdList" : -1 }     
{ "alxxxId" : 1, "state" : -1, "isTop" : 1 }    
{ "alxxxId" : 1, "state" : 1, "itemResxxxIdList" : 1, "updateTime" : -1 }   
{ "alxxxId" : 1, "state" : -1, "itexxxList.photoQiniuUrl" : 1 }  
{ "itexxxList.qiniuStatus" : 1, "itexxxList.photoNetUrl" : 1, "itexxxList.photoQiniuUrl" : 1 }       
{ "itemResxxxIdList" : 1  }
```

### Step 3. Optimize indexes
#### Deleting useless indexes
MongoDB allows you to get the number of hits of each index through the following index statistics command:
```
> db.xxxxx.aggregate({"$indexStats":{}})  
{ "name" : "alxxxId_1_parentItxxxId_1_parentAlxxxId_1", "key" : { "alxxxId" : 1, "parentItxxxId" : 1, "parentAlxxxId" : 1 },"host" : "TENCENT64.site:7014", "accesses" : { "ops" : NumberLong(11236765),"since" : ISODate("2020-08-17T06:39:43.840Z") } }
```
The fields are as described below:
- **name**: The name of the index for which to collect statistics. 
- **ops**: The number of index hits, i.e., the number of times query requests hit an index. If the value of an index is zero or very small, the index is seldom selected as the optimal index and can be considered useless.

Use the index statistics command to get the numbers of hits of all indexes as shown below. If the value of an index is zero or very small, directly delete the index. In addition, as the business has been operated for a period of time, indexes with an `ops` value smaller than 10,000 can also be deleted. At this point, 30 - 11 = 19 useful indexes are retained. 
```
db.xxx.aggregate({"$indexStats":{}})  
{ "alxxxId" : 1, "state" : -1, "updateTime" : -1, "itxxxId" : -1, "persxxal" : 1, "srcItxxxId" : -1 }                      "ops" : NumberLong(88518502)  
{ "alxxxId" : 1, "image" : 1 }                            "ops" : NumberLong(293104)  
{ "itexxxList.vidxxCheck" : 1, "itemType" : 1, "state" : 1 }    "ops" : NumberLong(0)  
{ "alxxxId" : 1, "state" : -1, "newsendTime" : -1, "itxxxId" : -1, "persxxal" : 1 }                                              "ops" : NumberLong(33361216)  
{ "_id" : 1 }                                              "ops" : NumberLong(3987)  
 { "alxxxId" : 1, "createTime" : 1, "checkStatus" : 1 }      "ops" : NumberLong(20042796) 
{ "alxxxId" : 1, "parentItxxxId" : -1, "state" : -1, "updateTime" : -1, "persxxal" : 1, "srcItxxxId" : -1 }                 "ops" : NumberLong(43042796)
{ "alxxxId" : 1, "state" : -1,  "parentItxxxId" : 1, "updateTime" : -1, "persxxal" : -1 }                                  "ops" : NumberLong(3042796)
{ "itxxxId" : -1 }      "ops" : NumberLong(38854593)
{ "srcItxxxId" : -1 }                                "ops" : NumberLong(0)  
{ "createTime" : 1 }                               "ops" : NumberLong(62)  
{ "itexxxList.boyunState" : -1, "itexxxList.wozhituUploadServerId" : -1, "itexxxList.photoQiniuUrl" : 1, "itexxxList.sourceType" : 1 }    "ops" : NumberLong(0)   
{ "alxxxId" : 1, "state" : 1, "digitalxxxrmarkId" : 1, "updateTime" : -1 }                  "ops" : NumberLong(140238342)  
{ "itxxxId" : -1 }                 "ops" : NumberLong(38854593)  
{ "alxxxId" : 1, "parentItxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }    "ops" : NumberLong(132237254)  
{ "alxxxId" : 1, "videoCover" : 1 }        { "ops" : NumberLong(2921857)  
{ "alxxxId" : 1, "itemType" : 1 }          { "ops" : NumberLong(457)  
{ "alxxxId" : 1, "state" : -1, "itemType" : 1, "persxxal" : 1, " itxxxId " : 1 }        "ops" : NumberLong(68730734)  
{ "alxxxId" : 1, "itxxxId" : 1 }       "ops" : NumberLong(232360252)  
{ "itxxxId" : 1, "alxxxId" : 1 }       "ops" : NumberLong(145640252)  
{ "alxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }          "ops" : NumberLong(689891)  
{ "alxxxId" : 1, "itemTagList" : 1 }                    "ops" : NumberLong(2898693682)  
{ "itexxxList.photoQiniuUrl" : 1, "itexxxList.boyunState" : 1, "itexxxList.sourceType" : 1, "itexxxList.wozhituUploadServerId" : 1 }        "ops" : NumberLong(511303207) 
{ "alxxxId" : 1, "parentItxxxId" : 1, "state" : 1 }                "ops" : NumberLong(0)  
{ "alxxxId" : 1, "parentItxxxId" : 1, "updateTime" : 1 }          "ops" : NumberLong(0)  
{ "updateTime" : 1 }                                         "ops" : NumberLong(1397)  
{ "itemPhoxxIdList" : -1 }        "ops" : NumberLong(0)  
{ "alxxxId" : 1, "state" : -1, "isTop" : 1 }       "ops" : NumberLong(213305)  
{ "alxxxId" : 1, "state" : 1, "itemResxxxIdList" : 1, "updateTime" : 1 }       "ops" : NumberLong(2591780)  
{ "alxxxId" : 1, "state" : 1, "itexxxList.photoQiniuUrl" : 1}  "ops" : NumberLong(23505)
{ "itexxxList.qiniuStatus" : 1, "itexxxList.photoNetUrl" : 1, "itexxxList.photoQiniuUrl" : 1 }                  "ops" : NumberLong(0)  
{ "itemResxxxIdList" : 1  }               "ops" : NumberLong(7) 
```

#### Deleting duplicate indexes
- Duplicate indexes caused by the query sequence
  Different developers of the business have written two SQL indexes as shown below. Analysis finds that the two indexes have the same purpose, so only one of them is needed.
```
db.xxxx.find({{ "alxxxId" : xxx, "itxxxId" : xxx }})  
db.xxxx.find({{ " itxxxId " : xxx, " alxxxId " : xxx }}) 
```
- Duplicate indexes caused by the leftmost match rule
Among the `{ itxxxId:1, alxxxId:1 }` and `{ itxxxId :1}` indexes, `{ itxxxId :1}` is a duplicate. 
- Duplicate indexes caused by inclusion
```
{ "alxxxId" : 1, "parentItxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }   
{ "alxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }  
{ "alxxxId" : 1, " state " : 1 }
```

There are three queries for the three indexes: 
```
Db.xxx.find({ "alxxxId" : xxx, "parentItxxxId" : xx, "parentAlxxxId" : xxx, "state" : xxx })  
Db.xxx.find({ "alxxxId" : xxx, " parentAlxxxId " : xx, " state " : xxx }) 
Db.xxx.find({ "alxxxId" : xxx,  " state " : xxx })
```
The queries all contain common fields, so the indexes can be combined into one to serve both types of SQL queries. Below is the combined index: 
```
{ "alxxxId" : 1, " state " : 1, " parentAlxxxId " : 1, parentItxxxId :1}
```
After duplicate indexes are combined and cleared, the following two indexes can be retained:
```
{ itxxxId:1, alxxxId:1 }  
{ "alxxxId" : 1, "parentItxxxId" : 1, "parentAlxxxId" : 1, "state" : 1 }
```

#### Analyzing the index uniqueness to remove duplicate indexes
By analyzing the combination of field modules in the collection data, you can find that the `alxxxId` and `itxxxId` fields are frequently used. By analyzing the schema information and extracting random data, you can find that the combination of these two fields are unique.
It is confirmed that any combination of the two fields represents a unique data entry. Therefore, all combinations of the two fields and any other fields are unique, and the following indexes can be combined into `{ itxxxId:1, alxxxId:1 }`.
```
{ "alxxxId" : 1, "state" : -1, "updateTime" : -1, "itxxxId" : 1, "persxxal" : 1, "srcItxxxId" : -1 }       
{ "alxxxId" : 1, "state" : -1, "itemType" : 1, "persxxal" : 1, " itxxxId " : 1 }   
{ "alxxxId" : 1, "state" : -1, "newsendTime" : -1, "itxxxId" : 1, "persxxal" : 1 }          
{ "alxxxId" : 1, "state" : 1, "itxxxId" : 1, "updateTime" : -1 }       
{ itxxxId:1, alxxxId:1 }
```

#### Optimizing useless indexes caused by non-equi query
As can be seen from the above 30 indexes, some are time fields, such as `createTime` and `updateTime`, which are used for various range queries. Range queries are non-equi queries. If range query fields are placed before index fields, index fields will fail to be indexed as shown below:
```
db.collection.find({{ "alxxxId" : xx, "parentItxxxId" : xx, "state" : xx, "updateTime" : {$gt: xxxxx}, "persxxal" : xxx, "srcItxxxId" : xxx }    })    
 
db.collection.find({{ "alxxxId" : xx, "state" : xx, "parentItxxxId" : xx, "updateTime" : {$lt: xxxxx}, "persxxal" : xxx}    })
```
Both queries contain the `updateTime` field and are range queries. Except the `updateTime` fields, all other fields are equi queries, and fields on the right of `updateTime` cannot use indexes; that is, the `persxxal` and `srcItxxxId` fields of the first index and the `persxxal` field of the second index cannot be matched with indexes. 

Set the following two indexes for the two queries:
```
{ "alxxxId" : 1, "parentItxxxId" : -1, "state" : -1, "updateTime" : -1, "persxxal" : 1, "srcItxxxId" : -1 }   
{ "alxxxId" : 1, "state" : -1,  "parentItxxxId" : 1, "updateTime" : -1, "persxxal" : -1 }
```

As the fields of the two indexes are basically the same, the indexes can be optimized into the following index to ensure that more fields can be matched:
```
{ "alxxxId" : 1, "state" : -1,  "parentItxxxId" : 1,  "persxxal" : -1, "updateTime" : -1 }
```

#### Removing indexes of infrequently queried fields
Indexes with less than 10,000 hits are removed when you delete useless indexes. However, compared with indexes with billions of hits, some indexes still have a relatively lower number of hits (like hundreds of thousands). Such indexes contain `image` and `videoCover` fields respectively as shown below:
```
{ "alxxxId" : 1, "image" : 1 }          "ops" : NumberLong(293104)    
{ "alxxxId" : 1, "videoCover" : 1 }     "ops" : NumberLong(292857)   
```

Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). On the **Slow Log Query** tab, lower the slow log latency threshold and analyze the logs of the two queries as shown below: 
```
Mon Aug  2 10:56:46.533 I COMMAND  [conn5491176] command xxxx.tbxxxxx command: count { count: "xxxxx", query: { alxxxId: "xxxxxx", itxxxId: "xxxxx", image: "http:/xxxxxxxxxxx/xxxxx.jpg" },   limit: 1 } planSummary: IXSCAN { itxxxId: 1.0,alxxxId:1.0 } keyUpdates:0 writeConflicts:0 numYields:1 reslen:62 locks:{ Global: { acquireCount: { r: 4 } }, Database:   { acquireCount: { r: 2 } }, Collection: { acquireCount: { r: 2 } } } protocol:op_query 4ms  

Mon Aug  2 10:47:53.262 I COMMAND  [conn10428265] command xxxx.tbxxxxx command: find { find: "xxxxx", filter: { $and: [ { alxxxId: "xxxxxxx" }, { state: 0 }, { itemTagList: { $size: 0 } } ] }, limit: 1, singleBatch: true } planSummary: IXSCAN { alxxxId: 1, videoCover: 1 } keysExamined:128 docsExamined:128 cursorExhausted:1 keyUpdates:0 writeConflicts:0 numYields:22 nreturned:0 reslen:108 locks:{ Global:{ acquireCount: { r: 46 } }, Database: { acquireCount: { r: 23 } }, Collection: { acquireCount: { r: 23 } } } protocol:op_command 148ms  
```
- `image` field: It is used together with `alxxxId` and `itxxxId` for combined query. However, the combination of `alxxxId` and `itxxxId` is already unique, and the `image` field is totally not indexed, so the `{ "alxxxId" : 1, "ixxxge" : 1 }` index can be deleted.
- `videoCover` field: By analyzing logs, it can be found that `videoCover` is not in the query conditions, only part of queries match the `{ alxxxId: 1, videoCover: 1 }` index, and `keysExamined` and `docsExamined` are different from `nreturned`. Therefore, it can be confirmed that only the `alxxxId` index field is matched, and the `{ alxxxId: 1, videoCover: 1 }` index can also be deleted.

#### Analyzing frequent queries in logs to add optimal index
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb). On the **Slow Log Query** tab, lower the slow log latency threshold. Use mtools to analyze queries for a period of time, and you can get the following information about frequent queries: 
![](https://qcloudimg.tencent-cloud.cn/raw/1d451566569f5721a563f61781246ccd.png)
These frequent queries account for more than 99% of queries. By analyzing their logs, you can get information similar to the following:
```
Mon Aug  2 10:47:58.015 I COMMAND  [conn4352017] command xxxx.xxx command: find { find: "xxxxx", filter: { $and: [ { alxxxId:"xxxxx" }, { state: 0 }, { itemTagList: { $in: [ xxxxx ] } }, { persxxal: 0 } ] }, projection: { $sortKey: { $meta: "sortKey" } },  sort: { updateTime: 1 }, limit: 3, maxTimeMS: 10000 } planSummary: IXSCAN { alxxxId: 1.0, itexxagList: 1.0 } keysExamined:1327 docsExamined:1327 hasSortStage:1 cursorExhausted:1 keyUpdates:0 writeConflicts:0 numYields:23 nreturned:3 reslen:12036 locks:{ Global: { acquireCount: { r: 48 } }, Database: { acquireCount: { r: 24 } }, Collection: { acquireCount: { r: 24 } } } protocol:op_command 151ms  
```
As can be seen from the log, the frequent query matches the `{ alxxxId: 1.0, itexxagList: 1.0 }` index, and there is a huge difference between the numbers of scanned data rows and returned rows: 1327 vs. 3.

The index is sub-optimal. The frequent query is a four-field equi query, and only two fields are indexed. In this case, you can optimize the index as follows: `{ alxxxId: 1.0, itexxagList: 1.0 , persxxal:1.0, stat:1.0}`.

In addition, the log also shows that the frequent query actually has a `sort` and a `limit`. Below is the entire raw query SQL statement:
```
db.xxx.find({ $and: [ { alxxxId:"xxxx" }, { state: 0 }, { itexxagList: { $in: [ xxxx ] } },{ persxxal: 0 } ] }).sort({updateTime:1}).limit(3)  
```

The query model consists of a common multi-field equi query, `sort` query, and `limit`, so the optimal index of the query can be one of the following two indexes: 
- Index 1: Index for a common multi-field equi query
Analyze the query conditions:
```
{ $and: [ { alxxxId:"xxx" }, { state: 0 }, { itexxagList: { $in: [ xxxx ] } }, { persxxal: 0 } ] }
```
All four fields of the SQL statement are equi queries. Create the optimal index based on the hash, and place fields from left to right by value hash. You can get the following optimal index: 
```
{ alxxxId: 1.0, itexxagList: 1.0 , persxxal:1.0, stat:1.0}
```
If you use the index as the optimal index, the execution process of the entire common multi-field equi query, `sort` query, and `limit` is as detailed below:
  - Use the `{ alxxxId: 1.0, itexxagList: 1.0 , persxxal:1.0, stat:1.0}` index to find all data entries meeting the conditions specified by `{ $and: [ { alxxxId:"xxxx" }, { state: 0 }, { itexxagList: { $in: [ xxxx ] } }, { persxxal: 0 } ] }`.
  - Perform memory sorting on the data entries meeting the conditions.
  - Get the first three data entries after sorting.
- Index 2: Optimal index of the equi query and `sort`
The `sort` query has a `limit`. Find the frequent sorting SQL statement, which is as shown below:
```
{ $and: [ { alxxxId:"xxxx" }, { state: 0 }, { itexxagList: { $in: [ xxxx ] } }, { persxxal: 0 } ] }.sort({updateTime :1}).limit(10) 
```
As the query is extremely frequent, we recommend you add the following index to such SQL statements:
```
{ alxxxId: 1.0, itexxagList: 1.0 , persxxal:1.0, stat:1.0, updateTime : 1}  
```

### Step 4. Sort out the final indexes to be retained
The following indexes are retained after the above optimization steps:
```
{ "itxxxId" : 1, "alxxxId" : 1 }       
{ "alxxxId" : 1, "state" : 1, "digitalxxxrmarkId" : 1, "updateTime" : 1 }  
{ "alxxxId" : 1, "state" : -1,  "parentItxxxId" : 1, "persxxal" : -1, "updateTime" : 1 } { "alxxxId" : 1, "itexxxList.photoQiniuUrl" : 1, }                       
{ "alxxxId" : 1, "parentAlxxxId" : 1, "state" : 1"parentItxxxId" : 1}       
{ alxxxId: 1.0, itexxagList: 1.0 , persxxal:1.0, stat:1.0, updateTime:1}   
{ "alxxxId" : 1, "createTime" : -1}
```

## Index Optimization Benefits
- CPU resource usage is reduced by over 90%.
  After optimization, the peak CPU utilization is reduced from over 90% to below 10%.

- Disk I/O resource usage is reduced by over 85%.
  Disk I/O utilization is reduced from 60%–70% to below 10%.

- Disk storage costs are reduced by 20%.
  Each index has an index file in the disk. After 30 indexes are reduced to 8, the final actual disk usage of data entries and indexes is reduced by about 20%.

- Slow logs are reduced by 99%.
  Before index optimization, thousands of slow logs are generated per second. After optimization, only dozens are generated per second.
  
