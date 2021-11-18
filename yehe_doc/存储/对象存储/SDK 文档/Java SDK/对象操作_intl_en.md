## Overview

This document provides an overview of advanced APIs and APIs for simple object operations and multipart upload operations, as well as their SDK code samples.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying object versions | Queries some or all objects in a bucket and their historical versions |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Upload an object by appending the object by parts   |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes an object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## Simple Operations

### Querying objects

#### Description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

>! In COS, if a listed object key is project/, it is an empty object to simulate the effects of a folder. For more information, please see [Folder and directory](https://intl.cloud.tencent.com/document/product/436/13324).
>

#### Sample request

[//]: # ".cssg-snippet-get-bucket"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates that the key of the object to be listed must start with this value
listObjectsRequest.setPrefix("images/");
// Set the delimiter to "/" to list objects in the current directory. To list all objects, leave it empty.
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
    // A common prefix indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary shows all listed objects.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // File path key
        // Files such as "aaa/" might be listed. Note that they are not directories but files.
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

The request parameters are described as follows:

| Request Member | Setting Method  | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| prefix | Constructor or set method | Returns objects prefixed with this value. <br>Default value: `""` (left empty), meaning to return all objects in the bucket | String |
| marker | Constructor or set method | Marks the starting object of the list. It can be left empty for the first request, but for subsequent requests, it should be set to the `nextMarker` value in the previous listObjects response | String |
| delimiter | Constructor or set method | Indicates that paths that start with the specified "prefix" and end with the first occurrence of the delimiter will be returned | String |
| maxKeys | Constructor or set method | Maximum number of returned members (up to 1,000). <br>Default value: `1000` | Integer |

#### Response description

- Success: returns `ObjectListing`, including all members and `nextMarker`.  
- Failure: throws a "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Querying an object version

#### Description

This API is used to query some or all the objects in a bucket and their version history.

#### Method prototype

```java
public VersionListing listVersions(ListVersionsRequest listVersionsRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";

ListVersionsRequest listVersionsRequest = new ListVersionsRequest();
listVersionsRequest.setBucketName(bucketName);
// The prefix indicates that the key of the object to be listed must start with this value
listVersionsRequest.setPrefix("");
// Set the maximum number of traversed objects (up to 1,000 per listobject request)
listObjectsRequest.setMaxKeys(1000);

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

    String keyMarker = versionListing.getNextKeyMarker();
    String versionIdMarker = versionListing.getNextVersionIdMarker();

    listVersionsRequest.setKeyMarker(keyMarker);
    listVersionsRequest.setVersionIdMarker(versionIdMarker);

} while (versionListing.isTruncated());
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

### Querying object metadata

#### Description

This API is used to query whether a specified object exists in a certain bucket.

#### Method prototype

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-head-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);

// Get requestId of the current request
System.out.println(objectMetadata1.getRequestId());
// Get the CRC64 check value of the object
System.out.println(objectMetadata.getCrc64Ecma());
// Get the last upload time of the object
System.out.println(objectMetadata1.getLastModified());
// Get the object size
System.out.println(objectMetadata.getContentLength());
// Get the object storage type
System.out.println(objectMetadata.getStorageClass());
```

#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String  |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: returns `ObjectMetadata`, including the user-defined headers and object metadata such as the ETag.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `ObjectMetadata` class is used to record the metadata of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than user-defined metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |


### Uploading an object (creating a directory)

#### Description

This API (PUT Object) is used to upload objects to the specified bucket. It can upload a local file or an input stream of a known length to COS. It is suitable for uploading small image files (below 20 MB), with a maximum of 5 GB (inclusive) supported. Please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) if the file is larger than 5 GB.

- The file length and MD5 hash are checked by default during upload (see the sample code for disabling MD5 check).
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one.
- Once uploaded, you can download the file by calling the GetObject API with the same key, or by generating a [pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31536) and sending the file to another device for download (Please specify GET as the download method; see the section below for API instructions.)
- COS uses slashes (/) to separate object paths to simulate the effect of directories. Therefore, you can upload an empty stream and append a slash to its name to create an empty directory in COS.
You can also upload an object whose name is separated with slashes. In this way, the directory that contains this object will be created automatically. If you need to upload new objects to this COS directory, you can set the prefix of the key to this directory. 

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

#### Sample 1. Uploading a file

[//]: # ".cssg-snippet-put-object-flex"
<dx-codeblock>
:::  java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";

File localFile = new File(localFilePath);
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // Obtain the file ETag.
:::
</dx-codeblock>

#### Sample 2: uploading an object to a COS directory

<dx-codeblock>
:::  java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";

File localFile = new File(localFilePath);
// In COS, a directory is a prefix that ends with a slash (/).
String dir = "exampledir/";
String filename = "exampleobject";

String key = dir+filename;
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // Obtain the file ETag.
:::
</dx-codeblock>

#### Sample 3. Uploading using a stream (the stream length should be set. Otherwise, an OOM error may occur)

<dx-codeblock>
:::  java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";

FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the length of an input stream (replace `STREAMLENGTH` with the actual stream length)
objectMetadata.setContentLength(STREAMLENGTH);
// Set the content type. Default: application/octet-stream
objectMetadata.setContentType("application/pdf");
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
String etag = putObjectResult.getETag();
// Close the input stream
:::
</dx-codeblock>

#### Sample 4. Creating a directory (uploading an empty-stream object)

<dx-codeblock>
:::  java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";

// Set the name of the directory, which must end with a slash (/).
String key = "cos_dir/";
// Create a stream whose size is 0.
InputStream emptyContent = new ByteArrayInputStream(new byte[0]);
ObjectMetadata metadata = new ObjectMetadata();
metadata.setContentLength(0);
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, emptyContent, objectMetadata);
String etag = putObjectResult.getETag();
// Close the input stream
:::
</dx-codeblock>

#### Sample 5: limiting the upload speed

<dx-codeblock>
:::  java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";

// 1 storage-class. Enumerated values are `Standard` (default), `Standard_IA`, and `Archive`. For more information, please see: https://intl.cloud.tencent.com/document/product/436/30925
// 2. content-type. For local file upload, the files are mapped based on the suffix by default. For example, a JPG file is mapped as image/jpeg.
// For input stream upload, the default is application/octet-stream.
// 3. To disable MD5 upload verification globally, set the system environment variable. This will affect all upload verification. Verification is performed by default.
// Disable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// Enable M5 verification: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
File localFile = new File(localFilePath);
String key = "picture.jpg";
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
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
// Get the ETag of the object.
String etag = putObjectResult.getETag();
// Get the CRC64 checksum of the object.
String crc64Ecma = putObjectResult.getCrc64Ecma();
:::
</dx-codeblock>



#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Setting Method   | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String         | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket.<br>For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |

The `ObjectMetadata` class is used to record the metadata of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than user-defined metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |


#### Response description

- Success: returns `PutObjectResult`, including the file ETag.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The PutObjectResult class is used to return result information. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Returns the version ID of an object in a version-enabled bucket | String |
| eTag | MD5 checksum of the object returned by PUT Object | String |
| crc64Ecma | CRC64 value computed by the server based on the object content | String |

### Appending parts

#### Description

This API is used to upload an object by appending parts.

#### Method prototype

```java
public AppendObjectResult appendObject(AppendObjectRequest appendObjectRequest)
        throws CosServiceException, CosClientException
```

#### Sample request

```java
// The bucket name must contain "appid".
String bucketName = "examplebucket-1251668577";
String key = "aaa/bbb.txt";
try {
    File localFile = new File("1M.txt");
    AppendObjectRequest appendObjectRequest = new AppendObjectRequest(bucketName, key, localFile);
    appendObjectRequest.setPosition(0L);
    AppendObjectResult appendObjectResult = cosclient.appendObject(appendObjectRequest);
    long nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);

    localFile = new File("2M.txt");
    appendObjectRequest = new AppendObjectRequest(bucketName, key, localFile);
    appendObjectRequest.setPosition(nextAppendPosition);
    appendObjectResult = cosclient.appendObject(appendObjectRequest);
    nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### Parameter description

| Parameter | Description | Type |
| -------------------- | ------------ | ---------------- |
| appendObjectRequest | Request to append upload | AppendObjectRequest |

Members of `AppendObjectRequest`:

| Request Member | Set Method | Description | Type | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String         | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket.<br>For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| localfile | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |
| position | Set method | Start position of the append, in bytes | Long | Yes |

#### Response description

- Success: `AppendObjectResult`
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `AppendObjectResult` class is used to return results. Its main members are as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| metadata | Headers | ObjectMetadata               |
| nextAppendPosition| Position of the next append | Long |


### Downloading an object

#### Description

This API (`GET Object`) is used to download an object.

#### Method prototype

```java
// Method 1. Download a file and get the input stream.
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// Method 2. Download the file locally.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### Sample 1. Obtaining the input stream

[//]: # ".cssg-snippet-get-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// Read stream
byte[] bytes = null;
try {
    bytes = IOUtils.toByteArray(cosObjectInput);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    cosObjectInput.close(); 
}

// Download the CRC64 value of the object.
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();

// Method 2. Download the file locally.
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

#### Sample 2. Downloading the object

```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

#### Sample 3: limiting the download speed

[//]: # ".cssg-snippet-get-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// Here, set the download bandwidth limit (in bit/s) to 10 MB/s.
getObjectRequest.setTrafficLimit(80*1024*1024);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// Read stream
byte[] bytes = null;
try {
    bytes = IOUtils.toByteArray(cosObjectInput);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    cosObjectInput.close();
}

// Download the CRC64 value of the object.
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | The file saved locally | File |

The request members are described as follows:

| Request Member | Setting Method  | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object key, the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | Set method | Download range | Long[] |
| trafficLimit | Set method | Traffic limits (in bit/s) on the downloaded object. The default setting is no limit. | Int |


#### Response description

- **Method 1 (Get the input stream of the downloaded file)**
  - Success: returns the `COSObject` class, including the input stream and object attributes.
  - Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
- **Method 2 (Download the file locally)**
  - Success: returns `objectMetadata`, including the file's custom headers, content-type, and other attributes.
  - Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `COSObject` class is used to return request results. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName |  Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| metadata | Object metadata  | ObjectMetadata |
| objectContent | Data stream containing COS object content  | COSObjectInputStream |


### Copying objects

#### Description 

This API (Put Object Cop) is used to copy an object. You can copy an object up to 5 GB in size across regions, accounts, and buckets, provided that you have read permission for the source file and write permission for the destination file. To copy files larger than 5 GB, use the [advanced replication API](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1).

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Sample 1. Copying an object

[//]: # ".cssg-snippet-copy-object"
```java
// Intra-region and intra-account replication
// Enter the source bucket name in the format of `BucketName-APPID`
String srcBucketName = "sourcebucket-1250000000";
// The source file to copy
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "examplebucket-1250000000";
// The destination file of the copy operation
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// Cross-account and cross-region replication (read permission for the source file and write permission for the destination file are required)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
// Get the CRC64 value of the object
String crc64Ecma = copyObjectResult.getCrc64Ecma();
```

#### Sample 2: modifying storage class

>!You can change STANDARD to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE. To modify ARCHIVE or DEEP ARCHIVE to other storage classes, you need to call `PostRestore` to restore objects in ARCHIVE or DEEP ARCHIVE first before calling this API. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

```java
// Intra-region and intra-account replication
// Enter the source bucket name in the format of `BucketName-APPID`
String srcBucketName = "sourcebucket-1250000000";
// The source file to copy
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "examplebucket-1250000000";
// The destination file of the copy operation
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// Cross-account and cross-region replication (read permission for the source file and write permission for the destination file are required)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
// Set the storage class of the object to STANDARD_IA.
copyObjectRequest.setStorageClass(StorageClass.Standard_IA);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
// Get the CRC64 value of the object
String crc64Ecma = copyObjectResult.getCrc64Ecma();
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
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Deleting an object

#### Description

This API is used to delete a specified object (file) from a bucket.

#### Method prototype

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-delete-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String  |
| key | Object key, the unique identifier of an object in a bucket. For example, in the object endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For details, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Delete objects in batch

#### Description

The API (DELETE Multiple Objects) is used to delete multiple objects.

#### Method prototype

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
    throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-delete-multi-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
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

The request members are described as follows:

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| quiet | Indicates how to return the deletion result. Valid values: true and false (default). If set to `true`, only error messages due to failed deletions are returned. If set to `false`, messages indicating successful and failed deletion are returned | Boolean |
| keys | List of object paths. The version ID of each object is optional. | List&lt;DeleteObjectsRequest.KeyVersion&gt; |

`DeleteObjectsRequest.KeyVersion` members are described as follows:

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| version | (Optional) Specifies the version ID of an object to delete from a versioning-enabled bucket | String |

#### Response description

- Success: No value is returned.
- Failure: an error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Restoring an archived object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Method prototype

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-restore-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

// Sets the number of days before a restored temporary copy expires to 1
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucketName, key, 1);
// Set the restoration mode to `Standard`. You can set it to `Standard`, `Expedited` or `Bulk` if the object's storage class is ARCHIVE. For DEEP ARCHIVE, you can set it to `Standard` or `Bulk`. Each restoration mode offers different restoration speeds and costs differently.
CASJobParameters casJobParameters = new CASJobParameters();
casJobParameters.setTier(Tier.Standard);
restoreObjectRequest.setCASJobParameters(casJobParameters);
cosClient.restoreObject(restoreObjectRequest);
```

#### Parameter description

| Parameter | Description | Type |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | Request class | RestoreObjectRequest |

The request members are described as follows:

| Parameter | Description | Type |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| expirationInDays | Specifies the number of days before a restored temporary file expires | int |
| casJobParameters | Specifies the restoration mode to call the `setTier` function. To restore objects from ARCHIVE, valid values are `Tier.Standard`, `Tier.Expedited`, and `Tier.Bulk`. To restore objects from DEEP ARCHIVE, valid values are `Tier.Standard` and `Tier.Bulk`. | CASJobParameters |

#### Response description

- Success: No value is returned.
- Failure: an error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Multipart Operations

Multipart operations include:

- Multipart upload: initializing a multipart upload operation, uploading parts, and completing a multipart upload operation
- Resuming a multipart upload operation: querying uploaded parts, uploading remaining parts, and completing a multipart upload operation
- Deleting uploaded parts

### Querying multipart uploads

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

[//]: # ".cssg-snippet-list-multi-upload"
```java
// Enter the bucket name in the format of `BucketName-APPID`
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

The request members are described as follows:

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| keyMarker | Specifies the key after which the listing should begin | String |
| delimiter | A symbol used to limit the results of a list operation. If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed. If no prefix is specified, the listing will start from the beginning of the path. | String |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when you use a prefix to query object keys, the returned key will contain the same prefix. | String |
| uploadIdMarker | Specifies the `uploadId` after which the listing should begin | String |
| maxUploads | Sets the maximum number of multipart uploads returned. Valid values: 1-1000 | String |
| encodingType | Encoding type of returned values. Valid value: `url` | String |

#### Response description

- Success: returns `MultipartUploadListing`, including the in-progress multipart uploads.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



### Initializing a multipart upload

#### Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-init-multi-upload"
```java
// Enter the bucket name in the format of `BucketName-APPID`.
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

The request members are described as follows:

| Parameter | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String |

#### Response description

- Success: returns `InitiateMultipartUploadResult`, including the `uploadId` that identifies the multipart upload.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


###  Uploading parts

This API (`Upload Part`) is used to upload parts.

#### Method prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-upload-part"
```java
// Up to 10,000 parts can be uploaded, ranging from 1 MB to 5 GB in size.
// Set the size of each part to 4 MB. If there are a total of n parts, the size of part 1 through part n-1 is the same, while the last part is less than or equal to it.
List<PartETag> partETags = new ArrayList<PartETag>();
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

The request members are described as follows:

| Parameter | Set Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | Set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |
| uploadId | Set method | Identifies the `uploadId` of the specified multipart upload | String |
| partNumber | Set method | Number (>= 1) that identifies the specified part | int |
| inputStream | Set method | Input stream to be uploaded in multi-parts | InputStream |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded parts. The default setting is no limit. | Int |


#### Response description

- Success: returns `UploadPartResult`, including the ETags of the uploaded parts.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


#### Response parameters

The `UploadPartResult` class is used to return request results. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | Number that identifies the specified part | String                |
| eTag        | Returns the MD5 hash of the uploaded part                   | String |
| crc64Ecma | CRC64 value computed by the server based on the part content | String |


### Copying an object part

#### Description

This API (Upload Part - Copy) is used to copy an object as a part from a source path to a destination path.

#### Method prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Sample request

[//]: # ".cssg-snippet-upload-part-copy"
```java
// Bucket name in the format of `BucketName-APPID`
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
List<PartETag> partETags = new ArrayList<PartETag>();
partETags.add(copyPartResult.getPartETag());
```


#### Parameter description

| Parameter | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

The request members are described as follows:

| Parameter | Set Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Set method | Destination bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| destinationKey | Set method | Name of the destination object (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to store the replicated part, for example, `folder/picture.jpg` | String |
| uploadId | Set method | Identifies the `uploadId` of the specified multipart upload | String |
| partNumber | Set method | Number (>= 1) that identifies the specified part | int |
| sourceBucketRegion | Set method | Region of the source bucket | Region |
| sourceBucketName | Set method | Source bucket name | String |
| sourceKey | Set method | Name/Path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the source object before the replication, for example, `folder/picture.jpg` | String |
| firstByte | Set method | First byte offset of the source object | Long |
| lastByte | Set method | Last byte offset of the source object | Long |

#### Response description

- Success: returns `CopyPartResult`, including the ETag of the part.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-list-parts"
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
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | `uploadId` of the multipart upload to be queried | String |
| maxParts | Set method | Maximum number of entries returned at a time. Default value: `1000` | String |
| partNumberMarker | Set method | By default, entries are listed in UTF-8 binary order, starting from the part number after the marker. | String |
| encodingType | Set method | Encoding type of the returned value | String |

#### Response description

- Success: returns `PartListing`, including the ETag and number of each part as well as the starting marker of the next list.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Completing a multipart upload 

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-complete-multi-upload"
```java
// Complete a multipart upload.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```


#### Parameter description

| Parameter | Set Method  | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String            |
| uploadId | Constructor or set method | Identifies a specified multipart upload. | String |
| partETags  | Constructor or set method | Identifies the number and ETag returned for an uploaded part. | List&lt;PartETag&gt; |

#### Response description

- Success: returns `CompleteMultipartUploadResult`, including the ETag of the completed object.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # ".cssg-snippet-abort-multi-upload"
```java
// abortMultipartUpload is used to abort an uncompleted multipart upload
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```


#### Parameter description

| Parameter | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String |
| uploadId | Constructor or set method | Identifies a specified multipart upload | String |

#### Response description

- Success: No value is returned.
- Failure: An error occurs (such as authentication failure), throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



## Advanced APIs (Recommended)

The advanced APIs encapsulate upload and download APIs using the TransferManger class. They have a thread pool to receive upload and download requests, so that you can choose to submit tasks asynchronously.

[//]: # ".cssg-snippet-transfer-init"
<dx-codeblock>
:::  java
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
:::
</dx-codeblock>


Close TransferManager manually after use to prevent resource leakage.

```java
// Close TransferManger and close cosClient inside it.
transferManager.shutdownNow();
```

#### Parameter description

The `TransferManagerConfiguration` class is used to record the configuration of advanced APIs. Its main members are described as follows:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set method | Part size of the multipart upload in bytes. Default: 5 MB | long |
| multipartUploadThreshold | Set method | If a file is greater than or equal to this value, it will be uploaded in concurrent parts. Unit: byte; default: 5 MB | long |
| multipartCopyThreshold | Set method | If a file is greater than or equal to this value, it will be replicated in concurrent parts. Unit: byte; default: 5 GB | long |
| multipartCopyPartSize | Set method | Part size in bytes for multipart replication. Default: 100 MB | long |

### Uploading an object (querying the progress)

#### Description

This advanced version of the PUT Object API automatically determines whether to use simple or multipart upload based on the length and data type of your file:
- Use simple upload (for streams) if the object size is below the multipart upload threshold or the `Content-Length` header is not carried.
- Use multipart upload (for streams) if the object size is above the multipart upload threshold and the `Content-Length` header is not carried.
- Use multipart upload with concurrent threads for files with File as the data type.
- Advanced APIs support calling the `getProgress()` method to obtain the multipart upload progress.
- Use multipart upload for files whose sizes are equal to or greater than 5 MB. The file size threshold can be adjusted by using the method described in sample request 3.

>? For more information about other attributes, storage classes, and MD5 checksum, please see [PUT Object API](https:///intl.cloud.tencent.com/document/product/436/7749).
>

#### Method prototype

```java
// Upload an object.
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample 1. Uploading with advanced APIs

[//]: # ".cssg-snippet-transfer-upload-file1"
```java
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file.
Upload upload = transferManager.upload(putObjectRequest);
// Wait for the upload to finish.
UploadResult uploadResult = upload.waitForUploadResult();
```

#### Sample 2. Uploading with advanced APIs and querying the upload progress

[//]: # ".cssg-snippet-transfer-upload-file2"
```java
// Write the callback function to print the upload progress.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Upload a local file.
Upload upload = transferManager.upload(putObjectRequest);
// Print the upload progress synchronously.
// You can call this function via a child thread, but be sure to start the child thread before `waitForUploadResult`, otherwise you will not see the progress because the upload is completed.
showTransferProgress(upload);
// Wait for the upload to finish.
UploadResult uploadResult = upload.waitForUploadResult();
```

#### Sample 3. Uploading with advanced APIs and setting the multipart upload threshold
```java
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// Set the threshold to trigger multipart upload to 10 MB.
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10*1024*1024);
transferManager.setConfiguration(transferManagerConfiguration);
// Upload a local file.
Upload upload = transferManager.upload(putObjectRequest);
// Wait for the upload to finish.
UploadResult uploadResult = upload.waitForUploadResult();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Setting Method  | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | 

>?When a file is uploaded in concurrent parts, `trafficLimit` is the limit on the upload speed of each part. In this case, you need to adjust the number of threads in your thread pool to control the upload speed.

#### Returned values

- Success: returns `Upload`. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Returns the object’s version ID for versioning-enabled buckets. | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |


#### Description of progress obtaining

You can use the `getProgress()` method of the `Upload` class to obtain the `TransferProgress` class, which has the following three methods to obtain the upload progress:

| Method Name | Description | Type |
| ----------------------- | ------------------ | -----   |
| getBytesTransferred     | Obtains the number of bytes uploaded  | long   |
| getTotalBytesToTransfer | Obtains the total number of bytes of the file | long   |
| getPercentTransferred   | Obtains the percentage of the number of bytes uploaded  | double |


### Downloading an object (checkpoint restart)

#### Description

This API is used to download a COS object.

#### Method prototype

```java
// Download an object.
public Download download(final GetObjectRequest getObjectRequest, final File file);

// Use checkpoint restart to download the object.
public Download download(final GetObjectRequest getObjectRequest, final File file,
        boolean resumableDownload, String resumableTaskFile,
        int multiThreadThreshold, int partSize);
```

#### Sample 1. Downloading an object with advanced APIs

[//]: # ".cssg-snippet-transfer-download-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`.
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

#### Sample 2. Using advanced APIs to download an object with checkpoint restart

```java
// Write the callback function to print the download progress.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localDownFile = new File(localFilePath);

GetObjectRequest getObj = new GetObjectRequest(bucketName, key);

Download download = transferManager.download(getObj, localDownFile, true);
// You can call this function via a child thread, but be sure to start the child thread before `waitForCompletion`, otherwise you will not see the progress because the download is completed.
showTransferProgress(download);
try {
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

transferManager.shutdownNow();
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request | GetObjectRequest | No |
| file | Destination file | File | No |
| resumableDownload | Whether to enable checkpoint restart for the download  | boolean | false |
| resumableTaskFile   | Name of the file that records the checkpoint restart information | boolean | file.cosresumabletask |
| multiThreadThreshold    | Minimum file size to use multi-thread download with checkpoint restart | int | 20 * 1024 * 1024              |
| partSize | Part size for downloading with checkpoint restart | int  | 8 * 1024 * 1024  |

The request members are described as follows:

| Request Member | Setting Method  | Description                                                     | Type   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method | Object key, the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| range | Set method | Download range | Long[] |
| trafficLimit | Set method | Traffic limits (in bit/s) on the downloaded object. The default setting is no limit. | int |

#### Returned values

- Success: returns Download. You can query whether the download is complete, or wait until the download is finished.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Copying objects

#### Description

This advanced replication API automatically determines whether to use simple replication or multipart replication based on the size of an object.

#### Method prototype

```java
// Upload an object.
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Sample 1. Intra-region replication

>?Intra-region replication refers to replicating objects to a bucket that resides in the same region.

[//]: # ".cssg-snippet-transfer-copy-object"
```java
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
// Region of the source bucket
COSCredentials credentials = new BasicCOSCredentials(secretId, secretKey);
Region bucketRegion = new Region("COS_REGION");

// Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "sourcebucket-1250000000";
// The source file to copy
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of `BucketName-APPID`.

String destBucketName = "examplebucket-1250000000";
// Destination file
String destKey = "exampleobject";

COSClient cosClient = new COSClient(credentials, new ClientConfig(bucketRegion));

ExecutorService threadPool = Executors.newFixedThreadPool(5);
// Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(cosClient, threadPool);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);

try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // Returns an asynchronous result "copy". You can call waitForCopyResult to wait synchronously for the replication to end. If successful, CopyResult is returned; otherwise, an exception will be thrown.
    CopyResult copyResult = copy.waitForCopyResult();
    // Get the CRC64 value of the replicated object.
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

#### Sample 2. Cross-region replication

>!
>- Cross-region replication refers to replicating objects to a bucket that resides in another region, such as copying objects from the Beijing region to the Guangzhou region.
>- Copying objects from Finance Cloud regions to Public Cloud regions (and vice versa) is not supported as they are not interconnected.

```java
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";

COSCredentials credentials = new BasicCOSCredentials(secretId, secretKey);

// Region of the source bucket
Region srcBucketRegion = new Region("COS_SRC_REGION");
Region destBucketRegion = new Region("COS_DEST_REGION");

// Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "sourcebucket-1250000000";
// The source file to copy
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of `BucketName-APPID`.

String destBucketName = "examplebucket-1250000000";
// Destination file
String destKey = "exampleobject";

// transferManager uses the destination file’s cosclient.
COSClient destCOSClient = new COSClient(cred, new ClientConfig(destBucketRegion));
ExecutorService threadPool = Executors.newFixedThreadPool(5);
// Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
TransferManager transferManager = new TransferManager(destCOSClient, threadPool);

// Generate srcCOSClient to get source file information.
COSClient srcCOSClient = new COSClient(cred, new ClientConfig(srcBucketRegion));

try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // Return an asynchronous result "copy". You can synchronously call waitForCopyResult to wait for the replication to end. If the replication is successful, CopyResult is returned; otherwise, an exception will be thrown.
    CopyResult copyResult = copy.waitForCopyResult();
    // Get the CRC64 value of the replicated object.
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

#### Sample 3. Async replication
```java
// You can log in to the CAM console to view and manage SECRETID and SECRETKEY.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
// Region of the source bucket
COSCredentials credentials = new BasicCOSCredentials(secretId, secretKey);
Region bucketRegion = new Region("COS_REGION");

// Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "sourcebucket-1250000000";
// The source file to copy
String srcKey = "sourceObject";
// Enter the destination bucket name in the format of `BucketName-APPID`.

String destBucketName = "examplebucket-1250000000";
// Destination file
String destKey = "exampleobject";

COSClient cosClient = new COSClient(credentials, new ClientConfig(bucketRegion));

ExecutorService threadPool = Executors.newFixedThreadPool(5);
// Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
final TransferManager transferManager = new TransferManager(cosClient, threadPool);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);

try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // Determine whether the async replication is completed in a child thread.
    new Thread(){
        @Override
        public void run() {
            while(!copy.isDone()) {
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println("wait for copy done");
            }
            transferManager.shutdownNow();
        };
    }.start();
    // Proceed with other logic
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
| copyObjectRequest | Object copy request | CopyObjectRequest |

The request members are described as follows:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default value: the value of "region" in `clientconfig`, meaning intra-region replication | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file. | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID` | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Returned values

- Success: returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Uploading multiple objects

#### Description

This API is used to upload all files in a folder.

#### Method prototype

```java
public MultipleFileUpload uploadDirectory(String bucketName, String virtualDirectoryKeyPrefix,
            File directory, boolean includeSubdirectories);
```

#### Sample request
[//]: # ".cssg-snippet-transfer-upload-directory"
```java
// Write the callback function to print the upload progress.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// Set the prefix of the directory to upload the objects to. If this parameter is set to “”, objects will be uploaded to the root directory of the bucket.
String cos_path = "/prefix";
// Absolute path of the folder to upload
String dir_path = "/to/mydir";
// Whether to upload subdirectories in the folder recursively. If this parameter is set to “true”, objects in subdirectories will also be uploaded with the original directory structure retained.
Boolean recursive = false;

try {
    // Return an asynchronous result “Upload”. You can synchronously call waitForUploadResult to wait for the upload to end. If the upload is successful, UploadResult is returned; otherwise, an exception will be thrown.
    MultipleFileUpload upload = transferManager.uploadDirectory(bucketName, cos_path, new File(dir_path), recursive);

    // You can view the upload progress.
    // You can call this function via a child thread, but be sure to start the child thread before `waitForCompletion`, otherwise you will not see the progress because the upload is completed.
    showTransferProgress(upload);

    // You can also wait for the upload to complete.
    upload.waitForCompletion();

    System.out.println("upload directory done.");
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
| ------------------------- | -------------------- | ---------------- |
| bucketName                | Name of the bucket in COS | GetObjectRequest |
| virtualDirectoryKeyPrefix | Prefix of the objects in COS | String           |
| directory                 | Absolute path of the folder to upload | File             |
| includeSubDirectory       | Whether to upload subdirectories recursively | Boolean          |

#### Returned values

- Success: returns MultipleFileUpload. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Downloading multiple objects

#### Description

This API is used to download objects that have a specified prefix.

#### Method prototype

```java
public MultipleFileDownload downloadDirectory(String bucketName, String keyPrefix,
        File destinationDirectory) {
```

#### Sample request
[//]: # ".cssg-snippet-transfer-upload-directory"
```java
// Write the progress callback function.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// Set the prefix of objects to download (similar to downloading a folder in COS). If this parameter is set to “”, the entire bucket will be downloaded.
String cos_path = "/prefix";
// Absolute path of the destination folder
String dir_path = "/to/mydir";

try {
    // Return an asynchronous result “download”. You can synchronously call waitForUploadResult to wait for the download to end.
    MultipleFileDownload download = transferManager.downloadDirectory(bucketName, cos_path, new File(dir_path));

    // You can view the download progress.
    // You can call this function via a child thread, but be sure to start the child thread before `waitForCompletion`, otherwise you will not see the progress because the download is completed.
    showTransferProgress(download);

    // You can also wait for the upload to complete.
    download.waitForCompletion();

    System.out.println("download directory done.");
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

transferManager.shutdownNow();
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | Name of the bucket in COS | GetObjectRequest |
| keyPrefix                 | Prefix of the objects in COS  | String           |
| destinationDirectory      | Absolute path of the destination directory | File             |

#### Returned values

- Success: returns MultipleFileUpload. You can query whether the download is complete, or wait until the download is finished.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Deleting a folder and the files contained

COS does not have folders, but users can use slashes (/) as the delimiter to stimulate folders.

In COS, deleting a folder and the objects contained actually means deleting objects that have the same specified prefix. Currently, COS’s Java SDK does not provide a standalone API to perform this operation. However, you can still do so with a combination of basic operations (**query object list** and **batch delete objects**).


#### Sample request

```java
// For batch delete
public void delete(ArrayList<DeleteObjectsRequest.KeyVersion> keyList) {
    DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
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
}

// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// "prefix" indicates the directory to delete.
listObjectsRequest.setPrefix("images/");
// Set the delimiter to "/" to list objects in the current directory. To list all objects, leave it empty.
listObjectsRequest.setDelimiter("/");
// Set the maximum number of traversed objects (up to 1,000 per listobject request)
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;

do {
    // Set the list of keys to be deleted. A maximum of 1,000 keys can be deleted at a time.
    ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();

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
        keyList.add(new DeleteObjectsRequest.KeyVersion(key));
    }

    try {
        delete(keyList);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());

```

### Moving an object

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Java SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” path that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to `doc/picture.jpg` and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.


#### Sample request

```java
// Intra-region replication. You can refer to the “copying an object” request sample.
public void copySameRegion(String srcBucket, String srcKey, String destBucket, String destKey) {
    CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucket, srcKey, destBucket, destKey);
    CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
}

// Cross-region replication. You can refer to the “copying an object” request sample.
public void copyDiffRegion(String srcRegion, String srcBucket, String srcKey,
        String destRegion, String destBucket, String destKey){
    CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucket, srcKey, destBucketName, destKey);
    CopyObjetResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
}

// Information about the source object to move
String srcRegion = "ap-shanghai";
String srcBucket = "mybucket-1250000000";
String srcKey = "picture.jpg";

// Information about the destination object
String destRegion = "ap-shanghai";
String destBucket = "myanotherbucket-1250000000";
String destKey = "doc/picture.jpg";

// The following uses intra-region replication as an example. You can use cross-region replication as needed.
copySameRegion(srcBcuket, srcKey, destBucket, destKey);

// Information about the source object to delete after the replication
cosClient.deleteObject(srcBucket, srcKey);
```
