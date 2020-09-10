## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file) to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

**Multipart upload operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart upload operations |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an existing object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specific multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload operation | Completes the multipart upload of an entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets the ACL of a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Simple Operations

### Querying an object list

#### API description

This API is used to query some or all objects in a bucket.

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. Default: null "", meaning return all objects in the bucket<br>| String |
| marker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxKeys | Constructor or set method | The maximum number of returned members (up to 1,000). <br>Default: 1,000 | Integer |

#### Response

- Success: returns ObjectListing class, including all members and nextMarker.  
- Failure: throws a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-get-bucket)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates to list objects whose key starts with this value
listObjectsRequest.setPrefix("images/");
// Set the delimiter to "/" to list objects in the current directory; and to null to list all objects
listObjectsRequest.setDelimiter("/");
// Set the maximum number of traversed objects (up to 1,000 per listobject request)
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
    // A common prefix indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary shows all listed objects
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // File path key
        String key = cosObjectSummary.getKey();
        // File Etag
        String etag = cosObjectSummary.getETag();
        // File length
        long fileSize = cosObjectSummary.getSize();
        // File storage class
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```

### Uploading an object using simple upload

#### API description

This API is used to upload an object, such as a local file or an input stream of known length, to a specified bucket. You can upload images and other small files (preferably below 20 MB) up to 5 GB (inclusive) in size. To files larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

- The file length and MD5 hash are checked by default during upload (see the sample code for disabling MD5 check).
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one.
- You can configure up to 1,000 bucket ACLs. Do not set object ACL control unless absolutely necessary. The object inherits bucket permissions by default.
- Once uploaded, you can download the file by calling the GetObject API with the same key, or by generating a [pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31536) and sending the file to another device for download (Please specify GET as the download method; see the section below for API instructions.)

#### Method prototype

```java
// Method 1. Upload a local file to COS
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the two methods above to support more fine-grained parameter control, such as content-type and content-disposition
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |Yes |
| key  | Constructor or set method |Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String ||Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
|trafficLimit | set method | Traffic limits (in bit/s) on the uploaded object. Default: none | int| No|

The ObjectMetadata class is used to record the metadata of an object. The main members are described below:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with x-cos-meta- | Map<String, String> |
| metadata | Headers other than user-defined metadata | Map<String, String> |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |


#### Response

- Success: returns PutObjectResult, including the file ETag.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The PutObjectResult class is used to return result information. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Returns the version ID of an object in a version-enabled bucket | String |
| eTag | MD5 value of the object returned by PUT Object | String |
|crc64Ecma| CRC64 value computed by the server based on the object content | String |

#### Sample request

