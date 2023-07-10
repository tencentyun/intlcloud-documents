## Overview

This document provides an overview of APIs and SDK code samples for deleting an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://www.tencentcloud.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |

## Deleting a Single Object

#### Feature description

This API is used to delete a specified object.

#### Sample code

```ts
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
let bucket = "examplebucket-1250000000";
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
let region = "COS_REGION";
// Location identifier of the object in the bucket, i.e., the object key
let cosPath = "exampleobject";
try {
  await Cos.getDefaultService().deleteObject(bucket, cosPath, undefined, region);
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  console.log(e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket    | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| cosPath | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. | String | Yes |
| versionId | ID of the object version to be deleted | String | No |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).
