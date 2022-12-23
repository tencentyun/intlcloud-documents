## MSP

MSP is a cloud data migration service and tool provided by Tencent Cloud. It enables you to easily migrate data from third-party data sources to Tencent Cloud COS or migrate data between different COS buckets.

### Supported data sources

Alibaba Cloud OSS, AWS S3 (International), HTTP URL list, and Tencent Cloud COS.

### Migration mode

#### Semi-managed migration

In semi-managed migration mode, after creating a task in the console, you also need to manually deploy the migration Agent on your own server as instructed in [Using Semi-Managed Migration Agent](https://www.tencentcloud.com/document/product/1036/51593). The Agent first obtains your task through a fixed network request and then pulls the source data and upload it to COS over the network. At the same time, it displays the real-time progress in the console, so that you can monitor your task just like in fully managed mode. For more information on how to create a task, see the corresponding instructions for different source vendors.

#### Notes
1. In semi-managed mode, there may be different traffic fees depending on the location of the deployed Agent server. Traffic is not billed during Agent semi-managed migration if a direct connection is established between the source data cloud vendor and Tencent Cloud COS. Therefore, we recommend you perform Agent semi-managed migration if Direct Connect is available.
2. The compute and network resources in semi-managed mode are dedicated to you, so you can accurately estimated the speed and resource usage as needed. This mode is suitable for those who need to migrate a high volume of data quickly or over direct connections.

### Data check

1. All data will be simply checked for size consistency.
2. If the header information of the source file carries a carries a CRC-64 or Content-MD5 checksum, it will be checked whether the source and target content checksums are the same.
3. If there are no such checksums, a spot check will be performed on sampled content bytes of the source and target files.









