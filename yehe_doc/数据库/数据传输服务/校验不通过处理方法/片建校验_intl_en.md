
## Check Details
- Check requirement: if the target database is a sharded instance, you can preset the shardkey in it. If the table shardkeys in the source and target databases are different, an warning will be triggered. It will not block the task but will affect the business. You need to assess and determine whether to ignore the warning.
- Impact on the business: if some shardkeys are different, the migration or sync task will fail.

## Fix
If the target database has preset shardkeys, run the following command to shard the source database:
```
sh.shardCollection("<database>.<collection>", { <shard key> : "hashed" } , false, {numInitialChunks: number of preset chunks}) 
```
Run the verification task again.

