## Overview

This document provides an overview of APIs and SDK code samples related to object downloads.

| API | Operation | Description |
| ------------------------------------------------------------ | -------- | ------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Downloading an object (checkpoint restart)

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.

#### Sample 1: downloading an object

[//]: #	".cssg-snippet-transfer-download-object"

```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally

// Download an object.
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
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

#### Sample 2: setting checkpoint restart for downloads

[//]: #	".cssg-snippet-transfer-download-resumable"

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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

#### Sample 3: batch downloads

[//]: #	".cssg-snippet-transfer-batch-download-objects"

```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
string localDir = System.IO.Path.GetTempPath();// Local file directory

for (int i = 0; i < 5; i++) {
  // Download an object.
  string cosPath = "exampleobject" + i; // Location identifier of the object in the bucket, i.e., the object key
  string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally
  COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(bucket, cosPath, 
    localDir, localFileName);
  await transferManager.DownloadAsync(downloadTask);
}
```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

## Simple Operations

### Downloading an object

#### Description

This API is used to download an object to the local file system.

#### Sample code

[//]: #	".cssg-snippet-get-object"

```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string localDir = System.IO.Path.GetTempPath();// Local file directory
  string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally
  GetObjectRequest request = new GetObjectRequest(bucket, key, localDir, localFileName);
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request
  GetObjectResult result = cosXml.GetObject(request);
  // Request successful
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

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetObject.cs).
