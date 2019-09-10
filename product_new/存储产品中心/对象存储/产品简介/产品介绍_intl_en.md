## Overview

Cloud Object Storages (COS) is a distributed storage service provided by Tencent Cloud to store massive files.You can store and view data at any time over network. Tencent Cloud COS provides scalable, affordable, reliable and secure data storage services for all users.

You can gain the access to COS easily via console, API, SDK or tools to store and manage massive data. COS allows you upload, download and manage files in different formats using its user-friendly Web interface. The CDN nodes distributed nationwide can accelerate your file download.

## COS Class

COS is available in three classes depending on the access frequency: COS Standard, COS Infrequent Access, and Archive Storage.

>Default is COS Standard.

#### COS Standard

COS Standard is an object storage service with high reliability, availability, and performance.

Its low latency and high throughout make it well suitable for the use cases involving lots of hotspot files or frequent data access.

**Use Cases:** Hotspot videos, social images, mobile Apps, game programs, and dynamic websites.

#### COS Infrequent Access

COS Infrequent Access is a reliable object storage service with low storage cost and low access latency.

COS Infrequent Access is provided at a low storage cost, and enables you to access the first byte in milliseconds. You can retrieve the data quickly without waiting. The data retrieval is chargeable, so this storage class is suitable for the use cases involving infrequent access.

**Use Cases:** Network disk data, big data analysis, government and enterprise business data, infrequently-accessed archives, and monitoring data.

#### Archive Storage

Archive Storage is a highly reliable object storage service that has ultra-low storage cost and long-term data retention.

Featuring the lowest storage price, Archive Storage needs a longer time to read data and is suitable for archived data that needs to be stored for a long time.

**Use Cases:** Archive data, medical images, scientific data, and film and video materials.

#### Comparison

|              | COS Standard | COS Infrequent Access | Archive Storage |
| ------------ | -------- | -------- | ------------------- |
| Response| In milliseconds| In milliseconds| Request for recovery is required in advance|
| Minimum billing period | -        | 30 days |90 days|
| Supported regions |All regions |All regions| Mainland China Only|
| Storage fee |Standard |Low| Extra-low|
| Data retrieval fee | -        | Low | High |
| Read/Write request fee |Extra-low |Low| Extra-low (read/write only after recovery)|

## Related Documents
See the following documents for information on the regions, features and specifications supported by Tencent Cloud COS.
- [Regions & Endpoints](https://cloud.tencent.com/document/product/436/6224)
- [Features](https://cloud.tencent.com/document/product/436/8186)
- [Specifications and Use Limits](https://cloud.tencent.com/document/product/436/14518)

See the following documents to learn about the basic elements of Tencent Cloud COS: buckets and objects.
- [Bucket Overview](https://cloud.tencent.com/document/product/436/13312)
- [Object Overview](https://cloud.tencent.com/document/product/436/13324)

