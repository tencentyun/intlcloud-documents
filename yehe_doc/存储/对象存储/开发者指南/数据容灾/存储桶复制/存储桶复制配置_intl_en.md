## Overview

Cross-bucket replication enables you to replicate objects from a source bucket to a destination bucket. This feature is well suited for use cases such as remote disaster recovery, industry compliance, data migration and backup, access latency reduction, and data access from clusters in different regions.

>!Once versioning is enabled, you can create multiple versions for any new object uploaded. Each of these versions occupies your storage capacity and is billed for storage equally.

## Usage

### Using COS console

For information on how to configure a cross-bucket replication rule in the COS console, please see [Setting Cross-Bucket Replication](https://intl.cloud.tencent.com/document/product/436/19235).

### Using REST APIs

You can configure and manage your cross-bucket replication rules through REST APIs as described in the following API documentation:

- [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) 
- [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) 
- [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) 

### Using SDKs

You can directly call the cross-bucket replication method in the SDKs. For more information, please see the language-specific SDK documentation below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/36196)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31519)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31523)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/35272)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31527)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/37696)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31535)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/35805)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/35859)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/34996)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31547)
