

Cloud Object Storage (COS) is a powerful Tencent Cloud distributed storage service that is accessible for all and features low cost, and high scalability, reliability and security. It enables you to store a massive number of files and view them on the cloud anytime.

You can easily and quickly access COS via the console, APIs, SDKs, or tools to store and manage massive data. You can leverage COS’s user-friendly Web management interface to upload, download and manage files in different formats. CDN nodes around the globe also boost your file download speed.

## Storage Class

COS provides the following storage classes for different access frequencies: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE.

>!COS objects are stored into the STANDARD storage class by default.


### STANDARD

COS STANDARD is a highly reliable, accessible and powerful object storage service. Its low latency and high throughout make it well suited for use cases involving lots of hotspot files or frequent data access.


**Use cases**

Hotspot videos, social images, mobile apps, game programs, and static websites.

### STANDARD_IA

COS STANDARD_IA is a highly reliable object storage service with low storage cost and low access latency. It enables you to save more on storage costs and access the first byte in milliseconds. You can retrieve the data quickly without waiting. The data retrieval is chargeable, so this storage class is suitable for the use cases involving infrequent access (e.g., once or twice per month).

**Use cases**

Online file storage, big data analytics, governmental/organizational business data, low-frequency archives, monitoring data, and more.

### ARCHIVE

COS ARCHIVE is a highly reliable object storage service that offers very low storage cost and long-term data retention. This storage class has a minimal storage duration of 90 days. To read data stored in ARCHIVE, you need to restore them first. Therefore, it is suited for archived data that needs to be stored for a long time.

**Use cases:** archive data, medical images, scientific data, and film and video materials.



### DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage cost and long-term data retention. This storage class has a minimal storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore them first. Therefore, it is suited for archived data that needs to be stored for a long time.

**Use cases**: medical images, security monitoring data, and logs.



### Comparison

| Metric           | STANDARD                    | STANDARD_IA                    | ARCHIVE                               | DEEP ARCHIVE                   |
| ------------  | ------------- | ------------- | ----------- |-------|
| Durability       | 99.999999999% <br>(11 9s) | 99.999999999% <br>(11 9s) | 99.999999999% <br>(11 9s)            | 99.999999999% <br>(11 9s)    |
| Availability      | 99.95%                      | 99.9%                       | 99.9%                                  | 99.9%                          |
| Response             | Millisecond level                      | Millisecond level                        | Requires restoration in advance                         | Requires restoration in advance               |
| Minimum allowed object size | Measured by actual object size         | 64 KB                        | 64 KB                                   | 64 KB                           |
| Minimum billing duration     | No limit                      | 30 days                        | 90 days                                   | 180 days                          |
| Supported regions | All regions| All regions | Only Public Cloud regions (currently excluding Nanjing) | Only Beijing, Guangzhou, and Chengdu regions |
| Storage fees | Standard | Low | Very low | Ultra-low |
| Data retrieval fees    | None          | Low                        | High                                   |High                          |
| Read/Write request fees     | Very low                       | Low                        | Very low (requires data to be restored into STANDARD)           | High (requires data to be restored into STANDARD) |

## Reference
See the following documents for information on the regions, features and specifications supported by Tencent Cloud COS.
- [Regions & Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)
- [Features](https://intl.cloud.tencent.com/document/product/436/8186)
- [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518)

See the following documents to learn about the basic elements of Tencent Cloud COS: buckets and objects.
- [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312)
- [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324)


