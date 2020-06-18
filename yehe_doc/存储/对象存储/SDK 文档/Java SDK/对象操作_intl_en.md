## Overview

This document provides an overview of APIs and SDK sample codes related to simple, multipart, and other operations on objects.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries all or a subnet of objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploads an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object in the bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a bucket with a single request|

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

Request member description:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Limiting the returned result objects, prefixed with prefix. By default, there is no limit, and the default value for all Bucket members<br>is empty: "" | String |
| marker | Constructor or set method | Marking the starting position of the list, which can be set to empty for the first time, and subsequent requests need to be set to the nextMarker in the previous  returned listObjects value | String |
| delimiter | Constructor or set method | Delimiter. It indicates that the path that starts with "prefix" and ends with delimiter for the first time will be returned. | String |
| maxKeys | Constructor or set method | The maximum number of returned members (up to 1,000). <br>Default: 1,000 | Integer |

#### Response

- Successful: Returns ObjectListing class, including all members and nextMarker.  
- Failure: Throws CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-get-bucket"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set bucket name
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates the keys of the listed objects started with the prefix
listObjectsRequest.setPrefix("images/");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
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
    // The common prefix indicates the path truncated by delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary indicates a list of all listed objects
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

#### Feature

This API (Put Object) is used to upload objects to the specified bucket. Uploading a local file or an input stream of known length to COS. It is suitable for uploading small image files (below 20MB), a maximum of 5GB (inclusive) is supported, please use [Multipart Upload](#multipart-operations) or [Advanced API](#advanced-apis-(recommended) to upload if more than 5GB.

- The file length and MD5 are checked by default during upload (see the sample code for disabling MD5 check).
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one.
The number of access policies is up to 1000. Do not set object ACL control if it is not required. The object inherits the bucket permissions by default.
- Once uploaded, you can download the file by calling the GetObject API with the same key, or by generating a [pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31536), and sending the file to another device for download.

#### Method prototype

```java
// Method 1: Upload a local file to COS
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2: Upload an input stream to COS
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3: Encapsulate the two methods above to support more fine-grained parameter control, such as content-type and content-disposition
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| file | Constructor or set method | Local File | File | No |
| input | Constructor or set method | Input Stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
|trafficLimit | set method |Traffic limits (in bit/s) on the uploaded object. Default: none | int| No|

The ObjectMetadata class is used to record the meta information of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache timeout, which is the value of the Expires field in the HTTP response header | Date |
| ongoingRestore | Restoring this object from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with x-cos-meta- | Map <String, String> |
| metadata | Headers other than user-defined metadata | Map<String, String> |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |


#### Response

- Successful: PutObjectResult, including the file ETag and other information.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The PutObjectResult class is used to return result information, and main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Enabling a versioned bucket and version ID of the object is returned | String |
| eTag | MD5 value of the object returned by simple upload API | String |
|crc64Ecma| The CRC64 value computed by the server based on the object | String |

#### Request samples

[//]: # ".cssg-snippet-put-object-flex"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
// Method 1: Upload a local file
File localFile = new File(localFilePath);
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // Obtain the file etag

// Method 2: Upload an input stream (The length of a input stream must be known in advance. Otherwise, it may cause oom)
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the length of an input stream to 500
objectMetadata.setContentLength(500);
// Set Content type. Default: application/octet-stream
objectMetadata.setContentType("application/pdf");
putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
etag = putObjectResult.getETag();
// Close the input stream...

// Method 3: Provide more fine-grained control. Common settings are as follows
// 1 Storage-class. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD
// 2. Content-type. For local file upload, the files are mapped based on the suffix by default. For example, the jpg file is mapped as image/jpeg
// For input stream upload, the default is application/octet-stream
// 3. Set permissions when uploading (or by calling API set object acl)
// 4 To disable MD5 upload verification globally, set the system environment variable. This will affect all upload verification. Verification is performed by default.
// Disable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// Enable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
localFile = new File(localFilePath);
key = "picture.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Set the storage class to STANDARD_IA
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// Set custom attributes (such as content-type, content-disposition)
ObjectMetadata objectMetadata = new ObjectMetadata();
// Here, set the upload bandwidth limit in bit/s to 10 MB/s
putObjectRequest.setTrafficLimit(80*1024*1024);
// Set Content type. Default: application/octet-stream
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
// Get Etag of the object
String etag = putObjectResult.getETag();
// Get CRC64 value of the object
String crc64Ecma = putObjectResult.getCrc64Ecma();
```

### Querying object metadata

#### Feature

This API (HEAD Object) is used to query whether the specified object exists in the bucket.

#### Method prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response

- Successful: No value is returned.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-head-object"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```

### Downloading an object

#### Feature

This API (Get Object) is used to download an object locally.

#### Method prototype

```java
// Method 1: Download the file and get the input stream
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// Method 2: Download the file locally.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | Locally saved file | File |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | Set Method | Download Range | Long[] |
|trafficLimit | Set Method |Traffic limits (in bit/s) on the downloaded object. Default: none. | int|


#### Response

- **Method 1 (Get the input stream of the downloaded file)**
  - Successful: Returns COSObject type, including the input stream and file attributes.
  - Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
- **Method 2 (Download the file locally)**
  - Successful: Returns the file attribute objectMetadata, including the file's custom header, content-type and other attributes.
  - Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The COSObject class is used to return request results, and includes main members as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| metadata | Object metadata  | ObjectMetadata |
| objectContent | Data stream that contains COS object content  | COSObjectInputStream |

#### Request samples

[//]: # ".cssg-snippet-get-object"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1: Get the input stream of the downloaded file
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// Here, set the download bandwidth limit in bit/s to 10 MB/s
getObjectRequest.setTrafficLimit(80*1024*1024);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// Download CRC64 value of the object
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();

// Method 2 (Download the file locally)
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Setting object replication

#### Feature 

This API [PUT Object - Copy] is used to replicate an object. You can replicate an object up to 5 G in size across regions, accounts, and buckets, provided that you have Read access to the source file and Write access to the destination file. To copy files larger than 5 G, use the [advanced APIs](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request members:

| Member Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source Bucket. Default: same with the region of the current clientconfig, which represents an intra-region copy | String |
| sourceBucketName | Source bucket name, naming format is BucketName-APPID. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file | String |
| destinationBucketName | Name of the destination bucket. The bucket should be named in a format of BucketName-APPID, where the name should be comprised of letters, numbers, and dashes. | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Sets file storage class. Enumerated values: STANDARD and STANDARD_IA. Default: STANDARD | String |

#### Response

- Successful: Returns CopyObjectResult, including Etag and other information of the new file.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-copy-object"
```java
// Replicate a file in the same account and region
// Enter the bucket name in the format of BucketName-APPID.
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the bucket name in the format of BucketName-APPID.
String destBucketName = "examplebucket-1250000000";
// The destination file to be copied into
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// Cross-account and cross-region replication (The read permission to source file and the write permission to destination file are required)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
// Get CRC64 value of the object
String crc64Ecma = copyObjectResult.getCrc64Ecma();
```

### Deleting a single object

#### Feature

This API (Delete Object) is used to delete the specified object.

#### Method prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response

- Successful: No value is returned.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-delete-object"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

### Deleting multiple objects

#### Feature

The API（DELETE Multiple Objects）is used to delete multiple objects.

#### Method prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
	throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | Request | DeleteObjectsRequest |

Request member description:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| quiet | Indicating the method by which the result is returned for the deletion. Available values: true and false. Defaults to false. If it is set to true, only error message for failed deletion is returned. If it is set to false, messages indicating successful and failed deletion are returned. | boolean |
| keys | list of object paths, version number of the object is optional | `List<DeleteObjectsRequest.KeyVersion>` |

DeleteObjectsRequest.KeyVersion members are described as follows:

| Member Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| version | When enabling bucket versioning, specify the version number of the deleted object, optional | String |

#### Response

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-delete-multi-object"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time
ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();
// Enter the names of files to be deleted
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder1/picture.jpg"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/text.txt"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/music.mp3"));
deleteObjectsRequest.setKeys(keyList);

// Delete files in batches
try {
    DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
    List<DeleteObjectsResult.DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // If not all the objects are deleted successfully, MultiObjectDeleteException is returned
    List<DeleteObjectsResult.DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<MultiObjectDeleteException.DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // For other errors such as parameter error, identity authentication will not throw CosServiceException
    e.printStackTrace();
    throw e;
} catch (CosClientException e) { // For client error, such as COS connection fails
    e.printStackTrace();
    throw e;
}
```

## Multipart Operations

### Querying multipart upload

#### Feature

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Parameter description

| Parameter Name | Description | Type |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | Request | ListMultipartUploadsRequest |

Request members:

| Member Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| keyMarker | The key value where the entry list starts | String |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path | String |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | String |
| uploadIdMarker | The `UploadId` value where the entry list starts | String |
| maxUploads | Sets the maximum number of multipart returned. Valid values: 1-1000 | String |
| encodingType | Specifies the encoding type of the returned values; valid value: `url` | String |

#### Response

- Successful: Returns MultipartUploadListing, which contains information that multipart upload is in progress.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-list-multi-upload"
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

### Uploading object via multipart upload

Operations related to multipart uploads include the following:

- Multipart upload of objects: initializing multipart upload, uploading parts, and completing multipart upload
- Resuming multipart upload: querying parts uploaded, uploading parts, and completing multipart upload
- Aborting multipart upload

### Initializing multipart upload

#### Feature

This API (Initiate Multipart Upload) is used to initialize a multipart upload task.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | Request | InitiateMultipartUploadRequest |

Request members:

| Member Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |

#### Response

- Successful: Returns InitiateMultipartUploadResult type, including the upload ID required for subsequent multipart upload.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-init-multi-upload"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
InitiateMultipartUploadRequest initRequest = new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
uploadId = initResponse.getUploadId();
```

### Uploading parts

This API (Upload Part) is used to upload a part.

#### Method prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | Request | UploadPartRequest |

Request members:

| Member Name | Setting Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | Set Method | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Set Method | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Set Method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | Set Method | Identifies the number of the specified multipart, must be>=1 | int |
| inputStream | Set Method | Input stream to be uploaded in multi-parts | InputStream |
|trafficLimit | Set Method |Traffic limits (in bit/s) on uploaded parts. Not configured by default. | int|


#### Response

- Successful: Returns UploadPartResult, which contains the eTag information of the uploaded parts.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


#### Response parameters

The UploadPartResult class is used to return request results, and includes members as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | An identifier of the specified part | String                |
| eTag        | Returns MD5 hash of the part                   | String |
|crc64Ecma| CRC64 value computed by the server based on the part | String |

#### Request samples

[//]: # ".cssg-snippet-upload-part"
```java
// Upload up to 10,000 parts with a size ranging from 1 M-5 G.
// Set the size of each part to 4 MB. If there are a total of n parts, the size of part 1 to part n-1 is the same, and the last part is less than or equal to the size of previous parts.
partETags = new ArrayList<PartETag>();
int partNumber = 1;
int partSize = 4 * 1024 * 1024;
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
byte data[] = new byte[partSize];
ByteArrayInputStream partStream = new ByteArrayInputStream(data);
// partStream represents the input stream of the part's data. The length of input stream is partSize.
UploadPartRequest uploadRequest = new UploadPartRequest().withBucketName(bucketName).
        withUploadId(uploadId).withKey(key).withPartNumber(partNumber).
        withInputStream(partStream).withPartSize(partSize);
UploadPartResult uploadPartResult = cosClient.uploadPart(uploadRequest);
// Obtain Etag of the part.
String etag = uploadPartResult.getETag();
// Obtain CRC64 value of the part.
String crc64Ecma = uploadPartResult.getCrc64Ecma();
partETags.add(new PartETag(partNumber, eTag));  // partETags records the Etags of all uploaded parts
// ... Upload parts with the partNumber of 2 to n
```

### Copying parts

#### Feature

This API (Upload Part - Copy) is used to copy the parts of an object from a source path to a destination path.

#### Method prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Parameter description

| Parameter Name | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

Request members:

| Member Name | Setting Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Set Method | Destination bucket name, Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| destinationKey | Set Method | Destination object key, i.e., the [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | Set Method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | Set Method | Identifies the number of the specified multipart, must be>=1 | int |
| sourceBucketRegion | Set Method | Source bucket region | Region |
| sourceBucketName | Set Method | Source bucket name | String |
| sourceKey | Set Method | Source object key, i.e., the [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| firstByte | Set Method | First byte offset of the source object | Long |
| lastByte | Set Method | Last byte offset of the source object | Long |

#### Response

- Successful: CopyPartResult is returned, including the ETag information of the part.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-upload-part-copy"
```java
// Bucket name. Format: BucketName-APPID
// Set destination bucket name, object name and multipart upload ID
String destinationBucketName = "examplebucket-1250000000";
String destinationTargetKey = "exampleobject";
int partNumber = 1;
CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setDestinationBucketName(destinationBucketName);
copyPartRequest.setDestinationKey(destinationTargetKey);
copyPartRequest.setUploadId(uploadId);
copyPartRequest.setPartNumber(partNumber);
// Set the region and name of the source bucket, object name and offset range
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

#### Feature

This API (List Parts) is used to query the uploaded parts in a specific multipart upload.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object Name | String |
| uploadId | Constructor or set method | UploadId of the multipart upload to be queried | String |
| maxParts | Maximum number of entries returned at a time. Default value: 1,000 | String |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String |
| - Encoding-type | Specifies the encoding type of the returned value | String |

#### Response

- Successful: Returns PartListing, including the ETag and No. of each part as well as the starting marker of the next list.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-list-parts"
```java
// ListPart is used to obtain the information of the uploaded part based on uploadId before the multipart upload is completed or aborted. It can be used to construct partEtags.
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

### Completing multipart upload 

#### Feature

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or set method | Identifies the specified uploadId for multipart upload | String |
| partETags  | Constructor or set method | Identifies the number of the parts and the eTag returned by the upload | ` List<PartETag>` |

#### Response

- Successful: Returns CompleteMultipartUploadResult, including the Etag of the entire file.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-complete-multi-upload"
```java
// Complete multipart upload
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```

### Aborting multipart upload

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Parameter description

| Member Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) of an object stored in COS | String |
| uploadId | Constructor or set method | Identifies the specified uploadId for multipart upload | string |

#### Response

- Successful: No value is returned.
-Failure: An error occurs (such as authentication failure), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-abort-multi-upload"
```java
// abortMultipartUpload is used to abort an uncompleted multipart upload
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```

## Other operations

### Restoring an archived object 

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method prototype

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | Request class | RestoreObjectRequest |

Request members:

| Member Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| expirationInDays | Specifies the number of days before a restored  temporary file expires | int |
| casJobParameters | Describes the restore mode configuration. You can call the setTier API to set one of the three restore modes: Tier.Standard, Tier.Expedited. Tier.Bulk. | CASJobParameters |

#### Response

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-restore-object"
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

// Set the number of days before a restored temporary copy expires to 1
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucketName, key, 1);
// Set the restore mode to Standard. Other available modes include Expedited and Bulk. The three restore modes have different cost and speed.
CASJobParameters casJobParameters = new CASJobParameters();
casJobParameters.setTier(Tier.Standard);
restoreObjectRequest.setCASJobParameters(casJobParameters);
cosClient.restoreObject(restoreObjectRequest);
```

### Setting object ACL

#### Feature

This API is used to set the ACL for the specified object in a bucket.

>The number of access policies is up to 1000. Do not set object ACL control if it is not required. The object inherits the bucket permissions by default.

ACL includes a predefined permission policy (CannedAccessControlList) or a custom permission control (AccessControlList). If both of them are set, the predefined policy will be ignored and the custom policy prevails. For more information on permissions, please see the permission section.

#### Method prototype

```java
// Method 1 (Set custom policy)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// Method 2 (Set predefined policy)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// Method 3 (Encapsulation of the two methods above, including setting of these two policies. If both of them are set, the custom policy prevails.)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

#### Parameter description

- **Method 3** Its parameters are illustrated because they contain those for Method 1 and 2.

| Parameter Name | Description | Type |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | Class for requesting permission configuration | setObjectAclRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| acl | Constructor or set method | Custom permission policy | AccessControlList |
| cannedAcl | Constructor or set method | Predefined policies, such as public read, public read and write, private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains information of all users to be authorized | Array |
| owner | The owner of the Object or Owner | Owner class |

Grant class members:

| Member Name | Description | Type |
| ---------- | -------------------------------------------- | ---------- |
| grantee | Grantee identity information | Grantee |
| permission | Authorized permission information (such as readable, writable, readable & writable) | Permission |

Owner class members:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Identity information of an owner | String |
| displayname | Owner's name (same as ID) | String |

CannedAccessControlList represents a preset policy for everyone. It is an enumeration type with the following enumerated values.

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read and write (only the owner can read and write) |
| PublicRead | Public read and private write (the owner can read and write, while other users can read) |
| PublicReadWrite | Public read and write (everyone can read and write) |

#### Response

- Successful: No value is returned.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-put-object-acl"
```java
// The identity information in permissions must be formatted. The format for the root account and sub-accounts is as follows:
// Both root_uin and sub_uin below must be valid QQ numbers
// The root account qcs::cam::uin/<root_uin>:uin/<root_uin> indicates that the root_uin is granted to the root account (that is, the first and second uin are the same)
// For example, qcs::cam::uin/2779643970:uin/2779643970
// The sub-account qcs::cam::uin/<root_uin>:uin/<sub_uin> indicates that the sub_uin is granted to the root_uin.
// For example, qcs::cam::uin/2779643970:uin/2779643970 
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Set a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// Set the owner, which can only be a root account.
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);

