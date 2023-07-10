## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PostAudioAudit](https://intl.cloud.tencent.com/document/product/436/48262) | Submitting an audio moderation job | Submits an audio moderation job.   |
| [GetAudioAudit](https://intl.cloud.tencent.com/document/product/436/48263) | Querying the audio moderation job result | Queries the result of the specified audio moderation job.         |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Submitting an Audio Moderation Job

#### Feature description

This API is used to submit an audio moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # (.cssg-snippet-post-audio-audit)
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
        String cosPath = "dir1/exampleobject.mp3";
        // URL of the audio. Either `Object` or `Url` can be selected at a time.
        String url = "https://myqcloud.com/%205Audio.mp3";
        PostAudioAuditRequest request = new PostAudioAuditRequest(bucket);
        request.setObject(cosPath);
        request.setUrl(url);
        // Set the original content, which can contain up to 512 bytes. This field will be returned in the response as-is.
        request.setDataId("DataId");
        // Callback address, which must start with `http://` or `https://`.
        request.setCallback("https://github.com");
        // Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`.
        request.setCallbackVersion("Detail");
        // The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
        request.setDetectType("Porn,Ads");

        // `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
        ciService.postAudioAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the submitted audio moderation job.
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

## Querying Audio Moderation Job Result

#### Feature description

This API is used to query the result of an audio moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # (.cssg-snippet-get-audio-audit)
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Moderation job ID
        String jobId = "iab1ca9fc8a3ed11ea834c525400863904";
        GetAudioAuditRequest request = new GetAudioAuditRequest(bucket, jobId);
        // `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
        ciService.getAudioAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the audio moderation job.
                // For detailed fields, see the API documentation or SDK source code.
                GetAudioAuditResult result = (GetAudioAuditResult) cosResult;
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
