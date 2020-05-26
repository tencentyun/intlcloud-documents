
### Can a TencentDB for MySQL read-only instance be accessed over the public network?
Read-only instances can be accessed over both public and private networks.

### How often does a TencentDB for MySQL master instance sync with a disaster recovery instance?
After sync is enabled and initial sync is completed, the master instance and disaster recovery instance will sync their data in real time.

### Can a temp instance be added to TencentDB for MySQL?
Temp instances cannot be added currently.

### Why would instance upgrade fail?
If the number of tables in a single instance exceeds one million, upgrade may fail, and database monitoring may be affected. Please control the number of tables in one single instance appropriately and make sure that it is below one million.

