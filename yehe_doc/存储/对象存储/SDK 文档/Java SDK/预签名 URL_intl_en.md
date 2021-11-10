## Overview
The COS SDK for Java provides APIs for getting pre-signed request URLs and for generating signatures. The URLs and signatures can be distributed to clients for download or upload. For private-read files, please note that a pre-signed URL is only valid for a certain period of time.
A generated pre-signed URL contains the protocol name (HTTP or HTTPS), which should be the same as that set in the COS client that requests the pre-signed URL.
For details, please see the request samples.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 


## Getting a Pre-signed Request URL 

#### Method prototype

```java
public URL generatePresignedUrl(GeneratePresignedUrlRequest req) throws CosClientException
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------ | --------------------------- |
| req | Class for requesting a pre-signed URL | GeneratePresignedUrlRequest |

The request members are described as follows:

| Request Member | Setting Method | Description | Type |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method | Constructor or set method | HTTP method. Options: GET, POST, PUT, DELETE, HEAD | HttpMethodName |
| bucketName | Constructor or set method | Bucket name, bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key | Constructor or set method | Object key (object name), a unique ID of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| expiration      | set method | Expiration time of the signature, which can be any time in the future. If this parameter is not specified, the signature will expire in one hour.  | Date                    |
| contentType | Set method | Content-Type in the request to get a signature | String |
| contentMd5 | Set method | Content-Md5 in the request to get a signature | String |
| responseHeaders | Set method | The returned http header to be overridden in the request to download a signature | ResponseHeaderOverrides |
| versionId | Set method | Specifying the version number of the object when the bucket is enabled with multiple versions | String |


#### Sample 1

Use a permanent key to generate a signed download link. The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-download-url)
```java
// Initialize the permanent key
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// To generate a URL that uses the HTTPS protocol, configure this line (recommended).
// clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the signature expiration time (optional). If it is not set, the signature expiration time in ClientConfig (1 hour) is used by default.
// Set it to any time in the future (10 minutes to 3 days are recommended).
// Set the signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);

// Parameters of the current request
req.addRequestParameter("param1", "value1");
// Headers of the current request. The Host header will be autocompleted.
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### Sample 2

Use a permanent key to generate a signed download URL that will never expire. The sample code is as follows:

```java
// Initialize the permanent key
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// To generate a URL that uses the HTTPS protocol, configure this line (recommended).
// clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the signature expiration time to a very distant time, for example, December 31, 3000 in this case.
Date expirationDate = new Date(3000, 12, 31);
req.setExpiration(expirationDate);

// Parameters of the current request
req.addRequestParameter("param1", "value1");
// Headers of the current request. The Host header will be autocompleted.
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### Sample 3

Use a temporary key to generate a signed download URL and set it to overwrite some public headers to be returned (such as `content-type` and `content-language`). The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-download-url-override-headers)
```java
// Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken)
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// To generate a URL that uses the HTTPS protocol, configure this line (recommended).
// clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// Enter the Bucket name in the format of `BucketName-APPID`. 
String bucketName = "examplebucket-1250000000";
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// Set the http header returned for download.
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// Set the returned header to contain filename information.
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
// Setting the signature expiration time (optional). If it is not configured, the signature expiration time in ClientConfig (1 hour) is used by default.
// Set the signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);

// Parameters of the current request
req.addRequestParameter("param1", "value1");
// Headers of the current request. The Host header will be autocompleted.
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### Sample 4

Generate a public read bucket (anonymous and readable) without a signed URL. The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-download-url-public)
```java
// To generate an anonymous request signature, you need to reinitialize an anonymous COSClient.
// Initialize user identity information. SecretId, SecretKey and any other key information are not required for an anonymous user.
COSCredentials cred = new AnonymousCOSCredentials();
// Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
// The bucket name must contain `appid`.
String bucketName = "examplebucket-1250000000";

// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### Sample 5

Generate pre-signed upload URLs that can be directly distributed to the client for file uploads. The sample code is as follows:

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";
// Set the signature expiration time (optional). If it is not set, the signature expiration time in ClientConfig (1 hour) is used by default.
// Set the signature to expire in half an hour.
Date expirationTime = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);

// Headers of the current request. The Host header will be autocompleted.
Map<String, String> headers = new HashMap<String,String>();
// params of the current request
Map<String, String> params = new HashMap<String,String>();

URL url = cosClient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT, headers, params);
System.out.println(url.toString());
cosClient.shutdown();
```

## Generating a Signature

The COSSigner class provides methods for constructing COS signatures to be distributed to mobile SDKs for file upload and download. The path of the signature matches the key to be operated on after distribution.

#### Method prototype

```java
// Construct a COS signature.
// The generated signature must also carry the corresponding header and param for uploads and downloads.
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        Map<String, String> headerMap, Map<String, String> paramMap, COSCredentials cred,
        Date expiredTime);
```

#### Parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | -------------- |
| methodName | HTTP request method, can be set to PUT, GET, DELETE, HEAD, or POST | HttpMethodName |
| resouce_path | Path to be signed, same as the key of the uploaded file, must start with `/` | HttpMethodName |
| cred | Credential Information | COSCredentials |
| expiredTime  | Expiration Date | Date |
| headerMap | HTTP Header map to be signed. Only `Host`, `Content-Type`, `Content-Md5`, and headers that start with x can be signed.  | Map |
| paramMap | URL Param map to be signed | Map |

#### Returned values
Signature string of the String type.


#### Sample 1: Generate an upload signature

[//]: # (.cssg-snippet-get-authorization-for-upload)
```java
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Setting the expiration time to 1 hour
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// For the key needing a signature, the generated signature can only be used for uploading the corresponding key.
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";

// Headers of the current request. The Host header will be autocompleted.
Map<String, String> headers = new HashMap<String,String>();
// params of the current request
Map<String, String> params = new HashMap<String,String>();

String sign = signer.buildAuthorizationStr(HttpMethodName.PUT, key, headers, params, cred, expiredTime);
```

#### Sample 2: Generate a download signature

[//]: # (.cssg-snippet-get-authorization-for-download)
```java
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Set the expiration time to 1 hour.
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// For the key needing a signature, the generated signature can only be used for downloading the corresponding key.
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";

// Headers of the current request. The Host header will be autocompleted.
Map<String, String> headers = new HashMap<String,String>();
// params of the current request
Map<String, String> params = new HashMap<String,String>();

String sign = signer.buildAuthorizationStr(HttpMethodName.GET, key, headers, params, cred, expiredTime);
```

#### Sample 3: Generate a delete signature

[//]: # (.cssg-snippet-get-authorization-for-delete)
```java
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// Set the expiration time to 1 hour.
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// For the key needing a signature, the generated signature can only be used for deleting the corresponding key.
// Object key, the unique identifier of the object in the bucket.
String key = "exampleobject";

// Headers of the current request. The Host header will be autocompleted.
Map<String, String> headers = new HashMap<String,String>();
// params of the current request
Map<String, String> params = new HashMap<String,String>();

String sign = signer.buildAuthorizationStr(HttpMethodName.DELETE, key, headers, params, cred, expiredTime);
```
