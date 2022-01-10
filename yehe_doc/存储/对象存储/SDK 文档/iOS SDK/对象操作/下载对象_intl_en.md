## Overview

This document provides an overview of APIs and SDK code samples related to object downloads.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Download an object

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.


#### Sample code 1. Downloading a single object

**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
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

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Monitor the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    
    // bytesDownload                   Number of new bytes downloaded
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

#### Sample code 2. Suspending, resuming, or canceling a download
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
[request cancel];
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

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
request.cancel();
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).

#### Sample code 3. Resumable download
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-resumable)
```objective-c
   QCloudCOSXMLDownloadObjectRequest *getObjectRequest = [[QCloudCOSXMLDownloadObjectRequest alloc] init];
    // Enable resumable download. Resumable download is disabled by default
    getObjectRequest.resumableDownload = true;
    // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    getObjectRequest.bucket = transferTestBucket.name;
    // Set the download URL. Once set, the file will be downloaded to the specified path
    getObjectRequest.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
    // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
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
        
        // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        request.bucket = "examplebucket-1250000000";
        
        // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
        request.object = "exampleobject";
        
        request.resumableDownload = true;
        // Set the download URL. Once set, the file will be downloaded to the specified path
        request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
        
        // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
        request.localCacheDownloadOffset = 100;

        // Monitor the download progress
        request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
            totalBytesExpectedToDownload) in
            
            // bytesDownload                   Number of new bytes downloaded
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

#### Sample code 4. Batch download
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```objective-c
for (int i = 0; i<20; i++) {
    QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
    // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    request.bucket = @"examplebucket-1250000000";
    
   // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
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
    
    // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    request.bucket = "examplebucket-1250000000";
    
    // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
    request.object = "exampleobject";
    
    // Set the download URL. Once set, the file will be downloaded to the specified path
    request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;
    
    // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
    request.localCacheDownloadOffset = 100;

    // Monitor the download progress
    request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
        totalBytesExpectedToDownload) in
        
        // bytesDownload                   Number of new bytes downloaded
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

#### Sample code 5. Downloading a folder and files contained
**Objective-C**

[//]: # (.cssg-snippet-transfer-download-folder)
```objective-c
    QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

    // Bucket name in the format: `BucketName-APPID`
    request.bucket = @"examplebucket-1250000000";
    // Maximum number of objects to return at a time. Default value: 1000
    request.maxKeys = 100;

    // The full path of a COS folder to be downloaded

    request.prefix = @"cos_path";


    [request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
        if(!error){
            for (QCloudBucketContents *content in result.contents) {
                QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
                
                // Bucket name in the format: `BucketName-APPID`
                request.bucket = @"examplebucket-1250000000";
                
                // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
                request.object = content.key;
                
                // Set the download URL. Once set, the file will be downloaded to the specified path
                request.downloadingURL = [NSURL fileURLWithPath:[@"Local File Path" stringByAppendingFormat:@"/%@",content.key]];
                
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
           
            
        }
    }];

    [[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-download-folder)
```swift
        let getBucketReq = QCloudGetBucketRequest.init();
        
        // Bucket name in the format: `BucketName-APPID`
        getBucketReq.bucket = "examplebucket-1250000000";
        
        // Maximum number of objects to return at a time. Default value: 1000
        getBucketReq.maxKeys = 100;
        
        // The full path of a COS folder to be downloaded
        getBucketReq.prefix = "cos_path";
        
        getBucketReq.setFinish { (result, error) in
            if let result = result {
                let contents = result.contents;
                for content in contents {
                    let info = QCloudDeleteObjectInfo.init();
                    let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
                    
                    // Bucket name in the format: `BucketName-APPID`
                    request.bucket = "examplebucket-1250000000";
                    
                    // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
                    request.object = content.key;
                    
                    // Set the download URL. Once set, the file will be downloaded to the specified path
                    
                    request.downloadingURL = NSURL.fileURL(withPath: "Local File Path" ) as URL?;
                    
                    // The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
                    request.localCacheDownloadOffset = 100;

                    // Monitor the download progress
                    request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
                        totalBytesExpectedToDownload) in
                        
                        // bytesDownload                   Number of new bytes downloaded
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
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift).


#### Sample code 6. Limiting the download speed

>! COS iOS SDK v5.9.5 or later is required.


**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Use `TrafficLimit` to limit the download speed, in bit/s. The speed range is 819200 to 838860800, that is, 100 KB/s to 100 MB/s.
request.trafficLimit = 819200;

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

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

// The size of the part of the file that has already been downloaded. Do not set this value for a new download operation
request.localCacheDownloadOffset = 100;

// Use `TrafficLimit` to limit the download speed, in bit/s. The speed range is 819200 to 838860800, that is, 100 KB/s to 100 MB/s.
request.trafficLimit = 819200;

// Monitor the download progress
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    
    // bytesDownload                   Number of new bytes downloaded
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

## Simple Operations

### Download an object

#### Description

This API is used to download an object to the local file system.

#### Sample code 1. Downloading an object
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    NSDictionary* info = (NSDictionary *) outputObject;
    // The CRC64 value of a server object
    result[@"x-cos-hash-crc64ecma"] 
    // The CRC64 value of a downloaded local object. If the returned CRC64 value is consistent with the local calculation, the downloaded object is the same as the server object.
    uint64_t localCrc64 = [Local object data qcloud_crc64];
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

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getObject.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getObject.object = "exampleobject";
// Set the download URL. Once set, the file will be downloaded to the specified path
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if let result = result {
        // The CRC64 value of a server object
        result["x-cos-hash-crc64ecma"] 
        // The CRC64 value of a downloaded local object. If the returned CRC64 value is consistent with the local calculation, the downloaded object is the same as the server object.
        uint64_t localCrc64 = Local object data.qcloud_crc64();
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

#### Sample code 2. Limiting the download speed
>! COS iOS SDK v5.9.5 or later is required.
>
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// Set the download URL. Once set, the file will be downloaded to the specified path
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Use `TrafficLimit` to limit the download speed, in bit/s. The speed range is 819200 to 838860800, that is, 100 KB/s to 100 MB/s.
request.trafficLimit = 819200;

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    NSDictionary* info = (NSDictionary *) outputObject;
    // Obtain the CRC64 value of the object.
    NSString * crc64 = [[outputObject __originHTTPURLResponse__].allHeaderFields valueForKey:@"x-cos-hash-crc64ecma"];
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

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getObject.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
getObject.object = "exampleobject";
// Set the download URL. Once set, the file will be downloaded to the specified path
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
    
// Use `TrafficLimit` to limit the download speed, in bit/s. The speed range is 819200 to 838860800, that is, 100 KB/s to 100 MB/s.
getObject.trafficLimit = 819200;

getObject.finishBlock = {(result,error) in
    if let result = result {
        // "result" contains response headers.
        // Obtain the CRC64 value of the object.
        let crc64 = result?.__originHTTPURLResponse__.allHeaderFields["x-cos-hash-crc64ecma"];
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
