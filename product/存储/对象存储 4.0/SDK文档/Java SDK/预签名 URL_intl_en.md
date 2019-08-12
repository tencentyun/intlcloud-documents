## Overview
The SDK for Java provides APIs to get pre-signed request URLs and generating signatures which can be distributed to clients for download or upload. Please note that if your file is private-read, then the pre-signed link is only valid for a certain period of time.

## Getting a Pre-signed Request URL 

### Method Prototype

```java
public URL generatePresignedUrl(GeneratePresignedUrlRequest req) throws CosClientException
```
### Parameter Descriptions
| Parameter Name | Description | Type |
| -------- | ------------ | --------------------------- |
| req | Pre-signed request class | GeneratePresignedUrlRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method | Constructor or set method | HTTP method: PUT (for upload), GET (for download), DELETE (for deletion) | HttpMethodName |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | An object key (Key) is a unique ID of an object in the bucket. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324#objectkey) | String |
| expiration | set method | Signature expiration time | Date |
| contentType | set method | Content-Type in the request to be signed | String |
| contentMd5 | set method | Content-Md5 in the request to be signed | String |
| responseHeaders | set method | The returned HTTP headers to be overwritten in the signed download request | ResponseHeaderOverrides |


### Example 1

Use a permanent key to generate a signed download link with the following sample code:

```java
// Initialize permanent key information
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
Region region = new Region("ap-guangzhou");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the signature expiration time (optional). If it is not set, the default expiration time in ClientConfig (1 hour) will be used
// Here, the signature is set to expire in half an hour
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL downloadUrl = cosClient.generatePresignedUrl(req);
String downloadUrlStr = downloadUrl.toString();
```

### Example 2

Use a temporary key to generate a signed download link and set to overwrite some of the returned common headers (such as content-type and content-language) with the following sample code:

```java
// 1. Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken)
String tmpSecretId = "COS_SECRETID";
String tmpSecretKey = "COS_SECRETKEY";
String sessionToken = "COS_TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2. Set the bucket region. For abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
// clientConfig contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, see the source code or the FAQs about the SDK for Java
Region region = new Region("ap-guangzhou");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client
COSClient cosClient = new COSClient(cred, clientConfig);
// Bucket name is in the format of BucketName-APPID 
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the HTTP headers returned when downloading
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
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
// Set the signature expiration time (optional). If it is not set, the default expiration time in ClientConfig (1 hour) will be used
// Here, the signature is set to expire in half an hour
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
```
### Example 3

Generate a signature-free link for a public-read (anonymously readable) bucket with the following sample code:

```java
// To generate an anonymous request signature, you need to reinitialize an anonymous cosClient
// 1. Initialize user identity information. An anonymous identity does not require key information such as SecretId or SecretKey to be passed in
COSCredentials cred = new AnonymousCOSCredentials();
// 2. Set the bucket region. For abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// 3. Generate a COS client
COSClient cosClient = new COSClient(cred, clientConfig);
// The bucket name should include the appid
String bucketName = "examplebucket-1250000000";

String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosClient.generatePresignedUrl(req);

System.out.println(url.toString());

cosClient.shutdown();
```

### Example 4

Generate some pre-signed upload links which can be directly distributed to clients for file uploads with the following sample code:

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";

String key = "exampleobject";
// Set the signature expiration time (optional). If it is not set, the default expiration time in ClientConfig (1 hour) will be used
// Here, the signature is set to expire in half an hour
Date expirationTime = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
URL url = cosClient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);
```

## Generating a Signature

The COSSigner class provides a way to construct COS signatures for distribution to mobile SDKs for file uploads and downloads. The signed path matches the key to be manipulated after the distribution.

### Method Prototype

```java
// Construct a COS signature
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        COSCredentials cred, Date expiredTime);

// Construct a COS signature
// Compared to the first method, the second method additionally signs some HTTP headers and all URL parameters passed in,
// which is used for more complex signature control. The generated signature must carry the corresponding headers and parameters too when upload and download operations are performed
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        Map<String, String> headerMap, Map<String, String> paramMap, COSCredentials cred,
        Date expiredTime);
```

### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | -------------- |
| methodName | HTTP request method; value range: PUT, GET, DELETE, HEAD, POST | HttpMethodName |
| resouce_path | The path to be signed, which is the same as the key of the file to be uploaded and should start with `/` | HttpMethodName |
| cred | Key information | COSCredentials |
| expiredTime | Expiration time | Date |
| headerMap | HTTP header map to be signed. Only Content-Type, Content-Md5, and headers starting with x passed in are signed | Map |
| paramMap | URL parameter map to be signed | Map |

### Return Value
Signature string in String type.

### Example 1. Generating an Upload Signature

```java
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Set the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// The key to be signed. The generated signature can only be used for uploads using this key
String key = "/exampleobject";
String sign = signer.buildAuthorizationStr(HttpMethodName.PUT, key, cred, expiredTime);
```

### Example 2. Generating a Download Signature

```java
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Set the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// The key to be signed. The generated signature can only be used for downloads using this key
String key = "/exampleobject";
String sign = signer.buildAuthorizationStr(HttpMethodName.GET, key, cred, expiredTime);
```

### Example 3. Generating a Deletion Signature

```java
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Set the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// The key to be signed. The generated signature can only be used for deletions using this key
String key = "/exampleobject";
String sign = signer.buildAuthorizationStr(HttpMethodName.DELETE, key, cred, expiredTime);
```
