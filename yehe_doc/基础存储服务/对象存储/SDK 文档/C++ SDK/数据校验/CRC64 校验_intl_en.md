## Overview

Errors may occur when data is transferred between the client and the server. COS can not only verify data integrity through [MD5 and custom attributes](https://intl.cloud.tencent.com/document/product/436/32467), but also the CRC64 check code.

COS will calculate the CRC64 of the newly uploaded object and store the result as object attributes. It will carry x-cos-hash-crc64ecma in the returned response header, which indicates the CRC64 value of the uploaded object calculated according to [ECMA-182 standard](https://www.ecma-international.org/publications/standards/Ecma-182.htm). If an object already has a CRC64 value stored before this feature is activated, COS will not calculate its CRC64 value, nor will it be returned when the object is obtained.

## Description

APIs that currently support CRC64 include:

- APIs for simple upload
  [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) and [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): you can get the CRC64 check value for your object from the response headers.
- Multipart upload APIs
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): you can compare and verify the CRC64 value returned by COS against the value calculated locally.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): returns a CRC64 value for the entire object only if each part has a CRC64 attribute. Otherwise, no value is returned.
- The [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) operation returns a corresponding CRC64 value.
- When you call the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881), the CRC64 value is returned only if the source object has one.
- The [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) and [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) operations return the CRC64 value provided the object has one. You can compare and verify the CRC64 value returned by COS against that calculated locally.

## API Samples

#### Upload Part response

The following example shows the response to an Upload Part request. The `x-cos-hash-crc64ecma` header represents the CRC64 value of a part, which you can compare against the locally calculated CRC64 value to verify the part integrity.

```shell
HTTP/1.1 200 OK
content-length: 0
connection: close
date: Thu, 05 Dec 2019 01:58:03 GMT
etag: "358e8c8b1bfa35ee3bd44cb3d2cc416b"
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0MmJfMjBiNDU4NjRfNjkyZl80ZjZi****
```

#### Complete Multipart Upload response

The following example shows the response to a Complete Multipart Upload request. The `x-cos-hash-crc64ecma` header represents the CRC64 value of an entire object, which you can compare against the locally calculated CRC64 value to verify the object integrity.

```shell
HTTP/1.1 200 OK
content-type: application/xml
transfer-encoding: chunked
connection: close
date: Thu, 05 Dec 2019 02:01:17 GMT
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0ZWRfMjNiMjU4NjRfOGQ4Ml81MDEw****

[Object Content]
```

## SDK Verification Methods

The default C++ SDK verification methods vary depending on APIs.

- APIs for simple upload 
 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749): MD5 verification by default, with CRC64 verification unavailable.
- APIs for multipart upload
  - [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): MD5 verification by default, with CRC64 verification unavailable.
  - [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): CRC64 verification by default, with MD5 verification unavailable.


#### Sample 1. Multipart upload
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Change to the bucket name
std::string object_name = "exampleobject"; // Change to the object name
std::string local_file = "./test"; // Change to the local file name

qcloud_cos::MultiUploadObjectReq req(bucket_name, object_name, local_file); // CRC64 verification enabled by default
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp); // Automatic verification of the CRC64 value
// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```
