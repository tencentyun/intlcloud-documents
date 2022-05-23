
## Overview

This document provides an overview of APIs and SDK code samples for video processing information in CI.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| GenerateMediainfo | Getting media file information | Queries the details of a media file in a bucket |

## Basic Operations

### Getting media file information

#### Feature description

This API is used to query the details of a media file in a bucket.

#### Method prototype

```java
public MediaInfoResponse generateMediainfo(MediaInfoRequest request);
```

#### Parameter description


| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| object | Location information of the object queried by `input.obget` in the bucket | String | Yes |

#### Response description

- Success: The media object information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a media information request object
MediaInfoRequest request = new MediaInfoRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.getInput().setObject("1.mp3");
//3. Call the API to get the media information response object
MediaInfoResponse response = client.generateMediainfo(request);
```
