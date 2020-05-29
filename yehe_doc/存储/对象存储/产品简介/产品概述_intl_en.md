
Cloud Object Storage (COS) is a distributed storage service created by Tencent Cloud to save massive numbers of files. Users can store and view data via network at any time. Tencent Cloud COS provides scalable, inexpensive, reliable and secure data storage services for all users.

You can easily and quickly access COS via the console, APIs, SDKs, or tools to store and manage massive data. You can leverage COS’s user-friendly web management interface to upload, download and manage files in different formats. CDN nodes across the country also boost your file download speed.


## COS Storage Class

COS is available in 3 classes depending on the access frequency: STANDARD, STANDARD_IA, and ARCHIVE.

>Objects are stored into STANDARD by default.



#### STANDARD
**Use cases:** hotspot videos, social images, mobile Apps, game programs, and static websites.

- COS STANDARD is a reliable, accessible and powerful object storage service.
- Its low latency and high throughout make it well suited for use cases involving lots of hotspot files or frequent data access.


#### STANDARD_IA
**Use cases:** online file storage, big data analytics, governmental/organizational business data, low-frequency archives, and monitoring data.

- STANDARD_IA is a reliable object storage service with low storage cost and low access latency.
- STANDARD_IA is provided at a low storage cost, and enables you to access the first byte in milliseconds. You can retrieve the data quickly without waiting. The data retrieval is chargeable, so this storage class is suitable for the use cases involving infrequent access.


#### ARCHIVE
**Used cases:** archive data, medical images, scientific data, and film and video materials.

- COS ARCHIVE is a highly reliable object storage service that has ultra-low storage cost and long-term data retention.
- Featuring the lowest storage price, COS ARCHIVE needs a relatively long time to read data and is suited for archived data that needed to be stored for a long time.



#### Comparison

Item |  STANDARD | STANDARD_IA | ARCHIVE
---|---|---|----|----
Data durability |99.999999999%|99.999999999%|99.999999999%
Service availability| 99.95%|99.9%|99.9%
| Response | In milliseconds | In milliseconds | Requires restoration in advance |
Minimum object size |  Calculated by actual object size |64 KB|64 KB
Minimum billing duration|  No limit | 30 days | 90 days
Supported regions |  All regions | All regions | Only Public Cloud regions
Storage fees |  Standard | Low | Very low
Data retrieval fees|  None | Low | High
Read/Write request fees|  Very low| lower| Very low (requires data to be restored into STANDARD)

## Related Documents
See the following documents for information on the regions, features and specifications supported by Tencent Cloud COS.
- [Regions & Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)
- [Features](https://intl.cloud.tencent.com/document/product/436/8186)
- [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518)

See the following documents to learn about the basic elements of Tencent Cloud COS: buckets and objects.
- [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312)
- [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324)