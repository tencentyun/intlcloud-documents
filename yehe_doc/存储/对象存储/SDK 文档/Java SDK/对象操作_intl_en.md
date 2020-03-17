## Introduction

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries a part of or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | Gets object metadata | Gets the meta information of an object |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | Gets an object | Downloads an object (file) locally |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Sets object replication | Copies a file to the destination path |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deletes a single object | Deletes the specified object in the bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

**Multipart Upload Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | Initializes multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying the object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method Prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request for obtaining a file list | ListObjectsRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Limiting the returned result objects, prefixed with prefix. By default, there is no limit, and the default value for all Bucket members<br>is empty: "" | String |
| marker | Constructor or set method | Marking the starting position of the list, which can be set to empty for the first time, and subsequent requests need to be set to the nextMarker in the previous  returned listObjects value | String |
| delimiter | Constructor or set method | Delimiter. It indicates that the path that starts with "prefix" and ends with delimiter for the first time will be returned. | String |
| maxKeys | Constructor or set method | The maximum number of returned members (less than 1,000). Default: 1,000 | Integer |

#### Returned Result

- Successful: Returns ObjectListing type, including all members and nextMarker.  
-Failure: Throws CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-get-bucket)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Setting bucket name
listObjectsRequest.setBucketName(bucket);
// The prefix indicates the key of the listed objects started with the prefix
listObjectsRequest.setPrefix("");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
listObjectsRequest.setDelimiter("/");
// Setting the maximum number of traversed objects (up to 1000 for one listobject)
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {
    try{
        ObjectListing objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosXmlServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosXmlClientException e) {
        e.printStackTrace();
        return;
    }
    // The common prefix indicates the path truncated by delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary indicates a list of all listed objects
    for (COSObjectSummary cosObjectSummary : objectListing.getObjectSummaries()) {
    for (COSObjectSummary cosObjectSummary : objectListing.getObjectSummaries()) {
        // File path key
        String key = cosObjectSummary.getKey();
        // File etag
        String etag = cosObjectSummary.getETag();
        // File length
        long fileSize = cosObjectSummary.getSize();
        // File storage type
        String storageClass = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```

### Uploading an object using simple upload

#### Feature

This API (Put Object) is used to upload objects to the specified bucket. Uploading a local file or an input stream of known length to COS. It is suitable for uploading small image files (below 20MB), a maximum of 5GB (inclusive) is supported, please use [Multipart Upload](# .E5.88.86.E5.9D.97.E6.93.8D.E4.BD.) 9C) or [Advanced API](# .E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D. 90.EF.BC.89) to upload if more than 5GB.

- The file length and MD5 are checked by default during upload (see the sample code for disabling MD5 check).
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one.
The number of access policies is up to 1000. Do not set object ACL control if it is not required. The object inherits the bucket permissions by default.
- After upload, you can use the same key to call the GetObject API to download the file locally, or you can generate a pre-signed URL (please specify the download method as GET, see specific API description below), and send it to other paths for download.

#### Method Prototype

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

#### Parameter Description

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| key | Constructor or set method | The key is the unique identifier of the object in the bucket. <br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| file | Constructor or set method | Local File | File | No |
| input | Constructor or set method | Input Stream | InputStream | No |
| metadata | Constructor or set method | Meta information of a file | ObjectMetadata |

The ObjectMetadata class is used to record the meta information of an object. The main members are described as follows:

| Parameter Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache timeout, which is the value of the Expires field in the HTTP response header | Date |
| ongoingRestore | Restoring this object from archive storage type | Boolean |
| userMetadata | User-defined meta information prefixed with x-cos-meta- | Map <String, String> |
| metadata | Headers other than user-defined meta information | Map<String, String> |

#### Returned Result

- Successful: PutObjectResult, including the file ETag and other information.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

### Response Parameters

The PutObjectResult class is used to return result information, and main members are described as follows:

| Parameter Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Enabling a versioned bucket and version ID of the object is returned | String |
| eTag | MD5 value of the object returned by simple upload API | String |

#### Request Samples

[//]: # (.cssg-snippet-put-object-flex)
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
// Setting the length of an input stream to 500
objectMetadata.setContentLength(500);
// Setting Content type. Default is application/octet-stream
objectMetadata.setContentType("application/pdf");
putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
etag = putObjectResult.getETag();
// Closing the input stream...

// Method 3: Provide more fine-grained control. Common settings are as follows
// 1 Storage-class. Enumerated values：Standard, Standard_IA, Archive. Default value: Standard
// 2. Content-type. For local file upload, the files are mapped based on the suffix by default. For example, the jpg file is mapped as image/jpeg
// For input stream upload, the default is application/octet-stream
// 3. Set permissions when uploading (or by calling API set object acl)
// 4 To disable MD5 upload verification globally, set the system environment variable. This will affect all upload verification. Verification is performed by default.
// Disable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// Enable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
localFile = new File(localFilePath);
Key='picture.jpg'
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Setting the storage type to low frequency
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// Setting custom attributes (such as content-type, content-disposition)
ObjectMetadata objectMetadata = new ObjectMetadata();
// Setting Content type. Default is application/octet-stream
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
String etag = putObjectResult.getETag();  // Obtain the file etag
```

### Querying object metadata

#### Feature

This API is used to query whether the specified object exists in the bucket.

#### Method Prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Returned Result

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-head-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```

### Downloading an object

#### Feature

This API (Get Object) is used to download an object locally.

#### Method Prototype

```java
// Method 1: Download the file and get the input stream
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// Method 2: Download the file locally.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | Locally saved file | File |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The key is the unique identifier of the object in the bucket. <br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| range | Set Method | Download range | Long[] |

#### Returned Result

- **Method 1 (Get the input stream of the downloaded file)**
  - Successful: Returns COSObject type, including the input stream and file attributes.
  -Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).
- **Method 1 (Download the file locally)**
  - Successful: Returns the file attribute objectMetadata, including the file's custom header, content-type and other attributes.
  -Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-get-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1: Get the input stream of the downloaded file
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// Method 2 (Download the file locally)
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Setting object replication

#### Feature 

This API (Put Object Copy) is used to copy one object to another. It supports cross-region, cross-account, and cross-bucket copying. You need to have read permission to the source file and write permission to the destination file. File copy supports a maximum of 5G, please use advanced API to copy files greater than 5G.

#### Method Prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Parameter Description

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request member description:

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source Bucket. Default: same with the region of the current clientconfig, which represents an intra-region copy | String |
| sourceBucketName | Source bucket name, naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Source Key. The key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Version ID of the source file with multiple versions. Default: The latest version of the source file | String |
| destinationBucketName | Name of destination Bucket. The bucket should be named in a format of {name}-{appid}, where name should be comprised of letters, numbers, and dashes. | String |
| key | Destination key. The key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| StorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string |

#### Returned Result

- Successful: Returns CopyObjectResult, including Etag and other information of the new file.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-copy-object)
```java
// Copying the same account in the same region
// Enter the bucket name in the format of BucketName-APPID.
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
// The destination file to be copied
String key = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// Cross-account and cross-region copy (The read permission to source file and the write permission to destination file are required)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
```

### Deleting a single object

#### Feature

This API (Delete Object) is used to delete the specified object.

#### Method Prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Returned Result

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-delete-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

### Deleting multiple objects

#### Feature

The API（DELETE Multiple Objects）is used to delete multiple specified objects.

#### Method Prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
	throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | Request | DeleteObjectsRequest |

Request member description:

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Quiet | Indicating the method by which the result is returned for the deletion. Available values: true and false. Defaults to false. If it is set to true, only error message for failed deletion is returned. If it is set to false, messages indicating successful and failed deletion are returned. | bool | No |
| keys | list of object paths, version number of the object is optional | `List<DeleteObjectsRequest.KeyVersion>` |

DeleteObjectsRequest.KeyVersion members are described as follows:

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| version | When enabling bucket versioning, specify the version number of the deleted object, optional | String |

#### Returned Result

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-delete-multi-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// Setting the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time
ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();
// Entering the names of files to be deleted
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder1/picture.jpg"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/text.txt"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/music.mp3"));
deleteObjectsRequest.setKeys(keyList);

// Deleting files in batches
try{
    DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
    List<DeleteObjectsResult.DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // If part of deletion succeeds and other fails, MultiObjectDeleteException is returned
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

#### Method Prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Parameter Description

| Parameter Name | Description | Type |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | Request | ListMultipartUploadsRequest |

Request member description:

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| - KeyMarker | The key value where the entry list starts | String |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path | NSString * |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | NSString |
| - UploadIdMarker | The `UploadId` value where the entry list starts | String |
| maxUploads | Sets the maximum number of multipart returned. Valid values: 1-1000 | int |
| EncodingType | Specifies the encoding type of the returned values; valid value: `url` | String | No |

#### Returned Result

- Successful: Returns MultipartUploadListing, which contains information that multipart upload is in progress.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

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

### Uploading object via multipart upload

This includes the following operations:

- Multipart upload objects: Initializing multipart upload, uploading parts, and completing all multipart uploads
- Resuming the multipart upload: Querying the parts uploaded, uploading parts, and completing all multipart uploads
### Terminating multipart upload

### Initializing multipart upload

#### Feature

This API (Initiate Multipart Upload) is used to initialize multipart upload job.

#### Method Prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | Request | InitiateMultipartUploadRequest |

Request member description:

| Parameter Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Stored on COS object’s [ Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Returned Result

- Successful: Returns InitiateMultipartUploadResult type, including the upload ID required for subsequent multipart upload.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-init-multi-upload)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
InitiateMultipartUploadRequest initRequest = new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
uploadId = initResponse.getUploadId();
```

### Uploading Parts

This API (Upload Part) is used to upload a part.

#### Method Prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | Request | UploadPartRequest |

Request member description:

| Parameter Name | Setting Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | Set Method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Set Method | Stored on COS object’s [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Set Method | Identifies the uploadId of the specified multipart upload | string |
| partNumber | Set Method | Identifies the number of the specified part, which should be ≥ 1. | int |
| inputStream | Set Method | Input stream to be uploaded in multipart | InputStream |

#### Returned Result

- Successful: Returns UploadPartResult, which contains the eTag information of the uploaded parts.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-upload-part)
```java
// Uploading up to 10,000 parts, supported size is 1M-5G.
// Setting the size of each part to 4 MB. If there are a total of n parts, the size of part 1 to part n-1 is the same, and the last part is less than or equal to the size of previous parts.
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
String eTag = uploadPartResult.getETag();  // Obtain the Etag of the part
partETags.add(new PartETag(partNumber, eTag));  // partETags records Etag information of all uploaded parts
// ... Uploading parts with the partNumber of 2 to n
```

### Copying Parts

#### Feature

This API (Upload Part - Copy) is used to copy the parts of an object from a source path to a destination path.

#### Method Prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Parameter Description

| Parameter Name | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

Request member description:

| Parameter Name | Setting Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Set Method | Destination bucket name, Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| destinationKey | Set Method | Destination object name, stored on COS object’s [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Set Method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | Set Method | Identifies the number of the specified multipart, must be>=1 | int |
| sourceBucketRegion | Set Method | Source bucket region | Region |
| sourceBucketName | Set Method | Source bucket name | String |
| sourceKey | Set Method | Source object name, stored on COS object’s [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| firstByte | Set Method | First byte offset of the source object | Long |
| lastByte | Set Method | Last byte offset of the source object | Long |

#### Returned Result

- Successful: CopyPartResult is returned, including the ETag information of the part.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-upload-part-copy)
```java
// Bucket name. Format: BucketName-APPID
// Setting destination bucket name, object name and multipart upload ID
String bucketName = "examplebucket-1250000000";
String destinationTargetKey = "exampleobject";
int partNumber = 1;
CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setDestinationBucketName(destinationBucketName);
copyPartRequest.setDestinationKey(destinationTargetKey);
copyPartRequest.setUploadId(uploadId);
copyPartRequest.setPartNumber(partNumber);
// Setting the region and name of the source bucket, object name and offset range
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

This API (List Parts) is used to query the uploaded parts in a specific multipart upload process.

#### Method Prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object Name | String |
| uploadId | Constructor or set method | UploadId of the multipart upload to be queried | String |
| MaxParts | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String |
| - Encoding-type | Specifies the encoding type of the returned value | String |

#### Returned Result

- Successful: Returns PartListing, including the ETag and No. of each part as well as the starting marker of the next list.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-list-parts)
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

#### Method Prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Stored on COS object’s [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Constructor or set method | Identifies the specified uploadId for multipart upload | string |
| partETags  | Constructor or set method | Identifies the number of the parts and the eTag returned by the upload | ` List<PartETag>` |

#### Returned Result

- Successful: Returns CompleteMultipartUploadResult, including the Etag of the entire file.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-complete-multi-upload)
```java
// Completing multipart upload
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```

