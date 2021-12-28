## Restoring a Physical Backup to a Self-built Database
A replica set instance has only one copy of data, while each shard of a sharding cluster has one copy of data. Please restore your data according to your business needs. This document describes how to restore a single copy of data.

### Restoring Data to a Single Node
1. Copy the data to an empty data directory in the self-built database, such as /data/27017/.
```
cp -r * /data/27017/
```
2. Restart mongod and check the data. Below is a command sample:
```
./mongod --dbpath /data/27017 --port 27017 --logpath /var/log/mongodb/27017.log --fork
```

### Restoring Data to a Replica Set
As a physical backup retains the configuration of the original instance by default, the original configuration needs to be removed first; otherwise, the data may become inaccessible.
1. Restore the data to a single-node self-built database and then restart the node in the form of replica set. Below is a command sample:
```
./mongod --replSet mymongo --dbpath /data/27017 --port 27017 --logpath /var/log/mongodb/27017.log --fork
```
2. Log in to the node and remove the replica set configuration of the original instance by running the following command:
```
rs.slaveOk()
use local
db.system.replset.remove({})
```
3. Restart the node, add a node to the replica set, initialize it, and check the data. The node added to the replica set should have been started with no data contained. Below is a command sample:
```
rs.initiate({"_id":"mymongo","members":[{"_id":0,"host":"127.0.0.1:27017"},{"_id":1, "host":"127.0.0.1:27018"},{"_id":2, "host":"127.0.0.1:27019"}]})
```
For more information on the `rs.initiate()` command, see [MongoDB Manual](https://docs.mongodb.com/manual/reference/method/rs.initiate/?spm=a2c4g.11186623.2.14.7baa7af8xkobmk).

> Data cannot be restored to a sharding cluster. As the route of physical backup is missing in a sharding cluster, mongos can only read the data of the master shard even if the data of each shard is restored to the self-built replica set (each shard of the sharding cluster).


## Restoring a Logical Backup to a Self-built Database
- To avoid any impact on data check after the data is restored to a self-built database, the self-built database must be empty.
- For v3.6, you need to delete the `config` directory manually and then run the `mongorestore` command to restore the data of each shard as shown below: ![](https://main.qcloudimg.com/raw/2ed5ed6172e17b5d6120d2572427e7fb.png)
- For v3.2, you need to merge all the files in individual tables manually before restoring the data. Below is a file merge operation sample:
The `c_10` table is in the `ycsb` directory in the database and contains data files from `c_10.bson.gz.chunk-64` to `c_10.bson.gz.chunk-127`. The merge command is `cat c_10.bson.gz.chunk-* > ./c_10.bson.gz`.
>?In some use cases, TencentDB for MongoDB v3.2 may have chunks.

Run the `mongorestore` command to restore the data, where the `-h` parameter specifies the self-built database address, `--dir` specifies the directory of the data file, and `--gzip` must be specified to decompress the backup file. The command is as follows:
```
./mongorestore  --gzip --drop -h127.0.0.1:27017 --dir ./1544517027220146694 --oplogReplay ./oplog.bson
```
