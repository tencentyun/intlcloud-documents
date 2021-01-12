## Background

If you want to migrate data using a URL list as the data source address, COS supports the following three ways:
<table>
   <tr>
      <th>Migration Method</th>
      <th>Description</th>
   </tr>
   <tr>
	 <td nowrap="nowrap"><a href="#msp">Migration Service Platform (MSP)</a></td>
      <td>MSP is a platform that integrates multiple migration tools and provides visual interfaces to help you monitor and manage large-scale data migration jobs with ease. The File Migration Tool on it can help you migrate data from various public clouds or data origin servers to COS.</td>
   </tr>
   <tr>
	 <td><a href="#huiyuan">COS Origin-Pull</a></td>
      <td>COS origin-pull automatically migrates data with read/write access requests from the data origin server to COS. This can help you separate hot data from cold data quickly and speed up reads/writes of hot data in your business system.</td>
   </tr>
   <tr>
	 <td><a href="#cos">COS Migration</a></td>
      <td>COS Migration is an all-in-one tool integrating COS data migration features. You can migrate data to COS quickly after completing simple configurations.</td>
   </tr>
</table>

In the process of migrating data from the origin server to the cloud, if you only want to migrate hot data while leaving the cold data in the origin server, you can use [COS origin-pull](#huiyuan), which migrates the hot data accessed by read/write requests to COS and automatically separates the business data with low access frequency.


## Migration Practice
<span id=msp>

### Migration Service Platform (MSP)

The steps are as follows:

1. Log in to [MSP](https://console.cloud.tencent.com/msp).
2. Click **Migration Tool** on the left sidebar, locate **File Migration Tool**, and click **Use Now**.
3. Create a migration task and configure task information.
4. Start the task.

For more information, please see [Migrating from a URL List](https://intl.cloud.tencent.com/document/product/1036/33185).


#### Tips

During data migration, how fast the data source can be read from depends on the network connection, and selecting a higher QPS concurrence value when creating a file migration task will help speed up the migration.

<span id=huiyuan>

### COS origin-pull



The steps are as follows:

1. Log in to the COS Console and enable the origin-pull setting in the destination bucket.
2. Configure the bucket origin-pull address and save the configuration.
3. Redirect the read/write requests from your business system to COS.

For more information, please see [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508).

#### Tips

The following steps demonstrate how to separate hot data and cold data. Hot data can be seamlessly migrated to COS for faster reads.

1. Redirect the read/write requests in your business system to COS, enable the origin-pull setting in the COS Console, and configure the data origin server as the source address. The system structure is as shown below.
![](https://main.qcloudimg.com/raw/455212542dc210f556b4d55ee86c9776.jpg)
2. After a period of time, the cold data remains in the origin server, while the hot data has been migrated to COS without any impact on your business system during migration.



<span id=cos>

### COS Migration

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
      <td>Threshold for small files. If the size of a file is higher than or equal to this threshold, multipart upload will be used; The default value is 5 MB.</td>
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
