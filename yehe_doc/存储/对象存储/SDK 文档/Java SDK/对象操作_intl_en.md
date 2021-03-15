## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and advanced APIs.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes an object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |

**Multipart upload operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information about an ongoing multipart upload |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts |

## Simple Operations

### Querying an object list

#### API description

This API is used to query some or all objects in a bucket.

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates that the key of the object to be listed must start with this value.
listObjectsRequest.setPrefix("images/");
// Set the delimiter to "/" to list objects in the current directory. To list all objects, leave it empty.
listObjectsRequest.setDelimiter("/");
// Set the maximum number of traversed objects (up to 1,000 per listobject request).
listObjectsRequest.setMaxKeys(1000);
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
    // A common prefix indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary shows all listed objects.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // File path key
        String key = cosObjectSummary.getKey();
        // File ETag
        String etag = cosObjectSummary.getETag();
        // File size
        long fileSize = cosObjectSummary.getSize();
        // File storage class
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```


#### Parameter description

| Parameter | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

Request members:

| Request Member | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. <br>Default value: "" (left empty), meaning to return all objects in the bucket | String |
| marker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxKeys | Constructor or set method | The maximum number of returned members (up to 1,000). <br>Default value: `1000` | Integer |

#### Response description

- Success: returns `ObjectListing`, including all members and `nextMarker`.  
- Failure: throws a "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Uploading an object using simple upload

#### API description

This API (PUT Object) is used to upload objects to the specified bucket. It can upload a local file or an input stream of a known length to COS. It is suitable for uploading small image files (below 20 MB), with a maximum of 5 GB (inclusive) supported. Please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) if the file is larger than 5 GB.

- The file length and MD5 hash are checked by default during upload (see the sample code for disabling MD5 check).
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one.
- Once uploaded, you can download the file by calling the GetObject API with the same key, or by generating a [pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31536) and sending the file to another device for download (Please specify GET as the download method; see the section below for API instructions.)

#### Method prototype

```java
// Method 1. Upload a local file to COS.
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS.
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the two methods above to support more fine-grained parameter control, such as content-type and content-disposition.
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-put-object-flex)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
// Method 1. Upload a local file.
File localFile = new File(localFilePath);
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // Obtain the file ETag.

// Method 2. Upload an input stream (The length of the input stream must be provided in advance. Otherwise, an OOM error may occur).
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the length of the input stream to 500.
objectMetadata.setContentLength(500);
// Set the content type. Default: application/octet-stream
objectMetadata.setContentType("application/pdf");
putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
etag = putObjectResult.getETag();
// Close the input stream.

// Method 3: Provide more fine-grained control. Common settings are as follows:
// 1 storage-class. Enumerated values are `Standard` (default), `Standard_IA`, and `Archive`. For more information, please see: https://intl.cloud.tencent.com/zh/document/product/436/30925
// 2. content-type. For local file upload, the files are mapped based on the suffix by default. For example, a JPG file is mapped as image/jpeg.
// For input stream upload, the default is application/octet-stream.
// 3. Specify permissions during the upload (or call the relevant API to set an object ACL).
// 4 To disable MD5 upload verification globally, set the system environment variable. This will affect all upload verification operations, which are performed by default.
// Disable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// Enable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
localFile = new File(localFilePath);
key = "picture.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Set the storage class to STANDARD_IA.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// Set custom attributes (such as content-type, content-disposition).
objectMetadata = new ObjectMetadata();
// Here, set the upload bandwidth limit (in bit/s) to 10 MB/s.
putObjectRequest.setTrafficLimit(80*1024*1024);
// Set the content type. Default: application/octet-stream
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
putObjectResult = cosClient.putObject(putObjectRequest);
// Get the ETag of the object.
etag = putObjectResult.getETag();
// Get the CRC64 checksum of the object.
String crc64Ecma = putObjectResult.getCrc64Ecma();
```


#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request members:

| Request Member | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket.<br>For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |

The ObjectMetadata class is used to record the metadata of an object. The main members are described below:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with x-cos-meta- | Map<String, String> |
| metadata | Headers other than user-defined metadata | Map<String, String> |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |


#### Response description

- Success: returns `PutObjectResult`, including the file ETag.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The PutObjectResult class is used to return result information. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Returns the version ID of an object in a version-enabled bucket | String |
| eTag | MD5 checksum of the object returned by PUT Object | String |
|crc64Ecma| CRC64 value computed by the server based on the object content | String |


### Querying object metadata

#### API description

This API is used to query whether a specified object exists in a certain bucket.

#### Method prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-head-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |

#### Response description

- Success: returns `ObjectMetadata`, including the user-defined headers and object metadata such as the ETag.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `ObjectMetadata` class is used to record the metadata of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with x-cos-meta- | Map<String, String> |
| metadata | Headers other than user-defined metadata | Map<String, String> |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |


### Downloading an object

#### API description

This API (GET Object) is used to download an object.

#### Method prototype

```java
// Method 1. Download a file and get the input stream.
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// Method 2. Download the file locally.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1. Get the input stream of the downloaded file.
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// Here, set the download bandwidth limit in bit/s to 10 MB/s
getObjectRequest.setTrafficLimit(80*1024*1024);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// Download the CRC64 value of the object.
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
// Close the input stream.
cosObjectInput.close();

