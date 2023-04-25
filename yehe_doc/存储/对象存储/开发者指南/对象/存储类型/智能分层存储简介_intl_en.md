## Overview

INTELLIGENT TIERING is a COS storage class designed to reduce storage costs by automatically moving objects between two storage tiers (frequent access and infrequent access) when access patterns change.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput as STANDARD while featuring lower costs. Users can change the storage class of objects with uncertain access patterns from STANDARD to INTELLIGENT TIERING as needed to reduce in-cloud storage costs.

>!
> - INTELLIGENT TIERING is currently supported in Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore regions. MAZ_INTELLIGENT TIERING is available only in Beijing, Shanghai, Guangzhou, and Singapore regions.
> - INTELLIGENT TIERING is a standalone storage class that will incur storage usage fees and object monitoring fees. You can purchase an INTELLIGENT TIERING storage pack to redeem the storage usage fees. For detailed pricing, see [Product Pricing](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
> 

## Advantages

The access patterns of data stored in INTELLIGENT TIERING will be monitored. COS moves objects that have not been accessed for a continuous period to the lower-cost infrequent access tier. If an object in the infrequent access tier is accessed later, it is automatically moved back to the frequent access tier to ensure the data retrieval performance. INTELLIGENT TIERING manages to strike a balance between storage costs and read/write performance and features the following strengths:

- **Cost-effective**: When you use INTELLIGENT TIERING for persistent storage, the longer your data is stored, the more you can save on your storage costs (up to about 20%) compared with the STANDARD storage class. INTELLIGENT TIERING is also involved in the object storage lifecycle, where you can transition your INTELLIGENT TIERING data to ARCHIVE to further lower storage costs.
- **Stable and durable**: INTELLIGENT TIERING provides the same low latency and high throughput as the STANDARD storage class. Besides, it offers durability of up to 99.999999999% (11 9s) by using erasure code-based redundancy, and up to 99.95% availability by using block storage and concurrent reads/writes. INTELLIGENT TIERING has also been integrated with the COS MAZ architecture, featuring high durability (99.9999999999%, that is, 12 9s) and availability (99.995%).
- **Easy-to-use**: To use INTELLIGENT TIERING, all you need to do is specify it as the storage class of your object. This COS storage class is inherently compatible with COS APIs, SDKs, tools, and applications, making it easy for you to manage your in-cloud data as needed.

## How to Use

To store your object in the COS INTELLIGENT TIERING storage class, enable INTELLIGENT TIERING for the bucket, and then specify the **storage class** of your object as INTELLIGENT TIERING.

### Using COS console

#### Setting INTELLIGENT TIERING upon object uploads

You can perform the following steps to store your object in the INTELLIGENT TIERING storage class:

1. On the bucket configuration page, enable INTELLIGENT TIERING. For more information on the process of enabling INTELLIGENT TIERING, see [Setting INTELLIGENT TIERING](https://www.tencentcloud.com/document/product/436/38306).
2. Upload a file and specify the storage class during the upload. For more information about how to upload a file, see [Uploading Objects](https://www.tencentcloud.com/document/product/436/13321).

>! Once INTELLIGENT TIERING is enabled for a bucket, it cannot be disabled.
>

#### Moving in-cloud objects to INTELLIGENT TIERING

You can perform the following steps to move in-cloud objects to the INTELLIGENT TIERING storage class:

1. On the bucket configuration page, create a lifecycle rule. For detailed directions, see [Setting Lifecycle](https://www.tencentcloud.com/document/product/436/14605).
2. Specify the application range and transition objects to INTELLIGENT TIERING.



### Using the REST API

You can use the following APIs to configure INTELLIGENT TIERING:

1. Use RESTful APIs to enable INTELLIGENT TIERING for your bucket. For more information, see the following API documentation:
	- [PUT Bucket IntelligentTiering](https://www.tencentcloud.com/document/product/436/38314)
	- [GET Bucket IntelligentTiering](https://www.tencentcloud.com/document/product/436/38315)
2. After enabling INTELLIGENT TIERING for the bucket, use the following APIs to store the object in the INTELLIGENT TIERING storage class:
	- [PUT Object](https://www.tencentcloud.com/document/product/436/7749)
	- [PUT Object - Copy](https://www.tencentcloud.com/document/product/436/10881)
	- [POST Object](https://www.tencentcloud.com/document/product/436/14690)
	- [Initiating Multipart Upload](https://www.tencentcloud.com/document/product/436/7746)
3. You can use the following APIs to query the storage class or storage tier of an object:
	- [GET Object](https://www.tencentcloud.com/document/product/436/7753)
	- [HEAD Object](https://www.tencentcloud.com/document/product/436/7745)
4. You can use the following RESTful APIs to delete objects in the INTELLIGENT TIERING storage class:
	- [DELETE Object](https://www.tencentcloud.com/document/product/436/7743)
	- [DELETE Multiple Objects](https://www.tencentcloud.com/document/product/436/8289)

### Using the SDK

Currently, all COS SDKs support INTELLIGENT TIERING. To use this storage class, set `StorageClass` to `INTELLIGENT_TIERING` or `MAZ_INTELLIGENT_TIERING` when uploading an object. For more information, see [Uploading Object](https://www.tencentcloud.com/document/product/436/14107).

## Use Limits

INTELLIGENT TIERING has the following limits:

- **Setting**: The setting cannot be changed once configured. To change it, [contact us](https://intl.cloud.tencent.com/contact-sales). The number of consecutive no-access days for moving objects to the infrequent access tier can be set to 30, 60, or 90.
- **Initial storage tier**: A new object is stored in the frequent access tier by default, and will only be moved to the infrequent access tier if it hasn’t been accessed for a certain period.
- **Minimum storage size**: An object smaller than 64 KB can only be stored in the frequent access tier and cannot be moved between the frequent and infrequent access tiers. Objects are billed based on their actual sizes.
- **Operation**: Uploading objects to INTELLIGENT TIERING using the APPEND Object API is not supported.
- **Lifecycle**: Objects in the INTELLIGENT TIERING storage class can only be transitioned to ARCHIVE or DEEP ARCHIVE. If a STANDARD object is transitioned to INTELLIGENT TIERING, it will be stored in the frequent access tier. If a STANDARD_IA object is transitioned to INTELLIGENT TIERING, it will be stored in the infrequent access tier.
- **Bucket replication**: During bucket replication, if INTELLIGENT TIERING is not enabled for the destination bucket, the object cannot be copied to the INTELLIGENT TIERING storage class.

## FAQs
### How is INTELLIGENT TIERING billed?

INTELLIGENT TIERING fees include **INTELLIGENT TIERING storage usage fees** and **INTELLIGENT TIERING object monitoring fees**.
1. INTELLIGENT TIERING storage usage fees are charged differently depending on the storage tier of objects.
 - When objects are stored in the frequent access tier, STANDARD storage usage fees are charged.
 - When objects are stored in the infrequent access tier, STANDARD_IA storage usage fees are charged.
>?
> - STANDARD and STANDARD_IA storage usage fees vary by region. For details about their pricing, see [Product Pricing](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).
>- Request fees and traffic fees are also incurred during object upload and download. For the billing examples, see [Traffic Fee Billing Example](https://www.tencentcloud.com/document/product/436/33776) and [Request Fee Billing Example](https://www.tencentcloud.com/document/product/436/40100).
>
2. INTELLIGENT TIERING object monitoring fees are charged based on the number of objects stored (excluding files smaller than 64 KB). For detailed pricing, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).

**Example**

Suppose an organization has 100,000 objects (all above 64 KB, 1 TB in total), and the data is stored in the INTELLIGENT TIERING storage class in Beijing region and transitioned to the infrequent access tier after 30 days. If 20% of the objects (i.e., 20,000 objects) are transitioned to the infrequent access tier every 30 days, the object monitoring fees and storage usage fees for **every 30 days** will be as follows:

>?
>In the table below, the object monitoring fees for Beijing region are 0.25 USD/10,000 objects per 30 days, that is, 0.00833333 (0.25 / 30) USD/10,000 objects per day.
| Storage Days | 30-day Object Monitoring Fees (USD) | 30-day INTELLIGENT TIERING Storage Usage Fees (USD) | 30-day STANDARD Storage Usage Fees (USD) |
|-----|----|----|----|
|30 * 1  |  0.25/10,000 objects * 100,000  |  1024 * 0.024 / 30 * 30 = 24.58  |  1024 * 0.024 / 30 * 30 = 24.58  |
|30 * 2  | 0.25/10,000 objects * 100,000   | 819.2 * 0.024 / 30 * 30 + 204.8 * 0.08 / 30 * 30 = 23.35 | 1024 * 0.024 / 30 * 30 = 24.58 |
|30 * 3  | 0.25/10,000 objects * 100,000  | 655.36 * 0.024 / 30 * 30 + 368.64 * 0.08 / 30 * 30 = 22.36 | 1024 * 0.024 / 30 * 30 = 24.58  |
|30 * 4  | 0.25/10,000 objects * 100,000 | 524.288 * 0.024 / 30 * 30 + 499.712 * 0.08 / 30 * 30 = 21.58 | 1024 * 0.024 / 30 * 30 = 24.58  |
|30 * 5  |  0.25/10,000 objects * 100,000  |  419.4304 * 0.024 / 30 * 30 + 604.5696 * 0.08 / 30 * 30 = 20.95  |  1024 * 0.024 / 30 * 30 = 24.58  |
|30 * 6  |  0.25/10,000 objects * 100,000   |  335.54432 * 0.024 / 30 * 30 + 688.45568 * 0.08 / 30 * 30 = 20.45  |  1024 * 0.024 / 30 * 30 = 24.58  |

As you can see, using INTELLIGENT TIERING reduces storage costs over time. Only a small amount of monitoring cost is required every 30 days.

### What types of objects is INTELLIGENT TIERING suitable for?

INTELLIGENT TIERING is suitable for large objects (such as audio and video, logs, etc.) whose access patterns change. Larger average object sizes mean you pay less for monitoring per GB objects. If your business has relatively fixed data access patterns, you can set lifecycle configuration to specify the time to transition objects to STANDARD_IA without the need to use INTELLIGENT TIERING.

### How can I store objects in INTELLIGENT TIERING?
You can store objects in INTELLIGENT TIERING as follows:
- Incremental objects: You just need to specify the storage class as INTELLIGENT TIERING when uploading the objects.
- Existing objects: You can modify the storage class to INTELLIGENT TIERING using the `COPY` API. You can also use the lifecycle feature to transition STANDARD or STANDARD_IA objects to INTELLIGENT TIERING.

>! In INTELLIGENT TIERING, objects smaller than 64 KB will always be stored in STANDARD. Therefore, for objects smaller than 64 KB, we recommend you upload them to the STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE storage class as needed to reduce costs.
>

### How do I disable INTELLIGENT TIERING configuration?

INTELLIGENT TIERING configuration **can't be disabled** once enabled. If you don't need to store your objects in INTELLIGENT TIERING, you just need to specify the storage class as a non-INTELLIGENT TIERING class such as STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE when uploading the objects.
