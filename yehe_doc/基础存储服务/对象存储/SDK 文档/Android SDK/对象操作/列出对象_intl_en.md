## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### Description

This API is used to query some or all the objects in a bucket.

#### Sample 1. Getting the first page of data

[//]: # (.cssg-snippet-get-bucket)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
final GetBucketRequest getBucketRequest = new GetBucketRequest(bucketName);

// Prefix match, which is used to specify the address prefix of the returned objects
getBucketRequest.setPrefix("dir/");

// The maximum number of entries returned at a time; the default value is 1,000
getBucketRequest.setMaxKeys(100);

cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketResult getBucketResult = (GetBucketResult) result;
        if (getBucketResult.listBucket.isTruncated) {
            // The data is truncated, and the next page of data needs to be pulled
            prevPageResult = getBucketResult;
        }
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ListObjects.java).

#### Sample 2. Requesting the next page of data

[//]: # (.cssg-snippet-get-bucket-next-page)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;


GetBucketRequest getBucketRequest = new GetBucketRequest(bucketName);

// Prefix match, which is used to specify the address prefix of the returned objects
getBucketRequest.setPrefix("dir/");

// `prevPageResult` is the result returned on the previous page, where `nextMarker` indicates the starting point of the next page
String nextMarker = prevPageResult.listBucket.nextMarker;
getBucketRequest.setMarker(nextMarker);

// The maximum number of entries returned at a time; the default value is 1,000
getBucketRequest.setMaxKeys(100);

cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketResult getBucketResult = (GetBucketResult) result;
        if (getBucketResult.listBucket.isTruncated) {
            // The data is truncated, and the next page of data needs to be pulled
        }
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ListObjects.java).

#### Sample 3. Getting an object list and subdirectories

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
GetBucketRequest getBucketRequest = new GetBucketRequest(bucketName);

// Prefix match, which is used to specify the address prefix of the returned objects
getBucketRequest.setPrefix("dir/");

// The maximum number of entries returned at a time; the default value is 1,000
getBucketRequest.setMaxKeys(100);

// The delimiter is a symbol. If the prefix exists,
// identical paths between the prefix and delimiter will be grouped as together and defined as a common prefix,
// and then all common prefixes are listed. If there is no prefix, the listing starts from the beginning of the path
getBucketRequest.setDelimiter("/");

cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketResult getBucketResult = (GetBucketResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ListObjects.java).

## Querying an Object Version List

#### Description

This API is used to query some or all objects in a versioning-enabled bucket.

#### Sample 1. Getting the object version list’s first page of data

[//]: # (.cssg-snippet-list-objects-versioning)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
final GetBucketObjectVersionsRequest getBucketRequest =
        new GetBucketObjectVersionsRequest(bucketName);

// Prefix match, which is used to specify the address prefix of the returned objects
getBucketRequest.setPrefix("dir/");

// The maximum number of entries returned at a time; the default value is 1,000
getBucketRequest.setMaxKeys(100);

cosXmlService.getBucketObjectVersionsAsync(getBucketRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketObjectVersionsResult getBucketResult =
                (GetBucketObjectVersionsResult) result;
        if (getBucketResult.listVersionResult.isTruncated) {
            // The data is truncated, and the next page of data needs to be pulled
            prevPageResult = getBucketResult;
        }
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ListObjectsVersioning.java).

#### Sample 2. Getting the object version list’s next page of data

[//]: # (.cssg-snippet-list-objects-versioning-next-page)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
final GetBucketObjectVersionsRequest getBucketRequest =
        new GetBucketObjectVersionsRequest(bucketName);

// Prefix match, which is used to specify the address prefix of the returned objects
getBucketRequest.setPrefix("dir/");

// The maximum number of entries returned at a time; the default value is 1,000
getBucketRequest.setMaxKeys(100);

// `prevPageResult` is the result returned on the previous page, where `nextMarker` and `nextVersionIdMarker`
// indicate the starting point of the next page
getBucketRequest.setKeyMarker(prevPageResult.listVersionResult
        .nextKeyMarker);
getBucketRequest.setVersionIdMarker(prevPageResult.listVersionResult
        .nextVersionIdMarker);

cosXmlService.getBucketObjectVersionsAsync(getBucketRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketObjectVersionsResult getBucketResult =
                (GetBucketObjectVersionsResult) result;
        if (getBucketResult.listVersionResult.isTruncated) {
            // The data is truncated, and the next page of data needs to be pulled
            prevPageResult = getBucketResult;
        }
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ListObjectsVersioning.java).