// Method 2. Download the file locally.
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```


#### Parameter description

| Parameter | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | The file saved locally | File |

Request members:

| Request Member | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | Set method | Download range | Long[] |
| trafficLimit | Set method | Traffic limits (in bit/s) on the downloaded object. The default setting is no limit. | Int |


#### Response description

- **Method 1 (Get the input stream of the downloaded file)**
  - Success: returns the `COSObject` class, including the input stream and object attributes.
  - Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
- **Method 2 (Download the file locally)**
  - Success: returns `objectMetadata`, including the file's custom headers, content-type, and other attributes.
  - Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `COSObject` class is used to return request results. Its main members as described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| metadata | Object metadata  | ObjectMetadata |
| objectContent | Data stream containing COS object content  | COSObjectInputStream |


### Copying an object

#### API description 

This API (Put Object Cop) is used to copy an object. You can copy an object up to 5 GB in size across regions, accounts, and buckets, provided that you have read permission for the source file and write permission for the destination file. To copy files larger than 5 GB, use the [advanced replication API](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

[//]: # (.cssg-snippet-copy-object)
```java
// Intra-region and intra-account replication
// Enter the bucket name in the format of BucketName-APPID.
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of BucketName-APPID.
String destBucketName = "examplebucket-1250000000";
// The destination file to be copied into
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// Cross-account and cross-region replication (read permission for the source file and write permission for the destination file are required)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
// Get the CRC64 value of the object
String crc64Ecma = copyObjectResult.getCrc64Ecma();
```


#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request members:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default: same as the "region" value in the current `clientConfig`, meaning intra-region replication | String |
| sourceBucketName | Source bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| sourceKey | Source object key. An object key is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: the latest version of the source file | String |
| destinationBucketName | Destination bucket name in the format of `BucketName-APPID`. It should contain letters, numbers, and hyphens. | String |
| destinationKey | Destination object key. An object key is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Response description

- Success: returns `CopyObjectResult`, including the ETag and other information on the new file.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Deleting a single object

#### API description

This API is used to delete a specified object (file/object) from a bucket.

#### Method prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Deleting multiple objects

#### API description

The API (DELETE Multiple Objects) is used to delete multiple objects.

#### Method prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
    throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-multi-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time.
ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();
// Pass the names of files to be deleted.
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder1/picture.jpg"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/text.txt"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/music.mp3"));
deleteObjectsRequest.setKeys(keyList);

// Delete multiple files in a single request.
try {
    DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
    List<DeleteObjectsResult.DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // If not all the objects are deleted successfully, MultiObjectDeleteException is returned
    List<DeleteObjectsResult.DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<MultiObjectDeleteException.DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // Throws a CosServiceException for other errors such as parameter errors and authentication failure
    e.printStackTrace();
    throw e;
} catch (CosClientException e) { // Throws this exception for client errors, such as COS connection failure
    e.printStackTrace();
    throw e;
}
```


#### Parameter description

| Parameter | Description | Type |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | Request | DeleteObjectsRequest |

Request members:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| quiet | Indicates how to return the deletion result. Valid values: `true`, `false` (default). If set to `true`, only error messages of failed deletions are returned. If set to `false`, messages of successful and failed deletion are returned. |  boolean |
| keys | list of object paths. The version ID of each object is optional. | `List<DeleteObjectsRequest.KeyVersion>` |

`DeleteObjectsRequest.KeyVersion` members are described as follows:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| version | (Optional) Specifies the version ID of an object to delete from a versioning-enabled bucket | String |

#### Response description

- Success: No value is returned.
- Failure: an error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Restoring an archived object 

#### API description

This (POST Object restore) API is used to restore an archived object for access.

#### Method prototype

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-restore-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

