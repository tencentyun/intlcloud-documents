COS offers the following storage classes for objects: INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. They indicate how active objects are in COS, and vary from one another in terms of access frequency, durability, availability, latency, and more. You can choose which storage class to upload your data to based on your use case.

>!
>If the storage class is not set when an object is uploaded, it defaults to **STANDARD**.

## STANDARD

COS STANDARD is a highly reliable, accessible, and powerful object storage service that is designed for hot data, featuring low access latency and high throughput.

**Use cases**

Use cases involving lots of hotspot files or frequent data access, such as hotspot videos, social images, mobile apps, game programs, and static websites.

STANDARD is a COS storage class that is designed for general-purpose storage and covers the majority of use cases.


## STANDARD_IA

COS STANDARD_IA is a highly reliable object storage service with low storage cost and low access latency. It allows you to access the first byte in milliseconds with the price reduced. You can retrieve data quickly without waiting. Unlike STANDARD, STANDARD_IA involves data retrieval fees when you access data.

**Use cases**

Use cases with rather low access frequency (for example, 1 to 2 times per month), such as cloud disk data, big data analysis, government and enterprise data, low-frequency archives, and monitoring data.

> STANDARD_IA has minimum storage requirements. If the storage duration is less than 30 days, the bill is calculated as 30 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual size). For more information, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).

## INTELLIGENT TIERING

COS INTELLIGENT TIERING automatically moves objects between the STANDARD and STANDARD_IA tiers according to the access frequency. Data retrieval fees are not involved, reducing storage costs. For more information, please see [Overview - INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38305).

**Use cases**

Use cases with uncertain data access patterns. If your business has tight controls on costs and is less sensitive to file reading performance, INTELLIGENT TIERING could be your choice for cost reduction.

> !INTELLIGENT TIERING has minimum storage requirements. If the storage duration is less than 30 days, the bill is calculated as 30 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual size). For more information, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).

## ARCHIVE

COS ARCHIVE is a highly reliable object storage service designed for cold data, and offers very low storage cost and long-term data retention. This storage class has a minimum storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it to STANDARD first.

You can restore your objects in the following three modes:

- Expedited: restores an object of up to 256 MB within 1-5 minutes.
- Standard: restores an object within 3-5 hours.
- Bulk: restores multiple objects within 5-12 hours.                      

> ?For the restoration guides, please see [Restoring an Archived Object](https://intl.cloud.tencent.com/document/product/436/30961).

**Use cases**

Use cases that require long-term data retention, such as archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

> !ARCHIVE has minimum storage requirements. If the storage duration is less than 90 days, the bill is calculated as 90 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual size). For more information, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).

## DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage cost and long-term data retention. This storage class has a minimum storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it to STANDARD first. For more information, please see [Overview - DEEP ARCHIVE](https://intl.cloud.tencent.com/document/product/436/38304).

You can restore your objects in either of the following modes:

- Standard: restores an object within 12-24 hours.
- Bulk: restores multiple objects within 24-48 hours. 

**Use cases**

Use cases that require long-term data retention, such as medical images, security monitoring data, and logs.

> !DEEP ARCHIVE has minimum storage requirements. If the storage duration is less than 180 days, the bill is calculated as 180 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual size). For more information, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos).

## Comparison of Storage Classes

| Metric           | INTELLIGENT<br>TIERING                         | STANDARD           | STANDARD_IA                     | ARCHIVE                                                     | DEEP ARCHIVE                                                 |
| ---------------- | ---------------------------------------- | ------------------ | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Durability       | 99.9999999<br>99%                        | 99.9999999<br>99%  | 99.9999999<br>99%            | 99.9999999<br>99%                                            | 99.9999999<br>99%                                            |
| Availability       | 99.99%                                   | 99.95%             | 99.9%                        | 99.9%                                                        | 99.9%                                                        |
| Response             | Milliseconds                                   | Milliseconds             | Milliseconds                       | Requires restoration in advance using one of these three restoration modes:<br><li>Expedited: restores an object of up to 256 MB in 1-5 minutes.<br><li>Standard: restores an object in 3-5 hours.<br><li>Bulk: restores multiple objects in 5-12 hours. | Requires restoration in advance using either of these restoration modes:<br><li>Standard: restores an object in 12-24 hours.<br><li>Bulk: restores multiple objects in 24-48 hours. |
| Minimum billable object size | 64 KB. Objects with sizes smaller than 64 KB are stored in the STANDARD tier | Calculated by actual object size | 64 KB                         | 64 KB                                                         | 64 KB                                                         |
| Minimum storage duration     | 30 days                                     | No limit             | 30 days                         | 90 days                                                         | 180 days                                                        |
| Supported region         | Only Beijing, Shanghai, Guangzhou, and Chongqing     | All regions           | All regions                     | Public cloud regions only                                           | Only Beijing, Shanghai, Guangzhou, and Chengdu                           |
| Storage fees         | Consistent with the price of storage class after the storage class movement                  | Standard               | Low                           | Very Low                                                         | Ultra-low                                                         |
| Data retrieval fees     | None                                       | None                 | Rather low. Charged by actual amount of data read | Rather high. Charged by actual amount of data restored depending on the restoration mode           | High. Charged by actual amount of data restored depending on the restoration mode             |
| Request fees         | Rather high. You will also be charged the INTELLIGENT TIERING object monitoring fees     | Standard               | Rather high                         | Standard (data needs to be restored to STANDARD first)                                 | High (data needs to be restored to STANDARD first). To retrieve DEEP ARCHIVED data, data retrieval request fees will be incurred. |
| Data processing         | Supported                                     | Supported               | Supported                         | Supported (available after data restoration)                                             | Supported (available after data restoration)                                             |

## Moving Objects Between Storage Classes

COS offers multiple storage classes that indicate how active objects are in COS. You can move objects between these storage classes as needed, for example, from a hot storage class (e.g., STANDARD) to a colder one (e.g., STANDARD_IA, ARCHIVE, and DEEP ARCHIVE). For more information, please see the following documents:

- [Modifying Storage Class](https://intl.cloud.tencent.com/document/product/436/30930) 
- [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605) 