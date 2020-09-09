## Overview

This document provides an overview of APIs and SDK sample codes related to object download.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (recommended)

### Downloading an object

The advanced download API uses more encapsulated logic and allows you to suspend, resume (via checkpoint restart), or cancel download requests.

#### Sample 1. Downloading an object
**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Monitor the download result
[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

// Monitor the download progress
[request setDownProcessBlock:^(int64_t bytesDownload,
                               int64_t totalBytesDownload,
                               int64_t totalBytesExpectedToDownload) {
    
    // “bytesDownload” indicates the number of new bytes downloaded
    // “totalBytesDownload” indicates the total number of bytes received in the download
    // “totalBytesExpectedToDownload” indicates the target number of bytes expected to be downloaded
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-download-object)
```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Monitor the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    
    // “bytesDownload” indicates the number of new bytes downloaded
    // “totalBytesDownload” indicates the total number of bytes received in the download
    // “totalBytesExpectedToDownload” indicates the target number of bytes expected to be downloaded
}

// Monitor the download result
request.finishBlock = { (result, error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

#### Sample 2. Suspending, resuming, or canceling a download
**Objective-C**

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```objective-c
[request cancel];
```

To resume a suspended download, use the code below:

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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```swift
request.cancel();
```

To resume a suspended download, use the code below:

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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

#### Sample 3. Downloading multiple objects
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```objective-c
for (int i = 0; i<20; i++) {
    QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
    // Bucket name in the format: `BucketName-APPID`
    request.bucket = @"examplebucket-1250000000";
    
    // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
    request.object = @"exampleobject";
    
    // Set the download URL. Once set, the file will be downloaded to the specified path
    request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];
    
    // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
    request.localCacheDownloadOffset = 100;
    
    // Monitor the download result
    [request setFinishBlock:^(id outputObject, NSError *error) {
        // outputObject contains all the HTTP response headers
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    
    // Monitor the download progress
    [request setDownProcessBlock:^(int64_t bytesDownload,
                                   int64_t totalBytesDownload,
                                   int64_t totalBytesExpectedToDownload) {
        
        // “bytesDownload” indicates the number of new bytes downloaded
        // “totalBytesDownload” indicates the total number of bytes received in the download
        // “totalBytesExpectedToDownload” indicates the target number of bytes expected to be downloaded
    }];
    
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```swift
for i in 1...10 {
    let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
    
    // Bucket name in the format: `BucketName-APPID`
    request.bucket = "examplebucket-1250000000";
    
    // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
    request.object = "exampleobject";
    
    // Set the download URL. Once set, the file will be downloaded to the specified path
    request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
    
    // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
    request.localCacheDownloadOffset = 100;

    // Monitor the download progress
    request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
        totalBytesExpectedToDownload) in
        
        // “bytesDownload” indicates the number of new bytes downloaded
        // “totalBytesDownload” indicates the total number of bytes received in the download
        // “totalBytesExpectedToDownload” indicates the target number of bytes expected to be downloaded
    }

    // Monitor the download result
    request.finishBlock = { (result, error) in
        if let result = result {
            // “result” contains response headers
        } else {
            print(error!);
        }
    }
    
    QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
}
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

## Simple Operations

### Downloading an object

#### API description 

This API is used to download an object to the local file system.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Bucket name in the format: BucketName-APPID
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    
    // Download progress
    // “bytesDownload” indicates the number of downloaded bytes
    // “totalBytesDownload” indicates the total number of bytes received for the download
    // “totalBytesExpectedToDownload” indicates the total number of bytes expected to download

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

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
getObject.object = "exampleobject";
// Set the download URL. Once set, the file will be downloaded to the specified path
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
};
getObject.downProcessBlock = {(bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    // “bytesDownload” indicates the number of downloaded bytes
    // “totalBytesDownload” indicates the total number of bytes received for the download
    // “totalBytesExpectedToDownload” indicates the total number of bytes expected to download
}
QCloudCOSXMLService.defaultCOSXML().getObject(getObject);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/GetObject.swift).