[//]: # (.cssg-snippet-put-object-flex)
```java
// Enter the bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
// Method 1. Upload a local file
File localFile = new File(localFilePath);
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // Obtain the file etag

// Method 2. Upload an input stream (The length of the input stream must be provided in advance. Otherwise, an OOM error may occur)
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the length of the input stream to 500
objectMetadata.setContentLength(500);
// Set the content type. Default: application/octet-stream
objectMetadata.setContentType("application/pdf");
putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
etag = putObjectResult.getETag();
// Close the input stream...

// Method 3. Provide more fine-grained control. Common settings outlined below
// 1. Storage-class. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD
// 2. Content-type. For local file upload, the files are mapped based on the suffix by default. For example, a jpg file is mapped as image/jpeg
// For input stream upload, the default is application/octet-stream
// 3. Specify permissions when uploading (or call the relevant API to set an object ACL)
// 4 To disable MD5 upload verification globally, set the system environment variable. This will affect all upload verification operations, which are performed by default.
// Disable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// Enable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
localFile = new File(localFilePath);
key = "picture.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Set the storage class to STANDARD_IA
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// Setting custom attributes (such as content-type, content-disposition)
objectMetadata = new ObjectMetadata();
// Here, set the upload bandwidth limit in bit/s to 10 MB/s
putObjectRequest.setTrafficLimit(80*1024*1024);
// Set the content type. Default: application/octet-stream
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
putObjectResult = cosClient.putObject(putObjectRequest);
// Get the Etag of the object
etag = putObjectResult.getETag();
// Get the CRC64 value of the object
String crc64Ecma = putObjectResult.getCrc64Ecma();
```

### Querying object metadata

#### API description

This API is used to query whether a specified object exists in a certain bucket.

#### Method prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String  |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response

- Success: Success: returns ObjectMetadata class, including user-defined headers, Etag and other object metadata.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The ObjectMetadata class is used to record metadata on an object, and its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------- ------------------ | ------------------- |
| httpExpiresDate | The cache expiration time, which is the value of the `Expires` field in HTTP response headers | Date |
| ongoingRestore | Indicates that the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with `x-cos-meta-` | Map<String, String> |
| metadata | Headers other than user-defined ones for metadata | Map<String, String> |
| restoreExpirationTime | Expiration time of a restored ARCHIVE object copy | Date |

#### Sample request

[//]: # (.cssg-snippet-head-object)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```

### Downloading an object

#### API description

This API is used to download an object to the local file system.

#### Method prototype

```java
// Method 1. Download a file and get the input stream
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// Method 2. Download a file locally
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | The file saved locally | File |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | set method | Download range | Long[] |
|trafficLimit | set method |Traffic limits (in bit/s) on the downloaded object. Default: none. | int|


#### Response

- **Method 1 (Get the input stream of the downloaded file)**
  - Success: returns COSObject class, including the input stream and object attributes.
  - Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
- **Method 2 (Download the file locally)**
  - Success: returns objectMetadata, including the file's custom headers, content-type, and other attributes.
  - Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The COSObject class is used to return request results, and includes the main members as outlined below:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName |  Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| metadata | Object metadata  | ObjectMetadata |
| objectContent | Data stream containing COS object content  | COSObjectInputStream |

#### Sample request

[//]: # (.cssg-snippet-get-object)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1. Get the input stream of the downloaded file
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// Here, set the download bandwidth limit in bit/s to 10 MB/s
getObjectRequest.setTrafficLimit(80*1024*1024);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// Download the CRC64 value of the object
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
// Close the input stream...
cosObjectInput.close();

// Method 2. Download the file locally
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Copying an object

#### API description 

This API is used to copy an object. You can copy an object up to 5 G in size across regions, accounts, and buckets, provided that you have read permission for the source file and write permission for the destination file. To copy files larger than 5 G, use the [advanced replication API](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Parameters

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request members:

| Member Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default: same as the “region” value in the current clientConfig, which represents intra-region replication | String |
| sourceBucketName | Source bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| sourceKey | Source object key. An object key is the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: the latest version of the source file | String |
| destinationBucketName | Name of the destination bucket in the format: BucketName-APPID. It should contain letters, numbers, and dashes. | String |
| destinationKey | Destination object key. An object key is the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Sets the storage class of the destination file. Enumerated values: STANDARD and STANDARD_IA. Default: STANDARD | String |

#### Response

- Success: returns CopyObjectResult, including the Etag and other information on the new file.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-copy-object)
```java
// Intra-region and intra-account replication
// Enter the bucket name in the format: BucketName-APPID
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the bucket name in the format: BucketName-APPID
String destBucketName = "examplebucket-1250000000";
// The destination file to be copied
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

### Deleting a single object

#### API description

This API is used to delete a specified object.

#### Method prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String  |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-delete-object)
```java
// Enter the bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

### Deleting multiple objects

#### API description

The API is used to delete multiple objects.

#### Method prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
	throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | Request | DeleteObjectsRequest |

Request members:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName |  Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| quiet | Indicates how to return the deletion result. Valid values: true and false (default). If set to `true`, only error messages due to failed deletions are returned. If set to `false`, messages indicating successful and failed deletion are returned |  boolean |
| keys | list of object paths; the version ID of each object is optional | `List<DeleteObjectsRequest.KeyVersion>` |

DeleteObjectsRequest.KeyVersion members are described as follows:

| Member Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| version | (Optional) Specifies the version ID of an object to delete from a versioning-enabled bucket | String |

#### Response

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-delete-multi-object)
```java
// Enter the bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time
ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();
// Pass the names of files to be deleted
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder1/picture.jpg"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/text.txt"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/music.mp3"));
deleteObjectsRequest.setKeys(keyList);

// Delete multiple files in a single request
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

## Multipart Operations

### Querying multipart uploads

#### API description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Parameters

| Parameter Name | Description | Type |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | Request | ListMultipartUploadsRequest |

Request members:

| Member Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName |  Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| keyMarker | Specifies the key after which the listing should begin | String |
| delimiter | A symbol used to limit the results of a list operation. If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed. If no prefix is specified, the listing will start from the beginning of the path. | String |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when using a prefix to query object keys, the returned key will contain the same prefix. | String |
| uploadIdMarker | Specifies the uploadId after which the listing should begin | String |
| maxUploads | Sets the maximum number of multipart uploads returned. Valid values: 1-1,000 | String |
| encodingType | Specifies the encoding type of returned values; valid value: `url` | String |

#### Response

- Success: returns MultipartUploadListing, which lists in-progress multipart uploads.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-list-multi-upload)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
listMultipartUploadsRequest.setDelimiter("/");
listMultipartUploadsRequest.setMaxUploads(100);
listMultipartUploadsRequest.setPrefix("");
listMultipartUploadsRequest.setEncodingType("url");
MultipartUploadListing multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
```

### Multipart upload operations

Operations related to multipart upload include the following:

- Multipart upload: initializing a multipart upload operation, uploading parts, and completing a multipart upload operation
- Resuming a multipart upload operation: querying uploaded parts, uploading remaining parts, and completing a multipart upload operation
- Aborting a multipart upload operation

### Initializing a multipart upload operation

#### API description

This API is used to initialize a multipart upload.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | Request | InitiateMultipartUploadRequest |

Request members:

| Member Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method |  Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |

#### Response

- Success: returns InitiateMultipartUploadResult, including the uploadId that identifies the multipart upload.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-init-multi-upload)
```java
// Enter the bucket name in the format: BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
InitiateMultipartUploadRequest initRequest = new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
uploadId = initResponse.getUploadId();
```

### Uploading parts

This API is used to upload parts in a multipart upload.

#### Method prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | Request | UploadPartRequest |

Request members:

| Member Name | Setting Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | set method | [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | set method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | set method | Number (>= 1) that identifies the specified part | int |
| inputStream | set method | Input stream to be uploaded in multi-parts | InputStream |
|trafficLimit | set method |Traffic limits (in bit/s) on the uploaded parts; left empty by default. | int|


#### Response

- Success: returns UploadPartResult, which contains the eTags of the uploaded parts.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


#### Response parameters

The UploadPartResult class is used to return request results and includes the following members:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | Number that identifies the specified part | String                |
| eTag        | Returns the MD5 hash of the uploaded part                   | String |
| crc64Ecma | CRC64 value computed by the server based on the part content | String |

#### Sample request

[//]: # (.cssg-snippet-upload-part)
```java
// Up to 10,000 parts can be uploaded, ranging from 1 M-5 G in size.
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
// Obtain the Etag of the part.
String etag = uploadPartResult.getETag();
// Obtain the CRC64 value of the part.
String crc64Ecma = uploadPartResult.getCrc64Ecma();
partETags.add(new PartETag(partNumber, eTag));  // partETags records the Etags of all the uploaded parts
// ... Upload parts with the partNumber of 2 to n
```

### Copying a part

#### API description

This API is used to copy an object as a part from a source path to a destination path.

#### Method prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Parameters

| Parameter Name | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

Request members:

| Member Name | Setting Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | set method | Destination bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| destinationKey | set method | Destination object key, i.e., the [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | set method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | set method | Number (>= 1) that identifies the specified part | int |
| sourceBucketRegion | set method | Source bucket region | Region |
| sourceBucketName | set method | Source bucket name | String |
| sourceKey | set method | Source object key, i.e., the [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| firstByte | set method | First byte offset of the source object | Long |
| lastByte | set method | Last byte offset of the source object | Long |

#### Response

- Success: returns CopyPartResult, including the ETag of the part.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-upload-part-copy)
```java
// Bucket name. Format: BucketName-APPID
// Set destination bucket name, object name, and multipart upload ID
String destinationBucketName = "examplebucket-1250000000";
String destinationTargetKey = "exampleobject";
int partNumber = 1;
CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setDestinationBucketName(destinationBucketName);
copyPartRequest.setDestinationKey(destinationTargetKey);
copyPartRequest.setUploadId(uploadId);
copyPartRequest.setPartNumber(partNumber);
// Set the region and name of the source bucket, object name, and offset range
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

### Querying uploaded parts

#### API description

This API is used to query the uploaded parts of a specific multipart upload operation.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Setting Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | UploadId of the multipart upload to be queried | String |
| MaxParts | set method | Maximum number of entries returned at a time. Default value: 1,000 | String |
| partNumberMarker | set method | By default, entries are listed in UTF-8 binary order starting with the part number after the marker | String |
| encodingType | set method | Specifies the encoding type of the returned value | String |

#### Response

- Success: returns PartListing, including the ETag and number of each part as well as the starting marker of the next list.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

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

### Completing a multipart upload operation 

#### API description

This API is used to complete a multipart upload operation.

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | 
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The [ObjectKey](https://cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or set method | Identifies a specified multipart upload | String |
| partETags  | Constructor or set method | Identifies the number and ETag returned for an uploaded part | ` List<PartETag>` |

#### Response

- Success: returns CompleteMultipartUploadResult, including the Etag of the completed object.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-complete-multi-upload)
```java
// Completing a multipart upload operation
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```

### Aborting a multipart upload operation

#### API description

This API is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Parameters

| Member Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or set method | Identifies a specified multipart upload | String |

#### Response

- Success: no value is returned.
-Failure: An error occurs (such as authentication failure), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)
```java
// abortMultipartUpload is used to abort an uncompleted multipart upload
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```

