### How do I select the instance specification?
- For functional testing in TDSQL for MySQL with no special performance requirements: 2 shards with 2 GB of memory and 25 GB of disk capacity each.
- In initial business stage when the total size of data is small but grows fast: 2 shards with 16 GB of memory and 200 GB of disk capacity each.
- In stable development stage when sharding is based on actual business demands: 4 shards, and the specification for each equals current business peak x growth rate / 4.
For more information on instance specifications, please see [Selecting TDSQL for MySQL Instance and Shard Configurations](https://intl.cloud.tencent.com/document/product/1042/33354).

### What are the differences between TDSQL for MySQL syntax and traditional MySQL syntax?
Currently, you cannot configure user permissions with command lines. Instead, you need to log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/dcdb) to do so.
Currently, TDSQL for MySQL does not support custom functions, views, triggers, foreign keys, etc.
For more information on the compatibility with MySQL's syntax, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1042/33356).

### What does the shardkey do?
- We recommend that you specify the shardkey field in a SELECT statement when querying a sharded table. The proxy can route a SQL request to the corresponding shard based on the hash value of the shardkey field; otherwise, the request needs to be sent to all shards in the cluster for execution, and then the proxy aggregates all the result sets returned by the shards, which lowers the efficiency of execution.
- You need to specify the shardkey field in an INSERT or REPLACE statement when querying a sharded table; otherwise, the SQL statement is not allowed to execute, because the proxy does not know which shard this SQL statement should be routed to.
- You need to specify the shardkey field in the WHERE condition in a DELETE or UPDATE statement when querying a sharded table; otherwise, for security reasons, this SQL statement is not allowed to execute.

### How do I select the shardkey?
The shardkey is a data table field used to generate the sharding rules during horizontal sharding, which should be specified when creating a table. In TDSQL for MySQL, we recommend that the shardkey be the field of the data on which most (or core) database operations are performed. Such a table sharding solution is called group-shard, as shown below:
![](https://main.qcloudimg.com/raw/f0a5b31d7c69eb34b84dbc9d57b5201a.png)
Group-shard solution can ensure that some of the associated data and complex business logical operations of different sharded tables can be aggregated into one physical shard. For example, if both the order table and user table of an e-commerce platform are sharded based on the `UserID`, it is quick to calculate how many orders a user has recently placed through join queries (without cross-node joins or distributed transactions).

Some typical cases of shardkey selection are as follows:
 - For user-based Internet applications, most (or core) database operations are based on users, so the field corresponding to user data can be used as a shardkey.
 - For e-commerce applications or O2O applications, most (or core) database operations are based on sellers and buyers, so the field corresponding to seller or buyer data can be used as a shardkey. In the case where super sellers account for the vast majority of transactions, the load and pressure on some shards will increase significantly.
 - For game applications, most (or core) database operations are based on players, so the field corresponding to player data can be used as a shardkey.
 - For Internet of Things (IoT) applications, most (or core) database operations are based on IoT information, so the field corresponding to the data of sensors, independent devices, or IMEIs of SIM cards can be used as a shardkey.
 - For taxation/industry and commerce/social insurance applications, most (or core) database operations of frontend businesses are based on the information of taxpayers, legal representatives, and residents, so the field corresponding to the data of taxpayers or legal representatives can be used as a shardkey.
In most other types of cases, the field of the data on which most (or core) database operations are based can be found in the same way, but there are certain restrictions on the selection of shardkey. For more information, please see [Shardkey Selection Restrictions](https://intl.cloud.tencent.com/document/product/1042/38506).

### Can the shardkey be changed?
Once selected, the shardkey cannot be changed. If you want to modify the shardkey of a table, you need to create a new table.
To modify a shardkey value in a row of a sharded table, you need to INSERT a new value and DELETE the old one. You cannot UPDATE it.
