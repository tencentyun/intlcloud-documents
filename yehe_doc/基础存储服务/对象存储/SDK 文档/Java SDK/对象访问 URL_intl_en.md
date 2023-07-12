## Overview
The Java SDK provides APIs to generate object URLs. You can distribute these URLs to clients for anonymous downloads/distribution.
>! The URL generated using this API cannot be used to access **private-read** objects.
>
A generated pre-signed URL contains the protocol name (HTTP or HTTPS), which should be the same as that set in the COS client that requests the pre-signed URL. For detailed directions, please see the sample requests below.

## Obtaining Object URLs

#### Method prototype

```java
public URL getObjectUrl(String bucketName, String key);
public URL getObjectUrl(String bucketName, String key, String versionId);
```



#### Sample request 1: obtaining an object URL

```java
// getObjectUrl does not require identity verification.
COSCredentials cred = new AnonymousCOSCredentials();
// Set the bucket region. For abbreviations of COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Set the URL protocol.
clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

String key = "picture/photo.jpg";
String bucketName = "examplebucket-1250000000";

System.out.println(cosclient.getObjectUrl(bucketName, key));
```

#### Sample request 2: obtaining the URL of a specified version of object

```java
// getObjectUrl does not require identity verification.
COSCredentials cred = new AnonymousCOSCredentials();
// Set the bucket region. For abbreviations of COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Set the URL protocol.
clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

String key = "picture/photo.jpg";
String bucketName = "examplebucket-1250000000";
String versionId = "xxxyyyzzz111222333";

System.out.println(cosclient.getObjectUrl(bucketName, key, versionId));
```

#### Sample request 3: obtaining a URL that has a specified domain name

```java
// getObjectUrl does not require identity verification.
COSCredentials cred = new AnonymousCOSCredentials();
// Set the bucket region. For abbreviations of COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Set the URL protocol.
clientConfig.setHttpProtocol(HttpProtocol.https);
// Set a custom domain name.
UserSpecifiedEndpointBuilder endpointBuilder = new UserSpecifiedEndpointBuilder("test.endpoint.com", "service.cos.myqcloud.com");
clientConfig.setEndpointBuilder(endpointBuilder);
// Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);

String key = "picture/photo.jpg";
String bucketName = "examplebucket-1250000000";
String versionId = "xxxyyyzzz111222333";

System.out.println(cosclient.getObjectUrl(bucketName, key, versionId));
```

#### Parameter description

| Parameter | Description | Type | Required | 
| --------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
| Key | Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes | 
| versionId | Version ID of the specified object if versioning is enabled for the bucket | String | No |

