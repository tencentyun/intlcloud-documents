## Preparations 
Before creating a data job, you need to configure the CAM role arn to secure the data access from the data job. For detailed directions, see [Configuring Data Access Policy](https://intl.cloud.tencent.com/document/product/1155/49494).

## Directions
1. Log in to the [Data Lake Compute console](https://console.cloud.tencent.com/dlc) and select **Data job** on the left sidebar.
2. Click **Create job**.
![]()

Configure parameters as follows:

| Parameter | Description |
|---------|---------|
| Job name	| It can contain up to 40 letters, digits, and underscores. |
| Job type	| **In batch**: Batch data jobs based on Spark JAR<br>**In flow**: Flow data jobs based on Spark Streaming |
| Data source connection| Data source for **In batch** data jobs. Currently, it can only be CKafka, which needs to be configured in advanced in **Job configuration**.|
| Data engine	| It can be a Spark job data engine for which you have the permission.<br>If you select **Data source**, you can only select a data engine connected to the data source. |
| Program package	| The JAR format is supported.<br>You can select a local file of up to 5 MB in size or a file in COS. If the local file exceeds 5 MB, upload it to COS for use. You can directly enter a COS path. |
| Dependency JAR resource	| The JAR format is supported. You can select multiple resources. <br>You can select a local file of up to 5 MB in size or a file in COS. If the local file exceeds 5 MB, upload it to COS for use. You can directly enter multiple COS paths and separate them by semicolon. |
| Dependency file resource	| You can select a local file of up to 5 MB in size or a file in COS. If the local file exceeds 5 MB, upload it to COS for use. You can directly enter multiple COS paths and separate them by semicolon. |
| CAM role arn	| The data access policy configured in **Job configuration**, which specifies the scope of data accessible to a data job. For more information, see [Configuring Data Access Policy](https://intl.cloud.tencent.com/document/product/1155/49494).|
| Main class | 	JAR package parameter in the main class. Separate multiple parameters by space. |
| Job parameter	| `-config` information of the job, which starts with `spark.` in the format of `k=v`. Separate multiple parameters by line break.<br>Example: spark.network.timeout=120s |
| Resource configuration	| The engine resources that can be configured with the data job, the number of which cannot exceed the specifications of the selected data engine. Resource description: 1 CU ≈ 1-core 4 GB MEM<br>Billable CUs = executor resource * executor quantity + driver resource <br>Pay-as-you-go data engines are billed by the billable CUs. |

3. After configuring the parameters, click **Save**.
