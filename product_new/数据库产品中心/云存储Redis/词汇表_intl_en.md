

### Read-only Replica
Transactional operations such as creation, modification, and deletion are taken care of by the master instance, while queries are processed by read-only instances.

### Region
Managed data centers of TencentDB are distributed in multiple locations around the world, which are composed of regions and availability zones. Each region is an independent geographical region and has multiple mutually isolated availability zones.

### Availability Zone
Availability zones refer to Tencent Cloud's physical IDCs in a region with independent power supply and network resources. They are designed to ensure that failures within an availability zone can be isolated (except for major natural disasters or power failures) without spreading to and affecting other zones, so as to ensure business stability and continuity. By starting an instance in an independent zone, you can protect your applications from being affected by the failures occurring in one single location.

### QPS
Queries per second (QPS) is a metric measuring how much traffic is processed by a particular query server within the specified period of time.

### Instance
A database instance is a standalone database environment that runs in the cloud.




