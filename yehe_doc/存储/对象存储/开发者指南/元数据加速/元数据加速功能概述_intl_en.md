
COS launched the metadata acceleration feature to provide high-performance file system features. Metadata acceleration leverages Cloud HDFS (CHDFS)’s powerful metadata management feature at the underlying layer to allow users to use file system semantics to access COS. The system design metrics can have a bandwidth of up to 2.4 GB/s, a 100,000-level QPS, and millisecond-level latency. A metadata acceleration−enabled can be widely used in scenarios such as big data, high-performance computing, machine learning, and artificial intelligence.

If you haven’t enabled metadata acceleration for a bucket, it cannot accelerate metadata access by default and does not support access with POSIX file semantics, making it less favorable in terms of file `LIST` and not support `RENAME`. After enabling metadata acceleration, you can use POSIX file semantics to access objects in buckets through native COS APIs or the Hadoop tool deployed on the client side, the console, or SDKs.

>! Metadata acceleration can only be enabled upon bucket creation and cannot be disabled once enabled. Please **think twice** before enabling it.
>

## Use Limits

The following table compares the product feature support between enabling and not enabling metadata acceleration:

| Metric | Metadata Acceleration Enabled  | Metadata Acceleration Disabled |
| ------------ | -------------------- | ---------------- |
| Creating/Querying/Deleting buckets | Supported | Supported         |
| Uploading/Downloading/Deleting objects | Supported                | Supported  |
| Setting bucket permissions  | Supported     | Supported    |
| Setting object permissions  | Not supported (inherit from bucket permissions)  | Supported |
| Intra-region disaster recovery | Not supported | Supported         |
| Bucket encryption | Not supported      | Supported |
| Object encryption | Not supported                         | Supported             |
| CORS | Not supported                         | Supported             |
| Hotlink protection | Not supported                         | Supported             |
| Versioning | Not supported                         | Supported             |
| Cross-bucket replication  | Not supported                         | Supported             |
| Static websites | Not supported                         | Supported             |
| Origin-pull configurations | Not supported                         | Supported             |
| Lifecycle  | Only STANDARD-to-ARCHIVE transition is supported  | Supported    |
| Inventory   | Not supported                         | Supported             |
| Bucket tagging   | Not supported                         | Supported             |
| COS Select    | Not supported                         | Supported             |
| COS batch operation    | Not supported                         | Supported             |
| CI features | Not supported                         | Supported             |

>? We are continuously optimizing metadata acceleration and will gradually support the product features above.
>

## Billing Description

Currently, metadata is still in beta testing and is not billed. If billing should be required in the future, we will notify you via [Message Center](https://console.cloud.tencent.com/message), emails, or SMS. You can check your message center or see [Billing Overview](https://cloud.tencent.com/document/product/436/16871) to keep up with the latest billing plans.
