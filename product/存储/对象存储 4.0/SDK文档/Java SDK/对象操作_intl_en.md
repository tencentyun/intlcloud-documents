## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
[HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries object metadata |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file/object) to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object (file/object) in a bucket |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Method Prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | Request to get the file list | ListObjectsRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| prefix | Constructor or set method | Limits that the returned object must be prefixed with the "prefix". No limitation is imposed by default, i.e., returning all members of the bucket. <br>Default value: "" | String |
| marker | Constructor or set method | Marks the starting position of the list, which can be set to null initially. In subsequent requests, it needs to be set to the nextMarker in the return value of the last listObjects operation | String |
| delimiter | Constructor or set method | Delimiter, limiting that the returned path must start with prefix and end in the first appearance of delimiter | String |
| maxKeys | Constructor or set method | Maximum number of members to be returned (up to 1,000) <br>Default value: 1,000 | Integer |

#### Return Result Descriptions

- Success: The ObjectListing type is returned, containing all members and nextMarker.  
- Failure: A CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";

// Request to get the members in the bucket
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
listObjectsRequest.setBucketName(bucketName);
// Set the prefix of the list, indicating that the listed file keys must start with this prefix
listObjectsRequest.setPrefix("");
// Set the delimiter to /, indicating to get direct members excluding recursive sub-members under the directory
listObjectsRequest.setDelimiter("/");
// Set the marker (which is obtained from the last list or is empty if listObjects is called for the first time)
listObjectsRequest.setMarker("");
// Set the maximum number of entries returned in the list (if this is not set, the default value of 1,000 will be used; up to 1,000 keys can be listed in one list)
listObjectsRequest.setMaxKeys(100);

ObjectListing objectListing = cosClient.listObjects(listObjectsRequest);
// Get the marker of the next list
String nextMarker = objectListing.getNextMarker();
// Determine whether the list is finished, and if yes, isTruncated is false; otherwise, true
boolean isTruncated = objectListing.isTruncated();
List<COSObjectSummary> objectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : objectSummaries) {
    // File path
    String key = cosObjectSummary.getKey();
    // Get the file length
    long fileSize = cosObjectSummary.getSize();
    // Get the file ETag
    String eTag = cosObjectSummary.getETag();
    // Get the last modified time
    Date lastModified = cosObjectSummary.getLastModified();
    // Get the file storage class
    String storageClass = cosObjectSummary.getStorageClass();
}
```

### Simply Uploading an Object

#### Feature Description

This API (Put Object) is used to upload an object to the specified bucket in order to upload a local file or input stream with a known length to COS. This is applicable to uploading small image files (below 20 MB). The maximum supported file size is 5 GB. For files over 5 GB, please use multipart upload or advanced API.

- The file length and MD5 are checked by default during the upload (for more information on how to disable MD5 check, see the sample code).
- If an object with the same key already exists in COS, it will be overwritten during the upload.
- Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, do not set it during the upload, so that the object will inherit the permissions of the bucket.
- After the file is uploaded, you can call the `GetObject` API using the same `key` to download the file to the local file system or generate a pre-signed link. (For a download operation, specify the method as `GET`. For detailed API descriptions, see below.) This link can be shared for download.

#### Method Prototype

```java
// Method 1. Upload a local file to COS
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the first two methods, which supports more fine-grained control of parameters such as content-type and content-disposition
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | File metadata | ObjectMetadata |

The ObjectMetadata class is used to record the metadata of an object. Its main members are as described below:

| Member Name | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------  |
| httpExpiresDate | Cache expiration time, which is the value of the Expires field in the HTTP response header | Date |
| ongoingRestore | The object is being restored from the archive storage class | Boolean |
| userMetadata | User-defined metadata prefixed with x-cos-meta- | Map<String, String> |
| metadata | Headers other than user-defined metadata | Map<String, String> |

#### Return Result Descriptions

- Success: PutObjectResult is returned, which contains the file's information such as ETag.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
// Method 1. Upload a local file
File localFile = new File("exampleobject");
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // Get etag of the file

// Method 2. Upload an input stream (the length of the input stream should be specified in advance; otherwise, OOM may occur)
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the input stream length to 500
objectMetadata.setContentLength(500);  
// Set the Content type which is application/octet-stream by default
objectMetadata.setContentType("application/pdf");
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
String etag = putObjectResult.getETag();
// Close the input stream...

