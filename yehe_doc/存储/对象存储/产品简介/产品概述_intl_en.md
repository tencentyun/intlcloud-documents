Cloud Object Storage (COS) is a powerful Tencent Cloud distributed storage service that is accessible for all and features low costs and high scalability, reliability and security. It enables you to store a massive number of files and view them on the cloud anytime.

You can readily access COS through the console, APIs, SDKs, or tools to store and manage massive data. You can leverage COS’s user-friendly Web management interface to upload, download and manage files in different formats. CDN nodes around the globe also boost your file download speed.


## Features

COS provides both enterprises and individual users with a suite of features, including data management, remote disaster recovery, data access acceleration and data processing for diverse use cases. For more information, please see [Features](https://intl.cloud.tencent.com/document/product/436/8186).

## Concepts

This section describes key concepts that help you better understand COS.

- [Bucket](https://intl.cloud.tencent.com/document/product/436/13312): a container for objects stored in COS. Each bucket can store an unlimited number of objects.
- [Object](https://intl.cloud.tencent.com/document/product/436/13324): the basic unit of COS storage. It can be data in any format, such as images, documents, audio and video, and others.
- [Region](https://intl.cloud.tencent.com/document/product/436/6224): a physical location where data centers are hosted on Tencent Cloud. COS data is stored in the buckets in these regions.
- [Endpoint](https://intl.cloud.tencent.com/document/product/436/6224): a COS endpoint used to access and download an object stored in a bucket.



## Storage Classes

COS offers the following storage classes of objects: INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. They indicate how active objects are in COS, and vary from one another in access frequency, durability, availability, latency, and more. You can choose which storage class to upload your data to based on your use case.

> ?For comparison among COS storage classes, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

### STANDARD

COS STANDARD is a highly reliable, accessible, and powerful object storage service that is designed for hot data and features low latency and high throughput.


**Use cases**

Use cases involving lots of hotspot files or frequent data access, including hotspot videos, social images, mobile apps, game programs, and static websites.


### STANDARD_IA

COS STANDARD_IA is a highly reliable object storage service with low storage costs and low access latency. It enables you to save more on storage costs and access the first byte in milliseconds. You can retrieve data quickly without waiting. Unlike STANDARD, STANDARD_IA bills you for data retrieval fees when you access data.


**Use cases**

Use cases with low access frequency (for example, 1 to 2 times per month), such as cloud disk data, big data analysis, government and enterprise data, low-frequency archives, and monitoring data.

### INTELLIGENT TIERING

COS INTELLIGENT TIERING delivers automatic cost savings by moving data between two access tiers - Frequent Access and Infrequent Access, as access patterns change. There are no fees for data retrievals from this storage class.

**Use cases**

Use cases where access patterns are unknown or changing. This storage class is ideal for you if your business demands strict cost control and is insensitive to read performance.

### ARCHIVE

COS ARCHIVE is a highly reliable object storage service designed for cold data, and offers very low storage costs and long-term data retention. This storage class has a minimum storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it to STANDARD first.

**Use cases**

Use cases that require long-term data retention, such as archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

### DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage costs and long-term data retention. This storage class has a minimum storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it to STANDARD first.

**Use cases**

Use cases that require long-term data retention, such as medical images, security monitoring data, and logs.

## Getting Started with COS

The table below describes different methods available for you to get started with COS:

<table>
<thead>
<tr>
<th align="left" width="30%">Method</th>
<th align="left" width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/32955">Console</a></td>
<td align="left" width="70%">The COS console is the easiest way to work with COS without using any code or programs</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser</a></td>
<td align="left" width="70%">Provides a user-friendly interface to easily upload and download objects and generate access URLs</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/10976">COSCMD</a></td>
<td align="left" width="70%">Enables you to use simple commands to upload, download, and delete objects in batches</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">APIs</a></td>
<td align="left" width="70%">COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests to and accept responses from COS directly over HTTP/HTTPS
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKs</a></td>
<td align="left" width="70%">Supports multiple mainstream programming languages including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Program</td>
</tr>
</tbody></table>




## How Is COS Billed?

COS is billed on a pay-as-you-go basis by default. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).


## Documentation

For other relevant documentation, please see [Developer Guide](https://intl.cloud.tencent.com/document/product/436/14102).
