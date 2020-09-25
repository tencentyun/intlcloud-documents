## Overview

INTELLIGENT TIERING is a COS storage class designed to reduce storage costs for users by moving data automatically between two storage tiers — frequent access and infrequent access — when access patterns change.

INTELLIGENT TIERING is ideal for data with unknown or changing access patterns. It offers the same low latency and high throughput performance as COS STANDARD, and even lower storage costs. You can reduce your in-cloud storage costs by transitioning proper data as needed from STANDARD to INTELLIGENT TIERING.

>!
>
>- Currently, INTELLIGENT TIERING is available in Beijing, Shanghai, and Guangzhou Public Cloud regions.
>- INTELLIGENT TIERING is billed for storage usage as follows:
   - The storage usage fees in the frequent access tier are charged at the same published prices as STANDARD storage class;
   - The storage usage fees in the infrequent access tier are charged at the same published prices as STANDARD_IA storage class.
>- INTELLIGENT TIERING requests are billed the same as STANDARD requests. The INTELLIGENT TIERING fees for traffic and management features are charged depending on the region, the same as in the other storage classes. There are no data retrieval fees, but additional charges apply for monitoring INTELLIGENT TIERING objects. For more information, please see [Product Pricing](https://buy.cloud.tencent.com/price/cos).

## Strengths

Once you choose to store your data uploaded to COS into INTELLIGENT TIERING, it will begin monitoring the data access patterns and move objects that have not been accessed for a continuous period to the lower-cost infrequent access tier. If an object in the infrequent access tier is accessed later, it is automatically moved back to the frequent access tier. The following strengths enable INTELLIGENT TIERING to help strike a balance between your storage costs and read/write performance:

- **Cost-effective**: when you use INTELLIGENT TIERING for persistent storage, the longer your data is stored, the more you can save on your storage costs (up to about 20%) compared with STANDARD storage class. INTELLIGENT TIERING is also involved in the object storage lifecycle, where you can transition your data to ARCHIVE for even lower storage costs.

- **Stable and durable**: INTELLIGENT TIERING provides the same low-latency and high-throughput as STANDARD storage class. Besides, it offers reliability of up to 99.999999999% (11 9s) using erasure code-based redundancy, and up to 99.95% availability using block storage and concurrent reads/writes. The integration of INTELLIGENT TIERING has also given the COS MAZ architecture the same high reliability and availability.

- **Easy to use**: to use INTELLIGENT TIERING, all you need to do is specify it as the storage class of your object. This COS storage class is inherently compatible with COS APIs, SDKs, tools, and applications, making it easy for you to manage your in-cloud data as needed.

## Directions

To store your data into INTELLIGENT TIERING, you need to enable the intelligent tiering configuration on your bucket first. After that, all you need to do is configure the **storage class** to intelligent tiering when you upload an object.

### Using COS console

You can follow the steps below to store an object into the INTELLIGENT TIERING storage class:

1. Go to the bucket configuration page in the console and enable the intelligent tiering configuration. For details, see [Setting INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38306).
2. Specify INTELLIGENT TIERING as storage class as you upload a file. For more information on how to upload a file, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

>!Note that once enabled on a bucket, the intelligent tiering configuration cannot be disabled, but only modified.


### Using REST APIs

You can also use the following APIs to configure intelligent tiering storage:

1. First, use the REST APIs as shown below to enable the intelligent tiering configuration on a bucket:
 - [PUT Bucket IntelligentTiering](https://cloud.tencent.com/document/product/436/48348)
 - [GET Bucket IntelligentTiering](https://cloud.tencent.com/document/product/436/48349)
2. Upload an object into INTELLIGENT TIERING using the APIs below:
 - [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
 - [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
 - [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
 - [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
3. To query the storage class or storage tier of an object, use these APIs:
 - [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
 - [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
4. To delete an object stored in INTELLIGENT TIERING, use the following APIs:
 - [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
 - [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)

### Using SDKs

You can make intelligent tiering configuration by using the following language-specific SDKs:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/36195)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31519)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31523)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35271)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31527)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/37695)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31535)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/35804)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/35858)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/34997)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31547)



## Use Limits

INTELLIGENT TIERING storage is subject to the following limits:

- **Initial access tier**: new objects stored into INTELLIGENT TIERING stay in the frequent access tier by default. Those that have not been accessed for a certain continuous period will be moved to the infrequent access tier.
- **Minimum storage duration**: INTELLIGENT TIERING has a minimum storage duration of 30 days. If an object is deleted before 30 days, you are charged for 30 days.
- **Minimum storage size**: objects smaller than 64 KB can only be stored persistently in the frequent access tier, and not be moved between the two tiers.
- **Operations**: it is not allowed to upload objects directly to INTELLIGENT TIERING using the APPEND Object API.
- **Lifecycle**: objects in the INTELLIGENT TIERING storage class can only be transitioned to ARCHIVE or DEEP ARCHIVE. Objects are stored in the frequent access tier when transitioned from STANDARD to INTELLIGENT TIERING, and in the infrequent access tier when transitioned from STANDARD_IA to INTELLIGENT TIERING.
- **Cross-Region replication**: cross-region replication cannot replicate an object into INTELLIGENT TIERING if the intelligent tiering configuration has not been configured on the destination bucket.