### Terminating multipart upload

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Stored on COS object’s [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Constructor or set method | Identifies the specified uploadId for multipart upload | string |

#### Returned Result

- Successful: No value is returned.
-Failure: An error occurs (such as authentication failure), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

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

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method Prototype

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | Request Type | RestoreObjectRequest |

Request member description:

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| expirationInDays | Expired days of restored temporary files | int |
| casJobParameters | Describes the configuration information of restored type, call the setTier API to set to one of the three restore types: Tier.Standard、Tier.Expedited、Tier.Bulk | CASJobParameters |

#### Returned Result

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-restore-object)
```java
/* Enter the bucket name in the format of BucketName-APPID.  */
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

// Setting the expiration days of temporary copies obtained by configuring restore to 1 day
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucketName, key, 1);
// Setting the restore mode to Standard. Other available modes include Expedited and Bulk. The three restore modes have different cost and speed.
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

#### Method Prototype

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

#### Parameter Description

- **方法3** 参数同时包含1和2，因此以方法3为例进行介绍。

| Parameter Name | Description | Type |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | Class for requesting permission configuration | setObjectAclRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The key is the unique identifier of the object in the bucket. <br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| acl | Constructor or set method | Custom permission policy | AccessControlList |
| cannedAcl | Constructor or set method | Predefined policies, such as public read, public read and write, private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains information of all users to be authorized | Array |
| owner | The owner of the Object or Owner | Owner class |

Grant type members description：

| Member Name | Description | Type |
| ---------- | -------------------------------------------- | ---------- |
| grantee | Grantee identity information | Grantee |
| permission | Authorized permission information (such as readable, writable, readable & writable) | Permission |

Owner type member description:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Identity information of an owner | String |
| displayname | Owner's name (same as id) | String |

CannedAccessControlList represents a preset policy for everyone. It is an enumeration type with the following enumerated values.

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read and write (only owner can read and write) |
| PublicRead | Public read and private write (owner can read and write, and other users can read) |
| PublicReadWrite | Public read and write (everyone can read and write) |

#### Returned Result

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-put-object-acl)
```java
// The identity information in permissions has format requirements. The format for the main account and sub-account is as follows:
// Both root_uin and sub_uin below must be valid QQ numbers
// The root account qcs::cam::uin/<root_uin>:uin/<root_uin> indicates that the root_uin is granted to the root account (that is, the first and second uin are the same)
// For example, qcs::cam::uin/2779643970:uin/2779643970
// The sub-account qcs::cam::uin/<root_uin>:uin/<sub_uin> indicates that the sub_uin is granted to the root_uin.
// For example, qcs::cam::uin/2779643970:uin/2779643970 
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Setting a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// Setting the owner information. Owner can only be a root account.
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);

