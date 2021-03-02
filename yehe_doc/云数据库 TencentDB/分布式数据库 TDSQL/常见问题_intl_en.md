### How do I select the instance specification?
- For functional testing in TDSQL for MySQL with no special performance requirements: 2 shards with 2 GB of memory and 25 GB of disk capacity each.
- In initial stage of business when the total size of data is small but grows fast: 2 shards with 16 GB of memory and 200 GB of disk capacity each.
- In stable development stage when sharding is based on actual business conditions: 4 shards, and the specification for each one should be current business peak * growth rate / 4.
For more information on instance specification, please see [TDSQL for MySQL Instance and Shard Configuration](https://intl.cloud.tencent.com/document/product/1042/33354).

### Is TDSQL for MySQL syntax compatible with MySQL? Are there any limitations?
For the current version of TDSQL for MySQL, you cannot configure user permissions on the command line. Instead, you need to log in to [console](https://console.cloud.tencent.com/dcdb) to do so.
The current version of TDSQL for MySQL does not support features such as custom function, view, trigger, foreign key, and subquery.
For more information on the compatibility with MySQL syntax, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1042/33356).

### What does the shardkey do?
When you use a sharded table, you are recommended to perform the SELECT operation with the shardkey, so that the route will be automatically redirected to the corresponding shard, achieving a higher efficiency. You can also perform the operation without the shardkey, but the system will automatically perform a full-table scan, which is less efficient.
When you use a sharded table, the shardkey must be included in an INSERT/REPLACE or DELETE/UPDATE operation; otherwise, the operations will be rejected. An INSERT/REPLACE operation requires the shardkey to be specified, indicating the location of the physical shard where the data is to be inserted. A DELETE/UPDATE operation requires the shardkey to be specified as a means of validation to avoid accidental deletion.

### How do I select the shardkey?
The shardkey is a data table field used to generate the splitting rules during horizontal splitting (sharding), which should be specified when the table is created. For TDSQL for MySQL, you are recommended to find the entity of the data in the data table on the business logic, determine that the majority or core part of database operations are performed around the data of the entity, and then use the field corresponding to the entity as the shardkey for sharding (this scheme is called Group-Shard) as shown below:
![](https://main.qcloudimg.com/raw/f0a5b31d7c69eb34b84dbc9d57b5201a.png)
Group-Shard ensures that some correlated data entries and complex business logic computation in different sharded tables can be aggregated into one physical shard. For example, if both the order table and user table of an ecommerce platform are sharded by `UserID`, then the platform can quickly calculate how many orders a user has recently placed through join queries (with no cross-node joins or distributed transactions caused).

Below are some typical application scenarios for shardkey selection:
 - For a user-oriented internet application, it involves various operations in the user dimension, so the business logic entity is user, and the field corresponding to user can be used as the shardkey.
 - For an ecommerce or O2O application, it involves various operations in the seller/buyer dimension, so the business logic entity is seller/buyer, and the field corresponding to seller/buyer can be used as the shardkey. However, please note that in some cases, several super-large sellers may account for the majority of transactions, resulting in significantly higher load and pressure on certain shards.
 - For a game application, it involves various operations in the player dimension, so the business logic entity is player, and the field corresponding to player can be used as the shardkey.
 - For an IoT application, it involves various operations in the IOT information dimension, so the business logic entity is sensor/SIM card, and the field corresponding to IMEI of sensor, independent device, or SIM card can be used as the shardkey.
 - For a taxation/business administration/social insurance application, it mainly involves frontend business in the taxpayer/legal representative/resident information dimension, so the business logic entity is taxpayer/legal representative/resident, and the field corresponding to taxpayer/legal representative/resident can be used as the shardkey.
For most other types of application scenarios, the most appropriate business logic entity can be determined in the same way. Please note that there are certain restrictions on the selection of shardkey. For more information, please see [Shardkey Selection Restrictions](https://intl.cloud.tencent.com/document/product/1042/33379).

### Can the shardkey be changed?
Once selected, the shardkey should not be arbitrarily changed. If you want to modify the shardkey of a table, you can do so only by creating another table.
If you want to modify the shardkey value in a row in a sharded table, you need to perform an INSERT operation first and then perform a DELETE operation. Direct UPDATE operations cannot modify the shardkey value.

### Are distributed joins and transactions supported?
For now, TDSQL only supports joins and transactions under a single shardkey and cross-node transactions but not cross-node joins.
