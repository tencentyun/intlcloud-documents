## Applicable Scenarios
You can replicate your object data from the source bucket in one region to the destination bucket in another region by configuring cross-region replication rules. This feature can apply to a range of scenarios including cross-region disaster recovery, industry-specific compliance, data migration and backup, low access latency for customers, and easy data access for clusters from different regions.

>After versionning is enabled, newly uploaded objects will generate multiple versions and take up storage space, so these versions of the object will also charge for storage.

## Directions

### Configuring via the COS Console
For information on how to configure a cross-region replication rule in the COS Console, see [Setting Cross-region Replication](https://intl.cloud.tencent.com/document/product/436/19235) documentation.

### Configuring via REST API
You can configure and manage cross-region replication via REST API as described in the following API documentation:

- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### Configuring with SDK
You can directly call the cross-region replication method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36196#cross-region-replication)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519#cross-region-replication)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523#cross-region-replication)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35272#cross-region-replication)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527#cross-region-replication)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31531#cross-region-replication)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31535#cross-region-replication)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805#cross-region-replication)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996#cross-region-replication)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547#cross-region-replication)
