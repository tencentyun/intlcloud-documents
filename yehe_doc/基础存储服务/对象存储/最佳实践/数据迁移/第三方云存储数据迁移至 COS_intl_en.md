## Background

If you use a third-party cloud storage platform, COS can help you quickly migrate your data from that platform to COS.


| Migration Method | Interactivity | Threshold for Large/Small Files | Concurrence | HTTPS Secure Transfer |
| ------------------------------------------------------------ | -------------- | ------------------ | ---------- | -------------- |
| [Migration Service Platform (MSP)](#msp) | Visual operations | Default configuration | Same for all files | Enabled |


This tool allows you to view the data migration progress, check file consistency, upload again after failure, and use checkpoint restart and other features, which can meet your basic migration requirements.


## Migration Practices

<span id=msp></span>

### MSP

MSP is a platform that integrates multiple migration tools and provides visual UIs to help you monitor and manage large-scale data migration tasks with ease. The File Migration Tool on it enables you to migrate data from various public clouds or data origins to COS.

The steps are as follows:

1. Log in to the [MSP console](https://console.cloud.tencent.com/msp).
2. Click **Object Storage Migration** on the left sidebar.
3. Click **Create Task** to create a task and configure it as needed.
4. Start the task.

For more information, see the following documents:

- [Migrating from Alibaba Cloud OSS](https://intl.cloud.tencent.com/document/product/1036/35578)
- Migrating from Huawei OBS
- Migrating from Qiniu KODO
- Migrating from UCloud UFile
- Migrating from Kingsoft Cloud KS3
- Migrating from Baidu AI Cloud BOS
- [AWS S3 Migration Tutorial](https://intl.cloud.tencent.com/document/product/1036/32522)

#### Tips

During data migration, how fast the data source can be read depends on the network connection, and selecting a higher QPS concurrency value during file migration task creation helps speed up the migration.

<span id=cos>



