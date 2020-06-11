## Background

To migrate your bucket data within COS, we recommend that you use the following methods:

- Online migration: [Migration Service Platform](#msp)
- Online migration: [Cross-Region Replication](https://intl.cloud.tencent.com/document/product/436/19237)

With a cross-region replication rule, COS can asynchronously automate incremental replication of objects across buckets in different regions. COS replicates the exact object content, including object metadata and version ID, along with the exact object operations, such as adding or deleting an object, from the source bucket to the destination bucket.

## Migration Practice

<span id="msp">

#### Migration Service Platform (MSP)

MSP is a user-friendly platform that integrates multiple migration tools to help you easily monitor and manage large-scale data migration tasks. The "File Migration Tool" can particularly help you migrate data from various public clouds and data origin servers to COS.

The steps are as follows:

1. Log in to the [MSP Console](https://console.cloud.tencent.com/msp).
2. Click **Object Storage Migration** in the left sidebar.
3. Click **Create a Task** to configure a new migration task.
4. Start the task.

For more information, see [Migration within Tencent Cloud COS](https://intl.cloud.tencent.com/document/product/1036/33184).

During data migration, how fast the data source can be read from depends on the network connection, and selecting a higher QPS concurrence value when creating a file migration task will help speed up the migration.
