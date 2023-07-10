## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for file moderation.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PostDocumentAudit](https://intl.cloud.tencent.com/document/product/436/48258) | Submitting a file moderation job | Submits a file moderation job.         |
| [GetDocumentAudit](https://intl.cloud.tencent.com/document/product/436/48259) | Querying the file moderation job result | Queries the result of the specified file moderation job.         |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Submitting a File Moderation Job

#### Feature description

This API is used to submit a file moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # ".cssg-snippet-post-document-audit"
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
        String cosPath = "dir1/exampleobject.pdf";
        // URL of the file. Either `Object` or `Url` can be selected at a time.
        String url = "https://myqcloud.com/%205Document.pdf";
        PostDocumentAuditRequest request = new PostDocumentAuditRequest(bucket);
        request.setObject(cosPath);
        request.setUrl(url);
        // Set the original content, which can contain up to 512 bytes. This field will be returned in the response as-is.
        request.setDataId("DataId");
        // Callback address, which must start with `http://` or `https://`.
        request.setCallback("https://github.com");
        // The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
        request.setDetectType("Porn,Ads");

        // `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
        ciService.postDocumentAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the submitted file moderation job.
                // For detailed fields, see the API documentation or SDK source code.
                PostAuditResult result = (PostAuditResult) cosResult;
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException clientException, CosXmlServiceException serviceException) {
                if (clientException != null) {
                    clientException.printStackTrace();
                } else {
                    serviceException.printStackTrace();
                }
            }
        });
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CiAudit.java).

## Querying File Moderation Job Result

#### Feature description

This API is used to query the result of the specified file moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # ".cssg-snippet-get-document-audit"
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Moderation job ID
        String jobId = "iab1ca9fc8a3ed11ea834c525400863904";
        GetDocumentAuditRequest request = new GetDocumentAuditRequest(bucket, jobId);
        // `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
        ciService.getDocumentAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the file moderation job.
                // For detailed fields, see the API documentation or SDK source code.
                GetDocumentAuditResult result = (GetDocumentAuditResult) cosResult;
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException clientException, CosXmlServiceException serviceException) {
                if (clientException != null) {
                    clientException.printStackTrace();
                } else {
                    serviceException.printStackTrace();
                }
            }
        });
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CiAudit.java).