// Grant the root account 73410000 read and write permissions
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
acl.grantPermission(uinGrantee1, Permission.FullControl);
cosClient.setObjectAcl(bucketName, key, acl);

// Set a predefined ACL
// Set private read and write (The object inherits bucket permissions by default)
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.Private);
// Set public read and private write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicRead);
// Set public read and write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicReadWrite);
```

### Getting object ACL

#### Feature

This API (Get Object ACL) is used to get the ACL of an object.

#### Method prototype

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response

- Successful: Returns the ACL to which the Object resides.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-get-object-acl"
```java
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList accessControlList = cosclient.getObjectAcl(bucketName, key);
// Get file permission in the form of preset ACL. Valid values: Private, PublicRead, Default
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```

## Advanced APIs (recommended)

The advanced API encapsulates upload and download APIs using the TransferManger class. It has a thread pool inside to accept users' upload and download requests, so users can choose to submit tasks asynchronously.

[//]: # ".cssg-snippet-transfer-init"
```java
// The size of the thread pool. If client and COS network are sufficient (for example, use Tencent Cloud CVM and upload COS in the same region), we recommended you set it to 16 or 32 to fully utilize network resources.
// If public network is used for transmission and network bandwidth quality is poor, we recommended you lower this value to avoid timeout caused by slow network speed.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// Input a threadpool. If there is no thread pool, a single-thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// Set the threshold and size of parts for multipart upload through advanced API to 10 MB
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10 * 1024 * 1024);
transferManagerConfiguration.setMinimumUploadPartSize(10 * 1024 * 1024);
transferManager.setConfiguration(transferManagerConfiguration);
```

Closing transferManager manually after use to prevent resource leakage.

```java
// Close TransferManger
transferManager.shutdownNow();
```

#### Parameter description

The TransferManagerConfiguration class is used to record the configuration of advanced APIs. Its main members are described as follows:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set Method | Part size in bytes for multipart upload. Default: 5 MB| long |
| multipartUploadThreshold | Set Method | If a file is greater than or equal to this value, it will be uploaded in concurrent parts. Unit: byte; default: 5 MB | long |
| multipartCopyThreshold | Set Method | If a file is greater than or equal to this value, it will be copied in concurrent parts. Unit: Byte; default: 5 GB | long |
| multipartCopyPartSize | Set Method | Part size in bytes for multipart replication. Default: 100 MB | long |

### Uploading an object

#### Feature

This API (Upload) automatically determines simple or multipart upload depending on the length and data type of your file, as shown below:
- Determines simple upload for stream uploads below the multipart upload threshold, OR without Content-Length header;
- Determines multipart upload for stream uploads above the multipart upload threshold, AND without Content-Length header;
- Determines multipart upload with concurrent threads for files with File as data type.

>For information on other configuration attributes, storage classes, and MD5 check, see [PUT Object API](https:///intl.cloud.tencent.com/document/product/436/7749).

#### Method prototype

```java
// Upload an object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local File | File |
| input | Constructor or set method | Input Stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
|trafficLimit | set method |Traffic limits (in bit/s) on the uploaded object. Default: none | int| No|