// Sets the number of days before a restored temporary copy expires to 1
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucketName, key, 1);
// Sets the restoration mode to Standard. Other alternative options include Expedited and Bulk. These three modes differ in cost and speed.
CASJobParameters casJobParameters = new CASJobParameters();
casJobParameters.setTier(Tier.Standard);
restoreObjectRequest.setCASJobParameters(casJobParameters);
cosClient.restoreObject(restoreObjectRequest);
```

#### Parameter description

| Parameter | Description | Type |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | Request class | RestoreObjectRequest |

Request members:

| Parameter | Description | Type |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName | Bucket in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| expirationInDays | Specifies the number of days before a restored temporary file expires | int |
| casJobParameters | Specifies the restoration mode for calling the `setTier` function. Valid values: `Tier.Standard`, `Tier.Expedited`, and `Tier.Bulk`. To restore objects from DEEP ARCHIVE, only `Tier.Standard` and `Tier.Bulk` are supported. | CASJobParameters |

#### Response description

- Success: No value is returned.
- Failure: an error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



## Multipart operations

Operations related to multipart uploads are as follows:

- Multipart upload: initializing a multipart upload operation, uploading parts, and completing a multipart upload operation
- Resuming a multipart upload operation: querying uploaded parts, uploading remaining parts, and completing a multipart upload operation
- Deleting uploaded parts

### Querying multipart uploads

#### API description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

[//]: # (.cssg-snippet-list-multi-upload)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
listMultipartUploadsRequest.setDelimiter("/");
listMultipartUploadsRequest.setMaxUploads(100);
listMultipartUploadsRequest.setPrefix("");
listMultipartUploadsRequest.setEncodingType("url");
MultipartUploadListing multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
```


#### Parameter description

| Parameter | Description | Type |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | Request | ListMultipartUploadsRequest |

Request members:

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| keyMarker | Specifies the key after which the listing should begin | String |
| delimiter | A symbol used to limit the results of a list operation. If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed. If no prefix is specified, the listing will start from the beginning of the path. | String |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when you use a prefix to query object keys, the returned key will contain the same prefix. | String |
| uploadIdMarker | Specifies the `uploadId` after which the listing should begin | String |
| maxUploads | Sets the maximum number of multipart uploads returned. Valid values: 1-1000 | String |
| encodingType | Encoding type of returned values. Valid value: `url` | String |

#### Response description

- Success: returns `MultipartUploadListing`, including the in-progress multipart uploads.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



### Initializing a multipart upload

#### API description

This API (Initiate Multipart Upload) is used to initialize a multipart upload.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-init-multi-upload)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
InitiateMultipartUploadRequest initRequest = new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
uploadId = initResponse.getUploadId();
```


#### Parameter description

| Parameter | Description | Type |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | Request | InitiateMultipartUploadRequest |

Request members:

| Parameter | Set Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |

#### Response description

- Success: returns `InitiateMultipartUploadResult`, including the `uploadId` that identifies the multipart upload.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Uploading parts

This API (Upload Part) is used to upload parts in a multipart upload.

#### Method prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-upload-part)
```java
// Up to 10,000 parts can be uploaded, ranging from 1 MB to 5 GB in size.
// Set the size of each part to 4 MB. If there are a total of n parts, the size of part 1 through part n-1 is the same, while the last part is less than or equal to it.
partETags = new ArrayList<PartETag>();
int partNumber = 1;
int partSize = 4 * 1024 * 1024;
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
byte data[] = new byte[partSize];
ByteArrayInputStream partStream = new ByteArrayInputStream(data);
// partStream represents the input stream of the part data. The length of the input stream is the partSize.
UploadPartRequest uploadRequest = new UploadPartRequest().withBucketName(bucketName).
        withUploadId(uploadId).withKey(key).withPartNumber(partNumber).
        withInputStream(partStream).withPartSize(partSize);
