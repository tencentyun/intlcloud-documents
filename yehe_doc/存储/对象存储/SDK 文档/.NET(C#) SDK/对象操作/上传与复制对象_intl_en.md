## Overview

This document provides an overview of APIs and SDK sample codes related to uploading and replicating objects.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using HTML form | Uploads an object using HTML form |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |

**Multipart operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Queries multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in multipart upload |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts |  Queries the uploaded parts of a specific multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (recommended)

### Uploading an object

The advanced upload API encapsulates both PUT Object (simple upload) and multipart upload APIs, and can automatically select the upload method based on file size. It also supports checkpoint restart for resuming a suspended multipart upload.

#### Sample 1. Uploading a local file

[//]: # (.cssg-snippet-transfer-upload-file)
```cs
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
String cosPath = "exampleobject"; // Identifier of the object in the bucket, i.e., the object key
String srcPath = @"temp-source-file";// Absolute path to the local file

// An object to upload
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath);
uploadTask.SetSrcPath(srcPath);

uploadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = await 
    transferManager.UploadAsync(uploadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample 2. Uploading binary data

[//]: # (.cssg-snippet-transfer-upload-bytes)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string cosPath = "exampleobject"; // Object key
  byte[] data = new byte[1024]; // Binary data
  PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
  
  cosXml.PutObject(putObjectRequest);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample 3. Suspending, resuming and canceling an upload

To suspend an upload, use the code below:

[//]: # (.cssg-snippet-transfer-upload-pause)
```cs
uploadTask.Pause();
```

To resume a suspended download, run the code below:

[//]: # (.cssg-snippet-transfer-upload-resume)
```cs
uploadTask.Resume();
```

To cancel an upload, run this code:

[//]: # (.cssg-snippet-transfer-upload-cancel)
```cs
uploadTask.Cancel();
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).

#### Sample 4. Uploading multiple objects

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID

for (int i = 0; i < 5; i++) {
  // A set of objects to upload
  string cosPath = "exampleobject" + i; // The location identifier of an object in the bucket, i.e. the object key
  string srcPath = @"temp-source-file";// Absolute path to the local file
  COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath); 
  uploadTask.SetSrcPath(srcPath);
  await transferManager.UploadAsync(uploadTask);
}
```

#### Sample 5. Creating a directory

[//]: # (.cssg-snippet-create-directory)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string cosPath = "dir/"; // Object key
  PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, new byte[0]);
  
  cosXml.PutObject(putObjectRequest);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Copying an object

The advanced replication API encapsulates PUT Object - Copy, and the APIs for multipart replication to allow asynchronous requests for suspending, resuming and canceling a replication request.

#### Sample code

[//]: # (.cssg-snippet-transfer-copy-object)
```cs
string sourceAppid = "1250000000"; // Account APPID
string sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
string sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
string sourceKey = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; // Destination bucket in the format: BucketName-APPID
string key = "exampleobject"; // Key of the destination object

COSXMLCopyTask copytask = new COSXMLCopyTask(bucket, key, copySource);

try {
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copytask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferCopyObject.cs).

## Simple Operations

### Uploading an object using simple upload

#### API description 

