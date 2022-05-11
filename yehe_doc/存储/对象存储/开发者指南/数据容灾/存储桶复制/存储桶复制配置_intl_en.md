## Overview

Cross-bucket replication enables you to replicate objects from a source bucket to a destination bucket. This feature is well suited for use cases such as remote disaster recovery, industry compliance, data migration and backup, access latency reduction, and access to the data located in different regions.

>!Once versioning is enabled, you can create multiple versions for any new object uploaded. Each of these versions occupies your storage capacity and is billed for storage equally.

## Usage

### Using COS console

For information on how to configure a cross-bucket replication rule in the COS console, see [Setting Cross-Bucket Replication](https://intl.cloud.tencent.com/document/product/436/19235).

### Using REST APIs

Configure and manage your cross-bucket replication rules through REST APIs as described in the following API documentation:

- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### Using SDKs

Directly call the cross-bucket replication method in the SDKs. For more information, see the SDK documentation for the corresponding programming language below:

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/36196)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31519)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31523)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/35272)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31527)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37696)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/10199)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/35805)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/35859)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/34996)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31547)
