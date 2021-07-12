## Overview

INTELLIGENT TIERING is a COS storage class designed to reduce storage costs by automatically moving objects between two storage tiers (frequent access and infrequent access) when access patterns change.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput as STANDARD while featuring lower costs. Users can change the storage class of objects with uncertain access patterns from STANDARD to INTELLIGENT TIERING as needed to reduce in-cloud storage costs.

> !
> - Currently, INTELLIGENT TIERING is only available for the Beijing, Shanghai, Guangzhou, and Chongqing, and Tokyo regions.
> - INTELLIGENT TIERING is a standalone storage class that will incur storage usage fees. You can purchase an INTELLIGENT TIERING storage pack to redeem the cost. For detailed pricing, please see [Product Pricing](https://buy.cloud.tencent.com/price/cos).

## Advantages

The access patterns of data stored in INTELLIGENT TIERING will be monitored. COS moves objects that have not been accessed for a continuous period to the lower-cost infrequent access tier. If an object in the infrequent access tier is accessed later, it is automatically moved back to the frequent access tier to ensure the data retrieval performance. INTELLIGENT TIERING manages to strike a balance between storage costs and read/write performance and features the following strengths:

- **Cost-effective**: When you use INTELLIGENT TIERING for persistent storage, the longer your data is stored, the more you can save on your storage costs (up to about 20%) compared with the STANDARD storage class. INTELLIGENT TIERING is also involved in the object storage lifecycle, where you can transition your INTELLIGENT TIERING data to ARCHIVE to further lower storage costs.
- **Stable and durable**: INTELLIGENT TIERING provides the same low latency and high throughput as the STANDARD storage class. Besides, it offers reliability of up to 99.999999999% (11 9s) by using erasure code-based redundancy, and up to 99.95% availability by using block storage and concurrent reads/writes. INTELLIGENT TIERING has also been integrated with the COS MAZ architecture, featuring high reliability (12 9s) and availability (99.995%).
- **Easy-to-use**: To use INTELLIGENT TIERING, all you need to do is specify it as the storage class of your object. This COS storage class is inherently compatible with COS APIs, SDKs, tools, and applications, making it easy for you to manage your in-cloud data as needed.

## Directions

To store your object in the COS INTELLIGENT TIERING storage class, enable INTELLIGENT TIERING for the bucket, and then specify the **storage class** of your object as INTELLIGENT TIERING.

### Using the COS console

#### Setting INTELLIGENT TIERING upon object uploads

You can perform the following steps to store your object in the INTELLIGENT TIERING storage class:

1. On the bucket configuration page, enable INTELLIGENT TIERING. For more information on the process of enabling INTELLIGENT TIERING, please see [Setting INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38306).
2. Upload a file and specify the storage class during the upload. For more information about how to upload a file, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

> !Once INTELLIGENT TIERING is enabled for a bucket, it cannot be disabled.

#### Moving in-cloud objects to INTELLIGENT TIERING

You can perform the following steps to move in-cloud objects to the INTELLIGENT TIERING storage class:

1. On the bucket configuration page, create a lifecycle rule. For detailed directions, please see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).
2. Specify the application range and transition objects to INTELLIGENT TIERING.



### Using RESTful APIs

You can use the following APIs to configure INTELLIGENT TIERING:

1. Use RESTful APIs to enable INTELLIGENT TIERING for your bucket. For more information, please see the following API documents:
	- [PUT Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38314)
	- [GET Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38315)
2. After enabling INTELLIGENT TIERING for the bucket, use the following APIs to store the object in the INTELLIGENT TIERING storage class:
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

Currently, all SDKs that COS releases support INTELLIGENT TIERING. To support INTELLIGENT TIERING, you can set `StorageClass` to `INTELLIGENT_TIERING` when uploading a file. For more information, please see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).



## Use Limits

INTELLIGENT TIERING has the following limits:

- **Configuration limit**: Once configured, INTELLIGENT TIERING cannot be modified. If you need modification, please [contact us](https://intl.cloud.tencent.com/contact-sales).
- **Initial storage tier**: A new object is stored in the frequent access tier by default, and will only be moved to the infrequent access tier if it hasn’t been accessed for a certain period.
- **Minimum storage duration**: If an object is stored in the INTELLIGENT TIERING storage class for fewer than 30 days, you will be billed for 30 days.
- **Minimum storage size**: An object smaller than 64 KB can only be stored in the frequent access tier and cannot be moved between the frequent and infrequent access tiers.
- **Operation**: Uploading objects to INTELLIGENT TIERING using the APPEND Object API is not supported.
- **Lifecycle**: Objects in the INTELLIGENT TIERING storage class can only be transitioned to ARCHIVE or DEEP ARCHIVE. If a STANDARD object is transitioned to INTELLIGENT TIERING, it will be stored in the frequent access tier. If a STANDARD_IA object is transitioned to INTELLIGENT TIERING, it will be stored in the infrequent access tier.
- **Bucket replication**: During bucket replication, if INTELLIGENT TIERING is not enabled for the destination bucket, the object cannot be copied to the INTELLIGENT TIERING storage class.
