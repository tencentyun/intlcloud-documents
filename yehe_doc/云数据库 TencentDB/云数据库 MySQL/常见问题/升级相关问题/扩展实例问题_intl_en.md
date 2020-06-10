### What is the difference between read-only, slave, and disaster recovery instances?
- Read-only instance: only allows read access, and is deployed in the same region as the master instance. A master instance can have up to 5 read-only instances.
- Slave instance: is used to back up databases, and deployed in the same region as the master instance. A master instance can have 1 or 2 slave instances.
- Disaster recovery instance: provides disaster recovery capabilities across availability zones and regions. A master instance can have up to 1 disaster recovery instance.

### Can a TencentDB for MySQL read-only instance connect to the public network?
Read-only instances can connect to both public and private networks.

### How often does a TencentDB for MySQL master instance sync with a disaster recovery instance?
After sync is enabled and initial sync is completed, the master instance and disaster recovery instance will sync their data in real time.

### Can a temp instance be added to TencentDB for MySQL?
Not supported for the time being.

### Why would instance upgrade fail?
If the number of tables in a single instance exceeds one million, upgrade may fail, and database monitoring may be affected. Please control the number of tables in a single instance appropriately and make sure that it is below one million.

