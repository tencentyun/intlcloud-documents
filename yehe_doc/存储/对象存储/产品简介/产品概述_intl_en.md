

Cloud Object Storage (COS) is a Tencent Cloud distributed storage service designed to keep massive numbers of files, which users can store and view online at any time. It is highly scalable, cost-effective, reliable, secure and accessible for all global users.

You can readily access COS through the console, APIs, SDKs, or tools to store and manage massive data. You can leverage COS’s user-friendly Web management interface to upload, download and manage files in different formats. CDN nodes around the globe also boost your file download speed.


## Features

COS provides both enterprises and individual users with a suite of features, including data management, remote disaster recovery, data access acceleration and data processing, for diverse use cases. For more information, please see [Feature Overview](https://intl.cloud.tencent.com/document/product/436/8186).

## Concepts

This section describes key concepts that help you have a good idea of COS.

- [Bucket](https://intl.cloud.tencent.com/document/product/436/13312): a container for objects stored in COS.
- [Object](https://intl.cloud.tencent.com/document/product/436/13324): the basic unit of COS storage. It can be the data in any format, such as images, documents, audio and video, and others.
- [Region](https://intl.cloud.tencent.com/document/product/436/6224): a physical location where data centers are hosted on Tencent Cloud. COS data is stored in the buckets in these regions.
- [Endpoint](https://intl.cloud.tencent.com/document/product/436/6224): a COS endpoint used to access and download an object stored in a bucket.



## Storage Classes

COS offers the following storage classes of objects: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE, which vary from one another in access frequency, durability, availability, latency, and more. You can choose which storage class to upload your data to based on your use case.


### STANDARD

COS STANDARD is a highly reliable, accessible and powerful object storage service designed for hot data. Its low latency and high throughout make it well suited for use cases involving lots of hotspot files or frequent data access.


**Use cases**

Hotspot videos, social images, mobile apps, game programs, and static websites.


### STANDARD_IA

COS STANDARD_IA is a highly reliable object storage service with low storage cost and low access latency. It enables you to save more on storage costs and access the first byte in milliseconds. You can retrieve the data quickly without waiting. The data retrieval is chargeable, so this storage class is suitable for the use cases involving infrequent access (e.g., once or twice per month).


**Use cases**

Online file storage, big data analytics, governmental/organizational business data, low-frequency archives, and monitoring data.

### ARCHIVE

COS ARCHIVE is a highly reliable object storage service that offers very low storage cost and long-term data retention. This storage class has a minimal storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it first. Therefore, it is suited for archived data that needs to be stored for a long time.

**Use cases:** archive data, medical images, scientific data, and film and video materials.



### DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage cost and long-term data retention. This storage class has a minimal storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it first. Therefore, it is suited for archived data that needs to be stored for a long time.

**Use cases**: medical images, security monitoring data, and logs.



### Comparison

| Metric           | STANDARD           | STANDARD_IA                     | ARCHIVE                                                     | DEEP ARCHIVE                                                 |
| ---------------- | ------------------ | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Durability       | 99.9999999<br>99%  | 99.9999999<br>99%            | 99.9999999<br>99%                                            | 99.9999999<br>99%                                            |
| Availability       | 99.95%             | 99.9%                        | 99.9%                                                        | 99.9%                                                        |
| Response             | Milliseconds             | Milliseconds                       | Requires restoration in advance using one of these three restoration modes:<br><li>Expedited: retrieves an object of up to 256 MB in 1 - 5 min.<br><li>Standard: retrieves an object in 3 - 5 hours.<br><li>Bulk: retrieves multiple objects in 5 - 12 hours. | Requires restoration in advance using either of these two restoration modes:<br><li>Standard: retrieves an object in 12 - 24 hours.<br><li>Bulk: retrieves multiple objects in 24 - 48 hours. |
| Minimum billable object size | Measured by actual object size | 64 KB                         | 64 KB                                                         | 64 KB                                                         |
| Minimum storage duration     | No limit             | 30 days                         | 90 days                                                         | 180 days                                                        |
| Supported regions         | All regions           | All regions                     | Only public cloud regions                                           | Only Beijing, Shanghai, Guangzhou, and Chengdu regions                           |
| Storage fees         | Standard               | Low                           | Very low                                                        | Ultra-low                                                         |
| Data retrieval fees     | None                 | Rather low. Charged by actual amount of data read | Rather high. Charged by actual amount of data restored depending on the restoration mode           | High. Charged by actual amount of data restored depending on the restoration mode             |
| Request fees         | Standard               | Rather high                         | Standard (requires restoration to STANDARD first)                                 | High (requires restoration to STANDARD first). Fees for both read/write requests and data retrieval requests apply to DEEP ARCHIVE storage class |
| Data processing         | Supported               | Supported                         | Supported (requires data restoration first)                                             | Supported (requires data restoration first)                                              |

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
<td align="left" width="70%">The COS console is the easiest way to work with COS without using any code or programs.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser</a></td>
<td align="left" width="70%">Provides a user-friendly interface to easily upload and download objects, and generate access URLs.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://cloud.tencent.com/doc/product/436/10976">COSCMD</a></td>
<td align="left" width="70%">Enables you to use simple commands to upload, download, and delete objects in batches.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">APIs</a></td>
<td align="left" width="70%">COS uses XML APIs, which are lightweight, connectionless, and stateless. By calling XML APIs, you can send requests to and accept responses from COS directly over HTTP/HTTPS.
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDKs</a></td>
<td align="left" width="70%">Supports multiple mainstream programming languages including Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, and WeChat Mini Program.</td>
</tr>
</tbody></table>




## How Is COS Billed?

COS is billed on a pay-as-you-go basis by default. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).


## Documentation

For other relevant documents, please see [Developer Guide](https://intl.cloud.tencent.com/document/product/436/14102).