UploadPartResult uploadPartResult = cosClient.uploadPart(uploadRequest);
// Get the ETag of the part.
String etag = uploadPartResult.getETag();
// Get the CRC64 value of the part.
String crc64Ecma = uploadPartResult.getCrc64Ecma();
partETags.add(new PartETag(partNumber, eTag));  // partETags records the ETags of all the uploaded parts.
// ... Upload parts with the partNumber of 2 to n
```


#### Parameter description

| Parameter | Description | Type |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | Request | UploadPartRequest |

Request members:

| Parameter | Set Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | Set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Set method | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Set method | Identifies the `uploadId` of the specified multipart upload | String |
| partNumber | Set method | Number (>= 1) that identifies the specified part | int |
| inputStream | Set method | Input stream to be uploaded in multi-parts | InputStream |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded parts. The default setting is no limit. | Int |


#### Response description

- Success: returns `UploadPartResult`, including the ETags of the uploaded parts.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


#### Response parameters

The `UploadPartResult` class is used to return request results. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | Number that identifies the specified part | String                |
| eTag        | Returns the MD5 hash of the uploaded part                   | String |
| crc64Ecma | CRC64 value computed by the server based on the part content | String |


### Copying a part

#### API description

This API (Upload Part - Copy) is used to copy an object as a part from a source path to a destination path.

#### Method prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Sample request

[//]: # (.cssg-snippet-upload-part-copy)
```java
// Bucket name in the format of BucketName-APPID
// Set destination bucket name, object name, and multipart upload ID.
String destinationBucketName = "examplebucket-1250000000";
String destinationTargetKey = "exampleobject";
int partNumber = 1;
CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setDestinationBucketName(destinationBucketName);
copyPartRequest.setDestinationKey(destinationTargetKey);
copyPartRequest.setUploadId(uploadId);
copyPartRequest.setPartNumber(partNumber);
// Set the region and name of the source bucket, object name, and offset range.
String sourceBucketRegion = "COS_REGION";
String sourceBucketName = "sourcebucket-1250000000";
String sourceKey = "sourceObject";
Long firstByte = 1L;
Long lastByte = 1048576L;
copyPartRequest.setSourceBucketRegion(new Region(sourceBucketRegion));
copyPartRequest.setSourceBucketName(sourceBucketName);
copyPartRequest.setSourceKey(sourceKey);
copyPartRequest.setFirstByte(firstByte);
copyPartRequest.setLastByte(lastByte);

CopyPartResult copyPartResult = cosClient.copyPart(copyPartRequest);
partETags = new ArrayList<PartETag>();
partETags.add(copyPartResult.getPartETag());
```


#### Parameter description

| Parameter | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

Request members:

| Parameter | Set Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Set Method | Destination bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| destinationKey | Set method | Destination object key, i.e., the [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | Set method | Identifies the `uploadId` of the specified multipart upload | String |
| partNumber | Set method | Number (>= 1) that identifies the specified part | int |
| sourceBucketRegion | Set method | Source bucket region | Region |
| sourceBucketName | Set method | Source bucket name | String |
| sourceKey | Set method | Source object key, i.e., the [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| firstByte | Set method | First byte offset of the source object | Long |
| lastByte | Set method | Last byte offset of the source object | Long |

#### Response description

- Success: returns `CopyPartResult`, including the ETag of the part.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Querying uploaded parts

#### API description

This API (List Parts) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-list-parts)
```java
// ListPart is used to list uploaded parts using the uploadId before a multipart upload is completed or aborted, and also to construct partEtags.
List<PartETag> partETags = new ArrayList<PartETag>();
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
PartListing partListing = null;
do {
    partListing = cosClient.listParts(listPartsRequest);
    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }
    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());
```


#### Parameter description

| Parameter  | Set Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | `uploadId` of the multipart upload to be queried | String |
| maxParts | Set method | Maximum number of entries returned at a time. Default value: `1000` | String |
| partNumberMarker | Set method | By default, entries are listed in UTF-8 binary order, starting from the part number after the marker. | String |
| encodingType | Set method | Encoding type of the returned value | String |

#### Response description

- Success: returns `PartListing`, including the ETag and number of each part as well as the starting marker of the next list.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Completing a multipart upload 

#### API description

This API (Complete Multipart Upload) is used to complete the multipart upload of the entire file.

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-complete-multi-upload)
```java
// Complete a multipart upload.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```


#### Parameter description

| Parameter | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | [Object Key](https://cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or set method | Identifies a specified multipart upload. | String |
| partETags  | Constructor or set method | Identifies the number and ETag returned for an uploaded part. | ` List<PartETag>` |

#### Response description

- Success: returns `CompleteMultipartUploadResult`, including the ETag of the completed object.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Aborting a multipart upload

#### API description

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)
```java
// abortMultipartUpload is used to abort an uncompleted multipart upload
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```


#### Parameter description

| Parameter | Set Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or set method | Identifies a specified multipart upload | String |

#### Response description

- Success: returns no value.
- Failure: An error occurs (such as authentication failure), throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



## Advanced APIs (Recommended)

The advanced APIs encapsulate upload and download APIs using the TransferManger class. They have a thread pool to receive upload and download requests, so that you can choose to submit tasks asynchronously.

