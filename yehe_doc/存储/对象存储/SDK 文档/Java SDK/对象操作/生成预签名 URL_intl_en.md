## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.

For details about how to use a pre-signed URL for uploads, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114). For details about how to use a pre-signed URL for downloads, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

>?
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> - Obtain the signed/pre-signed URL function. By default, it is signed to the Host header. You can also choose not to sign it to Host (the request might fail or vulnerabilities might occur).
> 

## Simple Operations

Requests for simple operations need to be initiated through `COSClient` instances. You need to create a `COSClient` instance before performing simple operations.

`COSClient` instances are concurrency-safe. You are advised to create only one COSClient instance for a process and then close it when it is no longer used to initiate requests.

### Creating a COSClient instance with a temporary key (recommended)

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For details on how to generate a temporary key, see [Generating Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048#cos-sts-sdk).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For details on how to generate temporary keys, please visit https://intl.cloud.tencent.com/document/product/436/14048#cos-sts-sdk.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `HTTP` or `HTTPS`.
    // For v5.6.53 or earlier, HTTPS is recommended.
    // For v5.6.54 or later, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional.

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30*1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30*1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

### Creating a COSClient instance with a permanent key (not recommended)

Before calling the COS API, first create a COSClient instance.

```java
// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
    SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `HTTP` or `HTTPS`.
    // For v5.6.53 or earlier, HTTPS is recommended.
    // For v5.6.54 or later, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional.

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30*1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30*1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

### Getting pre-signed URLs

#### Method prototype

```java
public URL generatePresignedUrl(String bucketName, String key, Date expiration, HttpMethodName method, Map<String, String> headers, Map<String, String> params, Boolean signPrefixMode, Boolean signHost) throws CosClientException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

// Set the signature expiration time (optional). If it is not set, the signature expiration time in `ClientConfig` (1 hour) is used by default.
// Set the signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30 * 60 * 1000);

// Enter the parameters of the current request, which should be the same as those of the actual request. This can prevent users from tampering with the HTTP request parameters. 
Map<String, String> params = new HashMap<String, String>();
params.put("param1", "value1");

// Enter the headers of the current request, which should be the same as those of the actual request. This can prevent users from tampering with the HTTP request headers.
Map<String, String> headers = new HashMap<String, String>();
headers.put("header1", "value1");

// HTTP method of the request. PUT for an upload request, GET for a download request, and DELETE for a deletion request.
HttpMethodName method = HttpMethodName.GET;

URL url = cosClient.generatePresignedUrl(bucketName, key, expirationDate, method, headers, params);
System.out.println(url.toString());

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Field description

| Parameter Name | Description | Type | Required |
| -------- | ------------ | --------------------------- | --------- |
| method          | HTTP method. Options: `GET`, `POST`, `PUT`, `DELETE`, `HEAD`                | HttpMethodName          | Yes |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| key             | Object key, the unique ID of an object in a bucket. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324#.E5.AF.B9.E8.B1.A1.E9.94.AE)（**Users do not need to encode the URL**） | String                  |  Yes |
| expiration      | Expiration time of the signature, which can be any time in the future. If this parameter is not specified, the signature will expire in one hour              | Date                    |  No |
| headers         | Signature headers   | Map&lt;String, String> | No |
| params         | Signature parameters   | Map&lt;String, String> | No |
| signPrefixMode | Whether to specify a signature with the `sign` parameter (not recommended). Default value: `false` | boolean | No |
| signHost  | Whether to sign the `Host` header (recommended). Default value: `true` |  boolean | No |

### Generating pre-signed download URLs overwriting headers

#### Method prototype

```java
public URL generatePresignedUrl(GeneratePresignedUrlRequest req, boolean signHost) throws CosClientException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);

// Set the http header returned for download.
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// Set the returned header to contain filename information.
String responseContentDispositon = "filename=exampleobject";
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
// Enter the headers of the current request
// `host` is required.
req.putCustomRequestHeader(Headers.HOST, cosClient.getClientConfig().getEndpointBuilder().buildGeneralApiEndpoint(bucketName));
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Field description

| Parameter  | Description | Type | Required |
| -------- | ------------ | ------------------------ | ------- |
| req | Class for requesting a pre-signed URL | GeneratePresignedUrlRequest | Yes |
| signHost  | Whether to sign the `Host` header (recommended). Default value: `true` |  boolean | No |

Description of the `Request` member:

| Request Member | Setting Method | Description | Type |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method | Constructor or set method | HTTP method. Options: GET, POST, PUT, DELETE, HEAD | HttpMethodName |
| bucketName | Constructor or set method | Bucket name, bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key             | Constructor or set method | Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324#.E5.AF.B9.E8.B1.A1.E9.94.AE)（**Users do not need to encode the URL**） | String                  |
| expiration      | set method | Expiration time of the signature, which can be any time in the future. If this parameter is not specified, the signature will expire in one hour.  | Date                    |
| contentType | Set method | Content-Type in the request to get a signature | String |
| contentMd5 | Set method | Content-Md5 in the request to get a signature | String |
| responseHeaders | Set method | The returned http header to be overridden in the request to download a signature | ResponseHeaderOverrides |
| versionId | Set method | Specifying the version number of the object when the bucket is enabled with versioning | String |

### Generating a signature

This API is used to construct a signature for a COS request. You are advised to use a temporary key to generate a signature.

#### Generating a signature using a temporary key (recommended)

```java
// Here, the temporary key information is needed.
// For details on how to generate temporary keys, please visit https://intl.cloud.tencent.com/document/product/436/14048#cos-sts-sdk.
String tmpSecretId = "TMPSECRETID";
String tmpSecretKey = "TMPSECRETKEY";
String sessionToken = "SESSIONTOKEN";

COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// If the `key` does not start with "/", you need to add "/" at the beginning; otherwise, the `resource_path` will be the `key`.
String resource_path="/" + key;

ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));

