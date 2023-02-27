## Overview

This document provides an overview of APIs and SDK code samples for deleting an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

## Simple Operations

Requests for simple operations need to be initiated through `COSClient` instances. You need to create a `COSClient` instance before performing simple operations.

`COSClient` instances are concurrency-safe. You are advised to create only one COSClient instance for a process and then close it when it is no longer used to initiate requests.

### Creating a COSClient instance

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

### Creating a COSClient instance with a temporary key

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For details on how to generate a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For details on how to generate temporary keys, visit https://intl.cloud.tencent.com/document/product/436/14048.
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

### Deleting an object

This API (`DELETE Object`) is used to delete a specified object.

#### Method prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
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

try {
    cosClient.deleteObject(bucketName, key);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Field description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName |  Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Delete objects in batch

This API (`DELETE Multiple Objects`) is used to delete a batch of objects.

#### Method prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
    throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Sample request
```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time.
ArrayList<KeyVersion> keyList = new ArrayList<>();
// Pass the names of files to be deleted.
// Note that filenames are not allowed to start with a forward slash (/) or backslash (\). For example:
// The bucket directory contains the `a/b/c.txt` file. If you want to delete the `a/b/c.txt` file, run `keyList.add(new KeyVersion("a/b/c.txt"))`. If you run `keyList.add(new KeyVersion("/a/b/c.txt"))`, the deletion fails.
keyList.add(new KeyVersion("aaa"));
keyList.add(new KeyVersion("bbb"));
keyList.add(new KeyVersion("ccc"));
deleteObjectsRequest.setKeys(keyList);

try {
    DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) {
    // If the deletion fails partially, `MultiObjectDeleteException` is returned.
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Field description

| Parameter | Description | Type |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | Request | DeleteObjectsRequest |

Description of the `Request` member:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| quiet | Indicates how to return the deletion result. Valid values: true and false (default). If set to `true`, only error messages due to failed deletions are returned. If set to `false`, messages indicating successful and failed deletion are returned | Boolean |
| keys | List of object paths. The version ID of each object is optional. | List&lt;DeleteObjectsRequest.KeyVersion&gt; |

`DeleteObjectsRequest.KeyVersion` members are described as follows:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| version | (Optional) Specifies the version ID of an object to delete from a versioning-enabled bucket | String |

#### Response description

- Success: No value is returned.
- Failure: an error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Deleting objects of a specified version in batches

This API (`DELETE Multiple Objects`) is used to delete a batch of objects of a specified version.

>? Versioning must be enabled for the corresponding bucket.
>

#### Method prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
    throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time.
ArrayList<KeyVersion> keyList = new ArrayList<>();
// Enter the name of the file to delete and the corresponding version number.
// You can obtain the version number at: Listing Objects -> Simple Operations -> Listing the historical versions of an object.
keyList.add(new KeyVersion("aaa", "aaa versionId"));
keyList.add(new KeyVersion("bbb", "bbb versionId"));
keyList.add(new KeyVersion("ccc", "ccc versionId"));
deleteObjectsRequest.setKeys(keyList);

try {
    DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) {
    // If the deletion fails partially, `MultiObjectDeleteException` is returned.
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Field description

| Parameter | Description | Type |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | Request | DeleteObjectsRequest |

Description of the `Request` member:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| quiet | Indicates how to return the deletion result. Valid values: true and false (default). If set to `true`, only error messages due to failed deletions are returned. If set to `false`, messages indicating successful and failed deletion are returned | Boolean |
| keys | List of object paths. The version ID of each object is optional. | List&lt;DeleteObjectsRequest.KeyVersion&gt; |

`DeleteObjectsRequest.KeyVersion` members are described as follows:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| version | (Optional) Specifies the version ID of an object to delete from a versioning-enabled bucket | String |

#### Response description

- Success: No value is returned.
- Failure: an error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Deleting a directory

The directory deletion operation consists of two steps: list all objects in the directory to be deleted, and delete the objects in batches.

```java
// For details about how to list all objects in a directory, see: Listing Objects -> Simple Operations -> Listing objects and subdirectories in a directory.
// For details about how to implement batch deletion, see "Deleting objects in batches" on the current page.

// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Directory to be deleted, which is a path relative to `bucket`.
String delDir = "exampledir";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name
listObjectsRequest.setBucketName(bucketName);
// `prefix` indicates to use `prefix` as the prefix of objected listed.
// Here, enter the path of the listed directory relative to `bucket`.
listObjectsRequest.setPrefix(delDir);
// Set the maximum number of objects to be traversed, which can be up to 1,000 in one listobject operation
listObjectsRequest.setMaxKeys(1000);

// Save each list result.
ObjectListing objectListing = null;

do {
    try {
        objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    // Save the list of listed objects.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();

    ArrayList<KeyVersion> delObjects = new ArrayList<KeyVersion>();

    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        delObjects.add(new KeyVersion(cosObjectSummary.getKey()));
    }

    DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);

    deleteObjectsRequest.setKeys(delObjects);

    try {
        DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
        List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
    } catch (MultiObjectDeleteException mde) {
        // If the deletion fails partially, `MultiObjectDeleteException` is returned.
        List<DeletedObject> deleteObjects = mde.getDeletedObjects();
        List<DeleteError> deleteErrors = mde.getErrors();
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    // Next start position.
    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```
