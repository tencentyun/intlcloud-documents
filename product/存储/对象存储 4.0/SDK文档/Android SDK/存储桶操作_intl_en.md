## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL configuration of a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL configuration of a bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API is used to query the list of all buckets under the specified account.

#### Method Prototype

```java
GetServiceResult getService(GetServiceRequest request)throws CosXmlClientException, CosXmlServiceException;

void getServiceAsync(GetServiceRequest request, CosXmlResultListener cosXmlResultListen);
```

#### Sample Request

```
GetServiceRequest getServiceRequest = new GetServiceRequest();
// Use the sync method
try {
    GetServiceResult result = cosXmlService.getService(getServiceRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getServiceAsync(getServiceRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket Lifecycle success
		GetServiceResult getServiceResult = (GetServiceResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getServiceRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ------------------------------- | -------------- |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener      | getServiceAsync                                                 | Result callback        | CosXmlResultListener   |

#### Return Result Descriptions

The result of the request is returned through GetServiceResult.

| Member Variable | Type | Description |
| ---------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| listAllMyBuckets | [ListAllMyBuckets](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListAllMyBuckets.java) | Returns the list of all buckets under the specified account |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to created a bucket.

#### Method Prototype

```java
PutBucketResult putBucket(PutBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketAsync(PutBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000";
PutBucketRequest putBucketRequest = new PutBucketRequest(bucket);

// Define the ACL attribute of the bucket. Value range: private, public-read-write, and public-read; default value: private
putBucketRequest.setXCOSACL("private");

// Grant the grantee read permission
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(readACLS);

// Grant the grantee write permission
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(writeACLS);

// Grant the grantee read-write permission
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putBucketRequest.setXCOSGrantRead(writeandReadACLS);

// Use the sync method
try {
    PutBucketResult putBucketResult = cosXmlService.putBucket(putBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketAsync(putBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket success
        PutBucketResult putBucketResult = (putBucketResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `putBucketRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | string |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener      | putBucketAsync                                                 | Result callback        | CosXmlResultListener   |

#### Return Result Descriptions

The result of the request is returned through PutBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Checking a Bucket and Its Permission

#### Feature Description

This API (HEAD Bucket) is used to check whether a bucket exists and you have permission to access it.

```java
HeadBucketResult headBucket(HeadBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void headBucketAsync(HeadBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
HeadBucketRequest headBucketRequest = new HeadBucketRequest(bucket);

// Use the sync method
try {
    HeadBucketResult headBucketResult = cosXmlService.headBucket(headBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.headBucketAsync(headBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Head Bucket success
		HeadBucketResult headBucketResult = (HeadBucketResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `headBucketRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | string |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | headBucketAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through HeadBucketResult.

| Member Variable | Type | Description |
| ------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Deleting a Bucket

#### Feature Description

This API (DELETE Bucket) is used to delete the specified bucket.

#### Method Prototype

```java
DeleteBucketResult deleteBucket(DeleteBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketAsync(DeleteBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketRequest deleteBucketRequest = new DeleteBucketRequest(bucket);

// Use the sync method
try {
    DeleteBucketResult deleteBucketResult = cosXmlService.deleteBucket(deleteBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.deleteBucketAsync(deleteBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket success
		DeleteBucketResult deleteBucketResult = (DeleteBucketResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `deleteBucketRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | string |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | deleteBucketAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through DeleteBucketResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

## ACL

### Setting Bucket ACL

#### Feature Description

This API (PUT Bucket acl) is used to set the access control list (ACL) for the specified bucket.

#### Method Prototype

```java
PutBucketACLResult putBucketACL(PutBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketACLAsync(PutBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketACLRequest putBucketACLRequest = new PutBucketACLRequest(bucket);

// Set bucket access permission
putBucketACLRequest.setXCOSACL("public-read");

// Grant the grantee read permission
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(readACLS);

// Grant the grantee write permission
ACLAccount writeACLS = new ACLAccount();
writeACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(writeACLS);

// Grant the grantee read-write permission
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "SubUin");
putBucketACLRequest.setXCOSGrantRead(writeandReadACLS);

// Use the sync method
try {
    PutBucketACLResult putBucketACLResult = cosXmlService.putBucketACL(putBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async callback to request
cosXmlService.putBucketACLAsync(putBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket ACL success
		PutBucketACLResult putBucketACLResult = (PutBucketACLResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `putBucketACLRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | string |
| cosAcl | SetCosAcl | Sets bucket ACL permission | string |
| grandtAccout | SetXCosGrantRead, SetXCosGrantWrite, or SetXCosReadWrite | Grants the user read and write permissions | GrantAccount |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | putBucketACLAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through PutBucketACLResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Querying Bucket ACL

#### Feature Description

This API (GET Bucket acl) is used to query the access control list (ACL) for the specified bucket.

#### Method Prototype

```java
GetBucketACLResult getBucketACL(GetBucketACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketACLAsync(GetBucketACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketACLRequest getBucketACLRequest = new GetBucketACLRequest(bucket);

// Use the sync method
try {
    GetBucketACLResult getBucketACLResult = cosXmlService.getBucketACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async callback to request
cosXmlService.getBucketACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
		GetBucketACLResult getBucketACLResult = (GetBucketACLResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getBucketACLRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | string |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketACLAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through GetBucketACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/AccessControlPolicy.java) | Returns the bucket ACL information |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.
