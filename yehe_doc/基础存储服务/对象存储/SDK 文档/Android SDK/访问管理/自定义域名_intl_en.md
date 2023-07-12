## Overview

This document provides an overview of APIs and SDK code samples for custom domains.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket domain](https://www.tencentcloud.com/document/product/436/35868) | Setting a custom domain | Sets a custom domain for a bucket |
| [GET Bucket domain](https://www.tencentcloud.com/document/product/436/35869) | Querying a custom endpoint  | Queries the custom endpoint of a bucket |
| [DELETE Bucket domain](https://www.tencentcloud.com/document/product/436/35870) | Deleting a custom domain | Deletes the custom domain configuration of a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Custom Domains

#### Feature description

This API is used to set a custom domain for a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-domain"
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
PutBucketDomainRequest putBucketDomainRequest =
        new PutBucketDomainRequest(bucket);
DomainConfiguration.DomainRule domainRule = new DomainConfiguration.DomainRule(
        DomainConfiguration.STATUS_ENABLED,
        "www.example.com",
        DomainConfiguration.TYPE_REST
);
domainRule.forcedReplacement = DomainConfiguration.REPLACE_CNAME;
putBucketDomainRequest.addDomainRule(domainRule);

cosXmlService.putBucketDomainAsync(putBucketDomainRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketDomainResult putBucketDomainResult =
                (PutBucketDomainResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketDomain.java).

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Feature description

This API is used to query the custom domain set for a bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-domain"
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
GetBucketDomainRequest getBucketDomainRequest =
        new GetBucketDomainRequest(bucket);
cosXmlService.getBucketDomainAsync(getBucketDomainRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketDomainResult getBucketTaggingResult =
                (GetBucketDomainResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketDomain.java).


#### Response parameters

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
<th>API Type</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">x-cos-domain-txt-verification</td>
<td>Endpoint verification information. This field is an MD5 checksum of a character string in the format: <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format</td>
<td>String</td>
</tr>
</tbody></table>

## Deleting Custom Domains

#### Feature description

This API is used to delete the custom domain set for a bucket.

>! The COS Android SDK version should not be earlier than v5.9.8.
>

#### Sample code

[//]: # ".cssg-snippet-delete-bucket-domain"
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
DeleteBucketDomainRequest deleteBucketDomainRequest =
        new DeleteBucketDomainRequest(bucket);
cosXmlService.deleteBucketDomainAsync(deleteBucketDomainRequest,
        new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
                // For detailed fields, see the API documentation or SDK source code.
                DeleteBucketDomainResult deleteBucketDomainResult =
                        (DeleteBucketDomainResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketDomain.java).