// It is used to generate a signature.
COSSigner signer = new COSSigner();
// Setting the signature expiration time (optional). If it is not configured, the signature expiration time in ClientConfig (1 hour) is used by default.
// Set the signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);

// Parameters of the current request
Map<String, String> params = new HashMap<String, String>();
params.put("param1", "value1");

// Enter the headers of the current request
Map<String, String> headers = new HashMap<String, String>();
// `host` is required.
headers.put(Headers.HOST, clientConfig.getEndpointBuilder().buildGeneralApiEndpoint(bucketName));
headers.put("header1", "value1");

// HTTP method of the request. PUT for an upload request, GET for a download request, and DELETE for a deletion request.
HttpMethodName method = HttpMethodName.GET;

String sign = signer.buildAuthorizationStr(method, resource_path, headers, params, cred, expirationDate, true);
```

### Generating a signature using a permanent key

```java
// Set the user identity information.
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// If the `key` does not start with "/", you need to add "/" at the beginning; otherwise, the `resource_path` will be the `key`.
String resource_path="/" + key;

ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));

// It is used to generate a signature.
COSSigner signer = new COSSigner();
// Setting the signature expiration time (optional). If it is not configured, the signature expiration time in ClientConfig (1 hour) is used by default.
// Set the signature to expire in half an hour.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);

// Parameters of the current request
Map<String, String> params = new HashMap<String, String>();
params.put("param1", "value1");

// Enter the headers of the current request
Map<String, String> headers = new HashMap<String, String>();
// `host` is required.
headers.put(Headers.HOST, clientConfig.getEndpointBuilder().buildGeneralApiEndpoint(bucketName));
headers.put("header1", "value1");

// HTTP method of the request. PUT for an upload request, GET for a download request, and DELETE for a deletion request.
HttpMethodName method = HttpMethodName.GET;

String sign = signer.buildAuthorizationStr(method, resource_path, headers, params, cred, expirationDate, true);
```

### Generating pre-signed download URL with speed limit

For instructions about the speed limits, see [Single-Connection Bandwidth Limit](https://intl.cloud.tencent.com/document/product/436/34072).

#### Sample request

The following takes generating a speed-limited pre-signed download URL as an example:

```java
public static void GenerateSimplePresignedDownloadUrl() {
        // 1. Initialize user authentication information (`secretId`, `secretKey`).
    		// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
    		SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    		SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    		COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
        // 2. Set the region of the bucket.
  			// COS_REGION parameter, which needs to be set to the actual region of the bucket, for example, ap-beijing. For the abbreviations for more COS regions, visit https://cloud.tencent.com/document/product/436/6224.
        ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));
        // 3. Generate a COS client
        COSClient cosclient = new COSClient(cred, clientConfig);
        // The bucket name must contain `appid`.
        String bucketName = "examplebucket-1250000000";
        
        String key = "exampleobject";
        GeneratePresignedUrlRequest req =
                new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
        // Set the signature expiration time (optional). If it is not set, the signature expiration time in `ClientConfig` (1 hour) is used by default.
        // Set the signature to expire in half an hour.
        Date expirationDate = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
        req.setExpiration(expirationDate);

        // Parameters of the current request
        // Set the speed limit value, such as 128 KB/s.
        req.addRequestParameter("x-cos-traffic-limit", "1048576");

        // Enter the headers of the current request. `Host` is required.
        req.putCustomRequestHeader(Headers.HOST,
        cosclient.getClientConfig().getEndpointBuilder().buildGeneralApiEndpoint(bucketName));
        //req.putCustomRequestHeader("header1", "value1");

        URL url = cosclient.generatePresignedUrl(req);
        System.out.println(url.toString());

        cosclient.shutdown();
    }
```

