## Check Details
- Check requirements: in a MongoDB migration task, if the source database is a sharded database, you need to enter the `mongos`, `config server`, and `mongod` node information.
- Check description: the information of the `mongos`, `config server`, and `mongod` nodes cannot be disordered; otherwise, data migration will also be disordered; for example, the `mongos` node information should not be entered in the box for the `mongod` node. Note that you only need to enter the information of one `mongod` node for each shard.

## Fix
- Enter the correct node information in the DTS task configuration items.
- Enter only one `mongod` for each shard.
