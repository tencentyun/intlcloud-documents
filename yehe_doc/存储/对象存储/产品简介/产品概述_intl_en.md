

Cloud Object Storage (COS) is a powerful Tencent Cloud distributed storage service that features low costs and high scalability, reliability, and security. It enables you to store a massive number of files and view them on the cloud anytime.

You can easily and quickly access COS via the console, APIs, SDKs, or tools to store and manage massive data. You can leverage COS’s user-friendly web management interface to upload, download, and manage files in different formats. CDN nodes around the globe also boost your file download speed.


## Product Features

COS provides both enterprises and individual users with a suite of features, including data management, remote disaster recovery, data access acceleration, and data processing for diverse use cases. For more information, see [Features](https://intl.cloud.tencent.com/document/product/436/8186).

## Concepts

This section describes key concepts that help you better understand COS.

- [Bucket](https://intl.cloud.tencent.com/document/product/436/13312): A container for objects stored in COS. Each bucket can store an unlimited number of objects.
- [Object](https://intl.cloud.tencent.com/document/product/436/13324): The basic unit of COS storage. It can be data in any format, such as image, document, audio, and video.
- [Region](https://intl.cloud.tencent.com/document/product/436/6224): A physical location where data centers are hosted in Tencent Cloud. COS data is stored in the buckets in these regions.
- [Endpoint](https://intl.cloud.tencent.com/document/product/436/6224): A COS endpoint used to access and download an object stored in a bucket.



## Storage Classes

COS offers the following storage classes of objects: INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. They indicate how active objects are in COS, and vary from one another in access frequency, durability, availability, latency, and more. You can choose which storage class to upload your data to based on your use case.

>? For comparison among COS storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
>



### ARCHIVE

COS ARCHIVE is a highly reliable object storage service designed for cold data, and offers very low storage costs and long-term data retention. This storage class has a minimum storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it to STANDARD first.

**Use cases**

Use cases that require long-term data retention, such as archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

### DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage costs and long-term data retention. This storage class has a minimum storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it to STANDARD first.

**Use cases**

Use cases that require long-term data retention, such as medical images, view data, and logs.

## Getting Started with COS

### Getting started

COS offers various tools and video tutorials to help you better understand and use COS.


### How to use

The table below describes different methods available for you to get started with COS:

<table>
<thead>
<tr>
<th align="left" width="30%">Method</th>
<th align="left" width="70%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/32955">Console</a></td>
<td align="left" width="70%">The COS console is the easiest way to work with COS without using any code or programs.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser</a></td>
<td align="left" width="70%">Provides a user-friendly interface to easily upload and download objects and generate access URLs</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://cloud.tencent.com/doc/product/436/10976">COSCMD</a></td>
<td align="left" width="70%">Enables you to use simple commands to upload, download, and delete objects in batches</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">APIs</a></td>
<td align="left" width="70%">COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests to and accept responses from COS directly over HTTP/HTTPS</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKs</a></td>
<td align="left" width="70%">Supports multiple mainstream programming languages including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Program</td>
</tr>
</tbody></table>





## How Is COS Billed?

COS is billed on a pay-as-you-go basis by default. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).

## References

For other relevant documentation, see [Developer Guide](https://intl.cloud.tencent.com/document/product/436/14102).

