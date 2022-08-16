Data engines empower the data analysis and computing service in Data Lake Compute. They are used in all computing operations and can be public or private based on your needs.
## Public engine
The Data Lake Compute service comes with the shared public engine, which is applicable to low-frequency analysis use cases with small data volumes. With this highly flexible and available engine, you don't need to configure or manage resources. Fees are charged by the scanned data volume of running tasks. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1155/48652).

Since Data Lake Compute adopts serverless architecture, it needs to schedule the data engine for task execution for the first time over a period of time, which may take a longer time.

## Private engine
A private engine is a dedicated data engine that you purchase on a pay-as-you-go basis. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1155/48652).
- Pay-as-you-go: This billing mode is highly flexible and stable, where fees are charged by the CU usage. It is applicable to use cases where data is analyzed regularly, with compute resources elastically scaled based on the business load.
- Monthly subscription: This billing mode is applicable to use cases where large amounts of data require long-term and stable analysis, with compute resources elastically scaled based on the business load. It guarantees always available resources with no need to wait for resource startup. Fees are charged by month based on the cluster specification (elastic clusters are billed by CU usage though).

## Compute engine types
A private engine can work with different compute engines in different use cases.
- SparkSQL: It is suitable for stable and efficient offline SQL tasks.
- Spark job: It is suitable for native Spark stream/batch data job processing.
- Presto: It is suitable for agile and fast interactive query and analysis.

>! The compute engine type does not affect the unit price of a private engine.

## Engine scaling rules
- Basic rule: Data engine scaling may occur only if the configured maximum cluster count is larger than the minimum cluster count.
- Scale-out rule: The system will scale out a data engine as configured when queuing tasks cannot be accommodated by the idle concurrency and no clusters are being initialized.
- Scale-in rule: The system will terminate clusters that have been idle for a certain period of time when the current cluster count is larger than the minimum cluster count of a data engine.

>! The cluster count of a data engine cannot be smaller than the minimum cluster count. A pay-as-you-go cluster can be suspended if it is not needed.

## Engine running status
A cluster may be in one of the following eight statuses: Starting, Running, Suspended, Suspending, Changing configuration, Isolated, Isolating, Recovering.
- Starting: The cluster is being started. In this case, a pay-as-you-go private engine is not billed. A starting cluster cannot be selected for data computing.
- Running: The cluster is running and can be selected for data computing.
- Suspended: The cluster is suspended and cannot be selected for data computing.
- Suspending: The cluster is being suspended and cannot be selected for data computing. This will affect running tasks.
- Changing configuration: The cluster is undergoing a configuration change and cannot be selected for data computing.
- Isolated: The cluster is isolated due to overdue payments and cannot be selected for data computing.
- Isolating: The cluster is being isolated due to overdue payments and cannot be selected for data computing. This will affect running tasks.
- Recovering: The cluster is being recovered from the **Isolated** status to the **Running** status after the account is topped up. It cannot be selected for data computing.

