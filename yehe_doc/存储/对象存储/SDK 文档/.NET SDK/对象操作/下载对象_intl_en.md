## Overview

This document provides an overview of APIs and SDK sample codes related to object download.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (recommended)

### Downloading an object

The advanced download API is used to suspend, resume (checkpoint restart), and cancel a download request.

#### Sample 1. Downloading an object

[//]: # (.cssg-snippet-transfer-download-object)
```cs
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally

// Download an object
 // COS_REGION is the bucket region
COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, "COS_REGION", cosPath, 
  localDir, localFileName);

// Sync invocation
var autoEvent = new AutoResetEvent(false);

downloadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};
downloadTask.successCallback = delegate (CosResult cosResult) 
{
    COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult result = cosResult 
      as COSXML.Transfer.COSXMLDownloadTask.DownloadTaskResult;
    Console.WriteLine(result.GetResultInfo());
    string eTag = result.eTag;
    autoEvent.Set();
};
downloadTask.failCallback = delegate (CosClientException clientEx, CosServerException serverEx) 
{
    if (clientEx != null)
    {
        Console.WriteLine("CosClientException: " + clientEx);
    }
    if (serverEx != null)
    {
        Console.WriteLine("CosServerException: " + serverEx.GetInfo());
    }
    autoEvent.Set();
};
transferManager.Download(downloadTask);
// Wait for the download to complete
autoEvent.WaitOne();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

#### Sample 2. Suspending, resuming, or canceling a download

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```cs
downloadTask.Pause();
```

To resume a suspended download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-resume)
```cs
downloadTask.Resume();
```

To cancel a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```cs
downloadTask.Cancel();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

#### Sample 3. Downloading multiple objects

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string bucket = "examplebucket-1250000000"; // Bucket in the format: `BucketName-APPID`
string localDir = System.IO.Path.GetTempPath();// Local file directory

for (int i = 0; i < 5; i++) {
  // Download a set of objects
  String cosPath = "exampleobject"; // The location identifier of an object in the bucket, i.e. the object key
  string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally
  // COS_REGION is the bucket region
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, "COS_REGION", cosPath, 
    localDir, localFileName);
  transferManager.Download(downloadTask);
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

## Simple Operations

### Downloading an object

#### API description 

This API is used to download an object to the local file system.

#### Sample code

[//]: # (.cssg-snippet-get-object)
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket in the format: `BucketName-APPID`
  string key = "exampleobject"; // Object key
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Specifies the name of the file to be saved locally
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  // Set the validity period of the signature
  request.SetSign(TimeUtils.GetCurrentTime(TimeUnit.SECONDS), 600);
  // Set progress callback
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
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).

