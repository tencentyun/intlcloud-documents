Multi-AZ (availability zone) refers to the multi-AZ storage architecture offered by [Tencent Cloud COS](https://intl.cloud.tencent.com/product/cos), which can provide IDC-level disaster recovery capabilities for your data.

Your data is scattered among multiple IDCs in a region. When an IDC fails due to extreme situations such as natural disasters or power failures, the multi-AZ storage architecture can still provide stable and reliable storage services.

Multi-AZ provides 99.9999999999% (12 nines) design data reliability and 99.995% design service availability. When you upload data objects to COS, you can store them in a multi-AZ region simply by specifying the storage class.

>
> - Currently, the multi-AZ feature of COS is supported only in the Guangzhou region and will be available in other public cloud regions in the future.
> - Multi-AZ storage is more costly. For more information, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

## Strengths of Multi-AZ

If you store your data in a multi-AZ region, the data will be divided into multiple chunks, and corresponding coding chunks will be calculated based on the erasure code algorithm. The original data chunks and coding chunks will be mixed up and evenly distributed to different IDCs in the region for storage and intra-region disaster recovery. When an IDC becomes unavailable, the data can still be read from or written to other IDCs normally, ensuring that your data can be persistently stored without loss, which maintains your business data continuity and high availability. The COS multi-AZ feature has the following strengths:

- **Intra-region disaster recovery**: cross-IDC disaster recovery is supported. In the multi-AZ storage architecture, object data is stored on different devices in different IDCs in the same region. When an IDC fails, other redundant IDCs remain available, guaranteeing that your business will not be affected, and data will not be lost.
- **Stability and durability**: the erasure code-based redundant storage mechanism is leveraged to provide up to 99.9999999999% design data reliability. Data is stored in chunks and read and written concurrently to provide up to 99.995% design service availability.
- **Ease of use**: you can specify the storage architecture for your data by specifying the object storage class. You can even select any objects in a bucket and store them in the multi-AZ architecture for greater ease of use.

Multi-AZ storage and non-multi-AZ storage are compared below for their specifications and limitations:

| Item         | Multi-AZ Storage           | Non-Multi-AZ Storage                                                 |
| -------------- | -------------------- | ------------------------------------------------------------ |
| Design data persistence | 99.9999999999% (12 nines)     | 99.999999999% (11 nines)                                                |
| Design service availability | 99.995%              | 99.99%                                                       |
| Supported region     | Guangzhou             | All regions. For more information, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) |
| Supported storage class | Standard (MAZ-STANDARD) | Standard (STANDARD), Standard_IA (STANDARD-IA), and Archive (ARCHIVE)       |



## Directions

You can enable multi-AZ for a bucket and set the object storage class to multi-AZ for objects uploaded to it. Currently, the multi-AZ storage architecture supports only the Standard storage class. When uploading an object, you can store it in the multi-AZ storage architecture by simply specifying the object storage class.
In short, you only need to perform the following two steps to store files in the multi-AZ architecture:

1. Create a bucket and enable multi-AZ **during creation**. For more information on how to create a bucket, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Upload a file and specify the file storage class during upload. For more information on how to upload a file, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

>
>
> - Once multi-AZ is enabled for the bucket, it cannot be disabled, so please enable it with caution. Multi-AZ is not enabled for existing buckets by default, and it can be enabled only for new buckets.
> - For buckets with multi-AZ enabled, objects can only be uploaded in the Multi-AZ Standard (MAZ_STANDARD) storage class. The Multi-AZ Standard_IA (MAZ_STANDARD_IA) and Multi-AZ Archive (MAZ_ARCHIVE) storage classes will be supported in the future.
> - If you want to store existing data to a multi-AZ bucket, you can create a bucket with multi-AZ enabled and use the batch replication feature of COS Batch to replicate files in the existing bucket to the new bucket in batches. For more information on how to use COS Batch, please see [Batch Operation](https://intl.cloud.tencent.com/document/product/436/32956).

## Use Limits

Currently, with the multi-AZ feature of COS, objects can only be uploaded in the Multi-AZ Standard storage class (MAZ_STANDARD). Therefore, there are limits on features related to storage class change as detailed below:

- Storage class limit: currently, only the Multi-AZ Standard (MAZ_STANDARD) storage class is supported. The Multi-AZ Standard_IA (MAZ_STANDARD_IA) and Multi-AZ Archive (MAZ_ARCHIVE) storage classes will be supported in the future.
- Operation limit: currently, objects can only be uploaded, downloaded, and deleted. Objects can be replicated to a multi-AZ bucket but not to a single-AZ bucket.
- Lifecycle limit: currently, expired objects can only be deleted but not transitioned to other storage classes.
- Cross-region replication limit: currently, multi-AZ is only supported in the Guangzhou region; therefore, cross-region replication is not supported.
