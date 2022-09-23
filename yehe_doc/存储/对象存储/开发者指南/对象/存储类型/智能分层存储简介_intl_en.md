## Overview

The INTELLIGENT TIERING storage class provides a hot/cold data tiering mechanism. It can automatically switch the hot and cold tiers of your data based on the data access mode, thereby reducing your storage costs.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput as STANDARD while featuring lower costs. You can change the storage class of objects with uncertain access patterns from STANDARD to INTELLIGENT TIERING as needed to reduce your cloud storage costs.

>!
> - INTELLIGENT TIERING is currently supported in Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore regions.
> - INTELLIGENT TIERING is a standalone storage class that incurs storage usage fees. For detailed pricing, see [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos).
> 

## Strengths

COS monitors the access patterns of data stored in INTELLIGENT TIERING and moves objects that have not been accessed for a continuous period of time to the lower-cost infrequent access tier. If an object in the infrequent access tier is accessed later, it will be automatically moved back to the frequent access tier to ensure the data retrieval performance. INTELLIGENT TIERING helps strike a balance between storage costs and read/write performance and features the following strengths:

- **Cost-effective**: When you use INTELLIGENT TIERING for persistent storage, the longer your data is stored, the more you can save on your storage costs (up to about 20%) compared with the STANDARD storage class. INTELLIGENT TIERING is also involved in the object storage lifecycle, where you can transition your INTELLIGENT TIERING data to ARCHIVE to further lower the storage costs.
- **Stable and durable**: INTELLIGENT TIERING provides the same low latency and high throughput as the STANDARD storage class. It also offers a reliability of up to 99.999999999% (eleven nines) by using erasure code to achieve redundancy, and up to 99.95% availability by using block storage and concurrent reads/writes.
- **Easy-to-use**: To use INTELLIGENT TIERING, all you need to do is specify it as the storage class of your object. This COS storage class is inherently compatible with COS APIs, SDKs, tools, and applications, making it easier for you to manage your in-cloud data as needed.

## Directions

To store your object in the INTELLIGENT TIERING storage class, enable INTELLIGENT TIERING for the bucket and specify the **storage class** of your object as INTELLIGENT TIERING.

### Using the COS console

#### Setting INTELLIGENT TIERING during object upload

You can perform the following steps to store your object in the INTELLIGENT TIERING storage class:

1. On the bucket configuration page, enable INTELLIGENT TIERING as instructed in [Setting INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38306).
2. Upload a file as instructed in [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321) and specify the storage class during the upload.

> !Once INTELLIGENT TIERING is enabled for a bucket, it cannot be disabled.

#### Moving in-cloud object to INTELLIGENT TIERING

You can perform the following steps to move existing in-cloud objects to the INTELLIGENT TIERING storage class:

1. On the bucket configuration page, create a lifecycle rule as instructed in [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).
2. Specify the application scope of the rule and transition objects to INTELLIGENT TIERING.



### Using RESTful APIs

You can use the following APIs to configure INTELLIGENT TIERING:

1. Use RESTful APIs to enable INTELLIGENT TIERING for your bucket. For more information, see the following API documents:
	- [PUT Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38314)
	- [GET Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38315)
2. After enabling INTELLIGENT TIERING for the bucket, use the following APIs to store objects in the INTELLIGENT TIERING storage class:
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
	- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
	- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
	- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
3. You can use the following APIs to query the storage class or storage tier of an object:
	- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
	- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