// Granting the main account 73410000 read and write permissions
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
acl.grantPermission(uinGrantee1, Permission.FullControl);
cosClient.setObjectAcl(bucketName, key, acl);

// Setting a predefined ACL
// Setting private read and write (Object integrates permissions of Bucket by default)
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.Private);
// Setting public read and private write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicRead);
// Setting public read and write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicReadWrite);
```

### Getting the object ACL

#### Feature

This API (Get Object ACL) is used to get the ACL of an object.

#### Method Prototype

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | The key is the unique identifier of the object in the bucket. For example, in the object's access `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Returned Result

- Successful: Returns the ACL to which the Object resides.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-get-object-acl)
```java
Bucket. Format: BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList acl = cosClient.getObjectAcl(bucketName, key);
```

## Advanced APIs (Recommended)

The advanced API encapsulates upload and download APIs using the TransferManger type. It has a thread pool inside to accept users' upload and download requests, so users can choose to submit tasks asynchronously.

[//]: # (.cssg-snippet-transfer-init)
```java
// The size of the thread pool. If client and COS network are sufficient (for example, use Tencent Cloud CVM and upload COS in the same region), we recommended you set it to 16 or 32 to fully utilize network resources.
// If public network is used for transmission and network bandwidth quality is poor, we recommended you lower this value to avoid timeout caused by slow network speed.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// Inputting a threadpool. If there is no thread pool, a single-thread pool will be generated in TransferManager by default.
transferManager = new TransferManager(cosClient, threadPool);
// Setting the threshold and size of parts for multipart upload through advanced API to 10MB
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10 * 1024 * 1024);
transferManagerConfiguration.setMinimumUploadPartSize(10 * 1024 * 1024);
transferManager.setConfiguration(transferManagerConfiguration);
```

Closing transferManager manually after use to prevent resource leakage.

```java
// Closing TransferManger
transferManager.shutdownNow();
```

#### Parameter Description

The TransferManagerConfiguration class is used to record the configuration information of advanced APIs. Its main members are described as follows:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set Method | Part size for multipart upload, unit in byte, default value is 5MB| long |
| multipartUploadThreshold | Set Method | If the value is greater than or equal to this value, file parts are uploaded concurrently, unit in byte, default value is 5MB | long |
| multipartCopyThreshold | Set Method | If the value is greater than or equal to this value, file parts are copied concurrently, unit in byte, default value is 5M | long |
| multipartCopyPartSize | Set Method | Part size for multipart copy, unit in byte, default value is 100MB | long |

### Uploading an object

#### Feature

The upload API automatically selects simple upload or multipart upload based on the size of users' files, making it easy for users to use. Besides, users do not need to care about each step of the multipart upload.

Tips for other configuration attributes, storage category, MD5 verification, etc., see [PUT Object API](https://cloud.tencent.com/document/product/436/7749).

#### Method Prototype

```java
// Uploading the object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The key is the unique identifier of the object in the bucket. <br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| file | Constructor or set method | Local File | File |
| input | Constructor or set method | Input Stream | InputStream |
| metadata | Constructor or set method | Meta information of a file | ObjectMetadata |

#### Return values

- Successful: Returns Upload. You can query whether the upload is completed, or wait until the upload finishes synchronously.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-transfer-upload-object)
```java
// Sample 1：
/* Enter the bucket name in the format of BucketName-APPID.  */
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Uploading local file
Upload upload = transferManager.upload(putObjectRequest);
// Waiting for the transfer to finish (call waitForCompletion if you want to wait for the upload to finish synchronously)
UploadResult uploadResult = upload.waitForUploadResult();
```

### Downloading an object

#### Feature

This APP is used to download COS object locally.

#### Method Prototype

```java
// Downloading the object
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| file | File to be downloaded locally | File |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | The key is the unique identifier of the object in the bucket. <br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| range | Set Method | Download Range | Long[] |

#### Return values

- Successful: Returns Download. You can query whether the download is completed, or wait until the download finishes synchronously.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-transfer-download-object)
```java
/* Enter the bucket name in the format of BucketName-APPID.  */
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localDownFile = new File(localFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
# Downloading a file
Download download = transferManager.download(getObjectRequest, localDownFile);
// Waiting for the transfer to finish (call waitForCompletion if you want to wait for the upload to finish synchronously)
download.waitForCompletion();
```

- Replicating objects

#### Feature

This API supports automatic selection of simple copy or multipart copy based on the size of the object, and the user does not need to worry about the size of the copied file.

#### Method Prototype

```java
// Uploading the object
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Parameter Description

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request member description:

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source Bucket. Default: same with the region of the current clientconfig, which represents an intra-region copy | String |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| key | Source key. The key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Version ID of the source file with multiple versions. Default: The latest version of the source file | String |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| key | Destination key. The key is the unique identifier of the object in the bucket. For example, in the object's access domain `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| StorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string |

#### Return values

- Successful: Returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-transfer-copy-object)
```java
// The region of bucket to copy. Cross-region copy is supported.
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
Region srcBucketRegion = new Region("COS_REGION");
/* Enter the bucket name in the format of BucketName-APPID.  */
String srcBucketName = "sourcebucket-1250000000";
// The source file to be copied
String srcKey = "sourceObject";
/* Enter the bucket name in the format of BucketName-APPID.  */
String bucketName = "examplebucket-1250000000";
// The destination file to be copied
String key = "exampleobject";
// Generating srcCOSClient to get source file information
COSClient srcCOSClient = new COSClient(srcCredentials, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
// Returning an asynchronous result copy. You can synchronously call waitForCopyResult to wait for copy to end. If successful, CopyResult is returned; If failed, an exception will be thrown.
CopyResult copyResult = copy.waitForCopyResult();
srcCOSClient.shutdown();
```

