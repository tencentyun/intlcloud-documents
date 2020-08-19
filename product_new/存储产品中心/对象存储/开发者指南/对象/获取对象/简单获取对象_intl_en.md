## Use Cases

You can initiate a request to obtain objects directly in COS. You have the following options when obtaining an object:

- Obtain a complete object: Obtain the complete object data directly by initiating a GET request.
- Obtain a part of an object: Use the Range request header in a GET request to retrieve a specific range of bytes of an object. Retrieving multiple ranges is not supported.

The object's metadata will be returned along with the object's content as an HTTP response header. The GET request supports overwriting certain metadata values in the response using URL parameters.
For example, the response value of Content-Dispositon can be overwritten. Response headers that support modification include:
- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## Directions

### Via the COS Console

You can obtain an object in the COS Console. For more information, see [Downloading Objects](https://intl.cloud.tencent.com/document/product/436/13322) in Console Guide.

### Via REST API

You can use the REST API directly to initiate an object obtaining request. For more information, see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

### Via the SDK

You can directly call the object download method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/37675#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/12296)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/30594)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E8.8E.B7.E5.8F.96.E5.AF.B9.E8.B1.A1)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1)
