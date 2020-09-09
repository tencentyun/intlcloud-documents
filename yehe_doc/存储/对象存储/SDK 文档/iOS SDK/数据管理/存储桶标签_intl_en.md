## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes specified bucket tags |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Tags

#### API description

This API is used to set tags for an existing bucket.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-tagging"
```objective-c
QCloudPutBucketTaggingRequest *putReq = [QCloudPutBucketTaggingRequest new];

// Bucket name in the format: `BucketName-APPID`
putReq.bucket = @"examplebucket-1250000000";

// A set of tags
QCloudBucketTagging *taggings = [QCloudBucketTagging new];

QCloudBucketTag *tag1 = [QCloudBucketTag new];

// Key of the tag, which can be up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.key = @"age";

// Value of the tag, which can be up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.value = @"20";
QCloudBucketTag *tag2 = [QCloudBucketTag new];
tag2.key = @"name";
tag2.value = @"karis";

// A set of tags. Up to 10 tags are supported
QCloudBucketTagSet *tagSet = [QCloudBucketTagSet new];
tagSet.tag = @[tag1,tag2];
taggings.tagSet = tagSet;

// A set of tags
putReq.taggings = taggings;

[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketTagging:putReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketTagging.m).

**Swift**

[//]: # ".cssg-snippet-put-bucket-tagging"
```swift
let req = QCloudPutBucketTaggingRequest.init();

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";
let taggings = QCloudBucketTagging.init();

// A set of tags
let tagSet = QCloudBucketTagSet.init();
taggings.tagSet = tagSet;
let tag1 = QCloudBucketTag.init();

// Key of the tag, which can be up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.key = "age";

// Value of the tag, which can be up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.value = "20";

let tag2 = QCloudBucketTag.init();
tag2.key = "name";
tag2.value = "karis";

// A set of tags. Up to 10 tags are supported
tagSet.tag = [tag1,tag2];

// A set of tags
req.taggings = taggings;
req.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketTagging(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketTagging.swift).

## Querying Bucket Tags

#### API description 

This API is used to query the existing tags of a specified bucket.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-tagging"
```objective-c
QCloudGetBucketTaggingRequest *getReq = [QCloudGetBucketTaggingRequest new];

// Bucket name in the format: `BucketName-APPID`
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudBucketTagging * result, NSError * error) {
    // A set of tags
    QCloudBucketTagSet * tagSet = result.tagSet;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketTagging:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketTagging.m).

**Swift**

[//]: # ".cssg-snippet-get-bucket-tagging"
```swift
let req = QCloudGetBucketTaggingRequest.init();

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in
    if let result = result {
        // A set of tags
        let tagSet = result.tagSet
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketTagging(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketTagging.swift).

## Deleting Bucket Tags

#### API description 

This API is used to delete the existing tags of a specified bucket.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-delete-bucket-tagging"
```objective-c
QCloudDeleteBucketTaggingRequest *delReq = [QCloudDeleteBucketTaggingRequest new];

// Bucket name in the format: `BucketName-APPID`
delReq.bucket =  @"examplebucket-1250000000";

[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketTagging:delReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketTagging.m).

**Swift**

[//]: # ".cssg-snippet-delete-bucket-tagging"
```swift
let req = QCloudDeleteBucketTaggingRequest.init();

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";
req.finishBlock =  { (result, error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketTagging(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketTagging.swift).

