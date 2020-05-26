

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```
PutBucketTaggingResult putBucketTagging(PutBucketTaggingRequest request)throws CosXmlClientException, CosXmlServiceException;

void putBucketTaggingAsync(PutBucketTaggingRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketTaggingRequest putBucketTaggingRequest = new PutBucketTaggingRequest(bucket);
putBucketTaggingRequest.addTag("key", "value");
putBucketTaggingRequest.addTag("hello", "world");

// Use the sync method
try {
    PutBucketTaggingResult putBucketTaggingResult = cosXmlService.putBucketTagging(putBucketTaggingRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketTaggingAsync(putBucketTaggingRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketTaggingResult putBucketTaggingResult = (PutBucketTaggingResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Tag key, which can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String |
| value | Tag value, which can contain letters, numbers, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```
GetBucketTaggingResult getBucketTagging(GetBucketTaggingRequest request)throws CosXmlClientException, CosXmlServiceException;

void getBucketTaggingAsync(GetBucketTaggingRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketTaggingRequest getBucketTaggingRequest = new GetBucketTaggingRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketTaggingRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketTaggingResult getBucketTaggingResult = cosXmlService.getBucketTagging(getBucketTaggingRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketTaggingAsync(getBucketTaggingRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketTaggingResult getBucketTaggingResult = (GetBucketTaggingResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ------- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| tagging  | Returns bucket object's `Tagging` information                            | Tagging |

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```
DeleteBucketTaggingResult deleteBucketTagging(DeleteBucketTaggingRequest request)throws CosXmlClientException, CosXmlServiceException;

void deleteBucketTaggingAsync(DeleteBucketTaggingRequest request, CosXmlResultListener cosXmlResultListener);

```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketTaggingRequest deleteBucketTaggingRequest = new DeleteBucketTaggingRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketTaggingRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketTaggingResult deleteBucketTaggingResult = cosXmlService.deleteBucketTagging(deleteBucketTaggingRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.deleteBucketTaggingAsync(deleteBucketTaggingRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketTaggingResult getBucketTaggingResult = (DeleteBucketTaggingResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {

    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
