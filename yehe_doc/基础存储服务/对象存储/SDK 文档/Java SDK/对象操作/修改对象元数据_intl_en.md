## Overview

This document provides SDK code samples related to object metadata modification.

Object metadata modification uses the object replication API and sets new metadata during object replication.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path |

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

### Modifying object metadata

This API uses the object replication API and sets new metadata during object replication. In the object replication API, only metadata is modified, and object data is not copied.

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Upload -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Region where the bucket resides
// For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
Region region = new Region("ap-beijing");
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

// Get the current object metadata.
ObjectMetadata objectMetadata = cosclient.getObjectMetadata(bucketName, key);
// `Replaced` must be set if you modify object metadata.
objectMetadata.setHeader("x-cos-metadata-directive", "Replaced");

// Set the new object metadata.
objectMetadata.setHeader("x-cos-storage-class", "STANDARD_IA");
objectMetadata.setContentType("text/plain");

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(region, bucketName, key, bucketName, key);
copyObjectRequest.setNewObjectMetadata(objectMetadata);

try {
    CopyObjectResult copyObjectResult = cosclient.copyObject(copyObjectRequest);
    System.out.print(copyObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

The request members are described as follows:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default: same as the `region` value in the current clientConfig, which represents intra-region replication | String |
| sourceBucketName | Source bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| sourceKey | Source object key. An object key is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file. | String |
| destinationBucketName | Destination bucket name in the format of `BucketName-APPID`. It should contain letters, numbers, and hyphens. | String |
| destinationKey | Destination object key. An object key is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Response description

- Success: returns `CopyObjectResult`, including the ETag and other information on the new file.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
