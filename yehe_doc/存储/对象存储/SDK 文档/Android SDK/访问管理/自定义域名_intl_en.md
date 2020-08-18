## Overview

This document provides an overview of APIs and SDK code samples related to custom endpoints.

| API | Operation Name | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom endpoint | Sets a custom endpoint for a bucket |
| GET Bucket domain    | Querying a custom endpoint | Queries the custom endpoint of bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Custom Endpoint

#### Feature description

This API is used to configure a custom endpoint for a bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-domain"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketDomain.java).

#### Error Codes

The following describes some common errors that may occur when making requests using this API.

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The endpoint record already exists, and forced overwrite is not specified in the request; OR the endpoint record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The endpoint is a domain name without ICP filing in the Chinese mainland.                          |

## Querying a Custom Endpoint

#### Feature description

This API is used to query the custom endpoint of a bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-domain"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketDomainRequest getBucketDomainRequest =
        new GetBucketDomainRequest(bucket);
cosXmlService.getBucketDomainAsync(getBucketDomainRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketDomainResult getBucketTaggingResult =
                (GetBucketDomainResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketDomain.java).


#### Response parameters

<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Description</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">x-cos-domain-txt-verification</td>
<td>Endpoint verification information. This field is an MD5 checksum of a character string in the format: <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format</td>
<td>String</td>
</tr>
</tbody></table>

