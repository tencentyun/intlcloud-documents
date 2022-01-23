## Overview

This document provides an overview of APIs and SDK code samples related to object copy and movement.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying parts | Queries in-progress parts. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a part | Initializes a part. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying copied/uploaded parts | Queries the copied/uploaded parts of a multipart operation. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload/copy | Completes the multipart upload/copy of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload/copy | Aborts a multipart operation and deletes the uploaded/copied parts. |


## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Copying objects

#### Description

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

>?
> - If the object size is less than the multipart copy threshold, simple copy is used. Otherwise, multiple copy is used. The multipart copy threshold is configurable and is 5 MB by default.
> - The part size is configurable and is 2 MB by default.
> 

#### Sample code

[//]: # ".cssg-snippet-transfer-copy-object"
```cs
using COSXML.Model.Tag;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;
using System.Threading.Tasks;

namespace COSSnippet
{
    public class TransferCopyObjectModel {

      private CosXml cosXml;

      TransferCopyObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Copy an object via advanced API
      public async Task TransferCopyObject()
      {
        TransferConfig transferConfig = new TransferConfig();
        // Manually set the multipart copy threshold. If the object size is less than the threshold, simple copy is used. Otherwise, multipart copy is used. If no value is specified, the default value 5 MB is used.
        transferConfig.DdivisionForCopy = 5242880;
        // Manually set the automatic part size for the advanced API. If no value is specified, the default value 2 MB is used.
        transferConfig.SliceSizeForCopy = 2097152;
        
        // Initialize TransferManager
        TransferManager transferManager = new TransferManager(cosXml, transferConfig);

        string sourceAppid = "1250000000"; // Account appid
        string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
        string sourceRegion = "COS_REGION"; // Source object bucket region
        string sourceKey = "sourceObject"; // Source object key
        // Construct source object attributes
        CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
            sourceRegion, sourceKey);

        string bucket = "examplebucket-1250000000"; // Destination bucket in the format of BucketName-APPID
        string key = "exampleobject"; // Object key of the destination bucket

        COSXMLCopyTask copytask = new COSXMLCopyTask(bucket, key, copySource);
        
        try {
          COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
            transferManager.CopyAsync(copytask);
          Console.WriteLine(result.GetResultInfo());
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
        
      }

      static void Main(string[] args)
      {
        TransferCopyObjectModel m = new TransferCopyObjectModel();

        /// Copy an object via advanced API
        m.TransferCopyObject().Wait();
      }
    }
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferCopyObject.cs).
>

## Simple Operations

### Copying an object (modifying object attributes)

#### Description

This API (`PUT Object - Copy`) is used to copy a file to a destination path. You can set and modify object attributes and metadata in the copy request. The API also supports in-situ copy, which allows you to modify object metadata where it is.


#### Sample code 1. Copying an object with its attributes preserved

[//]: # ".cssg-snippet-copy-object"
```cs
try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs).
>

#### Sample code 2. Modifying the storage class of an object

>?
> - You can change the storage class of an object from STANDARD to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE. 
> - To change ARCHIVE or DEEP ARCHIVE to other storage classes, you need to call [PostRestore](https://intl.cloud.tencent.com/document/product/436/38066) to restore objects in ARCHIVE or DEEP ARCHIVE first before calling this API. 
> - For more details about storage classes, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).
> 

[//]: # ".cssg-snippet-modify-object-storage-class"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string appId = "1250000000"; // Account APPID
  string region = "COS_REGION"; // Region where the bucket of the source object resides
  // Construct object attributes
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Change the storage class to ARCHIVE
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs).

#### Sample code 3. Copying an object while replacing its attributes

