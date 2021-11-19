COS offers the INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE storage classes for objects with different access frequency and disaster recovery levels. They indicate how active objects are in COS, and vary from one another in access frequency, durability, availability, latency, and more. You can choose which storage class to upload your objects to as needed.

> !
>
> - If you did not specify the storage class for an object upon upload, it will be uploaded to **STANDARD** by default.


## ARCHIVE

COS ARCHIVE is a highly reliable object storage service designed for cold data, and offers very low storage costs and long-term data retention. This storage class has a minimum storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it to STANDARD first.

COS supports the following three restoration modes for ARCHIVE:

- Expedited: restores an object within 1-5 minutes.
- Standard: restores an object within 3-5 hours.
- Bulk: restores objects within 5-12 hours.                      

> ? 
> - For more information about object restoration, please see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
> - The QPS for restoration requests is limited to 100.

**Use cases**

Use cases that require long-term data retention, such as archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

> !ARCHIVE has minimum storage requirements. If the storage duration is less than 90 days, the bill is calculated as 90 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual file size). For more information, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).

## DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage costs and long-term data retention. This storage class has a minimum storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it to STANDARD first. For more information, please see [Overview - DEEP ARCHIVE](https://intl.cloud.tencent.com/document/product/436/38304).

COS supports the following two restoration modes for DEEP ARCHIVE:

- Standard: retrieves an object within 12-24 hours.
- Bulk: retrieves multiple objects within 24-48 hours. 

> ? The QPS of data restoration requests is limited to 100.

**Use cases**

Use cases that require long-term data retention, such as medical images, security monitoring data, and logs.

> !DEEP ARCHIVE has minimum storage requirements. If the storage duration is less than 180 days, the bill is calculated as 180 days. Likewise, if the size of a file is smaller than 64 KB, the bill is calculated as 64 KB (if the size of a file is greater than or equal to 64 KB, the bill is calculated based on the actual file size). For more information, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).

## Storage Class Comparison

| Metric          | INTELLIGENT<br>TIERING                                        | STANDARD           | STANDARD_IA                     | ARCHIVE                                                     | DEEP ARCHIVE                                                 |
| ---------------- | ------------------------ | ------------------------ | ---------------- | ------------------------------------------------------- | ------------------ | ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Durability       | 99.9999999<br>99%                                       | 99.9999999<br>99%  | 99.9999999<br>99%            | 99.9999999<br>99%                                            | 99.9999999<br>99%                                            |
| Availability      | 99.99%                                                  | 99.95%             | 99.9%                        | 99.9%                                                        | 99.9%                                                        |
| Response             | Milliseconds                                   | Milliseconds             | Milliseconds                       | Requires restoration in advance using one of these three restoration modes:<br><li>Expedited: restores an object within 1-5 minutes.<br><li>Standard: restores an object within 3-5 hours.<br><li>Bulk: restores multiple objects within 5-12 hours. | Requires restoration in advance using either of these restoration modes:<br><li>Standard: restores an object within 12-24 hours.<br><li>Bulk: restores multiple objects within 24-48 hours. |
| Minimum billable object size | 64 KB. Objects with sizes smaller than 64 KB are stored in the STANDARD tier | Calculated by the actual object size | 64 KB                         | 64 KB                                                         | 64 KB                                                         |
| Minimum storage duration     | 30 days                             | No limit             | 30 days                         | 90 days                                                         | 180 days                                                        |
| Supported regions         | Only Beijing, Shanghai, Guangzhou, Chongqing, and Tokyo     | All regions           | All regions                     | Only public cloud regions                                           | Only Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, and Tokyo                          |
| Storage fees         | Differ depending on the storage class after intelligent tiering                                  | Standard               | Low                           | Very low                                                         | Ultra-low                                                         |
| Data retrieval fees     | None                                       | None                 | Rather low. Charged by the actual amount of data read | Rather high. Charged by the actual amount of data restored depending on the restoration mode           | High. Charged by the actual amount of data restored depending on the restoration mode             |
| Request fees         | Rather high. You will also be charged the INTELLIGENT TIERING object monitoring fees     | Standard               | Rather high                         | Standard (the data needs to be restored to STANDARD first)                                 | High (the data needs to be restored to STANDARD first). To retrieve DEEP ARCHIVED data, request fees for retrieving data will be incurred |
| Data processing        | Supported                                                    | Supported               | Supported                         | Supported (requires data restoration first)                                            | Supported (requires data restoration first)                                           |

## Storage Class Transition

COS offers various storage classes to indicate how active objects are in COS. You can still change the storage class for objects as needed, or transition objects to a less active storage class such as STANDARD_IA, ARCHIVE, or DEEP ARCHIVE.

>?
>- When transitioning objects, ensure that the target storage class is supported for the region where your object resides.
>- To modify the storage class of an object stored in **ARCHIVE** or **DEEP ARCHIVE**, you need to restore it first into STANDARD. For more information, see [Restoring an Archived Object](https://intl.cloud.tencent.com/document/product/436/30961).

How each storage class can be transitioned is described as follows:

| Storage Class | Available Target Storage Class                 | Transition Priority  |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| INTELLIGENT TIERING          | STANDARD, STANDARD_IA, ARCHIVE, DEEP ARCHIVE                   | INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE                       |
| STANDARD              | INTELLIGENT TIERING, STANDARD_IA, ARCHIVE, DEEP ARCHIVE               | STANDARD > STANDARD_IA > INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE |
| STANDARD_IA              | INTELLIGENT TIERING, STANDARD, ARCHIVE, DEEP ARCHIVE               | STANDARD_IA > INTELLIGENT TIERING > ARCHIVE > DEEP ARCHIVE            |
| ARCHIVE              | INTELLIGENT TIERING, STANDARD, STANDARD_IA, DEEP ARCHIVE (after restoration) | ARCHIVE > DEEP ARCHIVE                                      |
| DEEP ARCHIVE          | INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE (after restoration)  | None    |


For detailed directions, please see the following documents:

- [Modifying Storage Classes](https://intl.cloud.tencent.com/document/product/436/30930) 
- [Setting Lifecycles](https://intl.cloud.tencent.com/document/product/436/14605) 

  
