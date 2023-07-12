## Overview

This document provides an overview of APIs and SDK code samples for object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |


## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Tagging an Object
#### Feature description

This API is used to set tags for an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags.

#### Sample code

**Objective-C**
```objective-c

    QCloudPutObjectTaggingRequest *putReq = [QCloudPutObjectTaggingRequest new];

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
        // outputObject contains all the HTTP response headers
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    [[QCloudCOSXMLService defaultCOSXML] PutObjectTagging:putReq];
```

**Swift**
```swift
    let putReq = QCloudPutObjectTaggingRequest()

    // Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    putReq.bucket = "examplebucket-1250000000";

    // Set of tags
    let taggings = QCloudTagging();

    let tag1 = QCloudTag();

    // Tag key; this value can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
    // colons, and slashes
    tag1.key = "age";

    // Tag value; this value can contain up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots,
    // colons, and slashes
    tag1.value = "20";
    let tag2 = QCloudTag();
    tag2.key = "name";
    tag2.value = "karis";

    // Set of tags. Up to 10 tags are supported
    let tagSet = QCloudTagSet();
    tagSet.tag = [tag1,tag2];
    taggings.tagSet = tagSet;

    // Set of tags
    putReq.taggings = taggings;

    req.finishBlock = {(result,error) in
        if let result = result {
            // result contains response headers
        } else {
            print(error!);
        }
    }
    QCloudCOSXMLService.defaultCOSXML().putObjectTagging(putReq);
```

## Querying Object Tags

#### Feature description

This API is used to query the existing tags of a specified object.

#### Sample code

**Objective-C**
```objective-c
    QCloudGetObjectTaggingRequest *getReq = [QCloudGetObjectTaggingRequest new];

    // Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    getReq.bucket = @"examplebucket-1250000000";

    [getReq setFinishBlock:^(QCloudTagging * result, NSError * error) {

        // Set of tags
        QCloudTagSet * tagSet = result.tagSet;
    }];
    [[QCloudCOSXMLService defaultCOSXML] GetObjectTagging:getReq];
```

**Swift**
```swift
    let getReq = QCloudGetObjectTaggingRequest();

    // Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    getReq.bucket = "examplebucket-1250000000";

    req.finishBlock = {(result,error) in
        if let result = result {
            // Set of tags
            let tagSet = result.tagSet;
        } else {
            print(error!);
        }
    }

    QCloudCOSXMLService.defaultCOSXML().getObjectTagging(getReq);
```

## Deleting Object Tags

>! The COS iOS SDK version should be v5.9.9 or higher.

#### Feature description

This API is used to delete the existing tags of a specified object.

#### Sample request

**Objective-C**
```objective-c
    QCloudDeleteObjectTaggingRequest *request = [QCloudDeleteObjectTaggingRequest new];

    // File name
    request.object = @"test.png";
    // Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    request.bucket = @"examplebucket-1250000000";
    request.versionId = @"versionId";

    [request setFinishBlock:^(id * result, NSError * error) {

        if(!error){
            // Deletion succeed
        }else{
            // Deletion failed
        }
    }];
    [[QCloudCOSXMLService defaultCOSXML] DeleteObjectTagging:request];
```

**Swift**
```swift
    let request = QCloudDeleteObjectTaggingRequest();

    // File name
    request.object = "test.png";

    // Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    request.bucket = "examplebucket-1250000000";

    request.versionId = "versionId";

    req.finishBlock = {(result,error) in
        if(!error){
            // Deletion succeed
        }else{
            // Deletion failed
        }
    }

    QCloudCOSXMLService.defaultCOSXML().deleteObjectTagging(request); 
```
