## Use Cases

For copying an object greater than 5 GB, you must use the multipart copy. Use the multipart upload API to create an object, and use the Upload Part - Copy API to carry the x-cos-copy-source header to specify the source object. The process is as follows:

1. Initialize an object for multipart upload.
2. Copy the data of the source object. You can specify the x-cos-copy-source-range header and copy up to 5 GB of data at a time.
3. Complete the multipart upload.

> SDKs provided by COS can be used to easily implement multipart copy.

## Directions

### Via REST API

You can use the REST API directly to initiate a multipart copy request. For more information, see the following API documentations:

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### Via the SDK

You can call the multipart copy method in the SDK directly. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/31463#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/31467#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/31469#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E5.A4.8D.E5.90.88.E5.A4.8D.E5.88.B6)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
