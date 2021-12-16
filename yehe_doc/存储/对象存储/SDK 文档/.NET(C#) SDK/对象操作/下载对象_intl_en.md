## Overview

This document provides an overview of APIs and SDK code samples related to object downloads.

| API | Operation | Description |
| ------------------------------------------------------------ | -------- | ------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Downloading an object (checkpoint restart)

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.

>? If your .NET Framework version is 4.0 or earlier, advanced APIs are not available. For more information, please see [Backward Compatibility](https://intl.cloud.tencent.com/document/product/436/42378).
> 

#### Sample 1: downloading an object

[//]: #	".cssg-snippet-transfer-download-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using COSXML.Transfer;
using System;
using COSXML;

namespace COSSnippet
{
    public class TransferDownloadObjectModel {

      private CosXml cosXml;

      TransferDownloadObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Download an object via advanced API
      public async void TransferDownloadObject()
      {
        // Initialize TransferConfig
        TransferConfig transferConfig = new TransferConfig();
        
        // Initialize TransferManager
        TransferManager transferManager = new TransferManager(cosXml, transferConfig);
        
        String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
        String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
        string localDir = System.IO.Path.GetTempPath();// Local file directory
        string localFileName = "my-local-temp-file"; // Filename of the local file
        
        // Download an object
        COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
          localDir, localFileName);
        
        downloadTask.progressCallback = delegate (long completed, long total)
        {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
        };

        try {
          COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
            transferManager.DownloadAsync(downloadTask);
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
        TransferDownloadObjectModel m = new TransferDownloadObjectModel();

        /// Download an object via advanced API
        m.TransferDownloadObject();
      }
    }
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 2: setting checkpoint restart for download

[//]: #".cssg-snippet-transfer-download-resumable"

```cs
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
 // Enable checkpoint restart. If an object is not completely downloaded, the download will be started from the checkpoint.
 // If the local file contains content that does not meet the requirements of the current download, the download may fail. You can delete the file and try again.
 downloadTask.SetResumableDownload(true);
 try {
   COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = await 
   transferManager.DownloadAsync(downloadTask);
   Console.WriteLine(result.GetResultInfo());
   string eTag = result.eTag;
 } catch (Exception e) {
   Console.WriteLine("CosException: " + e);
 }
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 3: batch download

[//]: #	".cssg-snippet-transfer-batch-download-objects"

```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

// Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
string localDir = System.IO.Path.GetTempPath();// Local file directory

for (int i = 0; i < 5; i++) {
  // Download an object
  string cosPath = "exampleobject" + i; // Location identifier of an object in the bucket, i.e. the object key
  string localFileName = "my-local-temp-file"; // Filename of the local file
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
    localDir, localFileName);
  await transferManager.DownloadAsync(downloadTask);
}
```
>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

#### Sample 4: limiting single-URL download speed
[//]: #".cssg-snippet-transfer-download-objects-with-speed-limit"
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Filename of the local file
        
GetObjectRequest request = new GetObjectRequest(bucket, 
        cosPath, localDir, localFileName);
request.LimitTraffic(8 * 1000 * 1024); // Limit the speed to 1 MB/s.

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```


>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).
>

## Simple Operations

### Downloading an object

#### Description

This API is used to download an object to the local file system.

#### Sample 1: simple download of a single object

[//]: #	".cssg-snippet-get-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetObjectModel {

      private CosXml cosXml;

      GetObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224. 
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Download an object
      public void GetObject()
      {
        //.cssg-snippet-body-start:[get-object]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          string localDir = System.IO.Path.GetTempPath();// Local file directory
          string localFileName = "my-local-temp-file"; // Filename of the local file
          GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
          // Set the progress callback
          request.SetCosProgressCallback(delegate (long completed, long total)
          {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
          });
          // Execute the request
          GetObjectResult result = cosXml.GetObject(request);
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
      }

      static void Main(string[] args)
      {
        GetObjectModel m = new GetObjectModel();
        /// Download an object
        m.GetObject();
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).
>

#### Sample 2: downloading an object to memory

[//]: #".cssg-snippet-get-object"

```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetObjectModel {

      private CosXml cosXml;

      GetObjectModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224. 
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Download the returned bytes data
      public void downloadToMem() {
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
        
          GetObjectBytesRequest request = new GetObjectBytesRequest(bucket, key);
          // Set the progress callback
          request.SetCosProgressCallback(delegate (long completed, long total)
          {
            Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
          });
          // Execute the request
          GetObjectBytesResult result = cosXml.GetObject(request);
          // Get content for the byte array
          byte[] content = result.content;
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
      }

      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        GetObjectModel m = new GetObjectModel();

        /// Download the object to memory
        m.downloadToMem();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).
>
