## Introduction to COS

Cloud Object Storages (COS) is a distributed storage service in Tencent Cloud to save massive numbers of files. Users can store and view data via network at any time. Tencent Cloud COS provides scalable, inexpensive, reliable and secure data storage services for all users.

You can easily and quickly access COS via console, API or SDK to store and manage massive data. You can leverage COS’s user-friendly web management interface to upload, download and manage files in different formats. CDN nodes across the country also boost your file download speed.
## Types of Storage

COS provides three types of object storage catering to different access frequencies: COS Standard, COS Infrequent Access, and Archive Storage.

>!Default is COS Standard.

### COS Standard

COS Standard is a reliable, accessible and powerful object storage service.

Its low latency and high throughout make it well suited for use cases involving lots of hotspot files or frequent data access.

**Use Cases:** Hotspot videos, social images, mobile Apps, game programs, and dynamic websites.

### COS Infrequent Access

COS Infrequent Access is a reliable object storage service with low storage cost and low access latency.

You can cut your storage cost while still accessing the first byte in the milliseconds. You can pay and retrieve data without waiting and you can also quickly read data. It is well suited for use cases with low access frequency.

**Application scenarios:** Network disk data, big data analysis, government and enterprise business data, infrequent access archive, and monitoring data.

### Archive Storage

Archive Storage is a highly reliable object storage service that has ultra-low storage cost and long-term data retention.

Featuring the lowest storage price, Archive Storage needs a relatively long time to read data and is suited for archived data that needed to be stored for a long time.

**Use Cases:** Archive data, medical images, scientific data, and film and video materials.

### Comparison

| | COS Standard | COS Infrequent Access | Archive Storage |
| ------------ | -------- | -------- | ------------------- |
| Response | In milliseconds | In milliseconds | Request for recovery in advance |
| Minimum billing period | - | 30 days | 90 days |
| Supported regions | All regions | All regions | Mainland China Only |
| Storage fee | Standard | Low | Ultra-low |
| Data retrieval fee | - | Low | High |
| Read/Write request fee | Ultra-low | Low | Ultra-low (can only be read/write after recovery) |


For more information on Tencent Cloud COS, see the following documents:
[Getting Started](/document/product/436/6225)
[Bucket Management](/document/product/436/13312)
[Object Management](/document/product/436/13324)
