## Overview

This document describes how to limit the speed on a single URL when calling the upload or download API.

## Use Instructions

The speed range is **819200 to 838860800** (in bit/s), that is, 100 KB/s to 100 MB/s. If a value is not within this range, 400 will be returned.

#### Sample 1: limiting single-URL speed on uploads

[//]: # (.cssg-snippet-upload-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
string cosPath = "dir/exampleObject"; // Object key
string srcPath = @"temp-source-file";// Absolute path of the local file

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
putObjectRequest.LimitTraffic(8 * 1024 * 1024); // Limit the speed to 1 MB/s.

COSXMLUploadTask uploadTask = new COSXMLUploadTask(putObjectRequest);

uploadTask.SetSrcPath(srcPath);

await transferManager.UploadAsync(uploadTask);
```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).

#### Sample 2: limiting single-URL speed on downloads

[//]: # (.cssg-snippet-download-object-traffic-limit)
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

// Bucket name in the format of bucketname-APPID. You can get APPID by referring to https://console.cloud.tencent.com/developer.
string bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
string localDir = System.IO.Path.GetTempPath();// Local file directory
string localFileName = "my-local-temp-file"; // Filename of the local file

GetObjectRequest request = new GetObjectRequest(bucket, 
        cosPath, localDir, localFileName);
request.LimitTraffic(8 * 1024 * 1024); // Limit the speed to 1 MB/s.

COSXMLDownloadTask downloadTask = new COSXMLDownloadTask(request);
await transferManager.DownloadAsync(downloadTask);
```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferDownloadObject.cs).