This API is used to upload an object to a specified bucket. This operation requires the requester to have WRITE permission for the bucket and can upload a file of up to 5 GB in size. To upload larger objects, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [the advanced upload API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

> !
> 1. The Key (file name) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Each root account (APPID) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need ACL control over an object, please leave it to the default option of inheriting bucket permissions.

#### Sample code

[//]: # (.cssg-snippet-put-object)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string srcPath = @"temp-source-file";// Absolute path to the local file

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PutObjectResult result = cosXml.PutObject(request);
  // Object Etag
  string eTag = result.eTag;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PutObject.cs).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Uploading an object using HTML form

#### API description 

This API is used to upload an object using an HTML form.

#### Sample code

[//]: # (.cssg-snippet-post-object)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string srcPath = @"temp-source-file";// Absolute path to the local file
  PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PostObjectResult result = cosXml.PostObject(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PostObject.cs).

### Copying an object (modifying object attributes)

This API is used to copy a file to a destination path.

#### Sample 1. Copying an object while retaining its attributes

[//]: # (.cssg-snippet-copy-object)
```cs
try
{
  string sourceAppid = "1250000000"; // Account APPID
  string sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
  string sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
  string sourceKey = "sourceObject"; // Key of the source object
  // Construct the source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Copy);
  // Execute the request
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs).

#### Sample 2. Copying an object while replacing its attributes

[//]: # (.cssg-snippet-copy-object-replaced)
```cs
try
{
  string sourceAppid = "1250000000"; // Account APPID
  string sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
  string sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
  string sourceKey = "sourceObject"; // Key of the source object
  // Construct the source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Replace metadata
  request.SetRequestHeader("Content-Disposition", "attachment; filename=example.jpg");
  // Execute the request
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs).

#### Sample 3. Modifying object metadata

[//]: # (.cssg-snippet-modify-object-metadata)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string appId = "1250000000"; // Account APPID
  string region = "COS_REGION"; // Region where the bucket of the source object resides
  // Construct object attributes
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Replace metadata
  request.SetRequestHeader("Content-Disposition", "attachment; filename=example.jpg");
  request.SetRequestHeader("Content-Type", "image/png");
  // Execute the request
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs).

#### Sample 4. Modifying the storage class of an object

[//]: # (.cssg-snippet-modify-object-storage-class)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string appId = "1250000000"; // Account APPID
  string region = "COS_REGION"; // Region where the bucket of the source object resides
  // Construct object attributes
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Modify the storage class to ARCHIVE
  request.SetCosStorageClass("ARCHIVE");
  // Execute the request
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs).

## Multipart Operations

The multipart operation process is outlined below.

#### How to perform a multipart upload/replication

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload parts with `Upload Part` or copy parts with `Upload Part Copy`
3. Complete the multipart upload with `Complete Multipart Upload`.

#### How to resume a multipart upload/replication

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload with `List Multipart Uploads` to get it.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part` or copy the remaining parts with `Upload Part - Copy`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### How to abort a multipart upload/replication

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload with `List Multipart Uploads` to get it.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart uploads

#### API description 

This API is used to query in-progress multipart uploads in a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-list-multi-upload)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
  // Execute the request
  ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).

### Initializing a multipart upload

#### API description 

This API is used to initialize a multipart upload, and get its uploadId.

#### Sample code

[//]: # (.cssg-snippet-init-multi-upload)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
  // Execute the request
  InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
  // Request succeeded
  this.uploadId = result.initMultipartUpload.uploadId; // The uploadId to use for subsequent multipart uploads
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).

### Uploading a part

This API is used to upload parts in a multipart upload.

#### Sample code

[//]: # (.cssg-snippet-upload-part)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload was initialized
  int partNumber = 1; // Part number that increases starting from 1
  string srcPath = @"temp-source-file";// Absolute path to the local file
  UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, 
    uploadId, srcPath, 0, -1);
  // Set progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  UploadPartResult result = cosXml.UploadPart(request);
  // Request succeeded
  // Return Etag of the part for subsequent CompleteMultiUploads
  this.eTag = result.eTag;
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).

### Copying a part

#### API description 

This API is used to copy an object as a part.

#### Sample code

[//]: # (.cssg-snippet-upload-part-copy)
```cs
try
{
  string sourceAppid = "1250000000"; // Account APPID
  string sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
  string sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
  string sourceKey = "sourceObject"; // Key of the source object
  // Construct the source object attributes
  COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, 
    sourceBucket, sourceRegion, sourceKey);

  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = this.uploadId; // uploadId returned when the multipart upload was initialized
  int partNumber = 1; // Part number that increases starting from 1
  UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, 
    partNumber, uploadId);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set the byte range of an object to copy as a part, e.g., 0 to 1 M
  request.SetCopyRange(0, 1024 * 1024);
  // Execute the request
  UploadPartCopyResult result = cosXml.PartCopy(request);
  // Request succeeded
  // Return Etag of the part for subsequent CompleteMultiUploads
  this.eTag = result.copyPart.eTag;
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsCopyObject.cs).

### Querying uploaded parts

#### API description 

This API is used to query the uploaded parts of a specific multipart upload.

#### Sample code

[//]: # (.cssg-snippet-list-parts)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload was initialized
  ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
  // Execute the request
  ListPartsResult result = cosXml.ListParts(request);
  // Request succeeded
  // List the parts that have been uploaded
  List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).

### Completing a multipart upload

#### API description 

This API is used to complete the multipart upload of an entire file.

#### Sample code
[//]: # (.cssg-snippet-complete-multi-upload)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload was initialized
  CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, 
    key, uploadId);
  // Specify uploaded parts in an ascending order by partNumber
  request.SetPartNumberAndETag(1, this.eTag);
  // Execute the request
  CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).

### Aborting a multipart upload

#### API description 

This API is used to abort a multipart upload and delete the uploaded parts.

#### Sample code

[//]: # (.cssg-snippet-abort-multi-upload)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload was initialized
  AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
  // Execute the request
  AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
  // Request succeeded
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AbortMultiPartsUpload.cs).

