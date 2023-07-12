## Overview

This document provides an overview of APIs and SDK code samples related to object upload.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Uploads an object by appending the object by parts.   |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Uploading an object

#### Description


The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They also support checkpoint restart for resuming interrupted operations.

>?
> - If the file size is less than the multipart upload threshold, simple upload is used. Otherwise, multiple upload is used. The multipart upload threshold is configurable and is 5 MB by default.
> - The part size is configurable and is 1 MB by default.
> - If your .NET Framework version is 4.0 or earlier, advanced APIs are not available. For more information, please see [Backward Compatibility](https://intl.cloud.tencent.com/document/product/436/42378).
> 

#### Sample code 1. Uploading a local object via advanced API

[//]: # ".cssg-snippet-transfer-upload-file"
```cs
using COSXML.Model.Object;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;
using System.Threading.Tasks;

namespace COSSnippet
{
    public class TransferUploadObjectModel {

      private CosXml cosXml;

      TransferUploadObjectModel() {
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

      /// Upload a file via advanced API
      public async Task TransferUploadFile()
      {
        // Initialize TransferConfig
        TransferConfig transferConfig = new TransferConfig();
        // Set the object size threshold for multipart upload to 10 MB. Default value: 5 MB
        transferConfig.DivisionForUpload = 10 * 1024 * 1024;
        // Set the size of each object part for multipart upload to 2 MB. Default value: 1 MB
        transferConfig.SliceSizeForUpload = 2 * 1024 * 1024;
        
        // Initialize TransferManager
        TransferManager transferManager = new TransferManager(cosXml, transferConfig);
        // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
        String bucket = "examplebucket-1250000000"; 
        String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
        String srcPath = @"temp-source-file";// Absolute path to the local file
        
        // Upload an object
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

      }

      static void Main(string[] args)
      {
        TransferUploadObjectModel m = new TransferUploadObjectModel();
        /// Upload an object via advanced API
        m.TransferUploadFile().Wait();
        // .cssg-methods-pragma
      }
    }
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, please see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/38068). Please note that for private-read files, the download URL is only valid for a limited period of time.
>

#### Sample code 2. Uploading binary data

[//]: # ".cssg-snippet-transfer-upload-bytes"
```cs
using COSXML.Model.Object;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;

namespace COSSnippet
{
    public class TransferUploadObjectModel {

      private CosXml cosXml;

      TransferUploadObjectModel() {
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

      /// Upload binary data
      public void TransferUploadBytes()
      {
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string cosPath = "exampleObject"; // Object key
          byte[] data = new byte[1024]; // Binary data
          PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
          // Initiate an upload.
          PutObjectResult result = cosXml.PutObject(putObjectRequest);
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
      }

      static void Main(string[] args)
      {
        TransferUploadObjectModel m = new TransferUploadObjectModel();

        /// Upload binary data via an advanced API
        m.TransferUploadBytes();
      }
    }
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, please see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/38068). Please note that for private-read files, the download URL is only valid for a limited period of time.
>

#### Sample code 3. Uploading with a file stream

[//]: # ".cssg-snippet-transfer-upload-bytes"
```cs
using COSXML.Model.Object;
using COSXML.Utils;
using COSXML.Auth;
using System;
using COSXML;
using System.IO;

namespace COSSnippet
{
    public class PutObjectModel {

      private CosXml cosXml;

      PutObjectModel() {
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
      
      /// Uploading with a file stream, supported from v5.4.24
      public void PutObjectStream()
      {
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          string srcPath = @"temp-source-file";// Absolute path of the local file
          // Open the read-only file stream object
          FileStream fileStream = new FileStream(srcPath, FileMode.Open, FileAccess.Read);
          // Assemble the upload request, where offset sendLength is optional
          long offset = 0L;
          long sendLength = fileStream.Length;
          PutObjectRequest request = new PutObjectRequest(bucket, key, fileStream, offset, sendLength);
          // Set the progress callback
          request.SetCosProgressCallback(delegate (long completed, long total)
          {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
          });
          // Execute the request
          PutObjectResult result = cosXml.PutObject(request);
          // Close the file stream
          fileStream.Close();
          // Object ETag
          string eTag = result.eTag;
          // crc64ecma value of the object
          string crc64ecma = result.crc64ecma;
          // Print the request result.
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
      }

      static void Main(string[] args)
      {
        PutObjectModel m = new PutObjectModel();
        /// Upload the object with a file stream
        m.PutObjectStream();
      }
    }
}
```
>?
> - Uploading with a file stream is supported from v5.4.24. To download the latest version of SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or refer to [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - For the version changelog, see [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/PutObject.cs).
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, please see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/38068). Please note that for private-read files, the download URL is only valid for a limited period of time.
>

#### Sample code 4. Suspending, resuming, and canceling an upload

To suspend an upload, use the code below:

[//]: # ".cssg-snippet-transfer-upload-pause"
```cs
uploadTask.Pause();
```

To resume a suspended download, use the code below:

[//]: # ".cssg-snippet-transfer-upload-resume"
```cs
uploadTask.Resume();
```

To cancel an upload, use the code below:

[//]: # ".cssg-snippet-transfer-upload-cancel"
```cs
uploadTask.Cancel();
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>

#### Sample code 5. Uploading multiple objects

[//]: # ".cssg-snippet-transfer-batch-upload-objects"
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);
// Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";

for (int i = 0; i < 5; i++) {
  // Upload an object
  string cosPath = "exampleobject" + i; // Location identifier of an object in the bucket, i.e. the object key
  string srcPath = @"temp-source-file";// Absolute path of the local file
  COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath); 
  uploadTask.SetSrcPath(srcPath);
  await transferManager.UploadAsync(uploadTask);
}
```

#### Sample 6. Creating a directory

[//]: # ".cssg-snippet-create-directory"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
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
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, please see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/38068). Please note that for private-read files, the download URL is only valid for a limited period of time.
> 


## Simple Operations

### Uploading an object using simple upload

#### Description

This API (PUT Object) is used to upload an object smaller than 5 GB to a specified bucket. To call this API, you need to have permission to write to the bucket. If the object size is larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) for the upload.

>!
> - The key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> - Each root account (`APPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. Do not configure ACLs for an object during upload if you don’t need to control access to it. The object will inherit the permissions of its bucket by default.
> - Due to the limitations of the underlying SDK dependent language components, the general upload API may encounter unexpected exceptions in some environments when it is used to upload objects over 2 GB at a time. Therefore, we recommend you use the [advanced API](https://intl.cloud.tencent.com/document/product/436/38062) or [multipart upload](https://intl.cloud.tencent.com/document/product/436/38062) to avoid potential problems.
> 

#### Sample code

[//]: # ".cssg-snippet-put-object"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string srcPath = @"temp-source-file";// Absolute path of the local file

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  PutObjectResult result = cosXml.PutObject(request);
  // Object ETag
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
>- After the upload, you can generate a download URL for the uploaded file with the same key. For detailed directions, please see [Generating Pre-signed Links](https://intl.cloud.tencent.com/document/product/436/38068). Please note that for private-read files, the download URL is only valid for a limited period of time.
> 

### Uploading an object using an HTML form

#### Description

This API is used to upload an object using an HTML form.

#### Sample code

[//]: # ".cssg-snippet-post-object"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string srcPath = @"temp-source-file";// Absolute path of the local file
  PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
  // Set the progress callback
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PostObject.cs).
>


### Appending parts

#### Description

This API is used to upload an object by appending parts of the object.

>? This feature is supported starting from v5.4.22. For the version changelog, see [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
>

#### Sample code

[//]: # ".cssg-snippet-append-object"
```cs
try
{
    // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
    string bucket = "examplebucket-1250000000";
    string key = "exampleobject"; // Object key
    string srcPath = @"temp-source-file";// Absolute path of the local file

    // Append the first part. 0 is passed in for the appending position, and an appendable object is created
    long next_append_position = 0;
    AppendObjectRequest request = new AppendObjectRequest(bucket, key, srcPath, next_append_position);
    // Set the progress callback
    request.SetCosProgressCallback(delegate (long completed, long total)
    {
        Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
    });
    AppendObjectResult result = cosXml.AppendObject(request);
    // Get the next appending position
    next_append_position = result.nextAppendPosition;
    Console.WriteLine(result.GetResultInfo());

    // Execute appending and pass in the object end obtained last time
    request = new AppendObjectRequest(bucket, key, srcPath, next_append_position);
    request.SetCosProgressCallback(delegate (long completed, long total)
    {
        Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
    });
    result = cosXml.AppendObject(request);
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AppendObject.cs).

## Multipart Operations

The multipart upload process is outlined below.

#### Performing a multipart upload

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload the parts with `Upload Part - Copy`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### Resuming a multipart upload

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### Aborting a multipart upload

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart uploads

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

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

### Initializing a multipart upload

#### Description

This API is used to initialize a multipart upload operation and get its `uploadId`.

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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Uploading parts

#### Description

This API (`Upload Part`) is used to upload an object in parts.

#### Sample code

[//]: # ".cssg-snippet-upload-part"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  int partNumber = 1; // Part number, increases incrementally starting from 1
  string srcPath = @"temp-source-file";// Absolute path of the local file
  UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, 
    uploadId, srcPath, 0, -1);
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  UploadPartResult result = cosXml.UploadPart(request);
  // Request succeeded
  // Get the ETag of the returned part for subsequent CompleteMultiUploads.
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Sample code

[//]: # ".cssg-snippet-list-parts"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Completing a multipart upload

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

#### Sample code
[//]: # ".cssg-snippet-complete-multi-upload"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, 
    key, uploadId);
  // Concatenate uploaded parts in ascending order by partNumber.
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

### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Sample code

[//]: # ".cssg-snippet-abort-multi-upload"
```cs
try
{
  // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
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