## Other Operations

### Restoring an archived object 

#### API description

This API is used to retrieve an archived object for access.

#### Method prototype

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | Request class | RestoreObjectRequest |

Request members:

| Member Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| expirationInDays | Specifies the number of days before a restored temporary file expires | int |
| casJobParameters | Specifies the restoration mode for calling the setTier function. Valid values: Tier.Standard, Tier.Expedited, and Tier.Bulk | CASJobParameters |

#### Response

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-restore-object)
```java
// Enter the bucket name in the format: BucketName-APPID.
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

### Setting an object ACL

#### API description

This API is used to set an ACL for a specified object in a bucket.

> !You can configure up to 1,000 bucket ACLs. Do not set object ACL control unless absolutely necessary. The object inherits bucket permissions by default.

There are two types of ACL policies: predefined ACLs (CannedAccessControlList) and custom ACLs (AccessControlList). If both of them are set, the custom ACL prevails over the predefined ACL.

#### Method prototype

```java
// Method 1 (custom policy)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// Method 2 (predefined policy)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// Method 3 (Encapsulate the two methods above, allowing you to set both policies. In this case, the custom policy prevails.)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

#### Parameters

- Parameters for **Method 3** are described below because they encapsulate the parameters used in methods 1 and 2.

| Parameter Name | Description | Type |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | Request class | setObjectAclRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName | Constructor or set method | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| acl | Constructor or set method | Custom ACL policy | AccessControlList |
| cannedAcl | Constructor or set method | Predefined ACL policy, such as public read, public read and write, private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains information on all granted permissions | Array |
| owner | Owner of the object | Owner class |

