## Overview
There are multiple ways to migrate data in COS. You can choose how to migrate data based on different scenarios. This document summarizes several ways of migration for typical scenarios as well as the operation steps and techniques, to help users migrate data to COS efficiently and securely.

| Migration Type | Migration Method |
| -------- | ------------------------------------------------------------ |
| Online Migration | [COS Migration ](#cos), [Migration Service Platform (MSP)](#msp), [COS Origin-Pull](#huiyuan) |
| Offline Migration | [Cloud Data Migration (CDM)](#cdm) |

## Migration Scenario

### 1. Local data migrating to COS
COS supports the following migration methods to help users who have a local IDC migrate their massive local data to COS.

- Online migration: [COS Migration](#cos)
- Offline Migration: [Cloud Data Migration (CDM)](#cdm)

You can determine how to migrate data according to data volume for migration, IDC egress bandwidth, IDC idle machine resources, acceptable completion time of migration and other factors. The following figure shows the estimated time of online migration. We can see that if the migration exceeds 10 days or the amount of migrated data is more than 50 TB, it is recommended to select [Cloud Data Migration (CDM)](#cdm) for offline migration. Otherwise online migration is the best choice.
![](https://main.qcloudimg.com/raw/b07948f0626973d2d64753df39add6f4.png)
>**Note:**
>Data migration may be affected by the high number of files smaller than 1 MB, insufficient performance of disk IO, etc.

### 2. Data on third-party cloud storage migrating to COS
If you use a third-party cloud storage and want to implement data migration across the cloud platform, there are two migration methods available in COS:

- Online Migration: [COS Migration ](#cos), [Migration Service Platform (MSP)](#msp)


Both of these migration methods support to view data migration progress, check file consistency, upload again after failure, resume upload from breakpoint and other features, which can meet users' basic migration requirements. However, the two migration methods differ in terms of interactive form and features, as shown in the following table. You can select an appropriate method to migrate data according to the following table. Note that you need to apply for the permission to migrate data on MSP.

| Migration Method | Interactive Form | Threshold for Small Files | Migration Concurrence | HTTPS Secure Transfer |
| ---------------- | -------------------------- | ------------------ | ------------------------------ | -------------------------------------- |
| COS Migration | Modify configuration files in a non-visualized manner | Custom settings | Define concurrence for large files and small files | Select whether to enable it. It can be speeded up when it is disabled. |
| Migration Service Platform (MSP) | Visualized operations | Default settings | Global unified | Enable |

### 3. Data migrating to COS with URL as the source address

If you want to migrate data using the URL list as the data source address, COS support has the following 3 ways:

- Online Migration: [COS Migration ](#cos), [Migration Service Platform (MSP)](#msp), [COS Origin-Pull](#huiyuan)

For COS Migration and MSP, you can refer to Scenario 2 above. In the process of cloudification from the origin server, if you only want to migrate the hot data in the origin server to the cloud while the cold data remains in the source station, you can use [COS origin-pull](#huiyuan), which migrates the hot data accessed by read/write requests to COS, and automatically separates the service data with low frequency.

### 4. Data migration between COS
If you are using COS and want to migrate data in a bucket to another bucket under the same account (or other accounts in another region), you can use cross-region duplication in COS to migrate data. This feature has not been launched yet, but will be coming soon.

## Migration Practice

### <span id="cos"> COS Migration </span>

COS Migration is an all-in-one tool integrating COS data migration features. You can migrate data to COS quickly after simple configurations.

The migration operation has the following steps:

1. Install the Java environment
2. Install the COS Migration tools
3. Modify the configuration file
4. Start the tools

For more details, see [COS Migration documentation](https://cloud.tencent.com/document/product/436/15392).
#### Tips

Here describes how to configure COS Migration to maximize the migration speed:

1. Adjust the threshold of small files and the migration concurrence according to the network, enabling to upload large files in parts and transfer small files concurrently.
  In the `[common]` segment of the configuration file `config.ini`, modify the parameter `smallFileThreshold` (default setting is 5 MB), then any file that is larger than or equal to this threshold will be uploaded in parts. Modify the concurrence parameters `bigFileExecutorNum` (default setting is 64 for large files) and `smallFileExecutorNum` (default setting is 8 for small files). If COS is connected through an external network and the bandwidth is small, reduce the concurrence.

2. Adjust the execution time of the tool and set the bandwidth limit to ensure the operation of your service is not affected when part of the bandwidth is occupied by the migrated data.
  In the `[common]` segment of the configuration file `config.ini`, modify the parameter `executeTimeWindow` which defines the working time of the migration tool. During other time, migration goes into sleep mode, and it is suspended with migration progress retained. It resumes execution automatically until the next time window.

3. Distributed parallel transfer can further speed up the migration. You can install COS Migration on multiple machines and performing separate migration tasks for different sources.


### <span id="msp"> Migration Service Platform (MSP)</span>

MSP is a platform that integrates multiple migration tools and provides a visual interface to help you easily monitor and manage large-scale data migration tasks. The "File Migration Tool" can help you migrate data from various public clouds and data origin servers to COS.

The migration operation has the following steps:

1. You can find and enable the **File Migration Tool** in **Migration Tools** via the navigation bar on the console.
2. Create a new migration task and configure task information.
3. Start the task.

For more information, see [Migration Tools](https://cloud.tencent.com/document/product/659/15313).
#### Tips

During the data migration, how fast the data source can be read depends on the network. However, if you select a high QPS concurrence when creating a file migration task, this will speed up the migration.


### <span id="cdm">Cloud Data Migration (CDM)</span>

CDM uses the dedicated offline migration device provided by Tencent Cloud to help you migrate local data to the cloud. It can solve the problems that the local IDC migrates to cloud through network: long time, high cost and low security.

The migration operation has the following steps:

1. Go to the CDM Console to submit an application.
2. After the application is approved, you can wait to receive the device.
3. After receiving the device, copy the data to it according to the migration device manual.
4. Submit an return application on the console and wait for Tencent Cloud to migrate data to COS.

For more information, see [Cloud Data Migration (CDM)](https://cloud.tencent.com/document/product/623).

#### Tips

Here describes how to efficiently and securely migrate data to Tencent Cloud COS offline.

1. Configure a 10 Gbps network in IDC. To prevent the local data environment from becoming a transmission bottleneck, you can prepare a high-performance machine as a mount point to maximize the replication speed.
2. Parallel transfer is the fastest way to transfer data in CDM. The CPU and memory usage of the device are monitored. If the current migration speed is lower than expected, you can select the following methods:
 - Multiple devices connect to the same CDM device through different network interfaces.
 - Multiple devices connect to several CDM devices through different network interfaces.

### <span id="huiyuan">COS Origin-Pull</span>

COS Origin-Pull automatically migrates data with read/write access requests from the origin server to Tencent Cloud COS. This can not only help you to separate hot data from cold data quickly, but also increase the read/write speed of hot data in business systems.

The migration operation has the following steps:

1. Go to the COS Console, and enable the origin-pull setting in the destination bucket of the data to be migrated.
2. Configure the bucket origin-pull address and save.
3. Transfer the read and write requests in business systems to Tencent Cloud COS.

For more information, see [Origin-Pull Settings](https://cloud.tencent.com/document/product/436/13310) in the console.

#### Tips

The following steps demonstrate how to separate the hot data and cold data. The hot data is seamlessly migrated to Tencent Cloud COS to increase the speed of reading hot data.

1. Switch the read/write requests in business systems to COS. Enable the origin-pull setting in COS Console. Configure the data origin server as the source address. The system structure is shown in the following figure.
  ![](https://main.qcloudimg.com/raw/c30ed0391380420007bf9e2d89df89eb.png)

2. After a period of time, the cold data remains in the origin server, but the hot data has been migrated to Tencent Cloud COS. The business systems are not affected during migration.

