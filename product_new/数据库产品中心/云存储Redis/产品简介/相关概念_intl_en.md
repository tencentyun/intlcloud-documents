
TencentDB for Redis generally involves the following concepts:

**Instance**: A database environment running independently in Tencent Cloud. One database instance can contain multiple user-created databases.

[**VPC**](https://cloud.tencent.com/document/product/215/20046): A custom virtual network space that is logically isolated from other resources.

[**Security group**](https://cloud.tencent.com/document/product/239/30911): Security access control to Redis instances by specifying IP, protocol, and port rules for instance access.

[**Region and availability zone**](https://cloud.tencent.com/document/product/239/4106): The physical location of a Redis instance and other resources.

[** Tencent Cloud Console**](https://console.cloud.tencent.com/cdb): Web-based UIs.

[**Project**](https://cloud.tencent.com/document/product/378/10863): A feature developed to enable developers to better manage Tencent Cloud products based on the concept of projects. You can implement project management by assigning different Tencent Cloud products to different projects.

[**Read-write separation**](https://cloud.tencent.com/document/product/239/19543): TencentDB for Redis supports read-write separation for business scenarios with more reads but less writes, which can well cope with read requests concentrating on hotspot data. It supports up to 1-master 5-slave mode to offer 5x read performance.
