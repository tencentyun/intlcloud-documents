Cloud Object Storage (COS) offers the MAZ_STANDARD, MAZ_STANDARD_IA, MAZ_INTELLIGENT TIERING, INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE storage classes for objects with different access frequency and disaster recovery levels. They indicate how active objects are in COS, and vary from one another in access frequency, durability, availability, latency, and more. You can choose which storage class to upload your objects to as needed.

> !
> - If you did not specify the storage class when uploading an object, it will be uploaded to **STANDARD** by default.
> - For more information on multi-AZ, see [Overview of Multi-AZ Feature](https://intl.cloud.tencent.com/document/product/436/35208).
> 

## MAZ_STANDARD/STANDARD

Both MAZ_STANDARD and STANDARD storage classes are highly reliable, available, and powerful object storage service designed for hot data and feature low latency and high throughput.

MAZ_STANDARD has higher data durability and service availability than STANDARD. It uses a different storage mechanism to store the data in different data centers in the same region, so as to prevent failures in one data center from affecting the entire service and further guarantee your business stability.

**Use cases**

Use cases involving lots of hotspot files or frequent data access, including trending videos, social images, mobile apps, game programs, and static websites.

The STANDARD storage class is designed for general use and covers most use cases. It is more cost-effective than MAZ_STANDARD.

However, MAZ_STANDARD has higher data durability and service availability, making it suitable for business scenarios with higher requirements, including key files, commercial data, and sensitive information.

## MAZ_STANDARD_IA/STANDARD_IA

Both MAZ_STANDARD_IA and STANDARD_IA storage classes are highly reliable object storage services with low storage costs and access latency. They allow you to access the first byte in milliseconds at a reduced price, so you can retrieve data quickly without waiting. Unlike STANDARD, they involve data retrieval fees when you access data.

MAZ_STANDARD_IA uses a different storage mechanism from STANDARD_IA to store the data in different data centers in the same region, so as to prevent failures in one data center from affecting the entire service and further guarantee your business stability.

**Use cases**

Use cases with low access frequency (for example, 1 to 2 times per month), such as cloud disk data, big data analysis, government and enterprise data, low-frequency archives, and monitoring data.

>! Both MAZ_STANDARD_IA and STANDARD_IA have minimum storage requirements. If the storage duration is less than 30 days, the bill is calculated as 30 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual file size). For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
>

## MAZ_INTELLIGENT TIERING/INTELLIGENT TIERING

Objects in the MAZ_INTELLIGENT TIERING storage class can be stored in two storage layers: MAZ_STANDARD and MAZ_STANDARD_IA. Objects in the INTELLIGENT_TIERING storage class can also be stored in two storage classes: STANDARD and STANDARD_IA. COS will automatically switch between storage classes based on the access frequency of such objects with no data retrieval fees incurred, which reduces your storage costs. For more information, see [INTELLIGENT TIERING Overview](https://intl.cloud.tencent.com/document/product/436/38305).

MAZ_INTELLIGENT TIERING uses a different storage mechanism from INTELLIGENT TIERING to store the data in different data centers in the same region, so as to prevent failures in one data center from affecting the entire service and further guarantee your business stability.

**Use cases**

Use cases with uncertain data access patterns. If your business has tight controls on costs and is less sensitive to file reading performance, you can use MAZ_INTELLIGENT TIERING or INTELLIGENT TIERING to reduce costs.

>! For MAZ_INTELLIGENT TIERING and INTELLIGENT_TIERING, objects are billed based on their actual sizes. For more information on pricing, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
>

## ARCHIVE

COS ARCHIVE is a highly reliable object storage service designed for cold data, and offers very low storage costs and long-term data retention. This storage class has a minimum storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it to STANDARD first.

COS supports the following three restoration modes for ARCHIVE:

- Expedited: Restores an object within 1-5 minutes.
- Standard: Restores an object within 3-5 hours.
- Bulk: Restores objects within 5-12 hours.                      

>? 
> - For more information about object restoration, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
> - The QPS for restoration requests is limited to 100.
> 

**Use cases**

Use cases that require long-term data retention, such as archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

> !ARCHIVE has minimum storage requirements. If the storage duration is less than 90 days, the bill is calculated as 90 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual file size). For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
>

## DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage costs and long-term data retention. This storage class has a minimum storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it to STANDARD first. For more information, see [Overview - DEEP ARCHIVE](https://intl.cloud.tencent.com/document/product/436/38304).

COS supports the following two restoration modes for DEEP ARCHIVE:

- Standard: Retrieves an object within 12-24 hours.
- Bulk: Retrieves multiple objects within 24-48 hours. 

>? The QPS of data restoration requests is limited to 100.
>

**Use cases**

Use cases that require long-term data retention, such as medical images, view data, and logs.

> !DEEP ARCHIVE has minimum storage requirements. If the storage duration is less than 180 days, the bill is calculated as 180 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual file size). For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
>

## Storage Class Comparison

