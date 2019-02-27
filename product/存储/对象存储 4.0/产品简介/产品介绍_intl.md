## Introduction to COS

Cloud Object Storages (COS) is a distributed storage service provided by Tencent Cloud used to store a huge number of files. Users can store and view data at any time through network. Tencent Cloud COS allows users to use reliable and secure data storage service with high availability and low cost.

COS can be accessed simply and quickly through various ways such as console, API and SDK, to realize storage and management of massive data. With COS, you can upload, download and manage files in various formats. Tencent Cloud provides an intuitive Web management interface, and CDN nodes distributed across the country can accelerate the speed of file download.
## Storage Classes

COS provides three object storage classes based on the access frequency: COS Standard, COS Infrequent Access, and Archive Storage.

>!Default is COS Standard.

### COS Standard

COS Standard provides COS with high reliability, high availability and high performance for users.

Featuring low access latency and higher throughout, COS Standard is applicable to business scenarios with a large number of hotspot files and a need for frequent access to data.

**Application scenarios:** Hotspot videos, social images, mobile Apps, game programs, and dynamic websites.

### COS Infrequent Access

COS Infrequent Access provides COS with high availability, low storage cost and low access latency for users.

You can minimize the storage cost while keep the time to first byte in millisecond, and read data directly and quickly without waiting when retrieving it. However, you will be charged for data retrieval. It is mainly suitable for business scenarios with low access frequency.

**Application scenarios:** Network disk data, big data analysis, government and enterprise business data, infrequent access archive, and monitoring data.

### Archive Storage

Archive Storage provides COS with high availability, ultra-low storage cost and long-term data retention for users.

Featuring the lowest storage price but a long unfreezing time to read data, Archive Storage is applicable to archived data that needs to be kept for a long time.

**Application scenarios:** Archive data, medical images, scientific data, and film and video materials.

### Comparison

| | COS Standard | COS Infrequent Access | Archive Storage |
| ------------ | -------- | -------- | ------------------- |
| Response | Millisecond | Millisecond | Request for recovery in advance |
| Minimum billing period | - | 30 days | 90 days |
| Supported regions | All regions | All regions | Only Mainland China |
| Storage fee | Standard | Low | Ultra-low |
| Data retrieval fee | - | Low | High |
| Read/Write request fee | Ultra-low | Low | Ultra-low (can only be read/write after recovery) |


For more information on Tencent Cloud COS, see the following documents:
[Getting Started](/document/product/436/6225)
[Bucket Management](/document/product/436/13312)
[Object Management](/document/product/436/13324)
