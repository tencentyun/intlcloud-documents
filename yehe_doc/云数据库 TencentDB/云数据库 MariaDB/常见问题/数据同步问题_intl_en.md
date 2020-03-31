### Task Verification Failure
Possible causes:
- The account or password of the target instance is incorrect.
- The network is disconnected; for example, the firewall or security group blocks the egress IP of the sync tool, and cross-network access is not supported currently.
- The target instance does not exist.

Solution: check the above causes and make adjustments accordingly.

### Long Delay of Sync Task
Possible causes:
- The transaction on the source instance is large. Data sync is to sync data from the slave. As in a binlog, the timestamp of each transaction is the start time of the transaction, if there is a large transaction, the reported timestamp for data sync will still be the start time of the transaction even in concurrent sync.
- There is a delay in the slave; for example, DDL replay attacks or read-only accounts cause high pressure and delay on the slave, leading to database sync delay.

Solution: check whether there are large transactions or batch processing operations. If the delay persists after a period of time, please contact us for troubleshooting.

### Extra Data After Data Sync
Possible causes: write lock is not enabled for the target instance and some additional data is written to it; the corresponding table may lack a primary key; therefore, when the sync tool sends a request again, part of the data will be written to the target instance again.

Solution: add a primary key to the source table, delete existing data from the target table, and sync the data again. Or, you can manually delete extra data from the target table.

### Writable Target Database
Data sync does not lock the target database, which can still be read from/written to normally. Therefore, please manipulate the target database with caution.

### DDL Replay Failure
Possible causes: the source and target database are on different versions, leading to differences in DDL syntax.

Solution: manually run the DDL statements again in the target database.

### Database Sync Failure with Missing or No Data in the Corresponding Table
Possible causes: the account required by sync or the table structure of the target database is modified.

Solution: pause the sync task, modify the corresponding account, change the table structures of the target and source databases to the same, and perform sync again.
