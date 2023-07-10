## Overview

This document provides an overview of APIs and SDK code samples for bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Tags

#### Feature description

This API is used to set tags for an existing bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-tagging)
```objective-c
QCloudPutBucketTaggingRequest *putReq = [QCloudPutBucketTaggingRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
putReq.bucket = @"examplebucket-1250000000";

// Set of tags
QCloudTagging *taggings = [QCloudTagging new];

QCloudTag *tag1 = [QCloudTag new];

// Tag key; this value can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.key = @"age";

// Tag value; this value can contain up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.value = @"20";
QCloudTag *tag2 = [QCloudTag new];
tag2.key = @"name";
tag2.value = @"karis";

// Set of tags. Up to 10 tags are supported
QCloudTagSet *tagSet = [QCloudTagSet new];
tagSet.tag = @[tag1,tag2];
taggings.tagSet = tagSet;

// Set of tags
putReq.taggings = taggings;

[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketTagging:putReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketTagging.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-tagging)
```swift
let req = QCloudPutBucketTaggingRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
req.bucket = "examplebucket-1250000000";
let taggings = QCloudTagging.init();

// Set of tags
let tagSet = QCloudTagSet.init();
taggings.tagSet = tagSet;
let tag1 = QCloudTag.init();

// Tag key; this value can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.key = "age";

// Tag value; this value can contain up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
// colons, and slashes
tag1.value = "20";

let tag2 = QCloudTag.init();
tag2.key = "name";
tag2.value = "karis";

// Set of tags. Up to 10 tags are supported
tagSet.tag = [tag1,tag2];

// Set of tags
req.taggings = taggings;
req.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketTagging(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketTagging.swift).

## Querying Bucket Tags

#### Feature description

This API is used to query the existing tags of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-tagging)
```objective-c
QCloudGetBucketTaggingRequest *getReq = [QCloudGetBucketTaggingRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudBucketTagging * result, NSError * error) {
    // Set of tags
    QCloudTagSet * tagSet = result.tagSet;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketTagging:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketTagging.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-tagging)
```swift
let req = QCloudGetBucketTaggingRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in
    if let result = result {
        // Set of tags
        let tagSet = result.tagSet
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketTagging(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketTagging.swift).

## Deleting Bucket Tags

#### Feature description

This API (`DELETE Bucket tagging`) is used to delete the existing tags from a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-tagging)
```objective-c
QCloudDeleteBucketTaggingRequest *delReq = [QCloudDeleteBucketTaggingRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
delReq.bucket =  @"examplebucket-1250000000";

[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketTagging:delReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketTagging.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket-tagging)
```swift
let req = QCloudDeleteBucketTaggingRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
req.bucket = "examplebucket-1250000000";
req.finishBlock =  { (result, error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketTagging(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketTagging.swift).

