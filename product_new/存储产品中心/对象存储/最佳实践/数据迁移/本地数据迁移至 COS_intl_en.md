## Practice Scenario

If you have a local IDC, COS offers the following migration methods to help you quickly migrate massive amounts of local data to COS.

<table>
   <tr>
      <th>Migration Method</th>
      <th>Description</th>
   </tr>
   <tr>
	 <td nowrap="nowrap"><a href="#cos">COS Migration</a>(online migration)</td>
      <td>COS Migration is an all-in-one tool integrating COS data migration features. You can migrate data to COS quickly after completing simple configurations.</td>
   </tr>
   <tr>
      <td nowrap="nowrap"><a href="#cdm">Cloud Data Migration (CDM) </a>(offline migration)</td>
      <td>CDM uses a dedicated offline migration device provided by Tencent Cloud to help you migrate your local data to the cloud, solving the problems that arise from online migration from a local IDC to cloud, such as long time, high costs, and low security.</td>
   </tr>
</table>

You can determine how to migrate data based on the data volume, IDC egress bandwidth, IDC idle server resources, acceptable completion time, and other factors. The estimated time needed for online migration is shown in the figure below. As can be seen, if data migration needs to take more than 10 days or the amount of data to be migrated exceeds 50 TB, you are recommended to use [CDM](#cdm) for offline migration; otherwise, online migration is a better choice.
![](https://main.qcloudimg.com/raw/68430597098c909ae1fabbb5edcced35.jpg)

> Data migration may be affected if there is a high number of small files below 1 MB or the performance of disk IO is insufficient.



## Migration Practice

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
      <td>Threshold for small files. If the size of a file is higher than or equal to this threshold, multipart upload will be used; otherwise, simple upload will be used. The default value is 5 MB.</td>
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


<span id=cdm>

### Cloud Data Migration (CDM)


The steps are as follows:

1. Go to the CDM Console to submit an application.
2. After the application is approved, you can wait to receive a device.
3. After receiving the device, copy your data to it as instructed in the migration device user manual.
4. Then, submit a return application in the console and wait for Tencent Cloud to migrate your data to COS.

For more information, please see [Cloud Data Migration (CDM)](https://intl.cloud.tencent.com/document/product/623).

#### Tips

Below describes how to migrate data to COS offline efficiently and securely.

1. Configure a 10 Gbps network connection for your IDC. To remove potential constraints of the local data environment on data transfer, you can use a high-performance server as a mount point to maximize the replication speed.
2. Parallel transfer is the fastest way to transfer data though CDM. You can monitor the CPU and memory utilization of the device and if the current migration speed is lower than expected, you can speed the migration up in the following ways:
	- Connect multiple devices to the same CDM device via different network interfaces.
	- Connect multiple devices to several CDM devices via different network interfaces.

