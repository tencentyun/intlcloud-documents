Cloud Native Database TDSQL-C (TDSQL-C for MySQL) is a new-generation enterprise-grade distributed cloud database developed by Tencent Cloud. It features high performance and availability and combines the strengths of traditional databases, cloud computing, and cutting-edge hardware technologies. It is compatible with MySQL and PostgreSQL and able to achieve a high throughput of over one million QPS and a massive distributed smart storage capacity of 128 TB, comprehensively ensuring data security and reliability.



## Architecture
### Customized kernel
The deeply customized database kernel of TDSQL-C for MySQL empowers many enterprise-grade features and optimizations. It serves Tencent Cloud's internal users and external users at the level of hundreds of terabytes as the cornerstone of supporting the smooth operations of key businesses.

### Log as a database
TDSQL-C for MySQL is a computable smart storage service. Its distributed storage system automatically manages multiple data replicas to implement auto scaling, fault check, and repair. It adopts the concept of log as a database, which truly sinks the redo logs to the storage layer and minimizes the network I/O.

### Service-Oriented architecture
The architecture of TDSQL-C for MySQL is based on existing Tencent Cloud services such as COS, CBS, CVM, VPC, and TGW.

### Mix of software optimization and new hardware
Through SPDK- and RDMA-based zero copy technologies, TDSQL-C for MySQL reduces the performance losses caused by OS context switching and data copying between user mode and kernel mode, further optimizes the system performance at critical paths, and minimizes the request delay.

## Core Design Concepts
Cloud native: TDSQL-C for MySQL is service-oriented.
Creative: TDSQL-C for MySQL separates computing and storage and implements the concept of log as a database.
Comprehensive: TDSQL-C for MySQL is fully compatible with new open-source databases.
Cohesive: TDSQL-C for MySQL features minimalist software optimizations to release the hardware dividend.
Cost-Effective: TDSQL-C for MySQL doubles the database performance and is pay-as-you-go.
