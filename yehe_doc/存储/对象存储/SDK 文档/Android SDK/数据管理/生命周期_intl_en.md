## Overview
This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## Setting Lifecycle

#### Feature

This API (PUT Bucket lifecycle) is used to set lifecycle configuration on a bucket.

#### Method prototype
```java
PutBucketLifecycleResult putBucketLifecycle(PutBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketLifecycleAsync(PutBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketLifecycleRequest putBucketLifecycleRequest = new PutBucketLifecycleRequest(bucket);

// Declare lifecycle configuration rules
LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
rule.id = "Lifecycle ID";
LifecycleConfiguration.Filter filter = new LifecycleConfiguration.Filter();
filter.prefix = "prefix/";
rule.filter = filter;
rule.status = "Enabled";
LifecycleConfiguration.Transition transition = new LifecycleConfiguration.Transition();
transition.days = 100;
transition.storageClass = COSStorageClass.STANDARD.getStorageClass();
rule.transition = transition;
putBucketLifecycleRequest.setRuleList(rule);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketLifecycleRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketLifecycleResult putBucketLifecycleResult = cosXmlService.putBucketLifecycle(putBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.putBucketLifecycleAsync(putBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketLifecycleResult putBucketLifecycleResult = (PutBucketLifecycleResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `putBucketLifecycleRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket for which to set lifecycle in the format BucketName-APPID |string|
|rule|setRuleList | Sets the lifecycle configuration for a bucket | LifecycleConfiguration.Rule |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys  | setSignParamsAndHeaders  | Indicates whether to verify the query parameters in the request URL for the signature |`Set<String>` |
| cosXmlResultListener      | putBucketLifecycleAsync                                                 |   Result callback    | CosXmlResultListener    |

#### Response description

The result of the request is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

## Querying Lifecycle

#### Feature

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

#### Method prototype
```java
GetBucketLifecycleResult getBucketLifecycle(GetBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLifecycleAsync(GetBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples
[//]: # (.cssg-snippet-get-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLifecycleRequest getBucketLifecycleRequest = new GetBucketLifecycleRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketLifecycleRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketLifecycleResult getBucketLifecycleResult = cosXmlService.getBucketLifecycle(getBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.getBucketLifecycleAsync(getBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketLifecycleResult getBucketLifecycleResult = (GetBucketLifecycleResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `getBucketLifecycleRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket for which to query lifecycle in the format BucketName-APPID |string|
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys  | setSignParamsAndHeaders  | Indicates whether to verify the query parameters in the request URL for the signature |`Set<String>` |
| cosXmlResultListener      | getBucketLifecycleAsync                                                 |      Result callback  | CosXmlResultListener    |


#### Response description
The result of the request is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/LifecycleConfiguration.java)| The lifecycle configuration of the bucket is returned |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

## Deleting Lifecycle

#### Feature

This API (DELETE Bucket lifecycle) is used to delete the lifecycle management configuration from a bucket.

#### Method prototype
```java
DeleteBucketLifecycleResult deleteBucketLifecycle(DeleteBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketLifecycleAsync(DeleteBucketLifecycleRequest request,CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketLifecycleRequest deleteBucketLifecycleRequest = new DeleteBucketLifecycleRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketLifecycleRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketLifecycleResult deleteBucketLifecycleResult = cosXmlService.deleteBucketLifecycle(deleteBucketLifecycleRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.deleteBucketLifecycleAsync(deleteBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketLifecycleResult deleteBucketLifecycleResult = (DeleteBucketLifecycleResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Delete Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `deleteBucketLifecycleRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket for which to delete the lifecycle configuration in the format BucketName-APPID |string|
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys  | setSignParamsAndHeaders  | Indicates whether to verify the query parameters in the request URL for the signature |`Set<String>` |
| cosXmlResultListener      | deleteBucketLifecycleAsync                                                 |     Result callback    | CosXmlResultListener  |

#### Response description
The result of the request is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).