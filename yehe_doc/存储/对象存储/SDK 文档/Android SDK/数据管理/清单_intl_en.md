## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Creating an Inventory Job

#### Description

This API (PUT Bucket inventory) is used to create an inventory job for a bucket.

#### Sample code

[//]: # (.cssg-snippet-put-bucket-inventory)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
PutBucketInventoryRequest putBucketInventoryRequest =
        new PutBucketInventoryRequest(bucket);
putBucketInventoryRequest.setInventoryId("exampleInventoryId");
// Indicate whether to include object versions in the inventory:
// If set to All, all object versions are included in the inventory,
// with additional fields VersionId, IsLatest, and DeleteMarker
// If set to Current, no object versions are included in the inventory
putBucketInventoryRequest.setIncludedObjectVersions(InventoryConfiguration
        .IncludedObjectVersions.ALL);
// Backup frequency
putBucketInventoryRequest.setScheduleFrequency(InventoryConfiguration
        .SCHEDULE_FREQUENCY_DAILY);
// Backup path
putBucketInventoryRequest.setDestination("CSV", "1000000000",
        "examplebucket-1250000000", "region", "dir/");

cosXmlService.putBucketInventoryAsync(putBucketInventoryRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketInventoryResult putBucketInventoryResult =
                (PutBucketInventoryResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketInventory.java).


#### Error codes

The following describes some common errors that may occur when you call this API:

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Description

This API is used to query the inventory jobs of a bucket.

#### Sample code

[//]: # (.cssg-snippet-get-bucket-inventory)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
GetBucketInventoryRequest getBucketInventoryRequest =
        new GetBucketInventoryRequest(bucket);
getBucketInventoryRequest.setInventoryId("exampleInventoryId");

cosXmlService.getBucketInventoryAsync(getBucketInventoryRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketInventoryResult getBucketInventoryResult =
                (GetBucketInventoryResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketCORS.java).

## Deleting an Inventory Job

#### Description

This API is used to delete a specified inventory job from a bucket.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket-inventory)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
DeleteBucketInventoryRequest deleteBucketInventoryRequest =
        new DeleteBucketInventoryRequest(bucket);
deleteBucketInventoryRequest.setInventoryId("exampleInventoryId");

cosXmlService.deleteBucketInventoryAsync(deleteBucketInventoryRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketInventoryResult deleteBucketInventoryResult =
                (DeleteBucketInventoryResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
    }
});
```

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketCORS.java).

