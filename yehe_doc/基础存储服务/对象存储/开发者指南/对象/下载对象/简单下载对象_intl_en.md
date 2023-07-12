## Use Cases

You can directly initiate a request to download objects in COS. The following features are supported:

- Download a complete object: Download the complete object data by initiating a GET request.
- Download a part of an object: Use the Range request header in a GET request to retrieve a specific range of bytes of an object. Retrieving multiple ranges is not supported.

The object's metadata will be returned along with the object's content as an HTTP response header. The GET request supports overwriting certain metadata values in the response using URL parameters.
For example, the response value of Content-Disposition can be overwritten. Response headers that support modification include:
- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## How to Use

### Using COS console

Download an object in the COS console. For more information, see [Downloading Objects](https://intl.cloud.tencent.com/document/product/436/13322) in Console Guide.

### Using the REST API

Use the REST API to initiate an object download request. For more information, see [GET Object](https://intl.cloud.tencent.com/document/product/436/7753).

### Using SDKs

Directly call the object download method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/37675)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/44873)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/44065)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/37684)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/44016)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/43862)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/43872)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/45499)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/46469)
- [SDK for Weixin Mini Program](https://intl.cloud.tencent.com/document/product/436/43882)

