COS offers the following object storage classes for different access frequencies: STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE.

> !COS objects are uploaded to the **STANDARD** storage class by default.

## STANDARD

COS STANDARD is a highly reliable, accessible and powerful object storage service. Its low latency and high throughout make it well suited for use cases involving lots of hotspot files or frequent data access.

#### Features

- Durability: 99.999999999%
- Availability: 99.95%
- Response: within milliseconds
- Regions: all
- Storage cost: standard

#### Use cases

Hotspot videos, social images, mobile apps, game programs, and static websites.

## STANDARD_IA

COS STANDARD_IA is a highly reliable object storage service with low storage cost and low access latency. It enables you to save more on storage costs and access the first byte in milliseconds. You can retrieve the data quickly without waiting. The data retrieval is chargeable, so this storage class is suitable for the use cases involving infrequent access (e.g., once or twice per month).


#### Features

- Durability: 99.999999999%
- Availability: 99.9%
- Minimum storage duration: 30 days
- Minimum allowed object size: 64 KB
- First-byte latency: within milliseconds
- Regions: all
- Storage cost: low

**Use cases**

Online file storage, big data analytics, governmental/organizational business data, low-frequency archives, and monitoring data.

## ARCHIVE

COS ARCHIVE is a highly reliable object storage service that offers very low storage cost and long-term data retention. This storage class has a minimal storage duration of 90 days. To read data stored in ARCHIVE, you need to restore them first. Therefore, it is suited for archived data that needs to be stored for a long time.

#### Features

- Durability: 99.999999999%
- Availability: 99.9%
- Minimum storage duration: 90 days
- Minimum allowed object size: 64 KB
- Response: requires prior restore request
- Regions: currently only Public Cloud regions (excluding Nanjing)
- Storage fees: ultra-low

#### Use cases

Archival data, medical images, scientific data and other compliance files, lifecycle files, logs, and remote disaster recovery.

## DEEP ARCHIVE

COS DEEP ARCHIVE is a highly reliable object storage service that offers the lowest storage cost and long-term data retention. This storage class has a minimal storage duration of 180 days. To read data stored in DEEP ARCHIVE, you need to restore them first. Therefore, it is suited for archived data that needs to be stored for a long time.


#### Features

- Durability: 99.999999999%
- Availability: 99.9%
- Minimum billing duration: 180 days
- Minimum allowed object size: 64 KB
- Response: requires prior restore request
- Regions: Beijing, Guangzhou, and Chengdu
- Storage fees: ultra-low


#### Use cases

Medical images, security monitoring data, and logs.


## Comparison

| Metric | STANDARD | STANDARD_IA | ARCHIVE | DEEP ARCHIVE |
| ---------------- | ------------------ | ------------- | -------------------------------------- | ------------------------------ |
| Durability     | 99.999999999%      | 99.999999999% | 99.999999999%                          | 99.999999999%                  |
| Availability      | 99.95%             | 99.9%         | 99.9%                                  | 99.9%                          |
| Response | Millisecond level | Millisecond level | Requires restoration in advance |
| Minimum allowed object size | Measured by actual object size | 64 KB | 64 KB | 64 KB |
| Minimum storage duration | No limit | 30 days | 90 days | 180 days |
| Regions | All regions| All regions | Only Public Cloud regions (currently excluding Nanjing) | Only Beijing, Guangzhou, and Chengdu regions |
| Storage fees | Standard | Low | Very low | Ultra-low |
| Data retrieval fees | None | Low | High |High |
| Read/Write request fees | Very low | Low | Very low (requires objects to be restored into STANDARD first) | High (requires objects to be restored into STANDARD first) |