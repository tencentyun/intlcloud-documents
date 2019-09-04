## Use Cases

The copy operation creates a copy of an object that is already stored in COS. You can create a copy of your object up to 5 GB in a single operation. To copy an object over 5 GB, you must use the multipart upload API. With the copy operation, you can:

- Create a copy of an object.
- Rename the object by copying it and deleting the original one.
- Modify the storage class of the object. In the copy operation, you can select the same object key as both the source and destination and modify the storage class.
- Copy objects across different COS regions.
- Modify object metadata. In the copy operation, you can select the same object key as both the source and destination and modify object metadata.

In the copy operation, the metadata of the original object is inherited by default, but the creation date is subject to the new object.

## Directions

### Via REST API

You can use the REST API directly to initiate an object copying request. For more information, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### Via the SDK

You can directly call the object copying method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/31464#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for C#](https://intl.cloud.tencent.com/document/product/436/32869#.E7.AE.80.E5.8D.95.E5.A4.8D.E5.88.B6)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6)
