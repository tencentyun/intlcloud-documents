## Metadata Acceleration Overview

The metadata acceleration feature leverages the excellent metadata management capabilities of CHDFS for you to access COS through HDFS semantics. After the metadata accelerator is enabled for a bucket, you can access COS directly through native HDFS APIs. This not only saves the overheads of conversion from HDFS protocol to object protocol, but also provides some native HDFS features, such as efficient atomic directory renaming, file Atime/Mtime update, efficient directory DU statistics collection, and POSIX ACL. For more information, see [Metadata Acceleration](https://intl.cloud.tencent.com/document/product/436/43304).

After metadata acceleration is enabled, the Java APIs for bucket/file operations (the COS Java SDK version must be at least v5.6.80) are basically the same as those for operations in general buckets. For more information on how to call them, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/10199). This document mainly describes some new operation features available after metadata acceleration is enabled:
- Determine whether the metadata acceleration feature is enabled for a bucket.
- Determine whether an object is a directory through the `HeadObject` API.
- Delete a directory recursively through the `DeleteObject` API.
- Quickly rename a file through the `Rename` API.
- Upload a file to a bucket with metadata acceleration enabled through the `PutObject` API.

### Creating COSClient instance

Before calling the COS API, you must create a COSClient instance first. This document takes `SECRETID` and `SECRETKEY` as an example. To create a COSClient with a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

```
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SECRETID` and `SECRETKEY` of your project.
    // 1. Pass in the obtained temporary key (`secretId`, `secretKey`, and `sessionToken`).
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional:

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30 * 1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30 * 1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

### Checking whether metadata acceleration is enabled for a bucket

#### Sample request

```
String bucketName = "examplebucket-1250000000";
// Create a client
COSClient cosClient = createCOSClient();
HeadBucketRequest headBucketRequest = new HeadBucketRequest(bucketName);
HeadBucketResult headBucketResult = cosClient.headBucket(headBucketRequest);
bool isMetaAccBucket = headBucketResult.isMetaAccBucket(); // If metadata acceleration is enabled, `isMetaAccBucket` is `true`.
```
#### Parameter description

| Parameter | Description | Type |
|------------|----------------------------------------------------------------------------------------------------|--------|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |


### Determining whether an object is a directory through `HeadObject` 

You need to first query the metadata of the specified object through `HEAD Object` and then use the method in the following example for determination.

#### Sample request

```
String bucketName = "examplebucket-1250000000";
String key = "test";
// Create a client
COSClient cosClient = createCOSClient();
GetObjectMetadataRequest getObjectMetadataRequest = new GetObjectMetadataRequest(bucketName, key);
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(getObjectMetadataRequest);
boolean isDir = objectMetadata.isFileModeDir();  // If the object is a directory, `isDir` is `true`.
```


#### Parameter description

| Parameter | Description | Type |
|------------|-------------------------|--------|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |

### Recursively deleting directory through `DeleteObject`

#### Sample request

```
String bucketName = "examplebucket-1250000000";
String key = "test";
// Create a client
COSClient cosClient = createCOSClient();
DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, key);
deleteObjectRequest.setRecursive(true); // Recursively delete the directory
cosClient.deleteObject(deleteObjectRequest);
```

#### Parameter description


| Parameter | Description | Type |
|----------------|------------------------------------------|------------|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |

### Quickly renaming file through `Rename`

- In a general bucket, you cannot rename a directory with an intermediate path (i.e., a directory on a view). For example, if the `key` is `/test/demo/src`, you cannot rename `/test/demo`.
- After enabling the metadata acceleration feature for a bucket, you can rename the directory. This API is newly added for this type of bucket.

#### Sample request

```
String bucketName = "examplebucket-1250000000";
String srcKey = "/test/src";
String dstKey = "test/dst"
// Create a client
COSClient cosClient = createCOSClient();
RenameRequest renameRequest = new RenameRequest(bucketName, srcKey, dstKey);
cosClient.rename(renameRequest);
```

#### Parameter description

| Parameter | Description | Type |
|------------------|--------------------------------|--------|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| srcKey        | Original object key, which must start with `/`. | String |
| dstKey        | New object key. | String |

### Uploading file to bucket with metadata acceleration enabled through `PutObject`

When uploading a file to a bucket with metadata acceleration enabled, note the following differences:
- When uploading a file to a bucket with metadata acceleration enabled through `PutObject`, if there is an intermediate path, an intermediate subdirectory will be created recursively.
- When uploading a file to a general bucket through `PutObject`, even if there is an intermediate path, it will still be regarded as a key, so `ListObjects` will process it specially, and a directory will be displayed in the console. Therefore, `HeadObject` and `ListObjects` are used in Hadoop-COS to determine whether an intermediate path exist.

#### Sample request

```
// `putObject` has an intermediate path
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "/testdemo/test/README.md";

COSClient cosClient = createCOSClient();

// Local file
String localFilePath = "README.md";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, file);

// Determine whether the intermediate path is a file or a directory
// Intermediate path
dirKey = "/testdemo/test";
GetObjectMetadataRequest getObjectMetadataRequest = new GetObjectMetadataRequest(bucketName, dirKey);
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(getObjectMetadataRequest);  // `404` will be returned for a general bucket here
boolean isDir = objectMetadata.isFileModeDir();   // `isDir` is `true`
```

#### Parameter description

For parameters of the `Put Object` API, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/44015).

## Notes

- If the above code samples fail, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/10199).
- Buckets with metadata acceleration enabled currently don't support the following API operations:
 - [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
 - [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)
 - [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)
