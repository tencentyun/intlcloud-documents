## Business Background

In a TencentDB for MongoDB sharded cluster, multiple mongos nodes are available for receiving connection query requests from all client applications, routing the requests to the corresponding shards in the cluster, and splicing the received responses back to the clients. You can connect the cluster to a load balancer through one or multiple VIPs, so that the traffic is automatically distributed among the mongos nodes to increase the data processing capacity, throughput, availability, and flexibility of the network.

## How Load Balancing Works

A user program connects to a load balancer (through VIP) to block multiple real server IPs (RSIPs). The load balancing service of TencentDB for MongoDB routes different request source IPs to different mongos nodes through a 5-tuple hash policy (source IP, source port, target IP, target port, and communication protocol). In case of an RSIP change on the backend, an automated process will be initiated to change the mappings between the VIP and RSIPs, which is easy and imperceptible to the business.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e0c2ef0cbb30645548307a25481563c1.png"  style="zoom:70%;">

#### `getMore` problem during batch scan
If MongoDB could not return all the `find` results at a time, it will first return the first batch of data and `cursorID`, through which the client constantly calls `getMore` to iterate the remaining data. Therefore, a batch scan request may correspond to one `find` request and multiple `getMore` requests and associate the `find` request with returned `getMore` results through `cursorID`. 

- Each mongos node maintains a global [ClusterCursorManager](https://github.com/mongodb/mongo/blob/r4.2.11/src/mongo/s/query/cluster_cursor_manager.h#L72) in the memory and maintains the mapping between `cursorID` and `ClusterClientCursor` through [HashMap](https://github.com/mongodb/mongo/blob/r4.2.11/src/mongo/s/query/cluster_cursor_manager.h#L721). `cursorID` is a random int64 number, and `ClusterClientCursor` maintains the execution plan, current status, and other information of a request. 

- If the query result cannot be returned at a time (for example, it exceeds the limit of 16 MB), a `cursorID` other than `0` will be generated, which will be [registered in the ClusterCursorManager](https://github.com/mongodb/mongo/blob/r4.2.11/src/mongo/s/query/cluster_cursor_manager.cpp#L263-L328) together with `ClusterClientCursor` itself.
If the client needs subsequent results, it can send `getMore` requests carrying the returned `cursorID` value, and mongos will [find the cached ClusterClientCusor](https://github.com/mongodb/mongo/blob/r4.2.11/src/mongo/s/query/cluster_cursor_manager.cpp#L330-L383), continue to execute the query plan, and return subsequent results. The ID and cursor information independently exist on each mongos node.

Therefore, be sure to send the `find` request and the associated `getMore` requests to the same mongos node. If a `getMore` request is sent to a different mongos node, the cursor cannot be found, and the `CursorNotFound` error will be returned:
<img src="https://qcloudimg.tencent-cloud.cn/raw/e499837ef4f0a56adb20f8a42e3ecfcb.jpg"  style="zoom:50%;">

#### Transaction operation issue
MongoDB 4.2 supports distributed transactions, so you can connect to a mongos node to initiate transaction operations. You can perform multiple [read/write operations](https://www.mongodb.com/docs/manual/core/transactions-operations/) between `startTransaction` and `commitTransaction`/`abortTransaction`. mongos records the metadata carried in each request in a transaction such as `logicalSessionId` and `txnId` to maintain the context. Therefore, [MongoDB is designed](https://github.com/mongodb/mongo/blob/master/src/mongo/db/s/README.md#transactions) to guarantee that each operation in a transaction is sent to the same mongos node.

#### TencentDB for MongoDB load balancing policy

To address the `getMore` problem during batch scan and transaction operation issue, the TencentDB for MongoDB load balancing hash policy balances traffic based on the IP information of the accessing client (generally a CVM instance); that is, all requests from the same source IP will be routed to the same mongos node, which ensures that `getMore` and transaction operations are processed in the same context.

This policy works well for the production environment with many access IPs. However, when there are only a few access IPs, particularly in stress test scenarios, it tends to cause mongos load imbalance.

## Solution to mongos Load Imbalance

If you don't want to use the default TencentDB for MongoDB load balancing policy, you can enable the mongos access address. Under the current VIP of the instance, the system will bind different vports to different mongos nodes, so you can flexibly control the distribution of mongos requests. In addition, if a mongos node fails, the system will bind its VIP and vport to a new mongos process, which will not change the VIP and vport or affect the original load balancer address. For detailed directions, see [Enabling Mongos Access Address](https://intl.cloud.tencent.com/document/product/240/49126).

- After enabling the mongos access address, you can view it in **Access Address** in the **Network Configuration** section on the **Instance Details** page in the console, which displays connection strings of different connection types. Each connection string is configured with all mongos nodes in the instance, and the `authSource`, `readPreference`, and `readPreferenceTags` parameters are used to determine which type of node to access:  
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/gpSX725_4-en.png)

- To implement traffic balancing, you can directly copy a connection string and configure it in the application used to connect the client to the database SDK to access the corresponding mongos nodes. For more information on the connection method, see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092). However, as a connection string is long, proceed with caution.

- Note that if you configure all mongos nodes in a connection string, after you adjust the number of mongos nodes in the instance, you need to update the connection string in the application.

