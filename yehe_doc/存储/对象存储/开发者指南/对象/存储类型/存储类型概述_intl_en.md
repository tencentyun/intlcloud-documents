
COS offers the following storage classes of objects: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. They indicate how active objects are in COS, and vary from one another in access frequency, durability, availability, latency, and more. You can choose which storage class to upload your data to based on your use case.

>!
> If the storage class is not set when an object is uploaded, it defaults to **STANDARD**.

## STANDARD

COS STANDARD is a highly reliable, available and powerful object storage service. Its low latency and high throughout make it well suited for use cases involving lots of hotspot files or frequent data access.

#### Features

- Data durability: 99.999999999%
- Service availability: 99.95%
- Response: within milliseconds
- Regions: all
- Storage fees: standard

#### Use cases

Hotspot videos, social images, mobile apps, game programs, and static websites.

## STANDARD_IA

COS STANDARD_IA is a highly reliable object storage service with low storage cost and low access latency. It enables you to save more on storage costs and access the first byte in milliseconds. You can retrieve data quickly without waiting. As data retrievals are chargeable, this storage class is suitable for use cases involving infrequent access (e.g., once or twice per month).


#### Features

- Data durability: 99.999999999%
- Service availability: 99.9%
- Minimum storage duration: 30 days
- Minimum billable object size: 64 KB
- First-byte latency: milliseconds
- Regions: all
- Storage cost: low

**Use cases**

Online file storage, big data analytics, governmental/organizational business data, low-frequency archives, and monitoring data.

>! STANDARD_IA storage class has a minimum storage duration of 30 days. If you delete or modify objects before 30 days, you will still need to pay for 30 days of storage. For pricing information, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).

## ARCHIVE

COS ARCHIVE is a highly reliable object storage service that offers very low storage cost and long-term data retention. This storage class has a minimal storage duration of 90 days. To read data stored in ARCHIVE, you need to restore it to STANDARD first. Therefore, it is suited for archived data that needs to be stored for a long time.

#### Features

- Data durability: 99.999999999%
- Service availability: 99.9%
- Minimum storage duration: 90 days
- Minimum billable object size: 64 KB
- Response: requires data restoration first
- Supported regions: public cloud regions only
- Storage cost: very low

#### Use cases

Archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

>! ARCHIVE storage class has a minimum storage duration of 90 days. If you delete or modify objects before 90 days, you will still need to pay for 90 days of storage. For pricing information, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).

## DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage cost and long-term data retention. This storage class has a minimal storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore it to STANDARD first. Therefore, it is suited for archived data that needs to be stored for a long time.


#### Features

- Data durability: 99.999999999%
- Service availability: 99.9%
- Minimum storage duration: 180 days
- Minimum billable object size: 64 KB
- Response: requires data restoration first
- Supported regions: Beijing, Shanghai, Guangzhou, Chengdu
- Storage cost: ultra-low


#### Use cases

Medical images, security monitoring data, and logs.

>! DEEP ARCHIVE storage class has a minimum storage duration of 180 days. If you delete or modify objects before 180 days, you will still need to pay for 180 days of storage. For pricing information, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).

## Comparison of Storage Classes

| Metric           | STANDARD           | STANDARD_IA                     | ARCHIVE                                                     | DEEP ARCHIVE                                                 |
| ------------------- | ------------------ | ------------- | ------------------- |------| 
| Durability       | 99.9999999<br>99%  | 99.9999999<br>99%            | 99.9999999<br>99%                                            | 99.9999999<br>99%                                            |
| Availability       | 99.95%             | 99.9%                        | 99.9%                                                        | 99.9%                                                        |
| Response             | Milliseconds             | Milliseconds                       | Requires restoration in advance using one of these three restoration modes:<br><li>Expedited: retrieves an object of up to 256 MB in 1 - 5 min.<br><li>Standard: retrieves an object in 3 - 5 hours.<br><li>Bulk: retrieves multiple objects in 5 - 12 hours. | Requires restoration in advance using either of these two restoration modes:<br><li>Standard: retrieves an object in 12 - 24 hours.<br><li>Bulk: retrieves multiple objects in 24 - 48 hours. |
| Minimum billable object size | Measured by actual object size         | 64 KB                        | 64 KB                                   | 64 KB                           |
| Minimum storage duration     | No limit                      | 30 days                        | 90 days                                   | 180 days                          |
| Supported regions         | All regions           | All regions                     | Only public cloud regions                                           | Only Beijing, Shanghai, Guangzhou, and Chengdu regions                           |
| Storage fees         | Standard               | Low                           | Very low                                                        | Ultra-low                                                         |
| Data retrieval fees     | None                 | Rather low. Charged by actual amount of data read | Rather high. Charged by actual amount of data restored depending on the restoration mode           | High. Charged by actual amount of data restored depending on the restoration mode             |
| Request fees         | Standard               | Rather high                         | Standard (requires restoration to STANDARD first)                                 | High (requires restoration to STANDARD first). Fees for both read/write requests and data retrieval requests apply to DEEP ARCHIVE storage class |
|Data processing     |Supported |   Supported   |Supported (requires data restoration first)  |  Supported (requires data restoration first)  |



