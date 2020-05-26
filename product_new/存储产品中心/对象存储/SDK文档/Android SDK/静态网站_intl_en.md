

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```
PutBucketWebsiteResult putBucketWebsite(PutBucketWebsiteRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketWebsiteAsync(PutBucketWebsiteRequest request,  CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketWebsiteRequest putBucketWebsiteRequest = new PutBucketWebsiteRequest(bucket);
putBucketWebsiteRequest.setIndexDocument("index.html");

// Use the sync method
try {
    PutBucketWebsiteResult putBucketWebsiteResult = cosXmlService.putBucketWebsite(putBucketWebsiteRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketWebsiteAsync(putBucketWebsiteRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketWebsiteResult putBucketWebsiteResult = (PutBucketWebsiteResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| IndexDocument        | Index document                                                     | String |
| ErrorDocument        | Error document                                                     | String |
| RedirectAllRequestTo | Redirects all requests                                               | String |
| RoutingRules         | Redirect rule                                                   | List   |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```
GetBucketWebsiteResult getBucketWebsite(GetBucketWebsiteRequest request)throws CosXmlClientException, CosXmlServiceException;

void getBucketWebsiteAsync(GetBucketWebsiteRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketWebsiteRequest getBucketWebsiteRequest = new GetBucketWebsiteRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketWebsiteRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketWebsiteResult getBucketWebsiteResult = cosXmlService.getBucketWebsite(getBucketWebsiteRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketWebsiteAsync(getBucketWebsiteRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketWebsiteResult getBucketWebsiteResult = (GetBucketWebsiteResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

| Member Variable | Description | Type |
| -------------------- | -------------------------------------------------------- | -------------------- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
| websiteConfiguration | Returns bucket object's `WebsiteConfiguration` information               | WebsiteConfiguration |

## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```
DeleteBucketWebsiteResult deleteBucketWebsite(DeleteBucketWebsiteRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketWebsiteAsync(DeleteBucketWebsiteRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketWebsiteRequest deleteBucketWebsiteRequest = new DeleteBucketWebsiteRequest(bucket);
// Set signature verification host. All headers are to be verified by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketWebsiteRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketWebsiteResult deleteBucketWebsiteResult = cosXmlService.deleteBucketWebsite(deleteBucketWebsiteRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.deleteBucketWebsiteAsync(deleteBucketWebsiteRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketWebsiteResult getBucketWebsiteResult = (DeleteBucketWebsiteResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description

| Member Variable | Description | Type |
| -------- | -------------------------------------------------------- | ---- |
| httpCode            | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed | int                 |
