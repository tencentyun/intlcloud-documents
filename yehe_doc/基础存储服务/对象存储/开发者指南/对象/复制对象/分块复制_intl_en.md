## Overview

To copy an object that is greater than 5 GB, you must use multipart copy. First, use the multipart upload API to create an object. Then use the `Upload Part - Copy` API and specify the `x-cos-copy-source` header to determine the source object that you want to copy. The process is outlined below:

1. Initialize an object for multipart upload.
2. Copy the data of the source object; specify the `x-cos-copy-source-range` header to determine how much data to copy at a time (you can specify to copy up to 5 GB at a time). 
3. Complete the multipart upload.

>?The SDKs provided by COS can be used to easily implement a multipart copy operation.

## Directions

### Using REST APIs

Use REST APIs to directly initiate a multipart copy request. For more information, see the following API documentation:

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### Using SDKs

Use multipart copy directly through SDKs. For more information, see the SDK documentation for the corresponding programming language below:


- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [C SDK](https://www.tencentcloud.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [.NET(C#) SDK](https://www.tencentcloud.com/document/product/436/40171)
- [Go SDK](https://www.tencentcloud.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43885)
