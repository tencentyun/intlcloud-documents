Data Lake Compute provides Spark-based batch and flow computing capabilities for you to perform complex data processing and ETL operations through data jobs.
Currently, data jobs support the following versions:
- Scala 2.12
- Spark 3.1.2

## Preparations
Before starting a data job, you need to create a data access policy to ensure data security as instructed in [Configuring Data Access Policy](https://intl.cloud.tencent.com/document/product/1155/49494).
Currently, only CKafka data source is supported for data job configuration, with more data sources to come in the future.

## Billing mode
A data job is billed by the data engine usage. Currently, pay-as-you-go and monthly subscription billing modes are supported. For more information, see [Data Engine Overview](https://intl.cloud.tencent.com/document/product/1155/48681).
- Pay-as-you-go: It is applicable to scenarios with a small number of data jobs or periodic usage. A data job is started after creation and automatically suspended after successful execution, after which no fees will be incurred.
- Monthly subscription: It is applicable to scenarios where a large number of data jobs are regularly executed. Resources are reserved in this mode, so you don't need to wait for data engine start.
>! As a data job differs from a SQL job in terms of the compute engine type, you need to purchase a separate data engine for Spark jobs; otherwise, you can’t run data jobs on a SparkSQL data engine.
>

## Job management
On the **Data job** management page, you can create, start, modify, and delete a data job.
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select **Data job** on the left sidebar.
2. Click **Create job**. For detailed directions, see [Creating Data Job](https://intl.cloud.tencent.com/document/product/1155/49495).
3. In the list, you can view the current task status of the data job. You can also manage the job as instructed in [Managing Data Job](https://intl.cloud.tencent.com/document/product/1155/49496).