Grant class members:

| Member Name | Description | Type |
| ---------- | -------------------------------------------- | ---------- |
| grantee | Grantee information | Grantee |
| permission | Granted permission (such as read, write, read/write) | Permission |

Owner class members:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Identifies the owner | String |
| displayname | Owner's name (same as “id”) | String |

CannedAccessControlList represents a preset policy for everyone. It is an enumeration type with the following enumerated values.

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read and write (only the owner can read and write) |
| PublicRead | Public read and private write (the owner can read and write, other users can read) |
| PublicReadWrite | Public read and write (everyone can read and write) |

#### Response

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-put-object-acl)
```java
// The grantee information must be formatted. The format for root account and sub-account differs as follows:
// In this example, both root_uin and sub_uin below are valid QQ numbers
// The root account “qcs::cam::uin/<root_uin>:uin/<root_uin>” indicates that permission is granted to the root account “root_uin” itself
// For example, “qcs::cam::uin/2779643970:uin/2779643970”
// The sub-account “qcs::cam::uin/<root_uin>:uin/<sub_uin>” indicates that permission is granted by the root account “root_uin” to the sub account “sub_uin”
// For example, qcs::cam::uin/2779643970:uin/73001122 
// Bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Set custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// Set the owner, which can only be a root account
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);

// Grant root account 73410000 read and write permissions
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
acl.grantPermission(uinGrantee1, Permission.FullControl);
cosClient.setObjectAcl(bucketName, key, acl);

// Set predefined ACL
// Set private read and write (The object inherits bucket permissions by default)
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.Private);
// Set public read and private write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicRead);
// Set public read and write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicReadWrite);
```

### Getting an object ACL

#### API description

This API is used to get the ACL of an object.

#### Method prototype

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### Parameters

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response

- Success: returns the ACL of the object.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-get-object-acl)
```java
// Bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList accessControlList = cosClient.getObjectAcl(bucketName, key);
// Change the ACL policy type to predefined ACL. Value values: Private, PublicRead, Default
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```

## Advanced APIs (recommended)

The advanced APIs encapsulate upload and download APIs using the TransferManger class. They have a thread pool to receive upload and download requests, so that you can choose to submit tasks asynchronously.

