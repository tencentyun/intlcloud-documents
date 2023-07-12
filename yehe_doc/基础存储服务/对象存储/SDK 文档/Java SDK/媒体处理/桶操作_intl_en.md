
## Overview

This document provides an overview of APIs and SDK code samples for media processing buckets in CI.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/1045/43671) | Querying media buckets | Queries the list of buckets with media processing enabled under the current account. |

## Basic Operations

### Querying the list of buckets with media processing enabled

#### Feature description

This API is used to query buckets with media processing enabled under the current account.

#### Method prototype

```java
public MediaBucketResponse describeMediaBuckets(MediaBucketRequest mediaBucketRequest);
```

#### Parameter description


| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| bucketNames | Bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported. | String | No |
| regions |  Region. To specify multiple regions, separate them with commas. Valid values: All, ap-shanghai, ap-beijing. | String | No |
| pageNumber  | Page number.                  |  String | No       |
| pageSize    | Number of entries per page.                | String | No       |

#### Response description

- Success: The bucket object information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
 //1. Create a template request object
MediaBucketRequest request = new MediaBucketRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
//3. Call the API to get the bucket response object
MediaBucketResponse response = client.describeMediaBuckets(request);
```
