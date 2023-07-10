
Metadata acceleration is a high-performance file system feature offered by COS. Metadata acceleration leverages the powerful metadata management feature of Cloud HDFS (CHDFS) at the underlying layer to allow you to access COS over file system semantics. The system design metrics can reach a bandwidth of up to 100 GB/s, over 100,000 queries per second (QPS), and a latency of milliseconds. Buckets with metadata acceleration enabled can be widely used in scenarios such as big data, high-performance computing, machine learning, and AI.

If you haven't enabled metadata acceleration for a bucket, it cannot accelerate metadata access by default and does not support access with POSIX file semantics, making it less favorable in terms of file `LIST` and not support `RENAME`. After enabling metadata acceleration, you can use POSIX file semantics to access objects in buckets through native COS APIs or the Hadoop tool deployed on the client side, the console, or SDKs.

>! Metadata acceleration can only be enabled upon bucket creation and cannot be disabled once enabled. **Think twice** before enabling it.
>

## Use Limits

The following table compares the product feature support between enabling and not enabling metadata acceleration:

| Metric | Metadata Acceleration Enabled  | Metadata Acceleration Disabled |
| ------------ | -------------------- | ---------------- |
| Creating/Querying/Deleting buckets | Supported | Supported         |
| Uploading/Downloading/Deleting objects | Supported                | Supported  |
| Bucket permissions  | Supported     | Supported    |
| Object permissions | Inheriting bucket permissions by default | Supported |
| Intra-region disaster recovery | Supported | Supported         |
| Bucket encryption | N/A | Supported |
| Object encryption | N/A | Supported |
| CORS | N/A | Supported |
| Hotlink protection | N/A | Supported |
| Versioning | N/A | Supported |
| Cross-bucket replication | N/A | Supported |
| Static website | N/A | Supported |
| Origin-pull settings | N/A | Supported |
| Lifecycle | Supported | Supported |
| Inventory | N/A | Supported |
| Bucket tag | N/A | Supported |
| COS Select | N/A | Supported |
| COS Batch | N/A | Supported |
| CI | N/A | Supported |


## Billing Details

Currently, metadata acceleration is in free beta test. If billing is required in the future, we will notify you by [Message Center](https://console.cloud.tencent.com/message), email, or SMS. You can check the Message Center or see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871) to stay up to date with the latest billing plan.