// Method 3 provides more fine-grained controls. Common settings are as follows:
// 1. Storage class; enumerated values: Standard, Standard_IA, Archive; default value: Standard
// 2. content-type. For local file uploads, mapping based on the local file extensions will be performed by default, for example, .jpg files will be mapped to image/jpeg
// For streaming uploads, the default value is application/octet-stream
// 3. Specify the permission while uploading (which can also be set by calling the set object acl API)
// 4. To globally disable upload MD5 check, set the system environment variable, which will affect all upload checks. Checks are performed by default
// Disable MD5 check: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// Enable check again: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
File localFile = new File("picture.jpg");
String key = "picture.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
// Set the storage class to Standard_IA
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// Set custom attributes (such as content-type and content-disposition)
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the Content type which is application/octet-stream by default
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
String etag = putObjectResult.getETag();  // Get etag of the file
```

### Querying Object Metadata

#### Feature Description

This API is used to query whether the specified object exists in a bucket.

#### Method Prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```

### Downloading an Object

#### Feature Description

This API (Get Object) is used to download an object to the local file system.

#### Method Prototype

```java
// Method 1. Download a file and gets the input stream
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// Method 2. Download a file to the local file system
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | Locally saved file | File |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | set method | Download range | Long[] |

#### Return Result Descriptions

- **Method 1 (getting download input stream)**
  - Success: The COSObject class is returned, which contains the input stream and object attributes.
  - Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
- **Method 2 (downloading the file locally)**
  - Success: The ObjectMetadata attribute of the file is returned, which contains the file's custom headers and attributes such as content-type.
  - Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1. Get a download input stream
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// Method 2. Download a file to the local file system
File downFile = new File("output/exampleobject");
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Setting Object Replication

#### Feature Description 

This API (Put Object - Copy) is used to copy an object to another object. Cross-region cross-account cross-bucket copy is supported. You need to have read permission to the source file and write permission to the destination file. Maximum file size supported for copy is 5 GB. For files over 5 GB, please use the advanced copy API.

#### Method Prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request member description:

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Source bucket region. Default value: Same as the current clientConfig region, indicating copy in the same region | String |
| sourceBucketName | Source bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| sourceKey | Source object key. An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Source file version ID (for source buckets with versioning enabled). Default value: Current version of the source file | String |
| destinationBucketName | Destination bucket name in the format of BucketName-APPID, which is composed of letters, numbers, and a dash | String |
| destinationKey | Destination object key. An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| storageClass | Storage class of the destination file to copy to. Enumerated values: Standard, Standard_IA. Default value: Standard | String |

#### Return Result Descriptions

- Success: CopyObjectResult is returned, which contains the new file's information such as ETag.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Intra-region intra-account copy
// Source bucket. Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String srcBucketName = "srcBucket-1250000000";
// The source file to be copied
String srcKey = "srcobject";
// Destination bucket. Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String destBucketName = "examplebucket-1250000000";
// The destination file to copy to
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// Cross-account cross-region copy (you need to have read permission to the source file and write permission to the destination file)
String srcBucketNameOfDiffAppid = "srcBucket-125100000";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
```

### Deleting a Single Object

#### Feature Description

This API (Delete Object) is used to delete the specified object.

#### Method Prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucket, key);
```

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query multipart uploads in progress in the specified bucket.

#### Method Prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | Request | ListMultipartUploadsRequest |

Request member description:

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| keyMarker     | The entry list starts at this key value                                      | String |
| delimiter | The delimiter is a symbol. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path | String |
| prefix | Specifies that the returned object key must be prefixed with the "prefix". Note that when a prefix query is used, the returned key will still contain the prefix | String |
| uploadIdMarker | The entry list starts at this UploadId value                                      | String |
| maxUploads | Sets the maximum number of parts returned between 1 and 1,000 | String |
| encodingType | Specifies the encoding method of the return value. Value range: url | String |

#### Return Result Descriptions

- Success: MultipartUploadListing is returned, which contains information of the multipart uploads in progress.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
listMultipartUploadsRequest.setDelimiter("/");
listMultipartUploadsRequest.setMaxUploads(100);
listMultipartUploadsRequest.setPrefix("");
listMultipartUploadsRequest.setEncodingType("url");
MultipartUploadListing multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
```

### Uploading an Object in Parts

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the multipart upload.
- Resume a multipart upload, including querying uploaded parts, uploading parts, and completing the multipart upload.
- Abort a multipart upload.

### Initializing a Multipart Upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload task.

#### Method Prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;

