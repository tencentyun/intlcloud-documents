## Overview

Cloud Object Storage（COS）supports batch deletion of multiple objects. You can delete objects in batches using the console, API, or SDKs.

By default, when the deletion task is completed, an empty response is returned. If an error occurs, an error message is returned.

>! A maximum of 1,000 objects can be deleted in a single request. To delete more objects, split the list and send the request separately.

## Directions

### Using COS console

Delete multiple objects in batches in the COS console. For more information, see [Deleting Objects](https://intl.cloud.tencent.com/document/product/436/13323) in Console Guide.

### Using REST API

Use the REST API to initiate a multiple objects deleting request. For more information, see [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289).

### Using SDKs

Directly call the multiple objects deleting method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E5.88.A0.E9.99.A4.E5.A4.9A.E4.B8.AA.E5.AF.B9.E8.B1.A1)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43884)