>When concurrent parts are uploaded, `trafficLimit` is the limits on the upload speed of each part. In this case, you need to adjust the number of threads in the thread pool to control the upload speed.

#### Response

- Successful: Returns Upload. You can query whether the upload is completed, or wait until the upload finishes synchronously.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



#### Response parameters

The UploadResult class records uploaded objects requested by calling the waitForUploadResult() method from the Upload API. The main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key |The object key is the unique identifier of the object in the bucket.<br/>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| requestId  | Request Id                                                       | String |
| dateStr    | The current server time                                             | String |
| versionId | Returned version ID of an object in a versioning-enabled bucket | String |
| crc64Ecma  | The CRC64 computed by the server based on the object                           | String |


#### Request samples

[//]: # ".cssg-snippet-transfer-upload-object"
```java
// Sample 1:
// Enter the bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file
Upload upload = transferManager.upload(putObjectRequest);
// Wait for the transfer to finish (call waitForCompletion if you want to wait for the upload to finish synchronously)
UploadResult uploadResult = upload.waitForUploadResult();

// Sample 2. Use checkpoint restart for files larger than the maximum part size
// Step 1: Get PersistableUpload
String bucketName = "examplebucket-1250000000";
String key = "exmpleobject";
File localFile = new File("exmpleobject");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file
PersistableUpload persistableUpload = null;
// Set the speed in bit/s of simple upload or part upload to 8 MB/s in the SDK
// Note: concurrent parts are uploaded for data that exceeds the part threshold and has File as data type. To control the part upload speed, adjust the size of your thread pool.
putObjectRequest.setTrafficLimit(64*1024*1024);
Upload upload = transferManager.upload(putObjectRequest);
// Wait until the "Initiate multiple upload" operation is completed, and get `persistableUpload` (including uploadId)
while(persistableUpload == null) {
    persistableUpload = upload.getResumeableMultipartUploadId();
    Thread.sleep(100);
}
// Save persistableUpload

// Step 2. If the multipart upload of a large file is interrupted due to network problems, use PersistableUpload to resume the upload only for the remaining parts
Upload newUpload = transferManager.resumeUpload(persistableUpload);
 // Wait for the transfer to finish (call waitForCompletion if you want to wait for the upload to finish synchronously)
UploadResult uploadResult = newUpload.waitForUploadResult();
// The CRC64 value computed by the server for the object
String crc64Ecma = uploadResult.getCrc64Ecma();
```


### Downloading an object

#### Feature

This API (GET Object) is used to download a COS object.

#### Method prototype

```java
// Download an object
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

#### Parameter description

| Parameter Name | Description | Type |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| file | File to be downloaded locally | File |

Request members:

| Request Member | Setting Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | Set Method | Download Range | Long[] |
|trafficLimit | Set Method |Traffic limits (in bit/s) on the downloaded object. Default: none. | int|

#### Response

- Successful: Returns Download. You can query whether the download is completed, or wait until the download finishes synchronously.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-transfer-download-object"
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
// Wait for the transfer to finish (call waitForCompletion if you want to wait for the upload to finish synchronously)
download.waitForCompletion();
```

### Replicating objects

#### Feature

This API (Copy) supports automatic selection of simple copy or multipart copy based on the size of the object, and the user does not need to worry about the size of the copied file.

#### Method prototype

```java
// Upload an object
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request members:

| Member Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source Bucket. Default: same with the region of the current clientconfig, which represents an intra-region copy | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID` | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Sets file storage class. Enumerated values: STANDARD and STANDARD_IA. Default: STANDARD | String |

#### Response

- Successful: Returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
- Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Request samples

[//]: # ".cssg-snippet-transfer-copy-object"
```java
// The region of bucket to copy. Cross-region copy is supported.
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials srcCredentials = new BasicCOSCredentials(secretId, secretKey);
Region srcBucketRegion = new Region("COS_REGION");
// Enter the bucket name in the format of BucketName-APPID
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of BucketName-APPID
String destBucketName = "examplebucket-1250000000";
// The destination file to be copied into
String destKey = "exampleobject";
// Generate srcCOSClient to get source file information
COSClient srcCOSClient = new COSClient(srcCredentials, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // Return an asynchronous result copy. You can synchronously call waitForCopyResult to wait for copy to end. If successful, CopyResult is returned; If failed, an exception will be thrown.
    CopyResult copyResult = copy.waitForCopyResult();
    // Get CRC64 value of the replicated object
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

## Client Encryption

#### Feature

Java SDK supports client encryption, encrypting files before uploading and decrypting them when downloading. Client encryption supports symmetric AES and asymmetric RSA encryption.
The symmetry and asymmetry here are only used to encrypt the generated random keys. AES256 is always used to encrypt file data symmetrically.
Client encryption is suitable for users who store sensitive data. client encryption may sacrifice certain upload speed, and the SDK may use serial method for multipart upload.

### Preparing for client encryption

Client encryption uses AES256 internally to encrypt data. By default, earlier versions of JDK6-JDK8 do not support 256-bit encryption. If run, an exception will be reported: `java.security.InvalidKeyException: Illegal key size or default parameters`. We then need to supplement Oracle's JCE unrestricted permissions file and deploy it in JRE environment. Please download the corresponding files according to the JDK version used, unzip and save them in the jre/lib/security directory under JAVA_HOME.

1. [JDK6 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
2. [JDK7 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
3. [JDK8 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

### Uploading encryption process

1. Before uploading a file object, we randomly generate a symmetric encryption key. The random key is encrypted by the symmetric or asymmetric key provided by the user, and the encrypted result is encoded with base64 and stored in the metadata of the object.
2. When the file object is uploaded, AES256 algorithm is used to encrypt the file object in memory.

### Decryption for download

1. Obtain the necessary encryption information from the metadata of the file, and decrypt the information decoded with Base64 using the user key to obtain the key of the encrypted data.
2. Use the key to decrypt the downloaded input stream using AES256 to obtain the decrypted file input stream.

#### Request samples

Sample 1: Use symmetric AES256 encryption to generate a random key each time. For the complete sample code, see [Complete Example of Client Symmetric Key Encryption](https://github.com/tencentyun/cos-java-sdk-v5 /blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

[//]: # ".cssg-snippet-put-object-cse-c-aes"
```java
// Initialize user authentication information (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set COS region. For regions and their abbreviations, see https://www..com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// Generating a symmetric key and you can save it in a file
KeyGenerator symKeyGenerator = KeyGenerator.getInstance("AES");
symKeyGenerator.init(256);
SecretKey symKey = symKeyGenerator.generateKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// Use the AES/GCM mode and store the encrypted information in file metadata
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generating encryption client (EncryptionClient). The COSEncryptionClient is a subclass of COSClient, and all APIs supported by COSClient are also available.
// EncryptionClient overwrites the COSClient upload and download logic. It will perform the encryption operation internally. The other operations execution logic is consistent with that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Uploading the file
// Here is an example of putObject. For advanced API upload, use the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```

Sample 2: Use asymmetric RSA encryption to generate a random key each time. For the complete sample code, see [Complete Example of Client Symmetric Key Encryption](https://github.com/tencentyun/cos-java-sdk-v5 /blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

[//]: # ".cssg-snippet-put-object-cse-c-rsa"
```java
// Initialize user authentication information (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// COS region. For regions and their abbreviations, see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// Generating asymmetric keys
KeyPairGenerator keyGenerator = KeyPairGenerator.getInstance("RSA");
SecureRandom srand = new SecureRandom();
keyGenerator.initialize(1024, srand);
KeyPair asymKeyPair = keyGenerator.generateKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// Use the AES/GCM mode and store the encrypted information in file metadata
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generating encryption client (EncryptionClient). The COSEncryptionClient is a subclass of COSClient, and all APIs supported by COSClient are also available.
// EncryptionClient overwrites the COSClient upload and download logic. It will perform the encryption operation internally. The other operations execution logic is consistent with that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Uploading the file
// Here is an example of putObject. For advanced API upload, use the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```
