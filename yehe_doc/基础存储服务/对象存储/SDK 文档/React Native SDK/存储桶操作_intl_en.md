## Overview

This document provides an overview of APIs and SDK code samples for basic bucket operations.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://www.tencentcloud.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://www.tencentcloud.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://www.tencentcloud.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://www.tencentcloud.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |

## Querying a Bucket List

#### Feature description

This API (`GET Service (List Buckets)`) is used to query the list of all buckets under a specified account.

#### Sample code

```ts
try {
  let listAllMyBuckets: ListAllMyBuckets = await Cos.getDefaultService().getService();
  // For bucket list details, see the `ListAllMyBuckets` class.
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  console.log(e);
}
```

#### Parameter description

None.

#### Response description

- Success: `ListAllMyBuckets` is returned, including the list of buckets and bucket owner information.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).

Parameters in the `ListAllMyBuckets` response body are as follows:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| buckets | Bucket list | List&lt;Bucket&gt; |
| owner | Bucket owner information | Owner |

`Bucket` has the following sub-nodes:

| Parameter | Description | Type |
| ---------- | ----------------------------------------------------------- | ------ |
| name       | Bucket name                                                | String |
| location   | Bucket region                                              | String |
| createDate | Bucket creation time in ISO 8601 format, such as 2019-05-24T10:56:40Z | String |

`Owner` has the following sub-nodes:

| Parameter | Description | Type |
| ----------- | ------------------ | ------ |
| id          | Complete ID            | String |
| disPlayName | Bucket owner name | String |

## Creating a Bucket

#### Feature description

This API (`PUT Bucket`) is used to create a bucket.

#### Sample code

```ts
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
let bucket = "examplebucket-1250000000";
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
let region = "COS_REGION";
// Whether to enable multi-AZ
let enableMAZ = false;
try {
  await Cos.getDefaultService().putBucket(
      bucket, 
      {
        region: region,
        enableMAZ: enableMAZ
      }
  );
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  console.log(e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| bucket    | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| enableMAZ | Whether to create an MAZ bucket                                         | String | No       |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).

## Checking a Bucket and Its Permissions

#### Feature description

This API (`HEAD Bucket`) is used to verify whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Sample code

```ts
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
let bucket = "examplebucket-1250000000";
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
let region = "COS_REGION";
try {
  let header = await Cos.getDefaultService().headBucket(
      bucket,
      region
  );
  // The HTTP status code is 200, and the HTTP header is `header`.
} catch (e) {
  // View the specific HTTP status code in `e.statusCode`
  console.log(e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket    | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: The HTTP Header is returned.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).

## Deleting a Bucket

#### Feature description

This API (`DELETE Bucket`) is used to delete a specified bucket.

>! Before deleting a bucket, make sure that all the data and incomplete multipart uploads in the bucket have been cleared; otherwise, the bucket cannot be deleted.

#### Sample code

```ts
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
let bucket = "examplebucket-1250000000";
// Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
let region = "COS_REGION";
try {
  await Cos.getDefaultService().deleteBucket(
      bucket,
      region
  );
} catch (e) {
  // An exception will be reported in case of failure. Process the business logic accordingly.
  console.log(e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket    | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).
