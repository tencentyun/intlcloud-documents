### What is COS?
Tencent Cloud Cloud Object Storage (COS) is a cloud-based non-hierarchical distributed storage service that provides cost-effective, fast, and reliable data storage solutions. COS stores your data across multiple AZs, incorporating redundant storage to ensure data reliability, and allows multiple clients or application threads to read or write data at the same time.

You can use web APIs to store and retrieve data through CVM instances or over the internet. You can also use the URL of a specified domain name to store and retrieve individual data object in COS through HTTP or HTTPS protocol.

For more information about COS, please see [COS Documentation](https://www.tencentcloud.com/document/product/436).


### What is the difference between Cloud Object Storage (COS) and Cloud File Storage (CFS)?

[COS](https://www.tencentcloud.com/document/product/436) has no limit on directory hierarchy or data format and can store any amounts of data. There is no upper limit on the storage capacity of buckets where no partitioning is required. It supports HA deployment to ensure the eventual consistency of data but not features such as file locking. Its APIs are provided for data access using the HTTP or HTTPS protocol, and its SDKs and tools can be integrated into your businesses. Objects uploaded to COS can be accessed or downloaded directly through URL.

[Cloud File Storage (CFS)](https://www.tencentcloud.com/document/product/582) uses common network file transfer protocols, can create file systems and implement large-scale expansion, but needs to be mounted onto CVM. It can store data for a wide range of applications such as websites, online distribution, and archiving. Featuring high computing throughput and extremely high availability and persistence, it is also suitable for scenarios demanding high concurrence or shared storage.

### What is the difference between COS and CBS?

[COS](https://www.tencentcloud.com/document/product/436) has no limits on file systems, directory structure, number of files, and storage capacity. It needs to be managed and accessed via web APIs. It offers various SDKs and tools for integration, which can also be used separately without CVM. COS supports access to massive amounts of data but is not suitable for scenarios involving millisecond-level response or random I/O.

[Cloud Block Storage (CBS)](https://www.tencentcloud.com/document/product/362) needs to be used together with CVM and can only be mounted and used after the file system is partitioned or formatted. It comes in different types with varous performance metrics such as IOPS and throughput for different scenarios.


### Why does the access link of a public-read file expire?

If you use an access link with a temporary signature, the link expires when the temporary signature expires, regardless of whether the file is public-read.

If you want your public-read file to be always accessible, we recommend you use an unsigned access link, which is the object URL on the object details page of the [COS console](https://console.cloud.tencent.com/cos).


### What is a "folder" or "directory" in COS?

The concepts of folder and directory do not apply to COS. However, taking into account the usage habits of different users, COS displays “folders” in the console and COSBrowser just like in the directory structure of traditional file management. For more information, see [Folder and directory](https://www.tencentcloud.com/document/product/436/13324).

### Can COS files be recovered after being deleted?

The data redundancy storage mechanism of COS is designed for scenarios where it is necessary to recover data in case of hardware failure. When versioning is not enabled, if you manually delete your data from COS or configure automated deletion, Tencent Cloud will delete the data as requested after which the data is irrecoverable.

You can proactively delete files in the following ways:

- Deleting files using the COS console by deleting a single file, deleting files in batches, clearing incomplete multipart uploads, or emptying buckets.
- Deleting files using COS tools such as COSCMD or COSBrowser.
- Deleting files using the COS APIs or SDKs.
- Configuring the system to delete files regularly through the COS lifecycle management feature.
- Syncing the CRUD operations between buckets in different regions using the COS cross-region replication sync feature, so that existing files with the same name will be overwritten or deleted.

### How can I avoid accidental deletion?

- The best way to avoid accidental deletion is to back up the files in your bucket on a regular basis. You can protect your data in the following ways:
  - Download the objects in COS to your local file system or third-party servers using the [COSCMD tool](https://www.tencentcloud.com/document/product/436/10976).
  - Perform intra-region or cross-region bucket data backup using the [COS Migration Tool](https://www.tencentcloud.com/document/product/436/30585) or the cross-region replication feature.
  - Regularly backing up your data to other COS buckets using COS APIs or SDKs.
  - Saving your past versions of data using versioning.
- Use COS permission management. For more information, see [Cloud Access Management Practices](https://www.tencentcloud.com/document/product/436/12469):
  - Separating read permission and write permission. For businesses where it is only necessary to read data, use a sub-account with read permission or a temporary key to access the data.
  - Separating permissions for different buckets. For different businesses, only authorize permissions for buckets, directories, and operations within the scope of that particular business.
  - Not using a root account to access COS.
  - Accessing COS using a temporary key.
  - Properly managing your data access credentials, such as your Tencent Cloud account password, CAM sub-account access credentials, and TencentCloud API key.


### Does COS support statistics collection?

COS is capable of monitoring stored data and displaying the details and trends of various metrics in the monitoring window. To view general data trends, go to the **Overview** page in the [COS console](https://console.cloud.tencent.com/cos5), and you can view data such as storage size, request number, and traffic for each storage class.
To view statistics of a single bucket, see [Querying Monitoring Reports](https://www.tencentcloud.com/document/product/436/31634).

In addition to the COS Console, you can also view the monitoring information of different buckets on the [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) page where you can also configure different alarm policies to fit your business needs.

### Does COS support image processing, image compression, thumbnail generation, or video transcoding?

CI is integrated in the COS console to implement data processing features such as image processing, image compression, thumbnail generation, and video transcoding. For more information, see [Data Processing](https://www.tencentcloud.com/document/product/436/35279).


### What formats of audio/video files can COS process?

COS is a distributed storage service for unstructured data and cannot support image compression or audio/video file processing on its own. For more information on rich media file processing (MP4, AVI, TS, HLS, MP3, AAC, etc.), see [Cloud Infinite](https://www.tencentcloud.com/zh/products/ci).

### Does COS support the auto decompression of uploaded files?

COS is a distributed storage service for unstructured data and does not support file decompression; however, you can use the SCF service to decompress files. For more information, see [Setting File Decompression](https://www.tencentcloud.com/document/product/436/35663).

### What are the specifications and limits of COS?

For more information, see [Specifications and Limits](https://www.tencentcloud.com/document/product/436/14518).

### What is a bucket?

A bucket is a carrier of objects, which can be considered as a "container" for storing objects. You can manage buckets and configure attributes of buckets in various methods such as the Tencent Cloud console, APIs, and SDKs. For example, you can set a bucket for hosting a static website or set access permission on a bucket. For more information on buckets, see [Bucket Overview](https://www.tencentcloud.com/document/product/436/13312).

### What is the length limit on a bucket name?

The bucket length limit has been changed since the COS console update in September 2021. According to the new policy, the length of a bucket name is affected by the number of characters in the **region abbreviation** and **APPID**, as the combined full domain can contain 60 characters at most. Note that previous bucket names will not be affected. If you need longer names to meet special requirements, [contact us](https://www.tencentcloud.com/contact-sales).



### How do I monitor error code information?

You can use [Cloud Monitor](https://console.cloud.tencent.com/monitor/product/COS) to get different types of HTTP error code messages. For more information, see [Monitoring and Alarm](https://intl.cloud.tencent.com/document/product/436/31649). For information about how to work with Cloud Monitor and obtain relevant data, see Cloud Monitor’s [Console Guide](https://www.tencentcloud.com/document/product/248/13517) or [API Documentation](https://www.tencentcloud.com/zh/document/product/248/7239).  


### How do I calculate the availability of COS?
Please reference the following example for information on how to calculate COS availability:
Tom uses Tencent Cloud COS to run his e-commerce business. Assume that his business consumed a total of 100 USD in the service period from Nov. 1 to Nov. 30, 2018, during which two unavailability events occurred, as shown below:

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

In all other periods, Tom's requests **were successful and a 200 status code was returned**.

In this case, the overall availability for the service period is as follows:

**(1) Calculate the per-5-minute error rate for the current month**

According to the case details: when Tom's business is normal, the per-5-minute error rate is 0%.

Unavailability event 1: This event occurred on November 15, 2018 and lasted from 10:00 - 10:15. The per-5-minute error rate was: 
- **100 / 100 \* 100% = 100%** from 10:00 - 10:05
- **99 / 100 \* 100% = 99%** from 10:05 - 10:10
- **98 / 100 \* 100% = 98%** from 10:10 - 10:15

Unavailability event 2: This event occurred on November 20, 2018 and lasted from 16:00 - 16:15. The 5-minute error rate was:
- **150 / 150 \* 100% = 100%** from 16:00 - 16:05
- **148 / 150 \* 100% = 98.67%** from 16:05 - 16:10
- **140 / 150 \* 100% = 93.33%** from 16:10 - 16:15

**(2) Calculate the service availability for the current month**

In this case:

- Total duration of the service period: 30 days \* 24 hours/day \* 60 minutes/hour=43,200 minutes.
- Total number of 5-minute periods: 43,200 minutes / 5 minutes = 8,640.
- Total number of unavailable 5-minute periods: (15 + 15) minutes / 5 minutes = 6.
- Sum of the per-5-minute error rates: (100% + 99% + 98% + 100% + 98.67% + 93.33%) + (8640 - 6) \* 0% = 589%

The service availability for this month: **(1 - 589% / 8640) \* 100% = 99.93%**

**(3) Calculate relevant compensation**

In this example, the service availability is 99.93%, which is lower than the standard 99.95% but higher than 99.9%. According to compensation standards, Tom is eligible for compensation equivalent to 20% of the total monthly service fees, i.e., 20 USD.
Tom only needs to submit a ticket to apply for compensation within sixty (60) calendar days after the end of the service period, i.e., prior to January 29, 2019, and Tencent Cloud will compensate Tom for his losses by issuing a voucher.



### How do I deactivate the COS service and stop being charged?

You can deactivate COS or stop its billing as follows:

1. If you decide to stop using COS, you can avoid any further billing by permanently deleting all of your COS data (including incomplete multipart uploads and object versions) as instructed in [Payment Overdue](https://intl.cloud.tencent.com/document/product/436/10044). There is no need to remove your account, and if you use other Tencent Cloud products, avoid doing so as it will affect your other services.
2. If you don't use COS for more than one month, you can set lifecycle rules to transition data in STANDARD storage class in the bucket to a colder class such as STANDARD_IA, ARCHIVE, or DEEP ARCHIVE to reduce storage fees. For more information, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605). The transition will generate read requests in the original storage class and write requests in the target storage class, so transition by lifecycle will incur read/write [request fees](https://intl.cloud.tencent.com/document/product/436/40100).


**Note**

- Data, once deleted from the bucket, cannot be recovered, so make backups accordingly.
- If versioning is enabled for the bucket, disable it before deleting data.
- Check your billing cycle to avoid overdue payments. If all your billable items are settled daily, the bill for the day of data deletion will be generated on the next day. After the data is completely cleared, the system will stop billing. For more information, see [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871).
- If your account has overdue payment (i.e., your account balance is below 0), COS services will be suspended after 24 hours, regardless of whether your resource pack is within the validity period.
- If your account has overdue payment and COS services are suspended, the free tier for which your account is eligible won't be available.
- If data in your bucket is blocked for the second time due to non-compliance, it cannot be deleted. [Contact us](https://intl.cloud.tencent.com/contact-sales) if you have any questions. 

