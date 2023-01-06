This document describes the background of the parallel query capability of TDSQL-C for MySQL, which helps improve the efficiency in querying large tables with a large amount of computed data.

## Feature background
Traditional MySQL-based relational databases still face storage redundancy and lack elastic loading after cloud-native transformation and cloud deployment. In contrast, TDSQL-C for MySQL adopts the "log as a storage" architecture to separate computing from storage and allows compute nodes to share underlying storage through the distributed file system. This reduces user costs, makes compute nodes stateless, and implements elastic expansion and failover of computing resources within seconds.

TDSQL-C for MySQL goes beyond traditional MySQL-based relational databases in terms of computing, storage, disaster recovery, and elastic expansion; however, it still faces the following challenges:
- As the internet develops, cloud-native databases become more capable of storing data, and TDSQL-C for MySQL can store petabytes of data. Forms are carrying more and more data, with some containing terabytes of data online. When it comes to large table queries, SQL statements tend to be slow due to existing technical bottlenecks, which adversely affects the business process.
- The current market environment sees an increasing number of AP queries, such as report statistics and other analytical queries. Although not large in number, they involve a high data volume and are quite sensitive to query time. Gradually, data analysis capability, especially heterogeneous data processing, has become a must-have.

The above challenges are caused by the traditional technical implementation mode in the MySQL ecosystem. In particular, open-source releases support only the single-thread query mode, where only one thread (called user thread) is responsible for the parsing, optimization, and execution of a SQL statement. This mode cannot make full use of the hardware resources of modern multi-core CPUs and large memory devices, leading to a resource waste.

Therefore, it is important to streamline analysis and enhance performance by using multi-core services in the query of a large amount of data, which is also the key to query acceleration, cost reduction, and efficiency improvement. This is the so-called **parallel query (PQ)**, one of the core techniques to build HTAP product forms.

## Strengths
- **Performance enhancement at no extra costs**: You can upgrade the kernel capabilities at no extra costs, so that you can get the most out of the instance CPU computation for quicker statement response and higher computing performance.
- **Transparent process monitoring**: You can use various metrics to monitor the parallel query, so that you can keep track of any exceptions and keep your cluster running stably.
- **Support for common statements**: You can use most common SQL statements in virtually any business scenarios. This helps you accelerate your business smoothly.
- **Flexible parameter settings**: You have many parameters at hand to control the conditions of enabling or disabling parallel query. This helps you make queries smarter and more adaptable to your business scenarios with no transformation needed.
