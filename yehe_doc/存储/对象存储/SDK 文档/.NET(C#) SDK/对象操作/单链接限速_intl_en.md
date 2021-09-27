## Overview

This document describes the bandwidth limit on a single connection when calling the COS APIs for upload or download.

## Samples

This limit should have a value in bit/s ranging from **819200 - 838860800**, i.e. 100 KB/s - 100 MB/s. If this range is exceeded, a 400 error will be returned.

#### Sample 1. Single-connection bandwidth limit when uploading

[//]: # (.cssg-snippet-upload-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
string cosPath = "dir/exampleObject"; // Object key
string srcPath = @"temp-source-file";// Absolute path to the local file

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
putObjectRequest.LimitTraffic(8 * 1024 * 1024); // Set the limit to 1 MB/s

COSXMLUploadTask uploadTask = new COSXMLUploadTask(putObjectRequest);

uploadTask.SetSrcPath(srcPath);

await transferManager.UploadAsync(uploadTask);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).

#### Sample 2. Single-connection bandwidth limit when downloading

[//]: # (.cssg-snippet-download-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Specify the name of the file to be saved locally

GetObjectRequest request = new GetObjectRequest(bucket, 
        cosPath, localDir, localFileName);
request.LimitTraffic(8 * 1024 * 1024); // Set the limit to 1 MB/s

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

