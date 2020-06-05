## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

## Setting Cross-Origin Configuration

#### Feature

This API (PUT Bucket cors) is used to set cross-origin access configuration on a bucket.

#### Method prototype
```java
PutBucketCORSResult putBucketCORS(PutBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketCORSAsync(PutBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-put-bucket-cors)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketCORSRequest putBucketCORSRequest = new PutBucketCORSRequest(bucket);

/**
 * CORSConfiguration.cORSRule: cross-domain access configuration
 * corsRule.id: ID of the configuration rule
 * corsRule.allowedOrigin: allowed access sources. The wildcard "*" is supported. Format: protocol://domain_name[:port], for example, http://www.qq.com
 * corsRule.maxAgeSeconds: configures the valid period of the results obtained by OPTIONS
 * corsRule.allowedMethod: allowed HTTP request methods, such as GET, PUT, HEAD, POST, DELETE
 * corsRule.allowedHeader: when sending an OPTIONS request, notifies the server which custom HTTP request headers are allowed to be used by subsequent requests. The wildcard "*" is supported.
 * corsRule.exposeHeader: configures custom headers that can be received by the browser from the server
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

// Set cross-origin access configuration information
putBucketCORSRequest.addCORSRule(corsRule);

// Set the host for signature verification, which verifies all headers by default
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

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `putBucketCORSRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor |Bucket for which to set cross-origin access in the format BucketName-APPID |string|
|corsRule|addCORSRule | Sets cross-origin access configuration for a bucket | CORSConfiguration.CORSRule |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | putBucketCORSAsync                                                 |   Result callback      | CosXmlResultListener    |

#### Response description
The result of the request is returned through PutBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

## Querying Cross-Origin Configuration

#### Feature

This API (GET Bucket cors) is used to query the cross-origin access configuration of a bucket.

#### Method prototype
```java
GetBucketCORSResult getBucketCORS(GetBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketCORSAsync(GetBucketCORSRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-get-bucket-cors)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketCORSRequest getBucketCORSRequest = new GetBucketCORSRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
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

>When initiating a request, if you want to use a calculated signature string, you can do so by calling `getBucketCORSRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description
| Parameter Name | Setting Method | Description | Type |
|-----|-----|-----|------|
|bucket| Constructor | Bucket for which to query the cross-origin configuration in the format BucketName-APPID |string|
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketCORSAsync                                                 |    Result callback    | CosXmlResultListener |

#### Response description
The result of the request is returned through GetBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
|corsConfiguration|[CORSConfiguration](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/CORSConfiguration.java)| The CORS configuration for the bucket is returned |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

## Deleting Cross-Origin Configuration

#### Feature

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of a bucket.

#### Method prototype
```java
DeleteBucketCORSResult deleteBucketCORS(DeleteBucketCORSRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketCORSAsync(DeleteBucketCORSRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-delete-bucket-cors)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketCORSRequest deleteBucketCORSRequest = new DeleteBucketCORSRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
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
|bucket| Constructor | Bucket from which to delete the cross-origin configuration in the format BucketName-APPID |string|
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | deleteBucketCORSAsync                                                 |    Result callback    | CosXmlResultListener   |

#### Response description
The result of the request is returned through DeleteBucketCORSResult.

| Member Variable | Type | Description |
|-----|-----|----|
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).
