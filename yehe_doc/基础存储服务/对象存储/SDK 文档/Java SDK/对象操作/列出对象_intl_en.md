## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |

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

### Listing objects on the first page

This API is used to list some objects in a bucket.

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Sample request
```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name
listObjectsRequest.setBucketName(bucketName);
// Set to use `prefix` as the prefix of objected listed.
listObjectsRequest.setPrefix("");
// Set the maximum number of listed objects (up to 1,000 per `listobject` request).
listObjectsRequest.setMaxKeys(1000);

// Save the list result.
ObjectListing objectListing = null;

try {
    objectListing = cosclient.listObjects(listObjectsRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// `object summary` is the list of objects listed this time.
List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
    // Object key.
    String key = cosObjectSummary.getKey();
    // Object ETag.
    String etag = cosObjectSummary.getETag();
    // Object length
    long fileSize = cosObjectSummary.getSize();
    // Object storage class
    String storageClasses = cosObjectSummary.getStorageClass();
}

if (objectListing.isTruncated()) {
    // Indicates not all objects are listed and the list is truncated.

    // Next start position.
    String nextMarker = objectListing.getNextMarker();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

The request parameters are described as follows:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. <br>Default value: `""` (left empty), meaning to return all objects in the bucket | String |
| marker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxKeys | Constructor or set method | Maximum number of returned members (up to 1,000). <br>Default value: `1000` | Integer |

#### Response description

- Success: returns `ObjectListing`, including all members and `nextMarker`.  
- Failure: throws a "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Listing objects on the second page

This API is used to list the remaining objects on the truncated list.

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Sample request
```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Next start position.
// Obtained by using the requesting the objects on the truncated list. For details, see "Listing objects on the first page" above.
String nextMarker = "nextMarker";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name
listObjectsRequest.setBucketName(bucketName);
// Set to use `prefix` as the prefix of objected listed.
listObjectsRequest.setPrefix("");
// Set the maximum number of listed objects (up to 1,000 per `listobject` request).
listObjectsRequest.setMaxKeys(1000);
// Set the position for truncation.
listObjectsRequest.setMarker(nextMarker);

// Save the list result.
ObjectListing objectListing = null;

try {
    objectListing = cosclient.listObjects(listObjectsRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// `object summary` is the list of objects listed this time.
List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
    // Object key.
    String key = cosObjectSummary.getKey();
    // Object ETag.
    String etag = cosObjectSummary.getETag();
    // Object length
    long fileSize = cosObjectSummary.getSize();
    // Object storage class
    String storageClasses = cosObjectSummary.getStorageClass();
}

if (objectListing.isTruncated()) {
    // Indicates not all objects are listed and the list is truncated.

    // Next start position.
    String nextMarker = objectListing.getNextMarker();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

The request parameters are described as follows:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. <br>Default value: `""` (left empty), meaning to return all objects in the bucket | String |
| marker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxKeys | Constructor or set method | Maximum number of returned members (up to 1,000). <br>Default value: `1000` | Integer |

#### Response description

- Success: returns `ObjectListing`, including all members and `nextMarker`.  
- Failure: throws a "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Listing objects and subdirectories in a directory

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name
listObjectsRequest.setBucketName(bucketName);
// `prefix` indicates to use `prefix` as the prefix of objected listed.
// Here, enter the path of the listed directory relative to `bucket`.
listObjectsRequest.setPrefix("/dir/");
// `delimiter` is the directory truncation symbol. For example, `/` indicates that an object name with `/` is considered a level-1 directory.
listObjectsRequest.setDelimiter("/");
// Set the maximum number of objects to be traversed, which can be up to 1,000 in one listobject operation
listObjectsRequest.setMaxKeys(1000);

// Save each list result.
ObjectListing objectListing = null;

do {
    try {
        objectListing = cosclient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    // Save the subdirectories listed.
    List<String> commonPrefixes = objectListing.getCommonPrefixes();
    for (String commonPrefix : commonPrefixes) {
        System.out.println(commonPrefix);
    }

    // Save the list of listed objects.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // Object key.
        String key = cosObjectSummary.getKey();
        // Object ETag.
        String etag = cosObjectSummary.getETag();
        // Object length
        long fileSize = cosObjectSummary.getSize();
        // Object storage class
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    // Next start position.
    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

The request parameters are described as follows:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. <br>Default value: `""` (left empty), meaning to return all objects in the bucket | String |
| marker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxKeys | Constructor or set method | Maximum number of returned members (up to 1,000). <br>Default value: `1000` | Integer |

#### Response description

- Success: returns `ObjectListing`, including all members and `nextMarker`.  
- Failure: throws a "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Listing the historical versions of an object

This API is used to list each historical version of an object.

>? Versioning must be enabled for the bucket.
>

#### Method prototype

```java
public VersionListing listVersions(ListVersionsRequest listVersionsRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

ListVersionsRequest listVersionsRequest = new ListVersionsRequest();
// Set the bucket name
listVersionsRequest.setBucketName(bucketName);
// `prefix` indicates to use `prefix` as the prefix of objected listed.
// Here, enter the path of the listed directory relative to `bucket`.
listVersionsRequest.setPrefix("");
// `delimiter` is the directory truncation symbol. For example, `/` indicates that an object name with `/` is considered a level-1 directory.
listVersionsRequest.setDelimiter("/");
// Set the maximum number of objects to be traversed, which can be up to 1,000 in one listobject operation
listVersionsRequest.setMaxKeys(1000);

VersionListing versionListing = null;

do {
    try {
        versionListing = cosclient.listVersions(listVersionsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    List<COSVersionSummary> cosVersionSummaries = versionListing.getVersionSummaries();
    for (COSVersionSummary cosVersionSummary : cosVersionSummaries) {
        System.out.println(cosVersionSummary.getKey() + ":" + cosVersionSummary.getVersionId());
    }

    // The next start position has 2 flags: object name and object version.
    String keyMarker = versionListing.getNextKeyMarker();
    String versionIdMarker = versionListing.getNextVersionIdMarker();

    listVersionsRequest.setKeyMarker(keyMarker);
    listVersionsRequest.setVersionIdMarker(versionIdMarker);

} while (versionListing.isTruncated());

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listVersionsRequest | Request for obtaining object version information | ListVersionsRequest |

The request parameters are described as follows:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. <br>Default value: `""` (left empty), meaning to return all objects in the bucket | String |
| keyMarker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextKeyMarker` value in the previous listObjects response | String |
| versionIdMarker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextVersionIdMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxResults | Constructor or set method | Maximum number of returned members (up to 1,000). Default value: `1000` | Integer |

#### Response description

- Success: returns `ObjectListing`, including all members and `nextKeyMarker` and `nextVersionIdMarker`.
- Failure: throws a "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
