## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [SensitiveContentRecognition](https://intl.cloud.tencent.com/document/product/436/48537) | Moderating an image synchronously | Moderates an image synchronously.         |
| [PostImagesAudit](https://intl.cloud.tencent.com/document/product/436/48538) | Batch moderating images | Batch moderates images.         |
| [GetImageAudit](https://intl.cloud.tencent.com/document/product/436/48539) | Querying the image moderation job result | Queries the result of the specified image moderation job.         |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Single Image Moderation

#### Feature description

This API is used to moderate an image synchronously.

#### Sample code

[//]: # ".cssg-snippet-sensitive-content-recognition"
```java
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
String key = "exampleobject"; // Object key
SensitiveContentRecognitionRequest sensitiveContentRecognitionRequest = new SensitiveContentRecognitionRequest(bucket, key);
sensitiveContentRecognitionRequest.addType("ads");
// `CIService` is a subclass of `CosXmlService` and has the same initialization method as it.
ciService.sensitiveContentRecognitionAsync(sensitiveContentRecognitionRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        SensitiveContentRecognitionResult sensitiveContentRecognitionResult = (SensitiveContentRecognitionResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PictureOperation.java).

## Batch Image Moderation

#### Feature description

This API is used to batch moderate images.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # ".cssg-snippet-post-images-audit"
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
        String cosPath1 = "dir1/exampleobject1.jpg";
        String cosPath2 = "dir1/exampleobject2.jpg";
        // URL of the image. Either `Object` or `Url` can be selected at a time.
        String imageUrl = "https://myqcloud.com/%205image.jpg";
        PostImagesAuditRequest request = new PostImagesAuditRequest(bucket);
        PostImagesAudit.ImagesAuditInput image1 = new PostImagesAudit.ImagesAuditInput();
        image1.object = cosPath1;
        // Set the original content, which can contain up to 512 bytes. This field will be returned in the response as-is.
        image1.dataId = "DataId1";
        // Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included).
        image1.interval = 2;
        // The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0.
        image1.maxFrames = 5;
        PostImagesAudit.ImagesAuditInput image2 = new PostImagesAudit.ImagesAuditInput();
        image2.object = cosPath2;
        image2.dataId = "DataId2";
        image2.interval = 2;
        image2.maxFrames = 5;
        PostImagesAudit.ImagesAuditInput image3 = new PostImagesAudit.ImagesAuditInput();
        image3.url = imageUrl;
        image3.dataId = "DataId3";
        image3.interval = 2;
        image3.maxFrames = 5;
        request.addImage(image1);
        request.addImage(image2);
        request.addImage(image3);
        // The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
        request.setDetectType("Porn,Ads");

        ciService.postImagesAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the batch image moderation job.
                // For detailed fields, see the API documentation or SDK source code.
                PostImagesAuditResult result = (PostImagesAuditResult) cosResult;
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

## Querying Image Moderation Job Result

#### Feature description

This API is used to query the result of the specified image moderation job.

>! The COS Android SDK version should not be earlier than v5.8.7.
>

#### Sample code

[//]: # ".cssg-snippet-get-image-audit"
```java
        // Bucket name in the format of BucketName-APPID
        String bucket = "examplebucket-1250000000";
        // Moderation job ID
        String jobId = "iab1ca9fc8a3ed11ea834c525400863904";
        GetImageAuditRequest request = new GetImageAuditRequest(bucket, jobId);
        ciService.getImageAuditAsync(request, new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult cosResult) {
                // `result` is the result of the image moderation job.
                // For detailed fields, see the API documentation or SDK source code.
                GetImageAuditResult result = (GetImageAuditResult) cosResult;
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
