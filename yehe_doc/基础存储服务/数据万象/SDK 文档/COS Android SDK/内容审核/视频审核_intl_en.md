## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PostVideoAudit](https://intl.cloud.tencent.com/document/product/436/48249) | Submitting a video moderation job | Submits a video moderation job.         |
| [GetVideoAudit](https://intl.cloud.tencent.com/document/product/436/48250) | Querying the video moderation job result | Queries the result of the specified video moderation job.         |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Submitting Video Moderation Job

#### Feature description

This API is used to submit a video moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # (.cssg-snippet-post-video-audit)
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
        String cosPath = "dir1/exampleobject.mp4";
        // URL of the video. Either `Object` or `Url` can be selected at a time.
        String url = "https://myqcloud.com/%205video.mp4";
        PostVideoAuditRequest request = new PostVideoAuditRequest(bucket);
        request.setObject(cosPath);
        request.setUrl(url);
        // Set the original content, which can contain up to 512 bytes. This field will be returned in the response as-is.
        request.setDataId("DataId");
        // Callback address, which must start with `http://` or `https://`.
        request.setCallback("https://github.com");
        // Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`.
        request.setCallbackVersion("Detail");
        // The number of captured frames. Value range: (0, 10000].
        request.setCount(3);
        // Video frame capturing frequency. Value range: (0, 60] seconds. The value supports the float format, accurate to the millisecond.
        request.setTimeInterval(10);
        // The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
        request.setDetectType("Porn,Ads");
        // Specify whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`.
        request.setDetectContent(1);
        
        // `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
        ciService.postVideoAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the submitted video moderation job.
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

## Querying Video Moderation Job Result

#### Feature description

This API is used to query the result of the specified video moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # (.cssg-snippet-get-video-audit)
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Moderation job ID
        String jobId = "iab1ca9fc8a3ed11ea834c525400863904";
        GetVideoAuditRequest request = new GetVideoAuditRequest(bucket, jobId);
        // `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
        ciService.getVideoAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the video moderation job.
                // For detailed fields, see the API documentation or SDK source code.
                GetVideoAuditResult result = (GetVideoAuditResult) cosResult;
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