```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | Request | InitiateMultipartUploadRequest |

Request member description:

| Parameter Name | Setting Method | Description | Type |
| ---------- | ----------------- | ------------------------------------------------------------ | ------ |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | [Object key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |

#### Return Result Descriptions

- Success: InitiateMultipartUploadResult is returned, which contains the uploadId identifying this multipart upload.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
InitiateMultipartUploadRequest initRequest = new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
String uploadId = initResponse.getUploadId()

```

### Uploading Parts

This API (Upload Part) is used to upload parts.

#### Method Prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;

```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | Request | UploadPartRequest |

Request member description:

| Parameter Name | Setting Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | set method | [Object key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | set method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | set method | Identifies the number of the specified part, which must be >= 1 | int |
InputStream | set method | Input stream of the parts to be uploaded | InputStream |

#### Return Result Descriptions

- Success: UploadPartResult is returned, which contains eTag information of the uploaded parts.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Upload up to 10,000 parts of 1 MB to 5 GB in size.
// The part size is set to 4 MB. If there are n parts in total, parts 1 to n-1 are of the same size, and the size of the last part is less than or equal to that of the previous part.
List<PartETag> partETags = new ArrayList<PartETag>();
int partNumber = 1;
int partSize = 4 * 1024 * 1024;
// partStream represents the input stream of the part data, and the stream length is partSize
UploadPartRequest uploadRequest =  new    UploadPartRequest().withBucketName(bucketName).
 withUploadId(uploadId).withKey(key).withPartNumber(partNumber).
  withInputStream(partStream).withPartSize(partSize);  
UploadPartResult uploadPartResult = cosClient.uploadPart(uploadRequest);
String eTag = uploadPartResult.getETag();  // Get Etag of the part
partETags.add(new PartETag(partNumber, eTag));  // partETags records Etag information of all uploaded parts
// ... upload parts with partNumber 2 to n
```

### Copying Parts

#### Feature Description

This API (Upload Part Copy) is used to copy the parts of an object from the source path to the destination path.

#### Method Prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

Request member description:

