## Overview
This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |


## Cross-origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API (PUT Bucket cors) is used to set the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```java
PutBucketCORSResult putBucketCORS(PutBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketCORSAsync(PutBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketCORSRequest putBucketCORSRequest = new PutBucketCORSRequest(bucket);
    
/**
 * CORSConfiguration.cORSRule: Cross-origin access configuration information
 * corsRule.id: Configures the rule ID
 * corsRule.allowedOrigin: Allowed origin in the format of protocol://domain name[:port number], such as http://www.qq.com. Wildcard * is supported
 * corsRule.maxAgeSeconds: Sets the validity period of the result of the OPTIONS request
 * corsRule.allowedMethod: Allowed HTTP operations such as GET, PUT, HEAD, POST, and DELETE
 * corsRule.allowedHeader: Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported
 * corsRule.exposeHeader: Sets custom header information from the server that the browser can receive
 */
CORSConfiguration.CORSRule corsRule = new CORSConfiguration.CORSRule();

corsRule.id = "123";
corsRule.allowedOrigin = "https://intl.cloud.tencent.com";
corsRule.maxAgeSeconds = 5000;

List<String> methods = new LinkedList<>();
methods.add("PUT");
methods.add("POST");
methods.add("GET");
corsRule.allowedMethod = methods;

List<String> headers = new LinkedList<>();
headers.add("host");
headers.add("content-type");
corsRule.allowedHeader = headers;

List<String> exposeHeaders = new LinkedList<>();
headers.add("x-cos-metha-1");
corsRule.exposeHeader = headers;

// Set the cross-origin access configuration
putBucketCORSRequest.addCORSRule(corsRule);

// Use the sync method
try {
    PutBucketCORSResult putBucketCORSResult = cosXmlService.putBucketCORS(putBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketCORSAsync(putBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket CORS success
		PutBucketCORSResult putBucketCORSResult = (PutBucketCORSResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `putBucketCORSRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|corsRule|addCORSRule| Sets the cross-origin access configuration of a bucket |CORSConfiguration.CORSRule|
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | putBucketCORSAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through PutBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```java
GetBucketCORSResult getBucketCORS(GetBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketCORSAsync(GetBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketCORSRequest getBucketCORSRequest = new GetBucketCORSRequest(bucket);

// Use the sync method
try {
    GetBucketCORSResult getBucketCORSResult = cosXmlService.getBucketCORS(getBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketCORSAsync(getBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket CORS success
		GetBucketCORSResult getBucketCORSResult = (GetBucketCORSResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getBucketCORSRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketCORSAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through GetBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
|corsConfiguration|[CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/CORSConfiguration.java)| Returns the cross-origin resource sharing configuration information of a bucket |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype
```java
DeleteBucketCORSResult deleteBucketCORS(DeleteBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketCORSAsync(DeleteBucketCORSRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketCORSRequest deleteBucketCORSRequest = new DeleteBucketCORSRequest(bucket);

// Use the sync method
try {
    DeleteBucketCORSResult deleteBucketCORSResult = cosXmlService.deleteBucketCORS(deleteBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.deleteBucketCORSAsync(deleteBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket CORS success
		DeleteBucketCORSResult deleteBucketCORSResult = (DeleteBucketCORSResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `deleteBucketCORSRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | deleteBucketCORSAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through DeleteBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


## Lifecycle
### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype
```java
PutBucketLifecycleResult putBucketLifecycle(PutBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketLifecycleAsync(PutBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```java
PutBucketLifecycleRequest putBucketLifecycleRequest = new PutBucketLifecycleRequest(bucket);

// Lifecycle configuration rule information
LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
rule.id = "Lifecycle ID";
LifecycleConfiguration.Filter filter = new LifecycleConfiguration.Filter();
filter.prefix = "prefix/";
rule.filter = filter;
rule.status = "Enabled or Disabled";
LifecycleConfiguration.Transition transition = new LifecycleConfiguration.Transition();
transition.days = 100;
transition.storageClass = COSStorageClass.STANDARD.getStorageClass();
putBucketLifecycleRequest.setRuleList(rule);

// Use the sync method
try {
    PutBucketLifecycleResult putBucketLifecycleResult = cosXmlService.putBucketLifecycle(putBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.putBucketLifecycleAsync(putBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket Lifecycle success
		PutBucketLifecycleResult putBucketLifecycleResult = (PutBucketLifecycleResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `putBucketLifecycleRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
|rule|setRuleList| Sets the lifecycle configuration of a bucket |LifecycleConfiguration.Rule|
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | putBucketLifecycleAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle of the specified bucket.

#### Method Prototype
```java
GetBucketLifecycleResult getBucketLifecycle(GetBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLifecycleAsync(GetBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLifecycleRequest getBucketLifecycleRequest = new GetBucketLifecycleRequest(bucket);

// Use the sync method
try {
    GetBucketLifecycleResult getBucketLifecycleResult = cosXmlService.getBucketLifecycle(getBucketLifecycleRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketLifecycleAsync(getBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket Lifecycle success
		GetBucketLifecycleResult getBucketLifecycleResult = (GetBucketLifecycleResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getBucketLifecycleRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketLifecycleAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/LifecycleConfiguration.java)| Returns the lifecycle configuration information of a bucket |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle of the specified bucket.

#### Method Prototype
```java
DeleteBucketLifecycleResult deleteBucketLifecycle(DeleteBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketLifecycleAsync(DeleteBucketLifecycleRequest request,CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketLifecycleRequest deleteBucketLifecycleRequest = new DeleteBucketLifecycleRequest(bucket);

// Use the sync method
try {
    DeleteBucketLifecycleResult deleteBucketLifecycleResult = cosXmlService.deleteBucketLifecycle(deleteBucketLifecycleRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.deleteBucketLifecycleAsync(deleteBucketLifecycleRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Delete Bucket Lifecycle success
		DeleteBucketLifecycleResult deleteBucketLifecycleResult = (DeleteBucketLifecycleResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Bucket Lifecycle failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `deleteBucketLifecycleRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket name in the format of BucketName-APPID |string|
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | deleteBucketLifecycleAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
|httpCode|int| HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


## Versioning
### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set the versioning feature of the specified bucket.

#### Method Prototype
```
PutBucketVersioningResult putBucketVersioning(PutBucketVersioningRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketVersionAsync(PutBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request


```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest putBucketVersioningRequest = new PutBucketVersioningRequest(bucket);
putBucketVersioningRequest.setEnableVersion(true); // true: enable versioning; false: suspend versioning
// Use the sync method
try {
    PutBucketVersioningResult putBucketVersioningResult = cosXmlService.putBucketVersioning(putBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use the async callback to request
cosXmlService.putBucketVersionAsync(putBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo PUT Bucket versioning success
        PutBucketVersioningResult putBucketVersioningResult = (PutBucketVersioningResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo PUT Bucket versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                         |
| isEnable | Sets whether to enable versioning. true: enable; false: suspend | boolean |
| headerKeys          | Whether the signature verifies the header                | `Set<String>` |
| cosXmlResultListener | Result callback | CosXmlResultListener |


#### Return Result Descriptions
The result of the request is returned through PutBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning information of the specified bucket.

#### Method Prototype
```
GetBucketVersioningResult getBucketVersioning(GetBucketVersioningRequest request) throws CosXmlClientException, CosXmlServiceException;
void getBucketVersioningAsync(GetBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest getBucketVersioningRequest = new GetBucketVersioningRequest(bucket);
// Use the sync method
try {
    GetBucketVersioningResult getBucketVersioningResult = cosXmlService.getBucketVersioning(getBucketVersioningRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use the async callback to request
cosXmlService.getBucketVersioningAsync(getBucketVersioningRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo GET Bucket versioning success
        GetBucketVersioningResult getBucketVersioningResult = (GetBucketVersioningResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo GET Bucket versioning failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                         |
| headerKeys          | Whether the signature verifies the header                | `Set<String>` |
| cosXmlResultListener | Result callback | CosXmlResultListener |


#### Return Result Descriptions
The result of the request is returned through GetBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| versioningConfiguration | [VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/VersioningConfiguration.java) | Returns the versioning status of a bucket under the specified account |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set the cross-region replication rule for the specified bucket.

#### Method Prototype
```
PutBucketReplicationResult putBucketReplication(PutBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketReplicationAsync(PutBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```
#### Sample Request
```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String ownerUin = "OwnerUin"; // Initiator ID, i.e., OwnerUin 
String subUin = "SubUin"; // Initiator ID: SubUin 
PutBucketReplicationRequest putBucketReplicationRequest = new PutBucketReplicationRequest(bucket);
putBucketReplicationRequest.setReplicationConfigurationWithRole(ownerUin, subUin);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Mark the name of the specific rule
ruleStruct.isEnable = true; // Mark whether the rule takes effect: true: yes; false: no
ruleStruct.appid = "1250000000"; // appid
ruleStruct.region = Region.AP_Beijing.getRegion(); // Region information of the destination bucket
ruleStruct.bucket = "destExamplebucket-1250000000";  // Destination bucket name
ruleStruct.prefix = "34"; // Prefix matching policy
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);

// Use the sync method
try {
    PutBucketReplicationResult putBucketReplicationResult = cosXmlService.putBucketReplication(putBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}   
// Use the async callback to request
cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo PUT Bucket replication success
        PutBucketReplicationResult putBucketReplicationResult = (PutBucketReplicationResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo PUT Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});

```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                         |
| ownerUin  | Initiator ID: OwnerUin | String |
| subUin  | Initiator ID: SubUin    | String |
| ruleStruct  | Whether the signature verifies the query parameter in the request URL | RuleStruct |
| queryParameterKeys  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| headerKeys          | Whether the signature verifies the header                | `Set<String>` |
| cosXmlResultListener | Result callback | CosXmlResultListener |


#### Return Result Descriptions
The result of the request is returned through PutBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```
GetBucketReplicationResult getBucketReplication(GetBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void getBucketReplicationAsync(GetBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest getBucketReplicationRequest = new GetBucketReplicationRequest(bucket);
// Use the sync method
try {
    GetBucketReplicationResult getBucketReplicationResult = cosXmlService.getBucketReplication(getBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use the async callback to request
cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo GET Bucket replication success
        GetBucketReplicationResult getBucketReplicationResult = (GetBucketReplicationResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo GET Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                         |
| headerKeys          | Whether the signature verifies the header                | `Set<String>` |
| cosXmlResultListener | Result callback | CosXmlResultListener |

#### Return Result Descriptions
The result of the request is returned through GetBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| replicationConfiguration | [ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ReplicationConfiguration.java) | Returns the cross-region replication configuration information of a bucket under the specified account |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```
DeleteBucketReplicationResult deleteBucketReplication(DeleteBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void deleteBucketReplicationAsync(DeleteBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request
```
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketReplicationRequest deleteBucketReplicationRequest = new DeleteBucketReplicationRequest(bucket);
// Use the sync method
try {
    DeleteBucketReplicationResult deleteBucketReplicationResult = cosXmlService.deleteBucketReplication(deleteBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use the async callback to request
cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo DELETE Bucket replication success
        DeleteBucketReplicationResult deleteBucketReplicationResult = (DeleteBucketReplicationResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo DELETE Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                         |
| headerKeys          | Whether the signature verifies the header                | `Set<String>` |
| cosXmlResultListener | Result callback | CosXmlResultListener |


#### Return Result Descriptions
The result of the request is returned through DeleteBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


