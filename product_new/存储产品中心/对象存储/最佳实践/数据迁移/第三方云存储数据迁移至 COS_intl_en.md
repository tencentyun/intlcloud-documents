## Background

COS offers the following two migration methods to help you quickly migrate data in a non-Tencent Cloud storage platform to COS.


| Migration Method | Interactivity | Threshold for Large/Small Files | Concurrence | HTTPS Secure Transfer |
| ------------------------------------------------------------ | -------------------------- | ------------------ | ------------------------------ | -------------------------------------- |
| [Migration Service Platform (MSP)](#msp) | Visual operations | Default configuration | The same for all files | Enabled |
| [COS Migration](#cos) | Non-visual operations by modifying configuration files | Customizable | Different for large and small files | Optional; disabling it can speed up migration |


Both migration methods support viewing data migration progress, checking file consistency, uploading again after failure, resuming upload from breakpoint and other features, which can meet your basic migration requirements. However, the two differ in interactivity, specific features, and other aspects as shown in the table above. You can choose an appropriate method in light of the comparisons.


## Migration Practice

<span id=msp>

### Migration Service Platform (MSP)

MSP is a platform that integrates multiple migration tools and provides visual interfaces to help you monitor and manage large-scale data migration tasks with ease. The File Migration Tool on it can help you migrate data from various public clouds or data origin servers to COS.

The steps are as follows:

1. Log in to [MSP](https://console.cloud.tencent.com/msp).
2. Click **Migration Tool** on the left sidebar, locate "File Migration Tool", and click **Get Started**.
3. Create a migration task and configure task information.
4. Start the task.

For more information, please see the following documents:

- [Migrating from Alibaba Cloud OSS](https://cloud.tencent.com/document/product/659/37855)
- [Migrating from Qiniu KODO](https://cloud.tencent.com/document/product/659/38008)
- [Migrating from UCLOUD UFile](https://cloud.tencent.com/document/product/659/38003)
- [Migrating from Kingsoft Cloud KS3](https://cloud.tencent.com/document/product/659/38007)
- [Migrating from Baidu Cloud BOS](https://cloud.tencent.com/document/product/659/38006)
- [Migrating from AWS S3](https://cloud.tencent.com/document/product/659/38799)

#### Tips

During data migration, how fast the data source can be read depends on the network connection, and selecting a higher QPS concurrence value when creating a file migration task will help speed up the migration.





<span id=cos>

### COS Migration 

COS Migration is an all-in-one tool integrating COS data migration features. You can migrate data to COS quickly after completing simple configurations.

The steps are as follows:

1. Install the Java environment.
2. Install the COS Migration tools.
3. Modify the configuration file.
4. Launch the tool.

For more information, please see [COS Migration Tool](https://intl.cloud.tencent.com/document/product/436/15392).

#### Tips

Below describes how to configure COS Migration to maximize the migration speed:

1. Adjust the threshold and concurrence of large/small files based on your network environment to implement optimal migration where large files are split into multiple parts and small files are transferred concurrently. Adjust the tool execution time and set a bandwidth limit to ensure that bandwidth usage by data migration will not affect your business operations. Such adjustments can be made by modifying the following parameters in the `[common]` section of the `config.ini` configuration file:
<table>
   <tr>
      <th>Parameter Name</td>
      <th>Parameter Description</td>
   </tr>
   <tr>
      <td>smallFileThreshold</td>
      <td>Threshold for small files. If the size of a file is higher than or equal to this threshold, multipart upload will be used. The default value is 5 MB.</td>
   </tr>
   <tr>
      <td>bigFileExecutorNum</td>
      <td>Concurrence of large files, which is 8 by default. <br>If COS is connected to over the public network with low bandwidth, reduce this value.</td>
   </tr>
   <tr>
      <td>smallFileExecutorNum</td>
      <td>Concurrence of small files, which is 64 by default.<br>If COS is connected to over the public network with low bandwidth, reduce this value.</td>
   </tr>
   <tr>
      <td>executeTimeWindow</td>
      <td>This parameter defines the time range when the migration tool will execute a task every day, which will enter sleep mode at other times. In sleep mode, the migration will be paused and the migration progress will be retained until the next time window when the migration will be resumed automatically.</td>
   </tr>
</table>
2. Distributed parallel transfer can further speed up the migration. You can install COS Migration on multiple servers and perform migration tasks separately for different data sources.



