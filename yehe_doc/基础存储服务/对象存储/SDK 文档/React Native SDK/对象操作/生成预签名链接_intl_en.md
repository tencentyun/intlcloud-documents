## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.
For details about how to use a pre-signed URL for uploads, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114). For details about how to use a pre-signed URL for downloads, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

>?
> - To learn about signature rules, see [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 

## Generating a Pre-Signed URL for Downloading Objects

#### Feature description

This API is used to generate a pre-signed URL for downloading COS objects.

#### Sample code

```ts
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
let bucket = "examplebucket-1250000000";
// The location of the object in the bucket, i.e., the object key
let cosPath = "exampleobject";
// URL request parameters
let requestParameters = {"test1k":"test1v", "test2k":"test2v"};
try {
  // Get a pre-signed URL for downloading objects
  String objectUrl = await Cos.getDefaultService().getPresignedUrl(
    bucket, 
    cosPath, 
    {
      parameters: requestParameters
    }
  );
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  console.log(e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket | Bucket name, formatted as `BucketName-APPID`. For more information, see [Bucket Overview](https://www.tencentcloud.com/document/product/436/13312). | String |Yes |
| cosPath | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its object key is `doc/picture.jpg` | String | Yes |
| signValidTime | Signature validity period, in seconds. Note that this is the signature validity period. You need to ensure the key validity period by yourself. | Int | No |
| signHost | Whether to include the Host header in the signature. You can choose not to include it, but the request may fail or vulnerabilities may occur. | Bool | No |
| parameters | HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. | Map | No |

#### Response description

- Success: A pre-signed URL for downloading objects is returned.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).