[//]: # (.cssg-snippet-transfer-init)
```java
// We recommend setting the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, by using Tencent Cloud CVM and uploading to COS in the same region).
// We recommend using a smaller value to avoid timeout due to slow network speed if you are transferring data over a public network with poor bandwidth quality.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// Set the threshold and part size for multipart upload through the advanced upload API to 10 MB.
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10 * 1024 * 1024);
transferManagerConfiguration.setMinimumUploadPartSize(10 * 1024 * 1024);
transferManager.setConfiguration(transferManagerConfiguration);
```

Close transferManager manually after use to prevent resource leakage.

```java
// Close TransferManger.
transferManager.shutdownNow();
```

#### Parameter description

The `TransferManagerConfiguration` class is used to record the configuration of advanced APIs. Its main members are described as follows:

| Member Name | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set method | Part size of the multipart upload in bytes. Default: 5 MB| long |
| multipartUploadThreshold | Set method | If a file is greater than or equal to this value, it will be uploaded in concurrent parts. Unit: byte; default: 5 MB | long |
| multipartCopyThreshold | Set method | If a file is greater than or equal to this value, it will be replicated in concurrent parts. Unit: byte; default: 5 GB | long |
| multipartCopyPartSize | Set method | Part size in bytes for multipart replication. Default: 100 MB | long |

### Uploading an object

#### API description

This advanced version of the PUT Object API automatically determines whether to use simple or multipart upload based on the length and data type of your file, as shown below:
- Determines simple upload for stream uploads below the multipart upload threshold, OR without the Content-Length header;
- Determines multipart upload for stream uploads above the multipart upload threshold, AND without the Content-Length header;
- Determines multipart upload with concurrent threads for files with File as the data type.

>?For information on other configuration attributes, storage classes, and MD5 check, see [PUT Object](https:///intl.cloud.tencent.com/document/product/436/7749).

#### Method prototype

```java
// Upload an object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// Sample 1:
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file.
Upload upload = transferManager.upload(putObjectRequest);
// Wait for the upload to finish (call waitForCompletion if you want to wait synchronously for the upload to complete).
UploadResult uploadResult = upload.waitForUploadResult();

```


#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request members:

| Request Member | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |

>?When a file is uploaded in concurrent parts, `trafficLimit` is the limit on the upload speed of each part. In this case, you need to adjust the number of threads in your thread pool to control the upload speed.

#### Response

- Success: returns Upload. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId | Returns the version ID of an object in a versioning-enabled bucket | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |




### Downloading an object

#### API description

This API is used to download a COS object.

#### Method prototype

```java
// Download an object.
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

#### Sample request

[//]: # (.cssg-snippet-transfer-download-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localDownFile = new File(localFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// Here, set the download bandwidth limit in bit/s to 10 MB/s
getObjectRequest.setTrafficLimit(80*1024*1024);
// Download a file.
Download download = transferManager.download(getObjectRequest, localDownFile);
// Wait for the upload to finish (call waitForCompletion if you want to wait synchronously for the upload to complete).
download.waitForCompletion();
```


#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| file | File to be downloaded locally | File |

Request members:

| Request Member | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions). | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | Set method | Download range | Long[] |
| trafficLimit | Set method | Traffic limits (in bit/s) on the downloaded object. The default setting is no limit. | int |

#### Response

- Success: returns Download. You can query whether the download is complete, or wait until the download is finished.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Copying an object

#### API description

This advanced replication API automatically determines whether to use simple replication or multipart replication based on the size of an object.

#### Method prototype

```java
// Upload an object.
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Sample request

[//]: # (.cssg-snippet-transfer-copy-object)
```java
// The region of bucket to copy. Cross-region copy is supported.
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials srcCredentials = new BasicCOSCredentials(secretId, secretKey);
Region srcBucketRegion = new Region("COS_REGION");
// Enter the bucket name in the format of BucketName-APPID.
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of BucketName-APPID.
String destBucketName = "examplebucket-1250000000";
// The destination file to be copied into
String destKey = "exampleobject";
// Generate srcCOSClient to get source file information.
COSClient srcCOSClient = new COSClient(srcCredentials, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // Returns an asynchronous result "copy". You can call waitForCopyResult to wait synchronously for the replication to end. If successful, CopyResult is returned; otherwise, an exception will be thrown.
    CopyResult copyResult = copy.waitForCopyResult();
    // Get the CRC64 value of the replicated object
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```


#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request members:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default: same as the "region" value in the current `clientconfig`, meaning intra-region replication | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file. | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID` | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Response

- Success: returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

