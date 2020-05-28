

Cloud Object Storage (COS) is a distributed storage service created by Tencent Cloud to save massive numbers of files. Users can store and view data via network at any time. Tencent Cloud COS provides scalable, inexpensive, reliable and secure data storage services for all users.

You can gain the access to COS easily via the console, APIs, SDKs, tools, among other diverse ways, to store and manage massive data. COS allows you to upload, download and manage files in different formats using its user-friendly Web interface. The CDN nodes distributed nationwide can accelerate your file downloads.



## COS Storage Class

COS is available in 4 storage classes depending on the access frequency: MAZ_STANDARD, STANDARD, STANDARD_IA, and ARCHIVE.

>Objects are stored into STANDARD by default.

#### MAZ_STANDARD

**Scenarios**: mobile phone pictures, key files, business data, sensitive information, and more.

- COS MAZ_STANDARD is an object storage service that provides users with high data durability, availability, and performance.
- COS MAZ_STANDARD stores data across different data centers in one city to ensure the stability of user business against failures of a single data center.


#### STANDARD
**Scenarios:** trending videos, social images, mobile Apps, games, static websites, and more.

- COS STANDARD is a highly reliable, accessible and powerful object storage service.
- Its low latency and high throughout make it well suited for business scenarios involving lots of hot files or frequent data access.


#### STANDARD_IA
**Scenarios**: online file storage, big data analytics, governmental/organizational business data, low-frequency archives, monitoring data, and more.

- COS STANDARD_IA is a reliable object storage service with low storage cost and low access latency.
- It offers lower pricing for storage and keeps the first-byte access time within milliseconds, ensuring that data can be fast retrieved with no wait required. However, data retrieval incurs fees. It is suitable for business scenarios where the access frequency is low.


#### ARCHIVE
**Scenarios:** archive data, medical images, scientific data, video materials, and more

- COS ARCHIVE is a highly reliable object storage service with very low storage cost and long-term data retention.
- Featuring the lowest storage price, the ARCHIVE storage class needs a relatively long time to read data and is suited for archived data that needed to be stored for a long time.



#### Comparison

Item | MAZ_STANDARD  | STANDARD | STANDARD_IA | ARCHIVE
---|---|---|----|----
Data durability |99.999999999%|99.999999999%|99.999999999%
Service availability|  99.99%  |99.95%|99.9%|99.9%
| Response | In milliseconds | In milliseconds | In milliseconds | Requires restoration in advance |
| Minimum billable object size | 128 KB              | Billed for the actual size | 64 KB          | 64 KB                         |
Minimum storage duration for billing| No limit | No limit | 30 days | 90 days
| Regions | Currently only Guangzhou and Beijing| All | All | Only Public Cloud regions (currently excluding Nanjing) |
Storage fees | High | Standard | Low | Very low
Data retrieval fees| Free  | Free | Low | High
Read/Write request fees|   Very low| Very low| Very low| Very low (requires data to be restored into STANDARD)

## Related Documents
See the following documents for information on the regions, features and specifications supported by Tencent Cloud COS.
- [Regions & Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)
- [Features](https://intl.cloud.tencent.com/document/product/436/8186)
- [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518)

See the following documents to learn about the basic elements of Tencent Cloud COS: buckets and objects.
- [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312)
- [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324)


