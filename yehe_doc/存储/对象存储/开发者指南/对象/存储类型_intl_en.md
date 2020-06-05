COS is available in 3 storage classes depending on the access frequency: STANDARD, STANDARD_IA, and ARCHIVE.

>When an object is uploaded, if the storage class is not set, it defaults to **STANDARD**.


## STANDARD

COS STANDARD is an object storage service that provides users with high reliability, availability, and performance.

It offers low access latency and high throughput, making it suitable for business scenarios where a massive number of trending files are accessed in real time with frequent data interactions.

**Features**

- High reliability, availability, and performance
- Data durability: 99.999999999%
- Service availability: 99.95%
- Response: within milliseconds
- Regions: all
- Storage fees: standard

**Scenarios**

Trending videos, social networking photos, mobile apps, games, static websites, and more.

## STANDARD_IA

COS STANDARD_IA is an object storage service that provides users with high reliability, low storage cost, and low access latency.

It offers lower pricing for storage and keeps the first-byte access time within milliseconds, ensuring that data can be fast retrieved with no wait required. However, data retrieval incurs fees. It is suitable for business scenarios where the access frequency is low (e.g., once or twice per month).

**Features**

- Low-frequency access, real-time response
- Data durability: 99.999999999%
- Service availability: 99.9%
- Minimum storage duration for billing: 30 days
- Minimum billable object size: 64 KB
- First-byte latency: within milliseconds
- Regions: all
- Storage cost: low

**Scenarios**

Online file storage, big data analytics, governmental/organizational business data, low-frequency archives, monitoring data, and more.

## ARCHIVE

COS ARCHIVE is an object storage service that provides users with high reliability, extremely low storage cost, and long-term data retention.

Featuring the lowest storage price, the ARCHIVE storage class needs a relatively long time to read data and is suited for archived data that needed to be stored for a long time.

**Features**

- High data durability and service availability, low cost
- Data durability: 99.999999999%
- Service availability: 99.9%
- Minimum storage duration for billing: 90 days
- Minimum billable object size: 64 KB
- Response: requires prior restore request
- Regions: currently only Public Cloud regions (excluding Nanjing)
- Storage fees: very low

**Scenarios**

Archived compliance documents (e.g., archival data, medical images, and scientific materials), lifecycle files, operational logs, cross-region disaster recovery, and more.

## Comparison of Storage Classes

| Item           | STANDARD           | STANDARD_IA      |  ARCHIVE                     |
| ---------------- |------------------ | ------------- | ---------------------------- |
| Data durability       | 99.999999999%      | 99.999999999% | 99.999999999%                |
| Service availability       |99.95%             | 99.9%         | 99.9%                        |
| Response             |  Within milliseconds             | Within milliseconds        | Requires prior restore request               |
| Minimum billable object size | Billed for the actual size | 64 KB          | 64 KB                         |
| Minimum storage duration for billing     | N/A            | 30 days         | 90 days                         |
| Regions | All | All | Only Public Cloud regions (currently excluding Nanjing) |
| Storage fees         | Standard               | Low          | Very low                         |
| Data retrieval fees     | Free | Low          | High                         |
| Read/Write request fees     |  Very low               | Low          | Very low (requires data to be restored first into STANDARD) |