4. You can use the following RESTful APIs to delete objects in the INTELLIGENT TIERING storage class:
	- [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
	- [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### Using SDKs

Currently, all SDKs that COS releases support INTELLIGENT TIERING. To use INTELLIGENT TIERING, you can set `StorageClass` to `INTELLIGENT_TIERING` when uploading a file. For more information, see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).



## Use Limits

INTELLIGENT TIERING has the following limits:

- **Configuration limit**: Once configured, INTELLIGENT TIERING cannot be modified. If you need modification, [contact us](https://intl.cloud.tencent.com/contact-sales).
- **Initial storage tier**: A new object is stored in the frequent access tier by default and will only be moved to the infrequent access tier if it hasn't been accessed for a certain period of time.
- **Minimum storage size**: An object smaller than 64 KB can only be stored in the frequent access tier and cannot be moved between the frequent and infrequent access tiers. Objects are billed based on their actual size.
- **Operation**: Uploading objects to INTELLIGENT TIERING using the `APPEND Object` API is not supported.
- **Lifecycle**: Objects in the INTELLIGENT TIERING storage class can only be transitioned to ARCHIVE or DEEP ARCHIVE. If a STANDARD object is transitioned to INTELLIGENT TIERING, it will be stored in the frequent access tier. If a STANDARD_IA object is transitioned to INTELLIGENT TIERING, it will be stored in the infrequent access tier.
- **Bucket replication**: During bucket replication, if INTELLIGENT TIERING is not enabled for the destination bucket, objects cannot be copied to the INTELLIGENT TIERING storage class.

## FAQs
### How is INTELLIGENT TIERING billed?

INTELLIGENT TIERING fees include **INTELLIGENT TIERING storage usage fees** and **INTELLIGENT TIERING object monitoring fees**.
1. INTELLIGENT TIERING storage usage fees are charged differently depending on the storage tier of objects.
 - When objects are stored in the frequent access tier, STANDARD storage usage fees are charged.
 - When objects are stored in the infrequent access tier, STANDARD_IA storage usage fees are charged.
>?
> - STANDARD and STANDARD_IA storage usage fees vary by region. For details about their pricing, see [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos).
>- Request fees and traffic fees are also incurred during object upload and download. For the billing examples, see [Traffic Fees](https://intl.cloud.tencent.com/document/product/436/33776) and [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
>
2. INTELLIGENT TIERING object monitoring fees are charged based on the number of objects stored. 0.025 USD is charged per 10,000 monitored objects per month.

**Sample**

Assume that an organization has 100,000 objects (10 MB per object, 1 TB in total), and the data is stored in the INTELLIGENT TIERING storage class in Beijing region. If 20% of the objects (i.e., 20,000 objects) transition to the infrequent access tier every month, the object monitoring fees and storage usage fees for each month will be as follows:

| Month | Object Monitoring Fees (USD) | INTELLIGENT TIERING Storage Usage Fees (USD) | STANDARD Storage Usage Fees (USD)|
|----|----|----|----|
|1| 0.25|1024 x 0.024 = 24.58  |   1024 x 0.024 = 24.58  |
|2|0.25|819.2 x 0.024 + 204.8 x 0.018 = 23.35| 1024 x 0.024 = 24.58  |
|3|0.25|655.36 x 0.024 + 368.64 x 0.018 = 22.36 |  1024 x 0.024 = 24.58  |
|4|0.25|524.288 x 0.024 + 499.712 x 0.018 = 21.58 |  1024 x 0.024 = 24.58 |
|5|0.25|419.4304 x 0.024 + 604.5696 x 0.018 = 20.95  |  1024 x 0.024 = 24.58  |
|6|0.25|335.54432 x 0.024 + 688.45568 x 0.018 = 20.45  | 1024 x 0.024 = 24.58 |

As you can see, using INTELLIGENT TIERING reduces storage costs over time. Only a small amount of monitoring fees is incurred each month.

### What types of objects is INTELLIGENT TIERING suitable for?

INTELLIGENT TIERING is suitable for large objects (such as audios, videos, and logs) with changing access patterns. Larger average object sizes mean that you pay less for monitoring per GB of objects. If your business has relatively fixed data access patterns, you can set lifecycle configuration to specify the time to transition objects to STANDARD_IA without the need to use INTELLIGENT TIERING.

### How do I store objects in INTELLIGENT TIERING?
You can store objects in INTELLIGENT TIERING as follows:
- Incremental objects: You just need to specify the storage class as INTELLIGENT TIERING when uploading objects.
- Existing objects: You can modify the storage class to INTELLIGENT TIERING by using the `COPY` API. You can also use the lifecycle feature to transition STANDARD or STANDARD_IA objects to INTELLIGENT TIERING.

>!INTELLIGENT TIERING objects smaller than 64 KB will always be stored in STANDARD. For such objects, we recommend you upload them to the STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE storage class as needed to reduce costs.
>

### How do I disable INTELLIGENT TIERING configuration?

INTELLIGENT TIERING configuration **can't be disabled** once enabled. If you don't need to store your objects in INTELLIGENT TIERING, you just need to specify the storage class as a non-INTELLIGENT TIERING class such as STANDARD, STANDARD_IA, ARCHIVE, or DEEP ARCHIVE when uploading objects.
