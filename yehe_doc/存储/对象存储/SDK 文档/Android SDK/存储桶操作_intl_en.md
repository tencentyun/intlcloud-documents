## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Extracting a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |



## Querying Bucket List

#### Feature

This API (GET Service (List Buckets)) is used to query the list of all buckets under a specified account.

#### Method prototype

```java
GetServiceResult getService(GetServiceRequest request)throws CosXmlClientException, CosXmlServiceException;

void getServiceAsync(GetServiceRequest request, CosXmlResultListener cosXmlResultListen);
```

#### Request samples

[//]: # (.cssg-snippet-get-service)
```
GetServiceRequest getServiceRequest = new GetServiceRequest();
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getServiceRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetServiceResult result = cosXmlService.getService(getServiceRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.getServiceAsync(getServiceRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetServiceResult getServiceResult = (GetServiceResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `getServiceRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ------------------------------- | -------------- |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getServiceAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through GetServiceResult.

| Member Variable | Type | Description |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listAllMyBuckets | [ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListAllMyBuckets.java) | The list of buckets under the specified account is returned |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

## Creating a Bucket

#### Feature

This API (Put Bucket) is used to create a bucket.

#### Method prototype

```java
PutBucketResult putBucket(PutBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketAsync(PutBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000";
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);

// Define the ACL attribute of the bucket. Valid values: private, public-read-write, public-read; Default: private
putBucketRequest.setXCOSACL("private");

// Grant read permission to the grantee
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSGrantRead(readACLS);

// Grant write permission to the grantee
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSGrantWrite(writeACLS);

// Grant read and write permissions to the grantee
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSReadWrite(writeandReadACLS);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketResult putBucketResult = cosXmlService.putBucket(putBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.putBucketAsync(putBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketResult putBucketResult = (PutBucketResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `putBucketRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | putBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through PutBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

## Extracting a Bucket and its Permission

#### Feature

This API (HEAD Bucket) is used to verify whether a bucket exists and if you have the permission to access it.

```java
HeadBucketResult headBucket(HeadBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void headBucketAsync(HeadBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-head-bucket)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
HeadBucketRequest headBucketRequest = new HeadBucketRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
headBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    HeadBucketResult headBucketResult = cosXmlService.headBucket(headBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.headBucketAsync(headBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        HeadBucketResult headBucketResult = (HeadBucketResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `headBucketRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | headBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through HeadBucketResult.

| Member Variable | Type | Description |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


## Deleting a Bucket

#### Feature

This API (DELETE Bucket) is used to delete the specified bucket.

#### Method prototype

```java
DeleteBucketResult deleteBucket(DeleteBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketAsync(DeleteBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-delete-bucket)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketRequest deleteBucketRequest = new DeleteBucketRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketResult deleteBucketResult = cosXmlService.deleteBucket(deleteBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.deleteBucketAsync(deleteBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketResult deleteBucketResult = (DeleteBucketResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Delete Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `deleteBucketRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | deleteBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through DeleteBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

