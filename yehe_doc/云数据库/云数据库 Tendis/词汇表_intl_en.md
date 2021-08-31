

### Read-only replica
Transactional operations such as creation, modification, and deletion are taken care of by the primary instance, while queries are processed by read-only replicas.

### Region
TencentDB data centers are hosted in multiple locations world wide. These locations are known as regions. Each region is an independent geographic area containing multiple isolated availability zones (AZs).

### Availability zone
Availability zones (AZs) refer to Tencent Cloud's physical data centers that are in the same region. Each AZ is independently powered and have its own network resources. They are designed to ensure that failures within one AZ can be isolated from other zones, thereby ensuring service availability and business stability, excepting the occurrences of large-scale disasters or major power failures. Users can protect their applications from being affected by failures that occur in a single location by selecting instances in independent AZs.

### QPS
Queries per second (QPS) is a metric measuring how much traffic is processed by a particular query server within the specified period of time.

### Instance
A database instance is a standalone database environment that runs in the cloud.




