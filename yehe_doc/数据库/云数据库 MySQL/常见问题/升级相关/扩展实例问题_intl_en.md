
### What are the differences between read-only, replica, and disaster recovery instances?
- Read-only instance: It only allows the read operation and is deployed in the same region as the source instance. A source instance can have five read-only instances at most.
- Replica instance: It is used to back up the database and deployed in the same region as the source instance. A source instance can have one or two replica instances.
- Disaster recovery instance: It provides cross-AZ and cross-region disaster recovery capabilities. A source instance can have one disaster recovery instance at most.

### Can a TencentDB for MySQL read-only instance be accessed over the public network?
Read-only instances can be accessed over both public and private networks.

### How often does a TencentDB for MySQL source instance sync data with a disaster recovery instance?
After sync is enabled and initial sync is completed, the source instance and disaster recovery instance will sync data in real time.

### Can a temporary instance be added to TencentDB for MySQL?
Temporary instances cannot be added currently.

### Why does instance upgrade fail?
If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.

### How do I sync real-time data in two instances with an intra-region active-active architecture configured?
You can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the TencentDB for MySQL console.
