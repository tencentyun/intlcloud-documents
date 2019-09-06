## Use Cases

This operation is suitable for uploading an object smaller than 5 GB in a single request. For objects larger than 5 GB, you must use the [multipart upload](https://intl.cloud.tencent.com/document/product/436/14112) method.

If your object is large (for example, 100 MB), it is recommended that you use multipart upload in a high-bandwidth or weak network environment.

## Directions

### Via the COS Console
You can upload an object in the COS Console. For more information, see [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/13321) in Console Guide.

### Via REST API

You can use the REST API directly to initiate a simple object upload request. For more information, see [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749).

### Via the SDK
You can directly call the simple object upload method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:
- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for C#](https://intl.cloud.tencent.com/document/product/436/32869#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A12)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/31469#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E7.AE.80.E5.8D.95.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1)
