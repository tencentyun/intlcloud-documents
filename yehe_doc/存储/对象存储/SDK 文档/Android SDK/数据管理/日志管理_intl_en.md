

## Overview

This document provides an overview of APIs and SDK code samples related to log management.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting log management | Enables logging for the source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying log management | Queries the logging configuration information of the source bucket |

## Setting Log Management

#### Feature description

This API (PUT Bucket logging) is used to enable logging for the source bucket and store its access logs in a specified destination bucket.

#### Method prototype

```
PutBucketLoggingResult putBucketLogging(PutBucketLoggingRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketLoggingAsync(PutBucketLoggingRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String srcBucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String targetBucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketLoggingRequest putBucketLoggingRequest = new PutBucketLoggingRequest(srcBucket);
putBucketLoggingRequest.setTargetBucket(targetBucket);
putBucketLoggingRequest.setTargetPrefix("objectPrefix");

// Use the sync method
try {
    PutBucketLoggingResult putBucketLoggingResult = cosXmlService.putBucketLogging(putBucketLoggingRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketLoggingAsync(putBucketLoggingRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketLoggingResult putBucketLoggingResult = (PutBucketLoggingResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| srcBucket    | Source bucket for which to enable the logging feature in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| targetBucket | Destination bucket where to store logs in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| TargetPrefix | Specified path in the destination bucket for storing logs | string |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Querying Log Management

#### Feature description

This API (GET Bucket logging) is used to query the log configuration information of a specified bucket.

#### Method prototype

```
GetBucketLoggingResult getBucketLogging(GetBucketLoggingRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLoggingAsync(GetBucketLoggingRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLoggingRequest getBucketLoggingRequest = new GetBucketLoggingRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketLoggingRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketLoggingResult getBucketLoggingResult = cosXmlService.getBucketLogging(getBucketLoggingRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketLoggingAsync(getBucketLoggingRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketLoggingResult getBucketLoggingResult = (GetBucketLoggingResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket            | Source bucket in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

| Member Variable | Description | Type |
| ------------------- | -------------------------------------------------------- | ---------------------- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| bucketLoggingStatus | Returns bucket object's `Logging` information                | [BucketLoggingStatus](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/BucketLoggingStatus.java) |
