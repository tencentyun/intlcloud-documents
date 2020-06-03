### What is COS?
Tencent Cloud Cloud Object Storage (COS) is a cloud-based non-hierarchical distributed storage service that provides cost-effective, fast, and reliable data storage solutions. COS stores your data across multiple AZs in a redundant manner and allows multiple clients or application threads to read or write your data at the same time.

You can use web APIs to store and retrieve data on a CVM instance or over the internet. You can also use the URL of the specified domain name to store and retrieve individual data object in COS over the HTTP or HTTPS protocol.

For more information on COS, see [COS Product Overview](https://intl.cloud.tencent.com/document/product/436).


### What is the difference between Cloud Object Storage (COS) and Cloud File Storage (CFS)?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limit on directory hierarchy or data format and can store any amounts of data. There is no upper limit on the storage capacity of buckets where no partitioning is required. It supports HA deployment to ensure the eventual consistency of data but not features such as file locking. Its APIs are provided for data access using the HTTP or HTTPS protocol, and its SDKs and tools can be integrated into your businesses. Objects uploaded to COS can be accessed or downloaded directly through URL.

[Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582) uses common network file transfer protocols, can create file systems and implement large-scale expansion, but needs to be mounted onto CVM. It can store data for a wide range of applications such as websites, online distribution, and archiving. Featuring high computing throughput and extremely high availability and persistence, it is also suitable for scenarios demanding high concurrence or shared storage.

### What is the difference between COS and Cloud Block Storage (CBS)?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limits on file systems, directory structure, number of files, and storage capacity. It needs to be managed and accessed via web APIs. It offers various SDKs and tools for integration, which can also be used separately without CVM. COS supports access to massive amounts of data but is not suitable for scenarios involving millisecond-level response or random I/O.

[Cloud Block Storage (CBS)](https://intl.cloud.tencent.com/document/product/362) needs to be used together with CVM and can only be mounted and used after the file system is partitioned or formatted. It comes in different types with various performance metrics such as IOPS and throughput for different scenarios.


### Why does the access link of a public-read file expire?

You can go to the object details page in the [COS Console](https://console.cloud.tencent.com/cos) to get the object address and signature link.

If your file is public-read:

- If you want to make it accessible to others all the time, you are recommended to directly use the object address.
- If you want to make it accessible to others for a certain period of time, you are recommended to directly copy the signature link, which carries the signature parameter and is valid for 1 hour.

If your file is private:

- If you want to make it accessible to others all the time, you are recommended to change its access permission to public-read/private-write and use the object address.
- If you want to make it accessible to others for a certain period of time, you are recommended to directly copy the signature link, which carries the signature parameter and is valid for 1 hour.


### What is "folder" or "directory" in COS?

The concepts of folder and directory do not apply to COS. However, taking into account the usage habits of different users, COS displays “folders” in the console just like in the directory structure of traditional file management. For more information, see [Folder and directory](https://intl.cloud.tencent.com/document/product/436/13324).

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
  - Perform intra-region or cross-region bucket data backup using the [COS Migration Tool](https://intl.cloud.tencent.com/document/product/436/30585) or the cross-region replication feature.
  - Regularly back up your data to other COS buckets using the COS APIs or SDKs.
  - Save your historical versions of data using versioning.
- Use COS permission management. For more information, see [Cloud Access Management Practices](https://intl.cloud.tencent.com/document/product/436/12469):
  - Separate read permission and write permission. For businesses where it is only necessary to read data, use a sub-account with read permission or a temporary key to access the data.
  - Separate the permission to different buckets. For different businesses, only authorize the corresponding buckets, directories, and operations as needed.
  - Do not use a root account to access COS.
  - Access COS using a temporary key.
  - Keep the credentials for data access properly, such as Tencent Cloud account password, CAM sub-account access credentials, and TencentCloud API key.


### Does COS support statistics collection?

COS is capable of monitoring stored data and displaying details and trends of various metrics in the monitor window. To view general data trends, go to the **Overview** page in the [COS Console](https://console.cloud.tencent.com/cos5) where you can view data such as storage size, number of requests, and traffic by storage class.
To view statistics of a single bucket, see [Querying Monitoring Reports](https://intl.cloud.tencent.com/document/product/436/31634).

In addition to the COS Console, you can also view the monitoring information about different buckets on the [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) page, and configure different alarm policies based on your business needs.

### Does COS support image processing?

The COS console has integrated Cloud Infinite features, which enable you to scale, crop and add watermarks to your images. For more information, see [Enabling Image Processing](https://intl.cloud.tencent.com/document/product/436/35278).



### Does COS support image compression?

COS is a distributed storage service for unstructured data and cannot support image compression on its own. For image compression, see [Cloud Infinite](https://intl.cloud.tencent.com/product/ci).

### Does COS support thumbnails?

COS is a distributed storage service for unstructured data and cannot support thumbnails on its own. For more information on thumbnails, see [Cloud Infinite](https://intl.cloud.tencent.com/product/ci).

### Does COS support transcoding video files?

COS is a distributed storage service for unstructured data and cannot support video transcoding on its own. For information on how to transcode video files, see [Media Processing Service](https://intl.cloud.tencent.com/product/mps).

### Does COS support auto decompression of uploaded files?

COS is a distributed storage service for unstructured data and does not support file decompression on its own. To enable this feature, please use the integrated SCF service. For more information, see [File Decompression](https://intl.cloud.tencent.com/document/product/436/35663) or [Using SCF to Decompress Zip Packages](https://intl.cloud.tencent.com/document/product/436/31709).

### What are the specifications and limits of COS?

For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).


### How do I monitor the error code information?

You can use [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) to get different types of HTTP error code messages. For more information, see [Monitoring and Alarm](https://intl.cloud.tencent.com/document/product/436/31649). For information on how to work with Cloud Monitoring and obtain relevant data, see Cloud Monitoring’s [Console Guide](https://intl.cloud.tencent.com/document/product/248) or [API Documentation](https://intl.cloud.tencent.com/document/product/248/13655).  


### How do I calculate the availability of COS?
COS provides the following example of calculating the availability for your reference:
Tom uses Tencent Cloud COS to run his e-commerce business. Assume that his business consumed a total of 100 USD in a service month from Nov. 1 to Nov. 30, 2018, during which two unavailable events occurred, as shown below:

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
      <td rowspan=3>15 min</td>
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
      <td rowspan=3>15 min</td>
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

In other periods, Tom's requests **were successful and a 200 status code was returned**.

In this case, the overall availability of the service month is as follows:

**(1) Calculate the error rate per 5 minutes for the current month**

According to the case details: when Tom's business is normal, the error rate per 5 minutes is 0%.

Unavailability event 1: The duration was November 15, 2018, 10:00 - 10:15, and the 5-minute error rate was: 
- **100 / 100 \* 100% = 100%** from 10:00 - 10:05
- **99 / 100 \* 100% = 99%** from 10:05 - 10:10
- **98 / 100 \* 100% = 98%** from 10:10 - 10:15

Unavailability event 2: The duration was November 20, 2018, 16:00 - 16:15, and the 5-minute error rate was:
- **150 / 150 \* 100% = 100%** from 16:00 - 16:05
- **148 / 150 \* 100% = 98.67%** from 16:05 - 16:10
- **140 / 150 \* 100% = 93.33%** from 16:10 - 16:15

**(2) Calculate the service availability for the current month**

In this case:

- Total duration of the service month: 30 days \* 24 hours/day \* 60 minutes/hour=43,200 minutes.
- Total number of 5-minute periods: 43,200 minutes / 5 minutes = 8,640.
- Total number of unavailable 5-minute periods: (15 + 15) minutes / 5 minutes = 6.
- Sum of the 5-minute error rates: (100% + 99% + 98% + 100% + 98.67% + 93.33%) + (8640 - 6) \* 0% = 589%

The service availability for this month: **(1 - 589% / 8640) \* 100% = 99.93%**

**(3) Calculate the indemnification**

In this example, the service availability is 99.93%, which is lower than the standard 99.95% but higher than 99.9%. According to the indemnification standard, Tom is eligible for indemnification equivalent to 20% of the total monthly service fees, i.e., 20 USD.
Tom only needs to submit a ticket to apply for indemnification within sixty (60) calendar days after the end of the service month, i.e., prior to January 29, 2019, and Tencent Cloud will indemnify Tom for his losses by issuing a voucher.

### How do I disable COS or stop the billing of it?


There is no one-click option for disabling COS. If you are not using COS for a long time, you may save storage costs by transitioning your data to ARCHIVE storage class. For the transition operation, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).

If you decide to stop using COS, you can avoid any further billing by permanently deleting all of your COS data (including incomplete multipart uploads and object versions). You need not deregister your account lest your other Tencent Cloud services should be affected.

>To delete your COS data and incomplete multipart uploads, see [Deleting Objects](https://intl.cloud.tencent.com/document/product/436/13323), and [Deleting Incomplete Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/31632).

Before the complete deletion, consider the following:

- Data deleted completely from COS cannot be recovered, so please make backups in time.
- Check your billing cycle to avoid any arrears in your account. For more information, see [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871).
- If your account is in arrears (the balance is below 0), the COS service is suspended after 24 hours, regardless of whether your storage pack is within the effective period.
- If your account is in arrears and COS service is suspended, the free tier for which your account is eligible won’t be available.
