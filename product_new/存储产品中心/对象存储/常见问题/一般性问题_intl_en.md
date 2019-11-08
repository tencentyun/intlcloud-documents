### What is COS?
Tencent Cloud Cloud Object Storage (COS) is a cloud-based non-hierarchical distributed storage service that provides cost-effective, fast, and reliable data storage solutions. COS stores your data across multiple AZs in a redundant manner and allows multiple clients or application threads to read or write your data at the same time.

You can use web APIs to store and retrieve data on a CVM instance or over the internet. You can also use the URL of the specified domain name to store and retrieve individual data object in COS over the HTTP or HTTPS protocol.

For more information on COS, see [COS Product Overview](https://intl.cloud.tencent.com/document/product/436).


### What is the difference between COS and CFS?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limit on directory hierarchy or data format and can store any amounts of data. There is no upper limit on the storage capacity of buckets where no partitioning is required. It supports HA deployment to ensure the eventual consistency of data but not features such as file locking. Its APIs are provided for data access using the HTTP or HTTPS protocol, and its SDKs and tools can be integrated into your businesses. Objects uploaded to COS can be accessed or downloaded directly through URL.

[Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582) uses common network file transfer protocols, can create file systems and implement large-scale expansion, but needs to be mounted onto CVM. It can store data for a wide range of applications such as websites, online distribution, and archiving. Featuring high computing throughput and extremely high availability and persistence, it is also suitable for scenarios demanding high concurrence or shared storage.

### What is the difference between COS and Cloud Block Storage (CBS)?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limits on file systems, directory structure, number of files, and storage capacity. It needs to be managed and accessed via web APIs. It offers various SDKs and tools for integration, which can also be used separately without CVM. COS supports access to massive amounts of data but is not suitable for scenarios involving millisecond-level response or random I/O.

[Cloud Block Storage (CBS)](https://intl.cloud.tencent.com/document/product/362) needs to be used together with CVM and can only be mounted and used after the file system is partitioned or formatted. It comes in different types with varous performance metrics such as IOPS and throughput for different scenarios.


### Why does the access link of a public-read file expire?

You can go to the object details page in the [COS Console](https://console.cloud.tencent.com/cos5) to get the object address and signature link.

If your file is public-read:

- If you want to make it accessible to others all the time, you are recommended to directly use the object address.
- If you want to make it accessible to others for a certain period of time, you are recommended to directly copy the signature link, which carries the signature parameter and is valid for 1 hour.

If your file is private:

- If you want to make it accessible to others all the time, you are recommended to change its access permission to public-read/private-write and use the object address.
- If you want to make it accessible to others for a certain period of time, you are recommended to directly copy the signature link, which carries the signature parameter and is valid for 1 hour.


### What is "folder" or "directory" in COS?

The concepts of folder and directory do not apply to COS. However, taking into account the usage habits of different users, COS simulates the display mode of folders in the console based on the directory structure of traditional file management. For more information, see [Folder and Directory](https://intl.cloud.tencent.com/document/product/436/13324#.E6.96.87.E4.BB.B6.E5.A4.B9.E5.92.8C.E7.9B.AE.E5.BD.95).

### Can COS files be recovered after being deleted?

The data redundancy storage mechanism of COS is designed for scenarios where it is necessary to recover data in case of failures in hardware such as servers. If you manually delete your data from COS or configure automated deletion, Tencent Cloud will delete the data as requested in an irrecoverable manner.

You can proactively delete files in the following ways:

- Delete a single file, delete files in batches, clear incomplete multipart uploads, or empty buckets in the COS Console.
- Delete files using COSCMD or COSBrowser.
- Delete files using the COS APIs or SDKs.
- Configure the system to delete files regularly through the lifecycle management feature of COS.
- Sync the CRUD operations between buckets in different regions using the full sync feature of cross-region replication in COS, so that existing files with the same name will be overwritten or deleted.

### How can I avoid accidental deletion?

- Back up the files in your bucket on a regular basis:
  - Download the objects in COS to your local file system or third-party servers using the [COSCMD tool] (https://intl.cloud.tencent.com/document/product/436/10976).
  - Perform intra-region or cross-region bucket data backup using the [COS Migration] tool. (https://intl.cloud.tencent.com/document/product/436/15392) or the cross-region replication feature.
  - Regularly back up your data to other COS buckets using the COS APIs or SDKs.
  - Save your historical versions of data using versioning.
- Use COS permission management. For more information, see [Cloud Access Management Practices](https://intl.cloud.tencent.com/document/product/436/12469):
  - Separate read permission and write permission. For businesses where it is only necessary to read data, use a sub-account with read permission or a temporary key to access the data.
  - Separate the permission to different buckets. For different businesses, only authorize the corresponding buckets, directories, and operations as needed.
  - Do not use a root account to access COS.
  - Use a temporary key to access COS.
  - Keep the credentials for data access properly, such as Tencent Cloud account password, CAM sub-account access credentials, and TencentCloud API key.


### Does COS have the statistics collection feature?

COS is capable of monitoring stored data and displaying details and trends of various metrics in the monitor window. To view general data trends, go to the **Overview** page in the [COS Console](https://console.cloud.tencent.com/cos5) where you can view data such as storage size, number of requests, and traffic by storage class.
To view statistics of a single bucket, see [Querying Monitoring Reports](https://intl.cloud.tencent.com/document/product/436/31634).

In addition, you can also go to [Cloud Monitor](https://console.cloud.tencent.com/monitor/product/COS) to view the monitoring data of different buckets and configure different alarm policies based on your business needs.

### Does COS support image compression?

COS is a distributed storage service for unstructured data and does not support image compression.

### Does COS support thumbnails?

COS is a distributed storage service for unstructured data and does not support thumbnails.

### Does COS support transcoding video files?

COS is a distributed storage service for unstructured data and does not support transcoding video files.

### Does COS support automatic decompression of uploaded files?

COS is a distributed storage service for unstructured data and does not support file decompression; however, you can use the SCF service to decompress files. For more information, see [Using SCF to Decompress Zip Packages](https://intl.cloud.tencent.com/document/product/436/31709).

### What are the specifications and limits of COS?

For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Which version of COS should I use, a legacy version or the current version?

The implementation of legacy versions and that of the current version of COS are quite different. The current version has more features that will not be added to legacy versions. **You are recommended to use the current version** for a better experience. If you are using a legacy version, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to activate the current version.

The current version comes with different APIs and SDKs from those in legacy versions. JSON APIs are used in legacy versions, while XML APIs are used in the current version. Both types of APIs have the same underlying architecture where data is interoperable; however, they are incompatible with each other and have different domain names.

### How do I monitor error codes?

You can use [Cloud Monitor](https://console.cloud.tencent.com/monitor/product/COS) to get different types of HTTP return codes and messages. For more information, see [Monitoring and Alarming](https://intl.cloud.tencent.com/document/product/436/31649).

### How do I calculate the availability of COS?
Below is an example of calculating the availability of COS for your reference:
Tom uses COS to run his ecommerce business. Assume that his business incurred fees of 100 USD from November 1 to 30, 2018, during which two unavailability events occurred as shown below:

<table>
   <tr>
      <th>Unavailability Event No.</th>
      <th>Duration</th>
      <th>5-Minute Record of Unavailability Event</th>
      <th>HTTP Return Code</th>
      <th>Number of Failing Requests</th>
      <th>Number of Valid Requests</th>
   </tr>
   <tr>
      <td rowspan=3><center>1<center></td >
      <td rowspan=3>15 minutes</td>
      <td>November 15, 2018, 10:00 - 10:05</td>
      <td>503</td>
      <td>100</td>
      <td>100</td>
   </tr>
   <tr>
      <td>November 15, 2018, 10:05 - 10:10</td>
      <td>503</td>
      <td>99</td>
      <td>100</td>
   </tr>
   <tr>
      <td>November 15, 2018, 10:10 - 10:15</td>
      <td>503</td>
      <td>98</td>
      <td>100</td>
   </tr>
   <tr>
      <td rowspan=3><center>2<center></td>
      <td rowspan=3>15 minutes</td>
      <td>November 20, 2018, 16:00 - 16:05</td>
      <td>500</td>
      <td>150</td>
      <td>150</td>
   </tr>
   <tr>
      <td>November 20, 2018, 16:05 - 16:10</td>
      <td>500</td>
      <td>148</td>
      <td>150</td>
   </tr>
   <tr>
      <td>November 20, 2018, 16:10 - 16:15</td>
      <td>500</td>
      <td>140</td>
      <td>150</td>
   </tr>
</table>

In other periods of time, Tom's requests **were successful with 200 status codes returned**.

In this case, the overall availability of the service month is as follows:

**1. Calculate the 5-minute error rate for the current month**

As shown in the example, when Tom's business was normal, the 5-minute error rate was 0%.

Unavailability event 1: The duration was November 15, 2018, 10:00 - 10:15, and the 5-minute error rate was: 
- 100 / 100 \* 100% = 100%
- 99 / 100 \* 100% = 99%
- 98 / 100 \* 100% = 98%

Unavailability event 2: The duration was November 20, 2018, 16:00 - 16:15, and the 5-minute error rate was:
- 150 / 150 \* 100% = 100%
- 148 / 150 \* 100% = 98.67%
- 140 / 150 \* 100% = 93.33%

**2. Calculate the service availability of the service month**

In this example:

- Total duration of the service month: 30 days \* 24 hours/day \* 60 minutes/hour = 43,200 minutes
- Total number of 5-minute periods in the service month: 43,200 minutes / 5 minutes = 8,640
- Total number of unavailable 5-minute periods in the service month: (15+15) minutes / 5 minutes = 6
- Sum of the 5-minute error rates in the service month: (100%+99%+98%+100%+98.67%+93.33%)+(8,640-6) \* 0% = 589%

Service availability for the month: (1-589%/8640) \* 100% = 99.93%

**3. Calculate the indemnification**

In this example, the service availability is 99.93%, which is lower than the standard 99.95% but higher than 99.9%. According to the indemnification standard, Tom is eligible for indemnification equivalent to 20% of the total monthly service fees, i.e., 20 USD.
Tom only needs to submit a ticket to apply for indemnification within sixty (60) calendar days after the end of the service month, i.e., prior to January 29, 2019, and Tencent Cloud will indemnify Tom for his losses by issuing a voucher.

