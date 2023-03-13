TencentDB for MySQL supports parallel query. After this feature is enabled, large queries can be automatically identified. The parallel query capability leverages multiple compute cores to greatly shorten the response time of large queries.

## Concept
Parallel query uses more computing resources to complete the query workload. The traditional query method is relatively friendly to small amounts of data (hundreds of gigabytes), but as the business grows, the data volume has reached the TB level in many cases, which exceeds the processing capacity of traditional databases. Parallel query is designed to solve this problem. During parallel query, the data is distributed to different threads at the storage layer, multiple threads on a single node process the data in parallel, the result pipelines are aggregated to the main thread, and the main thread performs a simple merge and returns the result. This greatly improves the query efficiency.

## Feature background
TencentDB for MySQL goes beyond traditional MySQL databases in terms of computing, storage, disaster recovery, and elastic expansion; however, it still faces the following challenges:
- As the internet develops, databases become more capable of storing data, and forms are carrying more and more data. When it comes to big table queries, SQL statements tend to be slow due to existing technical bottlenecks, which adversely affects the business process.
- The current market environment sees an increasing number of report statistics and other analytical queries. Although not large in number, they involve a high data volume and are quite sensitive to query time. Gradually, data analysis capability, especially heterogeneous data processing, has become a must-have.

The above challenges are caused by the traditional technical implementation mode in the MySQL ecosystem. In particular, open-source releases support only the single-thread query mode, where only one thread (called user thread) is responsible for the parsing, optimization, and execution of a SQL statement. This mode cannot make full use of the hardware resources of modern multi-core CPUs and large memory devices, leading to a resource waste.

Therefore, it is important to streamline analysis and enhance performance by using multi-core services in the query of a large amount of data, which is also the key to query acceleration, cost reduction, and efficiency improvement.

## Strengths
- **Performance enhancement at no extra costs**: You can upgrade the kernel capabilities at no extra costs, so that you can get the most out of the instance CPU computation for quicker statement response and higher computing performance.
- **Support for common statements**: You can use most common SQL statements in virtually any business scenarios. This helps you accelerate your business smoothly.
- **Flexible parameter settings**: You have many parameters at hand to control the conditions of enabling or disabling parallel query. This helps you make queries smarter and more adaptable to your business scenarios with no transformation needed.
