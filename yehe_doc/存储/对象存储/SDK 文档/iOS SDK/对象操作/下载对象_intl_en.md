## Overview

This document provides an overview of APIs and SDK sample codes related to object download.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API Reference

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Downloading an object

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.

#### Sample 1. Downloading an object
**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Monitor the download result
[request setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

// Monitor the download progress
[request setDownProcessBlock:^(int64_t bytesDownload,
                               int64_t totalBytesDownload,
                               int64_t totalBytesExpectedToDownload) {
    
    // bytesDownload                   Number of new bytes downloaded
    // totalBytesDownload              Total number of bytes received in the download
    // totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-download-object)
```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Monitor the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    
    //      bytesDownload                   Number of new bytes downloaded
    // totalBytesDownload              Total number of bytes received in the download
    // totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
}

// Monitor the download result
request.finishBlock = { (result, error) in
    if let result = result {
        // "result" contains response headers.
    } else {
        print(error!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

#### Sample code 2: Suspending, resuming, or cancelling a download
**Objective-C**

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```objective-c
[request cancel];
```

To resume a suspended download, run the code below:

[//]: # (.cssg-snippet-transfer-download-object-resume)
```objective-c
// Size of the downloaded part of the file
int64_t localCacheDownloadOffset = 0;
request.localCacheDownloadOffset = localCacheDownloadOffset;
```

To cancel a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```objective-c
undefined
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```swift
request.cancel();
```

To resume a suspended download, run the code below:

[//]: # (.cssg-snippet-transfer-download-object-resume)
```swift
// Size of the downloaded part of the file

let localCacheDownloadOffset = 100;
request.localCacheDownloadOffset = Int64(localCacheDownloadOffset);
```

To cancel a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```swift
undefined
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

#### Sample code 3: Resumable download
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```objective-c
   QCloudCOSXMLDownloadObjectRequest *getObjectRequest = [[QCloudCOSXMLDownloadObjectRequest alloc] init];
    // Enable resumable download. Resumable download is disabled by default
    getObjectRequest.resumableDownload = true;
    // Bucket name in the format: `BucketName-APPID`
    getObjectRequest.bucket = transferTestBucket.name;
    // Set the download URL. Once set, the file will be downloaded to the specified path
    getObjectRequest.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
    // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
    getObjectRequest.object = put.object;
    // Monitor the download result
    [getObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
        // `outputObject` contains all the HTTP response headers
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    
    // Monitor the download progress
    [getObjectRequest setDownProcessBlock:^(int64_t bytesDownload,
                                   int64_t totalBytesDownload,
                                   int64_t totalBytesExpectedToDownload) {
        
        // bytesDownload                   Number of new bytes downloaded
        // totalBytesDownload              Total number of bytes received in the download
        // totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
    }];
    
    [[QCloudCOSTransferMangerService costransfermangerServiceForKey:kHTTPServiceKey] DownloadObject:getObjectRequest];
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```swift
        let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
        // Bucket name in the format: `BucketName-APPID`
        request.bucket = "examplebucket-1250000000";
        
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
        request.object = "exampleobject";
        
        request.resumableDownload = true;
        // Set the download URL. Once set, the file will be downloaded to the specified path
        request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
        
        // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
        request.localCacheDownloadOffset = 100;

        // Monitor the download progress
        request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
            totalBytesExpectedToDownload) in
            
            //      bytesDownload                   Number of new bytes downloaded
            // totalBytesDownload              Total number of bytes received in the download
            // totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
        }

        // Monitor the download result
        request.finishBlock = { (result, error) in
            if let result = result {
                // "result" contains response headers.
            } else {
                print(error!);
            }
        }
        
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

#### Sample code 3: Batch download
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```objective-c
for (int i = 0; i<20; i++) {
    QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
    // Bucket name in the format: `BucketName-APPID`
    request.bucket = @"examplebucket-1250000000";
    
   // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
    request.object = @"exampleobject";
    
    // Set the download URL. Once set, the file will be downloaded to the specified path
    request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];
    
    // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
    request.localCacheDownloadOffset = 100;
    
    // Monitor the download result
    [request setFinishBlock:^(id outputObject, NSError *error) {
        // `outputObject` contains all the HTTP response headers
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    
    // Monitor the download progress
    [request setDownProcessBlock:^(int64_t bytesDownload,
                                   int64_t totalBytesDownload,
                                   int64_t totalBytesExpectedToDownload) {
        
        // bytesDownload                   Number of new bytes downloaded
        // totalBytesDownload              Total number of bytes received in the download
        // totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
    }];
    
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
}
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```swift
for i in 1...10 {
    let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
    
    // Bucket name in the format: `BucketName-APPID`
    request.bucket = "examplebucket-1250000000";
    
    // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
    request.object = "exampleobject";
    
    // Set the download URL. Once set, the file will be downloaded to the specified path
    request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
    
    // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
    request.localCacheDownloadOffset = 100;

    // Monitor the download progress
    request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
        totalBytesExpectedToDownload) in
        
        //      bytesDownload                   Number of new bytes downloaded
        // totalBytesDownload              Total number of bytes received in the download
        // totalBytesExpectedToDownload    Target number of bytes expected to be downloaded
    }

    // Monitor the download result
    request.finishBlock = { (result, error) in
        if let result = result {
            // "result" contains response headers.
        } else {
            print(error!);
        }
    }
    
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

## Simple Operations

### Downloading an object

#### Feature description

This API is used to download an object to the local file system.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    
    // Download progress
    // bytesDownload       Number of downloaded bytes
    // totalBytesDownload  Total number of bytes received for the download
    // totalBytesExpectedToDownload Total number of bytes in the file

}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/GetObject.m).

**Swift**

[//]: # (.cssg-snippet-get-object)
```swift
let getObject = QCloudGetObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
getObject.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getObject.object = "exampleobject";
// Set the download URL. Once set, the file will be downloaded to the specified path
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if let result = result {
        // "result" contains response headers.
    } else {
        print(error!);
    }
};
getObject.downProcessBlock = {(bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    // bytesDownload       Number of downloaded bytes
    // totalBytesDownload  Total number of bytes received for the download
    // totalBytesExpectedToDownload Total number of bytes in the file
}
QCloudCOSXMLService.defaultCOSXML().getObject(getObject);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/GetObject.swift).
