## API Description

- For the API used to upload a small file (below 5 MB), please see [Simple File Upload](https://cloud.tencent.com/document/product/436/7749).
- For the API used to upload a large file (above 5 MB), please see [Initializing Multipart Upload](https://cloud.tencent.com/document/product/436/7746), [Uploading Parts One by One](https://cloud.tencent.com/document/product/436/7750), and [Ending Multipart Upload](https://cloud.tencent.com/document/product/436/7742).

## Feature Description
1. Upload media (and cover) files.
2. For how to upload from a client using an API, please see [Overview of Upload from Client](https://cloud.tencent.com/document/product/266/9760).

## Via SDK
It is recommended to use the [encapsulated SDK](/document/product/436/6474) to call the API.

## Via API

For usage, please see the documents in the API links above. The syntax of each API is as follows:
```
PUT <ObjectName> HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

The following variables in the syntax take the values in the return result of the [ApplyUpload API](/document/product/266/31767):  

- `<ObjectName>` is **MediaStoragePath** (or **CoverStoragePath** for a cover file).
- `<BucketName>-<APPID>` is **StorageBucket**.
- `<Region>` is **StorageRegion**.

For API requests, note the following:

- For the `Authorization` signature, use `SecretId` and `SecretKey` in **TempCertificate** in the return result of the [ApplyUpload API](/document/product/266/31767). For the calculation method, please see [Request Signature](/document/api/436/7778).
- Pass in the **x-cos-security-token** field (identifying the security token used in the request) in the HTTP header or `form-data` of the POST request packet, and assign it the value of the `Token` field in **TempCertificate**.