[//]: # ".cssg-snippet-copy-object-replaced"
```cs
try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs).
>

#### Sample code 4. Modifying object metadata

[//]: # ".cssg-snippet-modify-object-metadata"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string appId = "1250000000"; // Account APPID
  string region = "COS_REGION"; // Region where the bucket of the source object resides
  // Construct object attributes
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs).
>


### Moving an object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS .NET SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.



#### Sample code

[//]: #	".cssg-snippet-move-object"

```cs
string sourceAppid = "1250000000"; // Account APPID
// Name of the bucket where the source object resides, in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string sourceBucket = "sourcebucket-1250000000";
string sourceRegion = "COS_REGION"; // Source object bucket region
string sourceKey = "sourceObject"; // Source object key
// Construct source object attributes
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

// Name of destination bucket, in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
string key = "exampleobject"; // Object key of the destination bucket

COSXMLCopyTask copyTask = new COSXMLCopyTask(bucket, key, copySource);

try {
  // Copy the object.
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copyTask);
  Console.WriteLine(result.GetResultInfo());

  // Delete the object.
  DeleteObjectRequest request = new DeleteObjectRequest(sourceBucket, sourceKey);
  DeleteObjectResult deleteResult = cosXml.DeleteObject(request);
  // Print results.
  Console.WriteLine(deleteResult.GetResultInfo());
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

> ?For more samples, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MoveObject.cs).


## Multipart Operations

This section describes the process of multipart copy. COS APIs `InitiateMultipartUpload`, `UploadPart/UploadPartCopy`, and `CompleteMultipartUpload APIs can be used for both multipart upload and multipart copy. Therefore, there is a certain degree of overlap between the APIs and usages between multipart copy and multipart upload.

#### Performing a multipart copy

1. Initialize parts with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to copy the parts with `Upload Part - Copy`.
3. Complete the multipart copy with `Complete Multipart Upload`.

#### Continuing the multipart copy

1. If you did not record the `UploadId` of the multipart copy, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the copied parts with `List Parts`.
3. Use the `UploadId` to copy the remaining parts with `Upload Part - Copy`.
4. Complete the multipart copy with `Complete Multipart Upload`.

#### Aborting a multipart copy

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart copy and delete the copied parts with `Abort Multipart Upload`.

### Querying multipart copies

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart copies in a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-list-multi-upload"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Initializing a multipart copy

#### Description

This API (`Initiate Multipart Upload`) is used to initialize a multipart copy operation and get its `uploadId`.

#### Sample code

[//]: # ".cssg-snippet-init-multi-upload"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
  // Execute the request
  InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
  // Request succeeded
  this.uploadId = result.initMultipartUpload.uploadId; // The `uploadId` to use for subsequent multipart copies
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Copying an object part

#### Description

This API (`Upload Part - Copy`) is used to copy an object as a part.

#### Sample code

[//]: # ".cssg-snippet-upload-part-copy"
```cs
try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct source object attributes
  COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, 
    sourceBucket, sourceRegion, sourceKey);

  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = this.uploadId; // `uploadId` returned when the multipart upload/copy is initialized
  int partNumber = 1; // Part number, increases incrementally starting from 1
  UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, 
    partNumber, uploadId);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set the range of parts to be copied, e.g., 0 to 1M
  request.SetCopyRange(0, 1024 * 1024);
  // Execute the request
  UploadPartCopyResult result = cosXml.PartCopy(request);
  // Request succeeded
  // Get the ETag of the returned part for subsequent CompleteMultiUploads.
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsCopyObject.cs).
>

### Querying copied parts

#### Description

This API (`List Parts`) is used to query the copied parts of a multipart copy.

#### Sample code

[//]: # ".cssg-snippet-list-parts"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // `uploadId` returned when the multipart upload/copy is initialized
  ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
  // Execute the request
  ListPartsResult result = cosXml.ListParts(request);
  // Request succeeded
  // List uploaded/copied parts
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Completing a multipart copy

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart copy of a file.

#### Sample code
[//]: # ".cssg-snippet-complete-multi-upload"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // `uploadId` returned when the multipart upload/copy is initialized
  CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, 
    key, uploadId);
  // Concatenate copied parts in ascending order by `partNumber`.
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Aborting a multipart copy

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart copy and delete the copied parts.

#### Sample code

[//]: # ".cssg-snippet-abort-multi-upload"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // `uploadId` returned when the multipart upload/copy is initialized
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AbortMultiPartsUpload.cs).
>

