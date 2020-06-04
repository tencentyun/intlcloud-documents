## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

## Set Versioning

#### Feature

This API (PUT Bucket versioning) is used to set a versioning configuration on a specified bucket.

#### Method prototype
```java
PutBucketVersioningResult putBucketVersioning(PutBucketVersioningRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketVersionAsync(PutBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # ".cssg-snippet-put-bucket-versioning"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest putBucketVersioningRequest = new PutBucketVersioningRequest(bucket);
putBucketVersioningRequest.setEnableVersion(true); //true: enable versioning; false: suspend versioning
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketVersioningRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketVersioningResult putBucketVersioningResult = cosXmlService.putBucketVersioning(putBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.putBucketVersionAsync(putBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketVersioningResult putBucketVersioningResult = (PutBucketVersioningResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo PUT Bucket versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket for which to enable or suspend versioning in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| isEnable | Indicates whether to enable versioning: <br><li>true: enable<br><li>false: suspend | boolean |
| headerKeys  | Indicates whether to verify the header for the signature | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description 
The result of the request is returned through PutBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


## Querying Versioning

#### Feature

This API (GET Bucket versioning) is used to query the versioning information of a specified bucket.

#### Method prototype
```java
GetBucketVersioningResult getBucketVersioning(GetBucketVersioningRequest request) throws CosXmlClientException, CosXmlServiceException;
void getBucketVersioningAsync(GetBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # ".cssg-snippet-get-bucket-versioning"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest getBucketVersioningRequest = new GetBucketVersioningRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketVersioningRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketVersioningResult getBucketVersioningResult = cosXmlService.getBucketVersioning(getBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketVersioningResult getBucketVersioningResult = (GetBucketVersioningResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo GET Bucket versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket | Bucket for which to query versioning in the format: BucketName-APPID. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| headerKeys  | Indicates whether to verify the header for the signature | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description 
The result of the request is returned through GetBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |
| versioningConfiguration | [VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/VersioningConfiguration.java) | Returns the versioning status of the bucket under the specified account                      |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).
