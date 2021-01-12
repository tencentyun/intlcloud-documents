## Use Cases

Multipart upload is well suited for uploading large objects in weak network or high-bandwidth environments. The COS Console and SDKs can break a single object into multiple parts and then upload them. You can also do so by yourself and upload each part through API calls. Multipart upload has the following benefits:

- In a weak network, smaller part size minimizes the impact of restarting a failed upload due to network errors.
- In a high-bandwidth environment, multipart upload can maximize the use of your available bandwidth by uploading object parts in parallel. Uploading parts out of order does not affect the final merged object.
- With multipart upload, you can pause and resume the upload of a single large object at any time. All incomplete multipart uploads can be resumed unless aborted.
- Multipart upload can also be used to begin an upload before you know the final object size. You can initiate an upload and then merge the parts to get the full object size.

When uploaded, the parts are numbered consecutively. You can upload each part separately or upload them in any order. COS will merge the parts into an object based on their numbers. If the upload of any part fails, the failed part can be uploaded again without affecting other parts and the content as a whole. In a weak network environment, multipart upload is recommended for objects larger than 20 MB. In a high-bandwidth environment, multipart upload is recommended for objects larger than 100 MB.

## Directions

### Via REST API

You can use the REST API directly to initiate a multipart upload request. For more information, see the following API documents:

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### Via the SDK

You can directly call the multipart upload method in the SDK. For more information, see the SDK documentation for the corresponding programming language below:

- [SDK for Android](https://intl.cloud.tencent.com/document/product/436/37674#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for C](https://intl.cloud.tencent.com/document/product/436/12296)
- [SDK for C++](https://intl.cloud.tencent.com/document/product/436/31465#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for .NET](https://intl.cloud.tencent.com/document/product/436/38062)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/436/31466#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for iOS](https://intl.cloud.tencent.com/document/product/436/37683#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/436/31468#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for JavaScript](https://intl.cloud.tencent.com/document/product/436/31477#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/436/8629)
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/436/31470#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/436/31471#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C)