| Comparison Item           | MAZ_STANDARD<br>    | MAZ_STANDARD_IA<br>     |  MAZ_INTELLIGENT TIERING<br>    | INTELLIGENT TIERING<br>                                       | STANDARD           | STANDARND_IA                     | ARCHIVE                                     | DEEP ARCHIVE                                                 |
| ---------------- | ------------------------ | ------------------------ | ---------------- | ------------------------------------------------------- | ------------------ | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
|   Storage class parameter   |   MAZ_STANDARD    |  MAZ_STANDARD_IA  |  MAZ_INTELLIGENT_TIERING  |  INTELLIGENT_TIERING  |  STANDARD  |  STANDARD_IA  |  ARCHIVE  | DEEP_ARCHIVE   |
| Data durability       | 99.9999999<br>999%       | 99.9999999<br>999%           | 99.9999999<br>999%           |    99.9999999<br>99%                                       | 99.9999999<br>99%  | 99.9999999<br>99%            | 99.9999999<br>99%                                            | 99.9999999<br>99%                                            |
| Service availability       | 99.995%                   | 99.995%                       |  99.995%                       |  99.99%                                                  | 99.95%             | 99.9%                        | 99.9%                                                        | 99.9%                                                        |
| Response             | Milliseconds                   | Milliseconds            | Milliseconds              | Milliseconds                                                  | Milliseconds             | Milliseconds                       | Requires restoration in advance by using one of three restoration modes:<ul  style="margin: 0;"><li>Expedited: Restores an object within 1-5 minutes.</li><li>Standard: Restores an object within 3-5 hours.</li><li>Bulk: Restores multiple objects within 5-12 hours.</li></ul> | Requires restoration in advance by using one of two restoration modes:<ul  style="margin: 0;"><li>Standard: Restores an object within 12-24 hours.</li><li>Bulk: Restores multiple objects within 24-48 hours.</li></ul> |
| Minimum billable object size | Measured by actual object size       | 64 KB               | Measured by actual object size            | Measured by actual object size | Measured by actual object size | 64 KB                         | 64 KB                                                         | 64 KB                                                         |
| Minimum storage duration     | No limit                   | 30 days             | No limit                 | No limit                                                    | No limit             | 30 days                         | 90 days                                                         | 180 days                                                        |
| Supported regions         | Only Beijing, Shanghai, Guangzhou, and Singapore | Only Beijing, Shanghai, Guangzhou, and Singapore    | Only Beijing, Shanghai, Guangzhou, and Singapore     | Only Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore                    | All regions           | All regions                     | All public cloud regions except Jakarta                                           | Only Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore                         |
| Storage fees         | High                     | High                | Varied by the storage class after intelligent tiering            | Varied by the storage class after intelligent tiering                                  | Standard               | Low                           | Very low                                                         | Ultra low                                                         |
| Data retrieval fees     | None                       | Rather low. Charged by the actual amount of data read   | None       | None                                       | None                 | Rather low. Charged by the actual amount of data read | Rather high. Charged by the actual amount of data restored depending on the restoration mode           | High. Charged by the actual amount of data restored depending on the restoration mode             |
| Request fees         | Standard                     | Rather high                 | Rather high. You will also be charged the INTELLIGENT TIERING object monitoring fees               | Rather high. You will also be charged the INTELLIGENT TIERING object monitoring fees     | Standard               | Rather high                         | Standard (the data needs to be restored to STANDARD first)                                 | High (the data needs to be restored to STANDARD first). To retrieve DEEP ARCHIVED data, request fees for retrieving data will be incurred |
| Data processing         | Supported                     | Supported            | Supported                  | Supported                                                    | Supported               | Supported                         | Supported (requires data restoration first)                                            | Supported (requires data restoration first)                                           |

## Storage Class Transition

COS offers various storage classes to indicate how active objects are in COS. You can still change the storage class for objects as needed, or transition objects to a less active storage class such as STANDARD_IA, ARCHIVE, or DEEP ARCHIVE.

>?
> - When transitioning objects, ensure that the target storage class is supported for the region where your object resides.
> - To modify the storage class of an object stored in **ARCHIVE** or **DEEP ARCHIVE**, you need to restore it first into STANDARD. For more information, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
> 

How each storage class can be transitioned is described as follows:

| Storage Class | Available Target Storage Class                 | Transition Priority  |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MAZ_STANDARD     | MAZ_STANDARD_IA, MAZ_INTELLIGENT TIERING                    | MAZ_STANDARD > MAZ_STANDARD_IA > MAZ_INTELLIGENT TIERING |
| MAZ_STANDARD_IA     | MAZ_STANDARD, MAZ_INTELLIGENT TIERING                     | MAZ_STANDARD_IA > MAZ_INTELLIGENT TIERING                                                     |
| MAZ_INTELLIGENT TIERING | MAZ_STANDARD, MAZ_STANDARD_IA                         | None                                                           |
| INTELLIGENT TIERING          | STANDARD, STANDARD_IA, ARCHIVE, DEEP ARCHIVE                   | INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE                       |
| STANDARD              | INTELLIGENT TIERING, STANDARD_IA, ARCHIVE, DEEP ARCHIVE               | STANDARD > STANDARD_IA > INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE |
| STANDARD_IA              | INTELLIGENT TIERING, STANDARD, ARCHIVE, DEEP ARCHIVE               | STANDARD_IA > INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE            |
| ARCHIVE              | INTELLIGENT TIERING, STANDARD, STANDARD_IA, DEEP ARCHIVE (after restoration) | ARCHIVE > DEEP ARCHIVE                                      |
| DEEP ARCHIVE          | INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE (after restoration)  | None    |


For detailed directions, see the following documents:

- [Modifying Storage Classes](https://intl.cloud.tencent.com/document/product/436/30930) 
- [Setting Lifecycles](https://intl.cloud.tencent.com/document/product/436/14605) 