| Parameter Name | Setting Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | set method | Destination bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| destinationKey | set method | Destination object name, which is the [object key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | set method | Identifies the uploadId of the specified multipart upload | String |
| partNumber | set method | Identifies the number of the specified part, which must be >= 1 | int |
| sourceBucketRegion | set method | Source bucket region | Region |
| sourceBucketName | set method | Source bucket name | String |
| sourceKey | set method | Source object name, which is the [object key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| firstByte | set method | First byte offset of the source object | Long |
| lastByte | set method | Last byte offset of the source object | Long |

#### Return Result Descriptions

- Success: CopyPartResult is returned, which contains ETag information of the parts.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// 1. Initialize the user credentials (secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// New region names have been adopted. The list of availability regions can be viewed in the official documentation of COS. You can also see the region tables in the SDK for XML and SDK for JSON below
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
COSClient cosclient = new COSClient(cred, clientConfig);
// Bucket name in the format of BucketName-APPID
// Set the destination bucket name, object name, and multipart upload ID
String destinationBucketName = "examplebucket-1250000000";
String destinationTargetKey = "target_exampleobject";
String uploadId = "1559020734eeca6640329099e680457e0ef653a72dd70d4eade64205d270b532c22a38649e";
int partNumber = 1;
CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setDestinationBucketName(destinationBucketName);
copyPartRequest.setDestinationKey(destinationTargetKey);
copyPartRequest.setUploadId(uploadId);
copyPartRequest.setPartNumber(partNumber);
// Set the source bucket region and name, object name, and offset range
String sourceBucketRegion = "ap-guangzhou";
String sourceBucketName = "examplebucket-1250000000";
String sourceKey = "exampleobject";
Long firstByte = 1L;
Long lastByte = 5242880L;
copyPartRequest.setSourceBucketRegion(new Region(sourceBucketRegion));
copyPartRequest.setSourceBucketName(sourceBucketName);
copyPartRequest.setSourceKey(sourceKey);
copyPartRequest.setFirstByte(firstByte);
copyPartRequest.setLastByte(lastByte);

CopyPartResult copyPartResult = cosclient.copyPart(copyPartRequest);
```

### Querying Uploaded Parts

#### Feature Description

This API (List Parts) is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ---------------- | ----------------- | ------------------------------------------------------------ | ------ |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | uploadId of the multipart upload to be queried | String |
| maxParts | set method | Maximum number of entries returned at a time; 1,000 by default | String |
| partNumberMarker | set method | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | String |
| encodingType | set method | Specifies the encoding method of the return value | String |

#### Return Result Descriptions

- Success: PartListing is returned, which contains the ETag and number of each part and the starting marker of the next list.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// ListPart is used to get the information of uploaded parts corresponding to the uploadId before the multipart upload is completed or aborted, which can be used to construct partEtags
List<PartETag> partETags = new ArrayList<PartETag>();
ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, key, uploadId);
do {
      PartListing partListing = cosClient.listParts(listPartsRequest);
    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }
    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());
```

### Completing a Multipart Upload 

#### Feature Description

The API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method Prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ---------- | ----------------- | ------------------------------------------------------------ | ----------------- |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | [Object key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | Constructor or set method | Identifies the uploadId of the specified multipart upload | String |
| partETags | Constructor or set method | Identifies the part number and the eTag returned by the upload | `List<PartETag>` |

#### Return Result Descriptions

- Success: CompleteMultipartUploadResult is returned, which contains the eTag information of the completed object.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Complete a multipart upload
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result =  cosClient.completeMultipartUpload(compRequest);
```

### Aborting a Multipart Upload

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ---------- | ----------------- | ------------------------------------------------------------ | ------ |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | [Object key](https://intl.cloud.tencent.com/document/product/436/13324) of the object stored in COS | String |
| uploadId | Constructor or set method | Identifies the uploadId of the specified multipart upload | String |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// abortMultipartUpload is used to abort a multipart upload that has not been completed yet
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);

```

## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to retrieve an archived object for access.

#### Method Prototype

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;

```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | Request class | RestoreObjectRequest |

Request member description:

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| expirationInDays | Expiration time in days of the restored temporary file | int |
| casJobParameters | Describes the configuration information of the restoration type. You can call the setTier function to set one of the following three restoration types: Tier.Standard, Tier.Expedited, and Tier.Bulk | CASJobParameters |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucket = "examplebucket-1250000000";
String key = "exampleobject";
     
// Set the expiration time of the restored temporary copy to 1 day
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucket, key, 1);
// Set the restoration mode to Standard. Other modes available include Expedited and Bulk. These three modes are different in terms of fees and speed
CASJobParameters casJobParameters = new CASJobParameters();
casJobParameters.setTier(Tier.Standard);
restoreObjectRequest.setCASJobParameters(casJobParameters);
cosclient.restoreObject(restoreObjectRequest);

```

### Setting Object ACL

#### Feature Description

This API is used to set the ACL for the specified object in a bucket.

> Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, do not set it, so that the object will inherit the permissions of the bucket.

The ACL can be divided into predefined ACL (CannedAccessControlList) and custom ACL (AccessControlList). When both types of ACLs are set at the same time, the predefined ACL will be ignored and the custom one will prevail.
#### Method Prototype

```java
// Method 1 (setting a custom ACL)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// Method 2 (setting a preset ACL)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// Method 3 (encapsulating both methods above, i.e., containing two types of ACLs; if set simultaneously, the custom ACL will prevail)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

- The parameters of **method 3** cover methods 1 and 2 and thus are used here as an example.

| Parameter Name | Description | Type |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | Request class | setObjectAclRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| acl | Constructor or set method | Custom ACL | AccessControlList |
| cannedAcl | Constructor or set method | Predefined ACL such as public read, public read/write, and private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains all the information to be authorized | Array |
| owner | Represents the owner of the object or owner | Owner class |

Grant class member description:

| Member Name | Description | Type |
| ---------- | ------------------------------------------ | ---------- |
| Grantee | Grantee's identity | Grantee |
| Permission | Granted permission information (e.g., read, write, and read/write) | Permission |

Owner class member description:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Owner ID | String |
| displayname | Owner name (currently the same as ID) | String |

CannedAccessControlList represents a predefined ACL for everyone and is an enumeration class with the following enumerated values:

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read/write (i.e., only the owner can read and write) |
| PublicRead | Public read and private write (i.e, owner can read and write and other users can read) |
| PublicReadWrite | Public read/write (i.e., everyone can read and write) |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// The identity information in the permission information should be in the required format. The patterns of root accounts and sub-accounts are as follows:
// The root_uin and sub_uin below must be valid QQ account numbers
// Root account. qcs::cam::uin/<root_uin>:uin/<root_uin> indicates to grant permission to the root account root_uin (i.e., the two uins entered are identical)
// For example, qcs::cam::uin/2779643970:uin/2779643970
// Sub-account. qcs::cam::uin/<root_uin>:uin/<sub_uin> indicates to grant permission to the sub-account sub_uin
// For example, qcs::cam::uin/2779643970:uin/73001122 
// Bucket name is in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Set a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// Set the owner information. The owner can only be a root account
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);

// Grant the root main account 73410000 read/write permission
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/73410000:uin/73410000");
acl.grantPermission(uinGrantee1, Permission.FullControl);
// Grant the sub-account 72300000 of 2779643970 read permission
UinGrantee uinGrantee2 = new UinGrantee("qcs::cam::uin/2779643970:uin/72300000");
acl.grantPermission(uinGrantee2, Permission.Read);
// Grant the sub-account 7234444 of 2779643970 write permission
UinGrantee uinGrantee3 = new UinGrantee("qcs::cam::uin/7234444:uin/7234444");
acl.grantPermission(uinGrantee3, Permission.Write);
cosClient.setObjectAcl(buckeName, key, acl);

// Set a predefined ACL
// Set private read/write (the object inherits the permission of the bucket by default)
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.Private);
// Set public read and private write
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.PublicRead);
// Set public read/write
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.PublicReadWrite);
```

### Getting Object ACL

#### Feature Description

This API (Get Object ACL) is used to get the access control list (ACL) of an object.

#### Method Prototype

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Return Result Descriptions

- Success: The ACL of an object is returned.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList acl = cosClient.getObjectAcl(bucketName, key);
```

## Advanced API (Recommended)

The advanced API encapsulates the upload and download APIs through the TransferManager class. It has a thread pool to accept your upload and download requests, so that you can choose to submit tasks asynchronously.

```java
// Thread pool size. It is recommended to set this to 16 or 32 as long as the client and COS have sufficient network resources (for example, Tencent Cloud CVM is used, or the upload to COS is performed intra-region), which can fully utilize the network resources.
// For scenarios where a public network with low bandwidth and poor network quality is used for data transfer, it is recommended to lower this value to avoid request timeout due to slow network transfer.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// Pass in a thread pool. If no thread pool is passed in, a single-threaded thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// ...(submit an upload or download request as described below)
// Close TransferManger
transferManager.shutdownNow();
```

### Uploading an Object

#### Feature Description

The upload API automatically selects simple upload or multipart upload based on the file size, reducing the usage threshold and eliminating your need to take care of every step in multipart upload.

For other attributes, storage class, and MD5 checksum, see the Put Object API.

#### Method Prototype

```java
// Upload the object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | File metadata | ObjectMetadata |

#### Return Value

- Success: Upload is returned, which can be used to query whether the upload has been completed. You can also wait for the upload completion synchronously.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
String key = "/doc/picture.jpg";
File localFile = new File("/doc/picture.jpg");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
// Upload a local file
Upload upload = transferManager.upload(putObjectRequest);
 // Wait for the transfer to complete (call waitForCompletion if you want to wait for upload completion synchronously)
UploadResult uploadResult = upload.waitForUploadResult();
```

### Downloading an Object

#### Feature Description

This API is used to download an object in COS to the local file system.

#### Method Prototype

```java
// Download the object
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | Object download request | GetObjectRequest |
| file | Local file to download to | File |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |
| key | Constructor or set method | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | set method | Download range | Long[] |

#### Return Value

- Success: Download is returned, which can be used to query whether the download has been completed. You can also wait for the download completion synchronously.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
String key = "/doc/picture.jpg";
File localDownFile = new File("/doc/picture.jpg");
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, key);
// Download a file
Download download = transferManager.download(getObjectRequest, localDownFile);
 // Wait for the transfer to complete (call waitForCompletion if you want to wait for upload completion synchronously)
download.waitForCompletion();
```

### Copying an Object

#### Feature Description

The Copy API supports automatic selection of simple copy or multipart copy based on the object size, eliminating your need to care about the size of the copied files.

#### Method Prototype

```java
// Upload the object
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

Request member description:

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Source bucket region. Default value: Same as the current clientconfig region, indicating copy in the same region | String |
| sourceBucketName | Source bucket name, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| sourceKey | Source object key. An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| sourceVersionId | Source file version ID (for source buckets with versioning enabled). Default value: Current version of the source file | String |
| destinationBucketName | Name of the destination bucket, which is in the format of BucketName-APPID. The bucket name entered here must be in this format | String |
| destinationKey | Destination object key. An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| storageClass | Storage class of the destination file to copy to. Enumerated values: Standard, Standard_IA. Default value: Standard | String |

#### Return Value

- Success: Copy is returned, which can be used to query whether the copy has been completed. You can also wait for the copy completion synchronously.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Region of the bucket to copy to. Cross-region copy is supported
Region srcBucketRegion = new Region("ap-shanghai");
// Source bucket. Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String srcBucketName = "srcBucket-1251668577";
// The source file to be copied
String srcKey = "exampleobject";
// Destination bucket. Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String destBucketName = "examplebucket-1250000000";
// The destination file to copy to
String destKey = "exampleobject";

// Generate the srcCOSClient used to get the source file information
COSClient srcCOSClient = new COSClient(cred, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // An async result "copy" is returned. You can also call waitForCopyResult synchronously to wait for the copy completion. If the request succeeds, CopyResult will be returned; otherwise, an exception will be thrown
    CopyResult copyResult = copy.waitForCopyResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

```

## Client Encryption

#### Feature Description

The SDK for Java supports client-side encryption based on symmetric AES or asymmetric RSA where files are encrypted before uploaded and decrypted when downloaded.
The symmetry and asymmetry involved here are only used to encrypt the random key generated each time, while AES-256 symmetric encryption is always used for file data encryption.
Client-side encryption is suitable for storage of sensitive data at the expense of upload speed. For multipart uploads, the SDK uploads the files in a serial manner.

### Preparations Before Using Client-side Encryption

Client-side encryption uses AES-256 to encrypt data internally. By default, older versions (v6-8) of JDK do not support 256-bit encryption and will display the following exception during execution: `java.security.InvalidKeyException: Illegal key size or default parameters`. In this case, you need to deploy Oracle's JCE unlimited strength jurisdiction policy file to the JRE. Please download the file corresponding to the currently used JDK version and extract it to the jre/lib/security directory under JAVA_HOME.

1. [JDK6 JCE file](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
2. [JDK7 JCE file](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
3. [JDK8 JCE file](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

### Upload Encryption Flow

1. Before a file object is uploaded, a symmetric encryption key is generated randomly, which is encrypted with the user-supplied symmetric or asymmetric key, and the encryption result is Base64-encoded and stored in the object's metadata.
2. The file object is encrypted in the memory using the AES-256 algorithm during upload.

### Download Decryption Flow

1. The information necessary for encryption in the file metadata is obtained, Base64-decoded, and decrypted with the user-supplied key to obtained the key used to encrypt the data in the first place.
2. The downloaded input stream is decrypted with the obtained key using AES-256 to get the decrypted file input stream.

#### Sample Request

Example 1. Encrypt the key randomly generated each time using symmetric AES-256. For the complete sample code, see [Complete Sample of Client-side Encryption with a Symmetric Key](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

```java
// Initialize the user credentials (secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the bucket region. For abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));

// Load the key saved in the file. If it does not exist, use buildAndSaveSymmetricKey to generate a key first
// buildAndSaveSymmetricKey();
SecretKey symKey = loadSymmetricAESKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// Use AES/GCM mode and store the encrypted information in the file metadata
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
		.withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generate the encryption client EncryptionClient, which is a subclass of COSClient and supports all APIs supported by COSClient
// EncryptionClient overwrites the upload and download logics of COSClient and performs encryption internally. Its logics of other operations are the same as those of COSClient
COSEncryptionClient cosEncryptionClient =
		new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
				new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
				cryptoConf);

// Upload the file
// Here is an example of putObject. For an upload using the advanced API, just pass in the COSEncryptionClient object when generating TransferManager
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File("src/test/resources/plain.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
```

Example 2. Encrypt the key randomly generated each time using asymmetric RSA. For the complete sample code, see [Complete Sample of Client-side Encryption with an Asymmetric Key](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/AsymmetricKeyEncryptionClientDemo.java).

```java
// Initialize the user credentials (secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the bucket region. For abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));


// Load the key saved in the file. If it does not exist, use buildAndSaveAsymKeyPair to generate a key first
buildAndSaveAsymKeyPair();
KeyPair asymKeyPair = loadAsymKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// Use AES/GCM mode and store the encrypted information in the file metadata
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
		.withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generate the encryption client EncryptionClient, which is a subclass of COSClient and supports all APIs supported by COSClient
// EncryptionClient overwrites the upload and download logics of COSClient and performs encryption internally. Its logics of other operations are the same as those of COSClient
COSEncryptionClient cosEncryptionClient =
		new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
				new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
				cryptoConf);

// Upload the file
// Here is an example of putObject. For an upload using the advanced API, just pass in the COSEncryptionClient object when generating TransferManager
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File("src/test/resources/plain.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
```
