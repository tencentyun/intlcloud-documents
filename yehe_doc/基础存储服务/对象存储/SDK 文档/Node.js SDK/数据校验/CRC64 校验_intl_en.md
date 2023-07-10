## Overview

Errors may occur when data is transferred between the client and the server. COS can not only verify data integrity through [MD5 and custom attributes](https://intl.cloud.tencent.com/document/product/436/32467), but also the CRC64 check code.

COS will calculate the CRC64 value of the newly uploaded object and store the result as object attributes. It will carry x-cos-hash-crc64ecma in the returned response header, which indicates the CRC64 value of the uploaded object calculated according to [ECMA-182 standard](https://www.ecma-international.org/publications/standards/Ecma-182.htm). If an object already has a CRC64 value stored before this feature is activated, COS will not calculate its CRC64 value, nor will it be returned when the object is obtained.

## Description

APIs that currently support CRC64 include:

- APIs for simple upload
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) and [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): you can get the CRC64 check value for your file from the response headers.
- Multipart upload APIs
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): you can compare and verify the CRC64 value returned by COS against the value calculated locally.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): returns a CRC64 value for the entire object only if each part has a CRC64 attribute. Otherwise, no value is returned.
- The [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) operation returns a corresponding CRC64 value.
- When you call the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881), the CRC64 value is returned only if the source object has one.
- The [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) and [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) operations return the CRC64 value provided the object has one. You can compare and verify the CRC64 value returned by COS against that calculated locally.

## SDK Samples

#### Description

This API is used to verify the CRC64 value consistency of the object data when the object is uploaded or downloaded.

#### Sample request

The API for simple upload is used as an example. It is the same with other APIs.

[//]: # (.cssg-snippet-put-object)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject', /* Required */
    StorageClass: 'STANDARD',
    Body: fileObject, // Upload the file object.
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    if (err) {
      console.log(err);
    } else {
      // You need to add `x-cos-hash-crc64ecma` to Expose-Headers for a successful response.
      // Documentation: https://cloud.tencent.com/document/product/436/13318
      var crc64 = data.headers['x-cos-hash-crc64ecma'];
      console.log(crc64);
    }
});
```