[//]: # (.cssg-snippet-transfer-init)
```java
// We recommend setting the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, by using Tencent Cloud CVM and uploading to COS in the same region).
// We recommend using a smaller value to avoid timeout due to slow network speed if you are transferring data over a public network with poor bandwidth quality.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// Set the threshold and part size for multipart upload through the advanced upload API to 10 MB
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10 * 1024 * 1024);
transferManagerConfiguration.setMinimumUploadPartSize(10 * 1024 * 1024);
transferManager.setConfiguration(transferManagerConfiguration);
```

Close transferManager manually after use to prevent resource leakage.

```java
// Close TransferManger
transferManager.shutdownNow();
```

#### Parameters

The TransferManagerConfiguration class is used to record the configuration of advanced APIs. Its main members are described below:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | set method | Part size of the multipart upload in bytes. Default: 5 MB| long |
| multipartUploadThreshold | set method | If a file is greater than or equal to this value, it will be uploaded in concurrent parts. Unit: byte; default: 5 MB | long |
| multipartCopyThreshold | set method | If a file is greater than or equal to this value, it will be replicated in concurrent parts. Unit: byte; default: 5 GB | long |
| multipartCopyPartSize | set method | Part size in bytes for multipart replication. Default: 100 MB | long |

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

#### Parameters

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method |Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method |Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
|trafficLimit | set method |Traffic limits (in bit/s) on the uploaded object. Default: none | int| No|

>?When a file is uploaded in concurrent parts, `trafficLimit` is the limit on the upload speed of each part. In this case, you need to adjust the number of threads in your thread pool to control the upload speed.

#### Response

- Success: returns Upload class. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key |Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| requestId  | Request Id                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId | Returns the version ID of an object in a version-enabled bucket | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |


#### Sample request

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// Sample 1:
// Enter the bucket name in the format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file
Upload upload = transferManager.upload(putObjectRequest);
// Wait for the upload to finish (call waitForCompletion if you want to wait synchronously for the upload to complete)
UploadResult uploadResult = upload.waitForUploadResult();

// Sample 2. Use checkpoint restart for files larger than the maximum part size
// Step 1. Get PersistableUpload
bucketName = "examplebucket-1250000000";
key = "exmpleobject";
localFile = new File("exmpleobject");
putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file
PersistableUpload persistableUpload = null;
// Set the speed in bit/s for simple upload or part upload to 8 MB/s in the SDK
// Note: concurrent parts are uploaded for data that exceeds the part threshold and has File as the data type. To control the part upload speed, adjust the size of your thread pool.
putObjectRequest.setTrafficLimit(64*1024*1024);
upload = transferManager.upload(putObjectRequest);
// Wait until the "Initiate multiple upload" operation is completed, and get `persistableUpload` (including uploadId)
while(persistableUpload == null) {
    persistableUpload = upload.getResumeableMultipartUploadId();
    Thread.sleep(100);
}
// Save persistableUpload

// Step 2. If the multipart upload of a large file is interrupted due to network problems, use PersistableUpload to resume the upload only for the remaining parts
Upload newUpload = transferManager.resumeUpload(persistableUpload);
 // Wait for the upload to finish (call waitForCompletion if you want to wait synchronously for the upload to complete)
uploadResult = newUpload.waitForUploadResult();
// The CRC64 value computed by the server for the object
String crc64Ecma = uploadResult.getCrc64Ecma();
```


### Downloading an object

#### API description

This API is used to download a COS object.

#### Method prototype

```java
// Download an object
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

#### Parameters

| Parameter Name | Description | Type |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| file | File to be downloaded locally | File |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method |Bucket name in the format: BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key  | Constructor or set method |Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | set method | Download range | Long[] |
|trafficLimit | set method |Traffic limits (in bit/s) on the downloaded object. Default: none | int|

#### Response

- Success: returns Download. You can query whether the download is complete, or wait until the download is finished.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

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
// Download a file
Download download = transferManager.download(getObjectRequest, localDownFile);
// Wait for the upload to finish (call waitForCompletion if you want to wait synchronously for the upload to complete)
download.waitForCompletion();
```

### Copying object

#### API description

This advanced replication API automatically determines whether to use simple replication or multipart replication based on the size of an object.

#### Method prototype

```java
// Upload an object
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Parameters

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request members:

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default: same as the “region” value in the current clientconfig, which represents intra-region replication | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID` | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| storageClass | Sets the file storage class. Enumerated values: STANDARD and STANDARD_IA. Default: STANDARD | String |

#### Response

- Success: returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
- Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException thrown. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-transfer-copy-object)
```java
// The region of bucket to copy. Cross-region copy is supported.
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials srcCredentials = new BasicCOSCredentials(secretId, secretKey);
Region srcBucketRegion = new Region("COS_REGION");
// Enter the bucket name in the format: BucketName-APPID
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the destination bucket name in the format: BucketName-APPID
String destBucketName = "examplebucket-1250000000";
// The destination file to be copied
String destKey = "exampleobject";
// Generate srcCOSClient to get source file information
COSClient srcCOSClient = new COSClient(srcCredentials, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // Returns an asynchronous result “copy”. You can call waitForCopyResult to wait synchronously for the replication to end. If successful, CopyResult is returned; otherwise, an exception will be thrown.
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

## Client-Side Encryption

#### Description

The Java SDK allows client-side encryption that encrypts files before upload and decrypts them at the time of download. There are two types of client-side encryption: AES (symmetric) and RSA (asymmetric).
These two types are for the encryption of generated random keys. File data, however, is always encrypted symmetrically using AES256.
Client-side encryption is suitable for users who store sensitive data. As it may affect the upload speed, the SDK uses serial method for multipart upload.

### Preparing for client-side encryption

The client uses AES256 internally to encrypt data. By default, earlier versions of JDK6-JDK8 do not support 256-bit encryption. If run, an exception will be reported: `java.security.InvalidKeyException: Illegal key size or default parameters`. We then need to supplement Oracle's JCE unrestricted permissions file and deploy it in JRE environment. Please download the corresponding files according to the JDK version used, unzip and save them in the jre/lib/security directory under JAVA_HOME.

1. [JDK6 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
2. [JDK7 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
3. [JDK8 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

### Encryption for upload

1. Before each upload, COS generates a random symmetric key which is encrypted through the customer-provided symmetric or asymmetric key. The encryption result is then base64-encoded and stored in object metadata.
2. During the upload, the file is encrypted in memory using AES256 algorithm.

### Decryption for download

1. Get the necessary encryption information from the metadata of the file, base64-decode it, and then decrypt it using the customer managed key (CMK) to get the encryption key at upload.
2. Use the resulting key to decrypt the downloaded input stream using AES256.

#### Sample request

Sample 1. Use symmetric AES256 encryption to generate a random key each time. For the complete sample code, see [Complete Example of Client Symmetric Key Encryption](https://github.com/tencentyun/cos-java-sdk-v5 /blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

[//]: # (.cssg-snippet-put-object-cse-c-aes)
```java
// Initialize user authentication information (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the COS region. For regions and their abbreviations, see https://intl.cloud.tencent.com/zh/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// Generate a symmetric key to save as file metadata
KeyGenerator symKeyGenerator = KeyGenerator.getInstance("AES");
symKeyGenerator.init(256);
SecretKey symKey = symKeyGenerator.generateKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// Use AES/GCM mode and stores the encrypted information in the file metadata
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generate an encryption client (EncryptionClient), more specifically, COSEncryptionClient. It is a subclass of COSClient, and allows for the use of all APIs supported by COSClient.
// COSEncryptionClient overwrites the COSClient for upload and download logic, and additionally performs encryption. The other operations, however, use the same logic as that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Upload the file
// Here is an example of PUT Object. For the advanced upload API, all you need to do is pass in the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```

Sample 2. Use asymmetric RSA encryption to generate a random key each time. For the complete sample code, see [Complete Example of Client Symmetric Key Encryption](https://github.com/tencentyun/cos-java-sdk-v5 /blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

[//]: # (.cssg-snippet-put-object-cse-c-rsa)
```java
// Initialize user authentication information (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// COS region. For regions and their abbreviations, see https://intl.cloud.tencent.com/zh/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// Generate an asymmetric key
KeyPairGenerator keyGenerator = KeyPairGenerator.getInstance("RSA");
SecureRandom srand = new SecureRandom();
keyGenerator.initialize(1024, srand);
KeyPair asymKeyPair = keyGenerator.generateKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// Use AES/GCM mode and stores the encrypted information in the file metadata
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generate an encryption client (EncryptionClient), more specifically COSEncryptionClient. It is a subclass of COSClient, and allows for the use of all APIs supported by COSClient.
// COSEncryptionClient overwrites the COSClient for upload and download logic, and additionally performs encryption. The other operations, however, use the same logic as that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Upload the file
// Here is an example of putObject. For advanced API upload, use the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```
