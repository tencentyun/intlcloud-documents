TDSQL-C for MySQL is a new-generation cloud native relational database developed by Tencent Cloud. It combines the strengths of traditional databases, cloud computing, and cutting-edge hardware technologies to provide elastic scalable database services featuring high performance, security, and reliability, as well as full compatibility with MySQL 5.7 and 8.0. It can deliver a high throughput of over one million QPS and a smart storage capacity up to the petabyte level, fully ensuring data security and reliability.

TDSQL-C for MySQL uses an architecture where computing and storage resources are separated and all compute nodes share the same data. It supports configuration adjustment and disaster recovery within seconds. A single node can sustain millions of QPS, automatically maintain data and backups, and roll back gigabytes of data per second.

TDSQL-C for MySQL delivers high stability, reliability, performance, and scalability like commercial databases while featuring simplicity, openness, and efficient iteration like open-source cloud databases. Its engine is fully compatible with native MySQL, so you can migrate MySQL data to it without modifying any application code or configuration.

## Product Architecture Features
**Computing/Storage separation and shared distributed storage**
The design concept of computing/storage separation is leveraged to meet the need for elastic business expansion. Compute nodes share the underlying storage through the distributed file system, which reduces the storage costs.

**Single-write-multiple-read and read/write separation**
A TDSQL-C for MySQL cluster uses the multi-node architecture with one source node (readable and writable) and at least one read-only node.

**Customized kernel**
The deeply customized database kernel actualizes enterprise-grade features and optimizations. It not only deeply optimizes the InnoDB storage engine, query performance, and replication performance, but also improves the ease of use and maintainability of the product. While providing all the benefits of MySQL, it offers more enterprise-grade advanced features such as disaster recovery, restoration, monitoring, performance optimization, read/write separation, transparent data encryption, and auditing.

**Log as a database**
The distributed storage system automatically manages multiple data replicas to implement auto scaling, fault check, and repair. It adopts the concept of log as a database, which truly sinks the redo logs to the storage layer and minimizes the network I/O.

**Mix of software optimization and new hardware**
The product architecture and technical implementation have been continuously optimized based on the features of new hardware. The optimal hardware access mode integrating CPU access scheduling, hardware access granularity, and AEP is established, which further optimizes the system performance at critical paths and minimizes the request delay.

## Core Design Concepts
**Cloud native: TDSQL-C for MySQL is service-oriented.**
TDSQL-C for MySQL is built on Tencent Cloud's existing efficient and stable cloud services. It allows you to quickly build cloud databases featuring high performance, availability, and reliability.

**Creative: TDSQL-C separates computing and storage and implements the concept of log as a database.**
TDSQL-C for MySQL implements the architecture of "log as a database" and separates computing (CPU and memory) from storage. Through considerable modification of the MySQL kernel, it removes unnecessary feature modules and implements stateless compute nodes, enabling elastic scaling and disaster recovery within seconds for computing resources. Moreover, it is built on Tencent Cloud's distributed cloud storage, empowering the pooling of storage resources.

**Comprehensive: TDSQL-C is fully compatible with new open-source databases.**
TDSQL-C for MySQL is fully compatible with open-source MySQL and will regularly implement support for new versions. This allows you to smoothly migrate the query, application, and tool capabilities of your existing database almost without modifying the code, which notably reduces the costs and risks of data migration.

**Cohesive: TDSQL-C features minimalist software optimizations to release the hardware dividend.**
TDSQL-C for MySQL has been effectively improved in performance and stability through optimizations of the database kernel and system architecture. Compared with database products using traditional architectures, it delivers a better performance under the same hardware configuration, releases the hardware dividend first, and perfectly adapts to the trends in new hardware to maximize the database service efficiency.

**Cost-Effective: TDSQL-C doubles the database performance and is pay-as-you-go.**
Since cloud computing itself is actually a cost-effective service, TDSQL-C for MySQL can be truly pay-as-you-go and elastically scalable as a cloud database solution that outperforms traditional databases while being less expensive.

## Pricing
For more information, visit the [TDSQL-C for MySQL purchase page](https://buy.intl.cloud.tencent.com/cynosdb?regionId=8#/).

## How to Use TDSQL-C for MySQL
You can create TDSQL-C for MySQL clusters, databases, and accounts in the following ways:
- [Console](https://console.cloud.tencent.com/cynosdb): It offers easy-to-use web-based GUIs.
- [API](https://intl.cloud.tencent.com/document/product/1098/40725): All operations in the console can be performed through APIs.
