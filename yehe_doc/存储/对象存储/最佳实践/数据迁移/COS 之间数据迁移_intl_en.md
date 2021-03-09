## Background

If you are using COS and need to migrate data in a bucket within COS, you are advised to use either of the following migration methods:

- Online migration: [Migration Service Platform (MSP)](#msp)
- Online migration: [Cross-bucket replication](#replication)



## Migration Practice

<span id="msp">

#### MSP

MSP is a platform that integrates multiple migration tools and provides a visual interface to help you easily monitor and manage large-scale data migration tasks. The "File Migration Tool" can help you migrate data from various public clouds and data origin servers to COS.

The steps are as follows:

1. Log in to the [MSP console](https://console.cloud.tencent.com/msp).
2. Click **Object Storage Migration** in the left sidebar.
3. Click **Create a Task** to create a task and configure the task as needed.
4. Start the task.

For more information, please see [Migrating Between Tencent Cloud COS](https://intl.cloud.tencent.com/document/product/1036/33184).

During data migration, how fast the source data can be read depends on the network, and selecting a higher QPS concurrence when creating a file migration task will speed up the migration.

<span id="replication">

#### Cross-Bucket replication

COS introduces the cross-bucket replication feature, with which you can set a rule to automatically and asynchronously replicate **incremental objects** in buckets residing in different regions. If cross-bucket replication is enabled, COS will precisely replicate object content (for example, object metadata and version ID) in the source bucket to the destination bucket, where the replica’s attributes will be identical to those of the source. Moreover, operations on the source objects, for example, object upload and object deletion, will also be replicated to the destination bucket. For more information, please see [Cross-Bucket Replication](https://intl.cloud.tencent.com/document/product/436/19237).