## Client Encryption

#### Feature

Java sdk supports client encryption, encrypting files before uploading and decrypting them when downloading. Client encryption supports symmetric AES and asymmetric RSA encryption.
The symmetry and asymmetry here are only used to encrypt the generated random keys. AES256 is always used to encrypt file data symmetrically.
Client encryption is suitable for users who store sensitive data. client encryption may sacrifice certain upload speed, and the SDK may use serial method for multipart upload.

### Preparing for client encryption

Client encryption uses AES256 internally to encrypt data. By default, earlier versions of JDK6-JDK8 do not support 256-bit encryption. If run, an exception will be reported: `java.security.InvalidKeyException: Illegal key size or default parameters`. We then need to supplement Oracle's JCE unrestricted permissions file and deploy it in JRE environment. Please download the corresponding files according to the JDK version used, unzip and save them in the jre/lib/security directory under JAVA_HOME.

1. [JDK6 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
2. [JDK7 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
3. [JDK8 JCE supplement package](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

### Uploading encryption process

1. Before uploading a file object, we randomly generate a symmetric encryption key. The random key is encrypted by the symmetric or asymmetric key provided by the user, and the encrypted result is encoded with base64 and stored in the meta information of the object.
2. When the file object is uploaded, AES256 algorithm is used to encrypt the file object in memory.

### Downloading decryption process

1. Obtain the necessary encryption information in the meta information of the file, and decrypt the information decoded with base64 using the user key to obtain the key of the encrypted data
2. Use the key to decrypt the downloaded input stream using AES256 to obtain the decrypted file input stream.

#### Request Samples

Sample 1: Use symmetric AES256 encryption to generate a random key each time. For the complete sample code, see [Complete Example of Client Symmetric Key Encryption](https://github.com/tencentyun/cos-java-sdk-v5 /blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

[//]: # (.cssg-snippet-put-object-cse-c-aes)
```java
// Initialize user authentication information (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Setting the bucket region. For the abbreviation of COS region, refer to https: //www..com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(region);

// Generating a symmetric key and you can save it in a file
KeyGenerator symKeyGenerator = KeyGenerator.getInstance("AES");
symKeyGenerator.init(256);
SecretKey symKey = symKeyGenerator.generateKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// Use the AES/GCM mode and store the encrypted information in the meta information of the file.
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

[//]: # (.cssg-snippet-put-object-cse-c-rsa)
```java
// Initialize user authentication information (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// COS region. For regions and their abbreviations, see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(region);

// Generating asymmetric keys
KeyPairGenerator keyGenerator = KeyPairGenerator.getInstance("RSA");
SecureRandom srand = new SecureRandom();
keyGenerator.initialize(1024, srand);
KeyPair asymKeyPair = keyGenerator.generateKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// Use the AES/GCM mode and store the encrypted information in the meta information of the file.
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
