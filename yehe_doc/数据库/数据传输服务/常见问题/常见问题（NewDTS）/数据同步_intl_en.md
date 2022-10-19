
### Will the sync service be affected if high availability (HA) switch occurs between the source and target instances?
- If the source instance supports and enables global transaction identifier (GTID), when HA switch occurs in the source instance during incremental sync, the service will be automatically reconnected, and the synced data flow will resume soon after HA switch is completed.
- If HA switch occurs in the target instance during incremental sync, the service will also be automatically reconnected, and the synced data flow will resume soon after HA switch is completed.

### Can data in an instance on a later version be synced to an instance on an earlier version?
No. For data sync between instances of the same type, the major version of the target instance must be later than that of the source instance. Taking MySQL as an example, data cannot be synced from MySQL 5.7 to MySQL 5.6.

### Can the source/target instance be a local instance?
Yes. Data can be synced from TencentDB to a local database. Supported access types for such sync include public network and CCN.

### Can I perform two-way sync for DDL statements in a two-way sync topology?
No. During sync instance creation, DDL statements in only one instance can be synced; otherwise, the algorithm will detect a DDL loop and then prohibit the creation of one of the instances.

### Are non-transactional engines supported?
The current technical solution adds the routing information to transactions to mark transaction sources, which relies on the atomicity of transactions. However, such atomicity of databases/tables based on non-transactional engines is corrupted, and the data consistency cannot be guaranteed. Therefore, we recommend you not use non-transactional engines.
