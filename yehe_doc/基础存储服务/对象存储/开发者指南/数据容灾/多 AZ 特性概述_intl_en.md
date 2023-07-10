

MAZ refers to the multi-AZ storage architecture offered by [COS](https://www.tencentcloud.com/products/cos), which can provide IDC-level disaster recovery capabilities for your data.

Your data is scattered among multiple IDCs in a region. When an IDC fails due to extreme situations such as natural disasters or power failures, the multi-AZ storage architecture can still provide stable and reliable storage services.

Multi-AZ provides 99.9999999999% (12 nines) design data reliability and 99.995% design service availability. When you upload data objects to COS, you can store them in a multi-AZ region simply by specifying the storage class.

> ?
> - Currently, the MAZ configuration of COS is supported only in Beijing, Guangzhou, and Shanghai regions and will be available in other public cloud regions in the future.
> - Using the MAZ configuration incurs high storage usage fees. For more information, see [Pricing | Cloud Object Storage](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=).

## Strengths of Multi-AZ

If you store your data in a multi-AZ region, the data will be divided into multiple chunks, and corresponding coding chunks will be calculated based on the erasure code algorithm. The original data chunks and coding chunks will be mixed up and evenly distributed to different IDCs in the region for storage and intra-region disaster recovery. When an IDC becomes unavailable, the data can still be read from or written to other IDCs normally, ensuring that your data can be persistently stored without loss, which maintains your business data continuity and high availability. The COS multi-AZ feature has the following strengths:

- **Intra-region disaster recovery**: cross-IDC disaster recovery is supported. In the multi-AZ storage architecture, object data is stored on different devices in different IDCs in the same region. When an IDC fails, other redundant IDCs remain available, guaranteeing that your business will not be affected, and data will not be lost.
- **Stability and durability**: the erasure code-based redundant storage mechanism is leveraged to provide up to 99.9999999999% design data reliability. Data is stored in chunks and read and written concurrently to provide up to 99.995% design service availability.
- **Ease of use**: you can specify the storage architecture for your data by specifying the object storage class. You can even select any objects in a bucket and store them in the multi-AZ architecture for greater ease of use.

Multi-AZ storage and non-multi-AZ storage are compared below for their specifications and limitations:

<table>
<thead>
<tr>
<th>Comparison Item</th>
<th>MAZ Storage</th>
<th>Non-MAZ Storage</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">Designed data durability</td>
<td nowrap="nowrap">99.9999999999% (12 nines)</td>
<td>99.999999999% (11 nines)</td>
</tr>
<tr>
<td>Designed service availability</td>
<td>99.995%</td>
<td>99.99%</td>
</tr>
<tr>
<td>Supported regions</td>
<td colspan=2>See <a href="https://intl.cloud.tencent.com/document/product/436/30925">Storage Class Overview</a>.</td>
</tr>
<tr>
<td nowrap="nowrap">Supported storage classes</td>
<td>MAZ_STANDARD<br>MAZ_STANDARD_IA<br>MAZ_INTELLIGENT_TIERING</td>
<td>STANDARD<br>STANDARD_IA<br>ARCHIVE<br>DEEP ARCHIVE<br>INTELLIGENT TIERING</td>
</tr>
</tbody></table>


## How to Use

You can enable MAZ for a bucket and set the object storage class to MAZ for objects uploaded to it. When uploading an object, you can store it in the MAZ storage architecture by simply specifying the object storage class.
In short, you only need to perform the following two steps to store files in the multi-AZ architecture:

1. Create a bucket as instructed in [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309) and enable the MAZ configuration **during creation**.
2. Upload a file and specify the storage class during the upload. For more information about how to upload a file, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).

> ?
> - Once multi-AZ is enabled for the bucket, it cannot be disabled, so please enable it with caution. Multi-AZ is not enabled for existing buckets by default, and it can be enabled only for new buckets.
> - For a bucket with MAZ configuration enabled, objects can be uploaded to MAZ storage classes (MAZ_STANDARD, MAZ_STANDARD_IA, or MAZ_INTELLIGENT TIERING). To upload an object to MAZ_INTELLIGENT TIERING, the intelligent tiering configuration must also be enabled for the bucket.
> - If you want to store existing data in an MAZ bucket, you can create a bucket with MAZ enabled and use the batch replication feature of COS Batch to replicate files in the existing bucket to the new bucket in batches. For more information on how to use COS Batch, see [Batch Operation](https://intl.cloud.tencent.com/document/product/436/32956).

## Use Limits

Currently, COS allows you to upload objects to the MAZ_STANDARD, MAZ_STANDARD_IA, or MAZ_INTELLIGENT TIERING storage class. Therefore, there are also restrictions on features related to storage class changes as detailed below:

- Storage class limit: Currently, objects can be uploaded only to MAZ storage classes (MAZ_STANDARD, MAZ_STANDARD_IA, or MAZ_INTELLIGENT TIERING). To upload an object to MAZ_INTELLIGENT TIERING, both the MAZ configuration and intelligent tiering configuration must be enabled for the bucket.
- Operation limit: currently, objects can only be uploaded, downloaded, and deleted. Objects can be replicated to a multi-AZ bucket but not to a single-AZ bucket.
- Lifecycle limit: Currently, objects can be deleted only upon expiration but cannot be transitioned from an MAZ storage class to an OAZ storage class.
- Cross-region replication limit: Objects cannot be replicated from an MAZ storage class to an OAZ storage class.

