## Use Cases

Tencent Cloud COS supports listing keys by prefix. You can use the separator (`/`) in a key to implement a hierarchical structure similar to the traditional file system. In COS, you can use separators to select and browse keys hierarchically.

You can list all keys in a single bucket in UTF-8 binary order of prefixes or filter the key list by specifying the prefix. For example, adding the parameter `t`, would list the `tencent` object, while skipping objects prefixed with `a` or other characters.

Keys can be reorganized based on the added separator (`/`). You can use the prefix and separator together to implement a folder retrieval feature. For example, if you add the prefix parameter `t` and the separator (`/`), eligible keys such as `tencent/cos` will be listed.

COS supports storing an unlimited number of objects in a single bucket, so the key list may be very large. For management purposes, a maximum of 1,000 key values are returned for one List Objects request, and a marker will be returned to indicate whether the result is truncated. You can send a series of List Objects requests based on markers and separators to list all key values or search for the desired content.

## Directions

### Via REST API

You can use the REST API directly to initiate an object key listing request. For more information, see [GET Bucket](https://intl.cloud.tencent.com/document/product/436/30614).

### Via the SDK

You can directly call the object list querying method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/30594)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E8.8E.B7.E5.8F.96.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK Node.js](https://intl.cloud.tencent.com/document/product/436/8629)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8)
- [SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/436/30609)
