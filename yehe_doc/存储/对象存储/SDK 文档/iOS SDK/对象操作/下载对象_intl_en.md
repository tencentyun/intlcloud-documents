## Overview

This document provides an overview of APIs and SDK code samples related to object download.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Downloading an object

Advanced APIs support pausing, resuming, and canceling download requests as well as the use of checkpoint restart to resume interrupted downloads.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-transfer-download-object)
```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
// If this parameter is not set, the file will be downloaded to memory and stored in the `outputObject` of `finishBlock`.
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

// Cancel the download
// To cancel the download, call `cancel`
[request cancel];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/TransferObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-download-object)
```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Set the download URL. Once set, the file will be downloaded to the specified path
// If this parameter is not set, the file will be downloaded to memory and stored in the `result` of `finishBlock`.
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
request.finishBlock = { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);

// Cancel the download
// To cancel the download, call `cancel`
request.cancel();
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/TransferObject.swift).

## Simple Operations

### Downloading an object

#### Feature description

This API is used to download an object.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];

// Set the download URL. Once set, the file will be downloaded to the specified path
// If this parameter is not set, the file will be downloaded to memory and stored in the `outputObject` of `finishBlock`.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers in the response
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/GetObject.m).

**Swift**

[//]: # (.cssg-snippet-get-object)
```swift
let getObject = QCloudGetObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
getObject.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
getObject.object = "exampleobject";
// Set the download URL. Once set, the file will be downloaded to the specified path
// If this parameter is not set, the file will be downloaded to memory and stored in the `result` of `finishBlock`.
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!
    .appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/GetObject.swift).

