## Overview

This document provides an overview of APIs and SDK code samples related to object deletion.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Deleting a Single Object

#### API description

This API is used to delete a specified object from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket,
        cosPath);
cosXmlService.deleteObjectAsync(deleteObjectRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        DeleteObjectResult deleteObjectResult = (DeleteObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/DeleteObject.java).

## Deleting Multiple Objects

#### API description

This API is used to delete multiple objects in a single request.

#### Sample code

[//]: # (.cssg-snippet-delete-multi-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
List<String> objectList = new ArrayList<String>();
objectList.add("exampleobject1"); // The location identifier of the object in the bucket, i.e., the object key
objectList.add("exampleobject2"); // The location identifier of the object in the bucket, i.e., the object key

DeleteMultiObjectRequest deleteMultiObjectRequest =
        new DeleteMultiObjectRequest(bucket, objectList);
// In quiet mode, only information on objects that failed to be deleted will be returned; otherwise, the deletion result of each object will be returned.
deleteMultiObjectRequest.setQuiet(true);
cosXmlService.deleteMultiObjectAsync(deleteMultiObjectRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        DeleteMultiObjectResult deleteMultiObjectResult =
                (DeleteMultiObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

## Deleting a Directory

#### API description

COS uses slashes (/) as the delimiter to show directories in order to achieve the effect of a file system. Therefore, if you want to delete a directory in COS, you need to delete objects that are prefixed with a specified value. For example, the directory `prefix/` is actually all objects prefixed with `prefix/`. Therefore, you can delete all objects prefixed with `prefix/` to delete the `prefix/` directory.

Currently, COS’s Android SDK did not provide an API to perform this operation. However, you can still do it using a combination of basic operations.

#### Sample code

```
// Delete the parent/directory/ directory.
String directory = "parent/directory/";

GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);
getBucketRequest.setPrefix(directory);

// “prefix” indicates the directory to delete.
getBucketRequest.setPrefix(directory);
// Set the maximum number of traversed objects (up to 1,000 per listobject request).
getBucketRequest.setMaxKeys(1000);
GetBucketResult getBucketResult = null;

do {
    try {
        getBucketResult = cosXmlService.getBucket(getBucketRequest);
        List<ListBucket.Contents> contents = getBucketResult.listBucket.contentsList;
        DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket);
        for (ListBucket.Contents content : contents) {
            deleteMultiObjectRequest.setObjectList(content.key);
        }
        cosXmlService.deleteMultiObject(deleteMultiObjectRequest);
        getBucketRequest.setMarker(getBucketResult.listBucket.nextMarker);
    } catch (CosXmlClientException e) {
        e.printStackTrace();
        return;
    } catch (CosXmlServiceException e) {
        e.printStackTrace();
        return;
    }
} while (getBucketResult.listBucket.isTruncated);
```


>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/DeleteObject.java).

