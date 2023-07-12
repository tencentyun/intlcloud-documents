## Overview

This document provides an overview of APIs and SDK code samples related to querying object metadata.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

## Simple Operations

Requests for simple operations need to be initiated through COSClient instances. You need to create a COSClient instance before performing simple operations.

COSClient instances are concurrency safe. You are advised to create only one COSClient instance for a process and then close it when it is no longer used to initiate requests.

### Creating a COSClient instance

Before calling the COS API, you need to create a COSClient instance.

```java
// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol, `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
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

### Creating a COSClient client with a temporary key

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For how to generate a temporary key, please see [Generating a Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048#cos-sts-sdk).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For how to generate temporary keys, please visit https://intl.cloud.tencent.com/document/product/436/14048.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol, `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
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

### Querying object metadata

This API (`HEAD Object`) is used to query object metadata.

#### Method prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

try {
    ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
    System.out.println(objectMetadata.getCrc64Ecma());
    System.out.println(objectMetadata.getLastModified());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter  | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName |  Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: returns `ObjectMetadata`, including the user-defined headers and object metadata such as the ETag.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `ObjectMetadata` class is used to record the metadata of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than user-defined metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |