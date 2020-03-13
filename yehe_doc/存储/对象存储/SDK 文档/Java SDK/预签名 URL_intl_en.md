## Introduction
Java SDK provides a pre-signed URL for obtaining a request and an API for generating a signature, which can be distributed to the client for download or upload. If your files have private read permissions, note that pre-signed URL is only valid for a certain period of time.

## Obtaining pre-signed URL used for request 

#### Method Prototype

```java
public URL generatePresignedUrl(GeneratePresignedUrlRequest req) throws CosClientException
```

#### Parameter Description

| Parameter Name | Description | Type |
| -------- | ------------ | --------------------------- |
| req | Class for requesting a pre-signed URL | GeneratePresignedUrlRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method | Constructor and set method | HTTP method, options：GET、POST、PUT、DELETE、HEAD | HttpMethodName |
| bucketName | Constructor or set method | Bucket name, bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| expiration | set method | Signature expiration date | Date |
| contentType | set method | Content-Type in the request to get a signature | String |
| contentMd5 | set method | Content-Md5 in the request to get a signature | String |
| responseHeaders | set method | The returned http header to be overridden in the request to download a signature | ResponseHeaderOverrides |
| versionId | set method | Specifying the version number of the object when the bucket is enabled with multiple versions | String |


#### Example 1

Use a permanent key to generate a signed download link. The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-download-url)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Setting the signature expiration time (optional). If it is not set, the signature expiration time (5 minutes) in ClientConfig is used by default.
// Setting signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
```

#### Example 2

Use the temporary key to generate a signed download link and set it to overwrite some public headers to be returned (such as content-type, content-language). The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-download-url-override-headers)
```java
Bucket. Format: BucketName-APPID 
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Setting the http header returned during download
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
ResponseContentLanguage='string',
String responseContentDispositon = "filename=\"exampleobject\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// Setting the signature expiration time (optional). If it is not configured, the signature expiration time (5 minutes) in ClientConfig is used by default.
// Setting signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(e.toString());
```

#### Example 3

Generate a public read bucket (anonymous and readable) without a signed link. The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-download-url-public)
```java
// The bucket name must contain appid
String bucketName = "examplebucket-1250000000";

String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(e.toString());
```

#### Example 4

Generate some pre-signed upload URLs that can be directly distributed to the client for file uploads. The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Setting the signature expiration time (optional). If it is not set, the signature expiration time (5 minutes) in ClientConfig is used by default.
// Setting signature to expire in half an hour.
Date expirationTime = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
URL url = cosClient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);
System.out.println(e.toString());
```

## Generating a signature

COSSigner class provides methods for constructing COS signatures for distribution to mobile SDK for file upload and download. The path of the signature matches the key to be operated on after distribution.

#### Method Prototype

```java
// Constructing COS signature
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        COSCredentials cred, Date expiredTime);

// Constructing COS signature
// Compared with first method, the second method provides additional signatures for some HTTP Headers and all parameters in the entered URL.
// It is used for more complicated signature control. The generated signature must also carry the corresponding header and param for upload and download operations.
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        Map<String, String> headerMap, Map<String, String> paramMap, COSCredentials cred,
        Date expiredTime);
```

#### Parameter Description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | -------------- |
| methodName | HTTP request method, can be set to PUT、GET、DELETE、HEAD、POST | HttpMethodName |
| resouce_path | Path to be signed, same as the key of the uploaded file, must start with `/` | HttpMethodName |
| cred | Credential Information | COSCredentials |
| expiredTime  | Expiration Date | Date |
| headerMap | HTTP Header map to be signed, only sign Content-Type and Content-Md5 as well as headers that start with x  | Map |
| paramMap | URL Param map to be signed | Map |

#### Return values
Signature string, the type is String.


#### Example 1: Generate an upload signature

[//]: # (.cssg-snippet-get-authorization-for-upload)
```java
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Setting the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// The key that needs signature. The generated signature can only be used for uploading the corresponding key.
String key = "exampleobject";
String sign = signer.buildAuthorizationStr(HttpMethodName.PUT, key, cred, expiredTime);
```

#### Example 2: Generate a download signature

[//]: # (.cssg-snippet-get-authorization-for-download)
```java
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Setting the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// The key that needs signature. The generated signature can only be used for deleting the corresponding key.
String key = "exampleobject";
String sign = signer.buildAuthorizationStr(HttpMethodName.GET, key, cred, expiredTime);
```

#### Example 3: Generate a delete signature

[//]: # (.cssg-snippet-get-authorization-for-delete)
```java
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Setting the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// The key that needs signature. The generated signature can only be used for deleting the corresponding key.
String key = "exampleobject";
String sign = signer.buildAuthorizationStr(HttpMethodName.DELETE, key, cred, expiredTime);
```
