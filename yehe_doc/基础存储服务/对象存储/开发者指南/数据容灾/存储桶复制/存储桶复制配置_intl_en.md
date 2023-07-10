## Use Cases

Cross-bucket replication enables you to replicate objects from a source bucket to a destination bucket. This feature is well suited for use cases such as remote disaster recovery, industry compliance, data migration and backup, access latency reduction, and access to data located in different regions.

Special use cases:
- Multi-region backup: You can configure multiple replication rules for the source bucket to replicate objects to buckets in different regions for multi-region backup and disaster recovery.
- Two-way replication: You can create replication rules in the source and destination buckets respectively to implement two-way data replication.

>!Once versioning is enabled, you can create multiple versions for any new object uploaded. Each of these versions occupies your storage capacity and is billed for storage equally.

## Directions

### Using the COS console

You can configure a cross-bucket replication rule in the COS console as instructed in [Setting Cross-Bucket Replication](https://intl.cloud.tencent.com/document/product/436/19235).

### Using RESTful APIs

You can configure and manage cross-bucket replication rules through RESTful APIs as described in the following API documents:

- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### Using SDKs

You can directly call the cross-bucket replication method in SDKs. For more information, see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36196)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/12301)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/43245)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/30601)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37696)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
