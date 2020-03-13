## Introduction

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Retrieving information on a bucket and its permission | Checks whether a bucket exists and if you have the permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API (GET Service) is used to query the list of all buckets under a specified account.

#### Method Prototype

```java
GetServiceResult getService(GetServiceRequest request)throws CosXmlClientException, CosXmlServiceException;

void getServiceAsync(GetServiceRequest request, CosXmlResultListener cosXmlResultListen);
```

#### Sample Request

[//]: # (.cssg-snippet-get-service)
```
GetServiceRequest getServiceRequest = new GetServiceRequest();
// Set signature verification Host, verify all Headers by default
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

// Use the async callback to make requests
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ------------------------------- | -------------- |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getServiceAsync                                                 | Result callback        | CosXmlResultListener   |

#### Returned Result

The result of the request is returned through GetServiceResult.

| Member Variable | Type | Description |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |
| listAllMyBuckets | [ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListAllMyBuckets.java) | Returns the list of buckets under the specified account |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket.

#### Method Prototype

```java
PutBucketResult putBucket(PutBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketAsync(PutBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000";
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);

//Define the ACL attribute of the bucket. Valid values: private, public-read-write, public-read; Default: private
putBucketRequest.setXCOSACL("private");

// Grant read permission to the authorized user
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSGrantRead(readACLS);

// Grant write permission to the authorized user
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSGrantWrite(writeACLS);

// Grant read and write permissions to the authorized user
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putBucketRequest.setXCOSReadWrite(writeandReadACLS);
// Set signature verification Host, verify all Headers by default
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

// Use the async callback to make requests
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | putBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Returned Result

The result of the request is returned through PutBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Retrieving Information on a Bucket and Its Permission

#### Feature Description

This API (HEAD Bucket) is used to verify whether a bucket exists and if you have the permission to access it.

```java
HeadBucketResult headBucket(HeadBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void headBucketAsync(HeadBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

[//]: # (.cssg-snippet-head-bucket)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
HeadBucketRequest headBucketRequest = new HeadBucketRequest(bucket);
// Set signature verification Host, verify all Headers by default
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

// Use the async callback to make requests
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | headBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Returned Result

The result of the request is returned through HeadBucketResult.

| Member Variable | Type | Description |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Deleting a Bucket

#### Feature Description

This API (DELETE Bucket) is used to delete the specified bucket.

#### Method Prototype

```java
DeleteBucketResult deleteBucket(DeleteBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketAsync(DeleteBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

[//]: # (.cssg-snippet-delete-bucket)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketRequest deleteBucketRequest = new DeleteBucketRequest(bucket);
// Set signature verification Host, verify all Headers by default
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

// Use the async callback to make requests
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

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | deleteBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Returned Result

The result of the request is returned through DeleteBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

## ACL

### Setting Bucket ACL

#### Feature Description

This API (PUT Bucket ACL) is used to set the access control list ( ACL) for the specified bucket.

#### Method Prototype

```java
PutBucketACLResult putBucketACL(PutBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketACLAsync(PutBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

[//]: # (.cssg-snippet-put-bucket-acl)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketACLRequest putBucketACLRequest = new PutBucketACLRequest(bucket);

// Set bucket's access permission
putBucketACLRequest.setXCOSACL("public-read");

// Grant read permission to the authorized user
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putBucketACLRequest.setXCOSGrantRead(readACLS);

// Grant write permission to the authorized user
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("100000000001", "100000000001");
putBucketACLRequest.setXCOSGrantWrite(writeACLS);

// Grant read and write permissions to the authorized user
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putBucketACLRequest.setXCOSReadWrite(writeandReadACLS);
// Set signature verification Host, verify all Headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketACLRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketACLResult putBucketACLResult = cosXmlService.putBucketACL(putBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to make requests
cosXmlService.putBucketACLAsync(putBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketACLResult putBucketACLResult = (PutBucketACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `putBucketACLRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosAcl | SetCosAcl | Sets the ACL permissions for the bucket | string |
| grantAccount | SetXCosGrantRead, SetXCosGrantWrite, or SetXCosReadWrite | Grants users read and write permissions | GrantAccount |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSignParamsAndHeaders  | Indicates whether to verify the query parameters in the request URL for the signature |`Set<String>` |
| cosXmlResultListener      | putBucketACLAsync                                                 | Result callback        | CosXmlResultListener   |

#### Returned Result

The result of the request is returned through PutBucketACLResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying Bucket ACL

#### Feature Description

This API (GET Bucket ACL) is used to get the ACL of the specified bucket.

#### Method Prototype

```java
GetBucketACLResult getBucketACL(GetBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketACLAsync(GetBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

[//]: # (.cssg-snippet-get-bucket-acl)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketACLRequest getBucketACLRequest = new GetBucketACLRequest(bucket);
// Set signature verification Host, verify all Headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketACLRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketACLResult getBucketACLResult = cosXmlService.getBucketACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to make requests
cosXmlService.getBucketACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketACLResult getBucketACLResult = (GetBucketACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `getBucketACLRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketACLAsync                                                 | Result callback        | CosXmlResultListener   |

#### Returned Result

The result of the request is returned through GetBucketACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between 200-300 indicates a successful operation. Other values indicate a failure. |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/AccessControlPolicy.java) | The information of the bucket ACL is returned |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.
