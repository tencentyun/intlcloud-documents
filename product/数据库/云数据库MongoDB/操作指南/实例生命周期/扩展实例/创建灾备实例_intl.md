### Overview 
TencentDB for MongoDB allows you to create one or more disaster recovery instances for use cases with special regulation or reliability requirements. It is a cost-effective way to ensure continuous and reliable services. 

>!
- Creating read-only instances is currently being whitelisted. Please submit a ticket to use the service.
- Due to delay in data synchronization, disaster recovery instances may not synchronize the data in real-time.  You can find the synchronization latency between the disaster recovery instances and the master instance on the console. 

### How does it work 
Changes on the master instance can be synced to read-only instances using oplog. Each read-only instance have at least 1 master and 2 slaves. Disaster recovery instances can be activated as soon as the master instance fails to recover read and write abilities.

### Limitation
 - Backup and rollback: Not supported.
 - Data migration: Do not support migrating data to read-only instances.
 - Database management: Do not support creating and deleting a database.
 - Account management: Do not support creating/deleting accounts, resetting passwords and authorizing accounts.
 - Up to 3 disaster recovery instances allowed for each master instance.
 - Only prepaid (monthly/yearly subscription) master instances can create disaster recovery instances.
 - The engine of a disaster recovery instance is consistent with that of the master instance.
- Due to network isolation, you cannot create disaster recovery instances in finance zones for master instances in common regions, and vice visa.


