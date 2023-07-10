## Overview
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, versioning, and cross-region replication.

**Cross-origin access**

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration for a bucket |
| [GET Bucket versioning](https://cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rules of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |


## Cross-origin access
### Setting cross-origin access configuration

## Feature description

This API is used to set the cross-origin access configuration of a bucket.

#### Method prototype
```java
PutBucketCORSResult putBucketCORS(PutBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketCORSAsync(PutBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-cors)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketCORSRequest putBucketCORSRequest = new PutBucketCORSRequest(bucket);

/**
 * CORSConfiguration.cORSRule: Cross-origin access configuration information
 * corsRule.id: ID of the configuration rule
 * corsRule.allowedOrigin: Allowed access sources. The wildcard "*" is supported. Format: protocol://domain_name[:port], for example, http://www.qq.com
 * corsRule.maxAgeSeconds: Configures the validity period of the results obtained by OPTIONS
 * corsRule.allowedMethod: Allowed HTTP request methods, such as GET, PUT, HEAD, POST, DELETE
 * corsRule.allowedHeader: When sending an OPTIONS request, notifies the server end which custom HTTP request headers are allowed to be used by subsequent requests. The wildcard "*" is supported.
 * corsRule.exposeHeader: Configures the custom header information that can be received by the browser from the server.
 */
CORSConfiguration.CORSRule corsRule = new CORSConfiguration.CORSRule();

corsRule.id = "123";
corsRule.allowedOrigin = "https://cloud.tencent.com";
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
exposeHeaders.add("x-cos-meta-1");
corsRule.exposeHeader = exposeHeaders;

// Set the cross-origin access configuration information
putBucketCORSRequest.addCORSRule(corsRule);

// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketCORSRequest.setSignParamsAndHeaders(null, headerKeys);

// Use the sync method
try {
    PutBucketCORSResult putBucketCORSResult = cosXmlService.putBucketCORS(putBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.putBucketCORSAsync(putBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketCORSResult putBucketCORSResult = (PutBucketCORSResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `putBucketCORSRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
|corsRule|addCORSRule | Sets the cross-origin access configuration of a bucket | CORSConfiguration.CORSRule |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | putBucketCORSAsync                                                 |   Result callback      | CosXmlResultListener    |

#### Response description
The result of the request is returned through PutBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying cross-origin access configuration

## Feature description

This API is used to query the cross-origin access configuration of a bucket.

#### Method prototype
```java
GetBucketCORSResult getBucketCORS(GetBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketCORSAsync(GetBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-cors)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketCORSRequest getBucketCORSRequest = new GetBucketCORSRequest(bucket);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketCORSRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketCORSResult getBucketCORSResult = cosXmlService.getBucketCORS(getBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.getBucketCORSAsync(getBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketCORSResult getBucketCORSResult = (GetBucketCORSResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `getBucketCORSRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketCORSAsync                                                 |    Result callback    | CosXmlResultListener |

#### Response description
The result of the request is returned through GetBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
|corsConfiguration|[CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/CORSConfiguration.java)| Returns the CORS configuration of the bucket |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Deleting cross-origin configuration

## Feature description

This API is used to delete the cross-origin access configuration of a bucket.

#### Method prototype
```java
DeleteBucketCORSResult deleteBucketCORS(DeleteBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketCORSAsync(DeleteBucketCORSRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-cors)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketCORSRequest deleteBucketCORSRequest = new DeleteBucketCORSRequest(bucket);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketCORSRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketCORSResult deleteBucketCORSResult = cosXmlService.deleteBucketCORS(deleteBucketCORSRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.deleteBucketCORSAsync(deleteBucketCORSRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketCORSResult deleteBucketCORSResult = (DeleteBucketCORSResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Delete Bucket CORS failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `deleteBucketCORSRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | deleteBucketCORSAsync                                                 |    Result callback    | CosXmlResultListener   |

#### Response description
The result of the request is returned through DeleteBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Lifecycle
### Setting a lifecycle configuration

## Feature description

This API is used to set the lifecycle configuration of a bucket.

#### Method prototype
```java
PutBucketLifecycleResult putBucketLifecycle(PutBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketLifecycleAsync(PutBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

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
// Set the signature verification host, verifies all headers by default
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
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
|rule|setRuleList | Sets the lifecycle configuration of a bucket | LifecycleConfiguration.Rule |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | putBucketLifecycleAsync                                                 |   Result callback    | CosXmlResultListener    |

#### Response description

The result of the request is returned through PutBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying a lifecycle configuration

## Feature description

This API is used to query the lifecycle configuration of a bucket.

#### Method prototype
```java
GetBucketLifecycleResult getBucketLifecycle(GetBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketLifecycleAsync(GetBucketLifecycleRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketLifecycleRequest getBucketLifecycleRequest = new GetBucketLifecycleRequest(bucket);
// Set the signature verification host, verifies all headers by default
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
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketLifecycleAsync                                                 |      Result callback  | CosXmlResultListener    |


#### Response description
The result of the request is returned through GetBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
|lifecycleConfiguration|[LifecycleConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/LifecycleConfiguration.java)| Returns the lifecycle configuration of the bucket |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Deleting a lifecycle configuration

## Feature description

This API is used to delete the lifecycle configuration of a bucket.

#### Method prototype
```java
DeleteBucketLifecycleResult deleteBucketLifecycle(DeleteBucketLifecycleRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketLifecycleAsync(DeleteBucketLifecycleRequest request,CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketLifecycleRequest deleteBucketLifecycleRequest = new DeleteBucketLifecycleRequest(bucket);
// Set the signature verification host, verifies all headers by default
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
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | deleteBucketLifecycleAsync                                                 |     Result callback    | CosXmlResultListener  |

#### Response description
The result of the request is returned through DeleteBucketLifecycleResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Versioning
### Setting versioning

## Feature description

This API is used to set the versioning configuration of a bucket.

#### Method prototype
```java
PutBucketVersioningResult putBucketVersioning(PutBucketVersioningRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketVersionAsync(PutBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-versioning)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketVersioningRequest putBucketVersioningRequest = new PutBucketVersioningRequest(bucket);
putBucketVersioningRequest.setEnableVersion(true); //true: enable versioning; false: suspend versioning
// Set the signature verification host, verifies all headers by default
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
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| isEnable | Indicates whether to enable versioning: <br><li>true: enable<br><li>false: suspend | boolean |
| headerKeys  | Indicates whether the signature verifies the header | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description
The result of the request is returned through PutBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying versioning

## Feature description

This API is used to query the versioning configuration of a bucket.

#### Method prototype
```java
GetBucketVersioningResult getBucketVersioning(GetBucketVersioningRequest request) throws CosXmlClientException, CosXmlServiceException;
void getBucketVersioningAsync(GetBucketVersioningRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-versioning)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketVersioningRequest getBucketVersioningRequest = new GetBucketVersioningRequest(bucket);
// Set the signature verification host, verifies all headers by default
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
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| headerKeys  | Indicates whether the signature verifies the header | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description
The result of the request is returned through GetBucketVersioningResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| versioningConfiguration | [VersioningConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/VersioningConfiguration.java) | Returns the versioning status of the bucket under the specified account                      |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Cross-region replication
### Setting cross-region replication rules

## Feature description

This API is used to set the cross-region replication rules of a bucket

#### Method prototype
```java
PutBucketReplicationResult putBucketReplication(PutBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void putBucketReplicationAsync(PutBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
string ownerUin = "100000000001"; //Replication initiator identifier: OwnerUin
string subUin = "100000000001"; //Replication initiator identifier: SubUin
PutBucketReplicationRequest putBucketReplicationRequest = new PutBucketReplicationRequest(bucket);
putBucketReplicationRequest.setReplicationConfigurationWithRole(ownerUin, subUin);
PutBucketReplicationRequest.RuleStruct ruleStruct = new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; // Used to identify the name of the replication rule
ruleStruct.isEnable = true; // Indicates whether the rule is enabled. true: enabled; false: not enabled
ruleStruct.region = "ap-beijing"; // Destination bucket region
ruleStruct.bucket = "destinationbucket-1250000000";  // Destination bucket
ruleStruct.prefix = "34"; // Prefix matching policy
putBucketReplicationRequest.setReplicationConfigurationWithRule(ruleStruct);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putBucketReplicationRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutBucketReplicationResult putBucketReplicationResult = cosXmlService.putBucketReplication(putBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.putBucketReplicationAsync(putBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketReplicationResult putBucketReplicationResult = (PutBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo PUT Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| ownerUin  | Replication initiator identifier: OwnerUin  | string |
| subUin  | Replication initiator identifier: SubUin    | string |
| ruleStruct  | Indicates whether the signature verifies the query parameters in the request URL   | RuleStruct |
| queryParameterKeys |  Indicates whether the signature verifies the query parameters in the request URL |  `Set<String>` |
| headerKeys  | Indicates whether the signature verifies the header | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description
The result of the request is returned through PutBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Querying cross-region replication rules

## Feature description

This API is used to query the cross-region replication rules of a bucket.

#### Method prototype
```java
GetBucketReplicationResult getBucketReplication(GetBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void getBucketReplicationAsync(GetBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketReplicationRequest getBucketReplicationRequest = new GetBucketReplicationRequest(bucket);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketReplicationRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketReplicationResult getBucketReplicationResult = cosXmlService.getBucketReplication(getBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.getBucketReplicationAsync(getBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketReplicationResult getBucketReplicationResult = (GetBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo GET Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| headerKeys  | Indicates whether the signature verifies the header | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through GetBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| replicationConfiguration | [ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ReplicationConfiguration.java) | Returns the cross-region replication configuration of the bucket under the specified account                    |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Deleting cross-region replication rules

## Feature description

This API is used to delete the cross-region replication of a bucket.

#### Method prototype
```java
DeleteBucketReplicationResult deleteBucketReplication(DeleteBucketReplicationRequest request)throws CosXmlClientException, CosXmlServiceException;
void deleteBucketReplicationAsync(DeleteBucketReplicationRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-replication)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketReplicationRequest deleteBucketReplicationRequest = new DeleteBucketReplicationRequest(bucket);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketReplicationRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    DeleteBucketReplicationResult deleteBucketReplicationResult = cosXmlService.deleteBucketReplication(deleteBucketReplicationRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
// Use async callback to make requests
cosXmlService.deleteBucketReplicationAsync(deleteBucketReplicationRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketReplicationResult deleteBucketReplicationResult = (DeleteBucketReplicationResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo DELETE Bucket replication failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Description | Type |
| ----| ---- | ---- |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| headerKeys  | Indicates whether the signature verifies the header | `Set<String>` |
| cosXmlResultListener                                                  | Result callback        | CosXmlResultListener   |


#### Response description

The result of the request is returned through DeleteBucketReplicationResult.

| Member Variable | Type | Description |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


