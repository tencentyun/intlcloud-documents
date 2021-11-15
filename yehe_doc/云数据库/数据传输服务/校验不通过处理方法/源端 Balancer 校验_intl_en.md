
## Check Details
- Check requirements: if the source database is a sharded instance, you need to disable the balancer in it before you can start migration.
- Check description: an incremental migration task will get the oplog. If the balancer is enabled, `moveChunk` in the source database may cause data inconsistency in the target database.

## Fix
1. Log in to the source database.
2. Run the following command to disable the source database balancer:
```
sh.stopBalancer()
sh.getBalancerState()
```
3. Run the verification task again.

