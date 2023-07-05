### What is the difference between read-only, replica, and disaster recovery instances?
- Read-only instance: it only allows the read operation and is deployed in the same region as the source instance. A source instance can have up to 5 read-only instances.
- Replica instance: It is used to back up the database and deployed in the same region as the source instance. A source instance can have 1 or 2 replica instances.
- Disaster recovery instance: It provides cross-AZ and cross-region disaster recovery capabilities. A source instance can have up to 1 disaster recovery instance.

### Why can't I select a specific AZ when creating a read-only instance?
If you can't select an AZ, it means that there are no resources in this AZ. You can choose another AZ as displayed on the actual purchase page, which will not affect your use of the read-only instance.

### Can I select an AZ different from that of the source instance when creating a read-only instance?
Yes. When creating a read-only instance, you can choose to create a new RO group for it and select an AZ different from that of the source instance. However, if you select an existing RO group, the AZ of the new read-only instance can only be the same as that of the selected existing RO group, which may not necessarily be the same as that of the source instance.

### Can I connect a TencentDB for MySQL read-only instance via the public network?
Read-only instances can be connected via public and private networks.

### How often does a TencentDB for MySQL source instance sync data with a disaster recovery instance?
After sync is enabled and initial sync is completed, the source instance and disaster recovery instance will sync data in real time.

### Can I add a temp instance to TencentDB for MySQL?
This operation is currently not supported.

### Why would instance upgrade fail?
If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.

### Can I sync real-time data in two instances with an intra-city active-active architecture configured?
For this purpose, you can purchase [disaster recovery instances](https://www.tencentcloud.com/document/product/236/7272) in the TencentDB for MySQL console.
